# BugTracker API + Automated Tests

> **Projekt #2: TypeScript → testowanie API → Playwright**  
> Status: do rozpoczęcia — **poniedziałek, 12.10.2026**  
> Deadline głównej ścieżki: **31.10.2026**; konflikt dostępnego czasu opisano w `ROADMAP.md`.
> Język kodu/README: English | Wskazówki mentora: polski

## 1. Po co budujesz ten projekt?

Twoim celem zawodowym jest **Test Automation Engineer (Playwright + TypeScript)**. Ukończyłeś kurs TS i tworzysz już projekt Watchlist. Ten projekt ma utrwalić samodzielne kodowanie oraz nauczyć praktycznych zagadnień, które wykorzystasz w Playwright: `async/await`, HTTP, typowanie danych, testy, fixtures, izolacja testów, debugging i CI.

**Rezultat na GitHubie:** działające REST API do zarządzania zgłoszeniami błędów i osobny, sensownie zaprojektowany zestaw testów jednostkowych i integracyjnych, uruchamiany automatycznie w GitHub Actions.

**Definicja sukcesu:** umiesz wyjaśnić projekt bez AI, pokazać testy oraz samodzielnie zaplanować i wykonać przynajmniej jedną nową, małą zmianę w API wraz z testem. Korzystanie z dokumentacji jest dozwolone; pomoc AI przy nowych narzędziach nie przekreśla postępu.

### Czego NIE budujesz

- Frontendu ani aplikacji React.
- Logowania i autoryzacji.
- Bazy SQL, Dockera, mikroserwisów, wdrożenia w chmurze.
- Własnego frameworka testowego od zera.
- Testów Playwright — te będą Twoim kolejnym projektem.

Te rzeczy nie są potrzebne do zamknięcia etapu TypeScript.

> **Zasada:** To ostatni większy projekt TypeScript przed Playwrightem. Nie dodawaj tutaj Playwright, Allure ani MCP. One należą do osobnego projektu #3.

## 2. Stack

| Obszar          | Technologia                                          | Dlaczego                                                       |
| --------------- | ---------------------------------------------------- | -------------------------------------------------------------- |
| Runtime         | Node.js 24 LTS                                       | Aktualna wspierana linia LTS do nauki                          |
| Język           | TypeScript, `strict: true`                           | Bezpieczna praca na typach                                     |
| API             | Express                                              | Poznanie routingów, request/response, middleware               |
| Walidacja       | Zod                                                  | Bezpieczna walidacja nieznanych danych w runtime               |
| Testy           | Vitest                                               | Testy jednostkowe i integracyjne                               |
| Testy HTTP      | Supertest                                            | Testowanie aplikacji Express bez osobnego uruchamiania serwera |
| Uruchamianie TS | `tsx` (dev), `tsc` (typecheck/build)                 | Rozdzielenie uruchamiania od sprawdzania typów                 |
| Jakość          | ESLint + Prettier                                    | Spójność kodu                                                  |
| CI              | GitHub Actions                                       | Automatyczne sprawdzanie zmian                                 |
| Dane            | Początkowo pamięć, później plik JSON (`fs/promises`) | Ćwiczenie asynchroniczności i separacji odpowiedzialności      |

**Ważne:** Nie instaluj wszystkich pakietów na raz. Dodawaj zależności, gdy pojawi się zadanie, które ich wymaga. Wersje zależności sprawdzaj w oficjalnej dokumentacji w momencie instalacji.

## 3. Kontrakt domenowy — obiekt Issue

Każde zgłoszenie zawiera:

| Pole          | Typ / reguła                                                           |
| ------------- | ---------------------------------------------------------------------- |
| `id`          | UUID, nadawany przez aplikację                                         |
| `title`       | string; po `trim()` długość 3–100, obowiązkowe                         |
| `description` | string; max 1000 znaków, domyślnie `""`                                |
| `priority`    | `low \| medium \| high \| critical`, domyślnie `medium`                |
| `status`      | `open \| in_progress \| resolved`, nowy issue zaczyna jako `open`      |
| `createdAt`   | ISO 8601 string, nadawany przez aplikację                              |
| `updatedAt`   | ISO 8601 string, nadawany przez aplikację, zmieniany przy aktualizacji |

**Nie ufaj danym przychodzącym przez HTTP.** Samo typowanie TypeScript nie waliduje JSON otrzymanego od klienta. Użytkownik API nie może sam przypisywać `id`, dat ani statusu przy tworzeniu zgłoszenia.

Wersja podstawowa pozwala zmienić status na dowolną wartość ze zbioru dozwolonych statusów. Rozbudowane reguły przejść między statusami to BONUS, nie wymóg.

### Kontrakt REST API

| Metoda   | Endpoint      | Zachowanie                        | Sukces           |
| -------- | ------------- | --------------------------------- | ---------------- |
| `GET`    | `/health`     | Kontrola działania aplikacji      | `200`            |
| `POST`   | `/issues`     | Nowe zgłoszenie                   | `201`            |
| `GET`    | `/issues`     | Lista zgłoszeń, opcjonalne filtry | `200`            |
| `GET`    | `/issues/:id` | Pojedyncze zgłoszenie             | `200`            |
| `PATCH`  | `/issues/:id` | Częściowa aktualizacja            | `200`            |
| `DELETE` | `/issues/:id` | Usunięcie zgłoszenia              | `204` bez treści |

**Przykładowy request:**

```http
POST /issues
Content-Type: application/json

{
  "title": "Login button does not respond",
  "description": "Clicking Login has no effect",
  "priority": "high"
}
```

**Odpowiedź sukcesu (przykładowy kształt; identyfikator i daty tworzy serwer):**

```json
{
  "data": {
    "id": "de09dcd4-1956-44e7-adc6-ce1687c75cd8",
    "title": "Login button does not respond",
    "description": "Clicking Login has no effect",
    "priority": "high",
    "status": "open",
    "createdAt": "2026-10-10T10:00:00.000Z",
    "updatedAt": "2026-10-10T10:00:00.000Z"
  }
}
```

Oba endpointy pobierające zwracają obiekt z polem `data`. W `/issues` jest to tablica, a w `/issues/:id` pojedynczy obiekt.

**Błędy:**

```json
{
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Title must contain between 3 and 100 characters"
  }
}
```

- `400` — nieprawidłowy body, pusty PATCH, nieprawidłowy format `id` lub niedozwolone wartości filtrów.
- `404` — poprawnie sformatowane `id`, dla którego nie znaleziono zgłoszenia.
- `500` — nieoczekiwany błąd aplikacji; nie ujawniaj stack trace klientowi.
- `DELETE` po usunięciu zwraca `204` i **puste body**.
- Nieznane pola w JSON request body odrzucaj (`400`), zamiast ignorować je bez wyjaśnienia.

**Filtry listy:** `GET /issues?status=open&priority=high`. Oba filtry są opcjonalne, mogą występować razem, muszą akceptować tylko dozwolone wartości. Na początek zwracaj zgłoszenia w kolejności dodawania.

## 4. Architektura docelowa

Nie twórz tej struktury całej od razu. Dodawaj pliki w miarę postępu.

```text
bugtracker-api-ts/
├── .github/
│   └── workflows/
│       └── ci.yml
├── src/
│   ├── domain/          # typy i reguły biznesowe
│   ├── repositories/    # pamięć / JSON, warstwa danych
│   ├── services/        # operacje na zgłoszeniach
│   ├── routes/          # endpointy i mapowanie HTTP
│   ├── app.ts           # Express app bez listen()
│   └── server.ts        # uruchomienie serwera
├── tests/
│   ├── unit/
│   ├── integration/
│   └── helpers/         # fabryki danych / fixtures
├── AGENTS.md
├── PROJECT.md
├── README.md
├── .gitignore
├── .env.example        # tylko jeśli konfiguracja go wymaga
├── package.json
└── tsconfig.json
```

**Zasada architektoniczna:** route obsługuje HTTP, service logikę, repository zapis/odczyt. Test integracyjny nie może wymagać ręcznego uruchamiania serwera w osobnym terminalu.

**Obowiązkowe OOP i dependency injection:** repository w pamięci, repository JSON i service implementuj jako klasy. Konstruktor inicjalizuje stan i przyjmuje potrzebne zależności; service zależy od kontraktu repository, nie od jego konkretnej implementacji. Połączenie zależności wykonuj w miejscu składania aplikacji, a w testach podmieniaj je bez zmiany service. Wyjaśnij różnicę między klasą a instancją, rolę konstruktora, `this`, enkapsulację i kompozycję. Funkcje domenowe mogą pozostać czyste. Nie wymagamy dziedziczenia, kontenera DI, dekoratorów ani klas dla każdej funkcji.

## 5. Backlog — ucz się etapami

Codex ma dawać Ci **po jednym podzadaniu**, a nie wszystko za jednym razem. Checkbox zaznaczaj dopiero po samodzielnym wykonaniu i weryfikacji.

### ETAP 0 — Fundament repozytorium i środowisko

- [x] **0.1** Załóż publiczne repozytorium `bugtracker-api-ts`, dodaj ten `PROJECT.md` i `AGENTS.md`. Ustal, jak będziesz robić małe commity.
- [x] **0.2** Zainicjuj Node + TypeScript. Skonfiguruj `strict: true`, `.gitignore` i skrypt sprawdzania typów. Wyjaśnij, po co są `tsconfig.json` i `package.json`.
- [x] **0.3** Stwórz minimalne działające wejście do aplikacji. Uruchom projekt lokalnie i sprawdź kompilację.
  - Weryfikacja debugowania TS: w VS Code zatrzymaj wykonanie na breakpoincie w pliku `.ts`, obejrzyj wartość lokalną i call stack oraz wykonaj krok. Wyjaśnij, jak debugger trafia do źródła TS (w tym rolę source maps, jeśli używasz kompilacji). Nie wystarczy sam plik konfiguracji debuggera.
- [x] **0.4** Dodaj podstawowe zasady formatowania i sprawdzania jakości kodu. Nie dodawaj jeszcze żadnej funkcji biznesowej.

**Checkpoint:** Umiesz bez AI wyjaśnić różnicę między `tsc`, uruchamianiem JS/TS i `npm scripts`.

### ETAP 1 — Model domenowy i czysty TypeScript

- [ ] **1.1** Zdefiniuj typy `Issue`, `IssuePriority`, `IssueStatus`, `CreateIssueInput`, `UpdateIssueInput`. Rozróżnij pola wymagane, opcjonalne i tylko do odczytu.
- [ ] **1.2** Zaimplementuj czystą funkcję normalizującą tytuł (`trim`) i określ, co się dzieje przy pustym tytule.
- [ ] **1.3** Zaimplementuj tworzenie obiektu Issue z poprawnymi domyślnymi wartościami, UUID i datami. Zapewnij możliwość kontrolowania czasu/ID w testach bez skomplikowanych abstrakcji.
- [ ] **1.4** Przygotuj funkcję aktualizującą dozwolone pola bez mutowania danych wejściowych; `updatedAt` musi się zmieniać.

**Checkpoint:** Potrafisz wyjaśnić `type` kontra `interface`, `Partial<T>`, `readonly`, referencje obiektów oraz różnicę między `undefined` i brakującym polem.

### ETAP 2 — Warstwa przechowywania i logika CRUD

- [ ] **2.1** Zaprojektuj prosty kontrakt repository dla operacji: `create`, `findAll`, `findById`, `update`, `delete`.
- [ ] **2.2** Zaimplementuj jako klasę repozytorium trzymające zgłoszenia w pamięci, zgodnie z kontraktem 2.1. Konstruktor inicjalizuje niezależny stan każdej instancji. Nie ujawniaj przypadkowo mutowalnego wewnętrznego stanu; pokaż, że zmiana danych jednej instancji nie zmienia drugiej.
- [ ] **2.3** Zaimplementuj jako klasę operacje usługi: dodaj, pobierz jedno, pobierz wszystkie, aktualizuj, usuń. Wstrzyknij repository przez konstruktor i uzasadnij zależność od kontraktu. Wskaż miejsce składania zależności; nie twórz konkretnego repository wewnątrz service.
- [ ] **2.4** Dodaj filtrowanie po `status` i `priority`. Zastanów się, co powinno się stać, gdy brak wyników.
- [ ] **2.5** Wymyśl trzy sytuacje, w których warstwa logiki musi obsłużyć brak zgłoszenia lub błędne dane.

**Checkpoint:** Rozumiesz, po co oddziela się reguły biznesowe od zapisu danych; potrafisz bez AI dodać nową metodę repository.

### ETAP 3 — HTTP, Express i walidacja runtime

- [ ] **3.1** Dodaj Express i oddziel `app.ts` od `server.ts`. Uruchom `GET /health`.
- [ ] **3.2** Dodaj `POST /issues` z walidacją danych (Zod) i statusem `201`.
- [ ] **3.3** Dodaj `GET /issues` i `GET /issues/:id`.
- [ ] **3.4** Dodaj `PATCH /issues/:id` i `DELETE /issues/:id`.
- [ ] **3.5** Dodaj spójne kody i komunikaty błędów (`400`, `404`, `500`). Nie zwracaj stack trace.
- [ ] **3.6** Dodaj walidację i filtrowanie `GET /issues?status=...&priority=...`.
- [ ] **3.7** Ręcznie przetestuj API (np. Postman, Insomnia albo `curl`) dla co najmniej jednego poprawnego i jednego błędnego scenariusza każdej operacji.
  - Na własnych requestach wskaż metodę, URL, path parameters, query parameters, headers i body; wyjaśnij przepływ request–response oraz różnicę między błędem HTTP a brakiem odpowiedzi wskutek błędu sieciowego. Pokaż request z `Content-Type: application/json`, odczytaj status i nagłówki odpowiedzi oraz porównaj jej JSON z kontraktem (dla 204 sprawdź brak body).
- [ ] **3.8** Napisz niewielki skrypt kliencki z natywnym `fetch()` do lokalnego API, bez nowej biblioteki i bez frontendu. Wyślij poprawny POST z nagłówkiem JSON i odczytaj utworzone zgłoszenie po ID; pokaż osobno odpowiedź HTTP 400/404 i błąd połączenia przy zatrzymanym lokalnym serwerze. Kryteria: interpretujesz status/`ok`, sprawdzasz istotne pola odpowiedzi, obsługujesz błąd HTTP oraz odrzucenie Promise, oczekujesz na zakończenie operacji i wyjaśniasz, dlaczego odpowiedź 404 sama w sobie nie oznacza odrzucenia Promise przez `fetch`. To pojedyncze ćwiczenie manualne, nie drugi zestaw testów ani wymaganie uruchamiania serwera dla Supertest.

**Checkpoint:** Umiesz wyjaśnić, kiedy HTTP zwraca `200`, `201`, `204`, `400`, `404`, `500`, po co jest middleware i dlaczego typy TS nie walidują body HTTP.

### ETAP 4 — `async/await` i trwały zapis do JSON

- [ ] **4.1** Poznaj `Promise`, `async/await` oraz `try/catch` na samodzielnym minićwiczeniu z `fs/promises`.
  - W jednym minićwiczeniu użyj tymczasowego katalogu: obsłuż sukces oraz odrzucenie Promise i zapewnij sprzątanie w `finally` w obu przypadkach. Porównaj sekwencyjny odczyt dwóch niezależnych plików z `Promise.all`; uzasadnij, które operacje zależne muszą pozostać sekwencyjne. Nie wykonuj współbieżnych zapisów do tego samego pliku. Wyjaśnij, że odrzucenie `Promise.all` nie anuluje innych rozpoczętych operacji; sprzątanie nie może z nimi konkurować. Wskaż na swoim przykładzie skutek pominięcia `await` i popraw go. Dowód: wynik obu odczytów, obsłużony błąd, posprzątany katalog i wyjaśnienie kolejności; bez testów opartych na czasie wykonania.
- [ ] **4.2** Dodaj klasę repository JSON zgodną z tym samym kontraktem co repository w pamięci, zapisującą dane asynchronicznie, bez `readFileSync` i `writeFileSync`. Konstruktor przyjmuje potrzebną konfigurację, np. ścieżkę. Nie duplikuj logiki biznesowej service.
- [ ] **4.3** Obsłuż uruchomienie bez istniejącego pliku (pusta baza) i odczyt już zapisanych zgłoszeń po restarcie aplikacji.
- [ ] **4.4** Obsłuż uszkodzony JSON i błąd odczytu/zapisu w sposób jawny; nie zamieniaj uszkodzonego pliku po cichu na pustą listę.
- [ ] **4.5** Dodaj możliwość wyboru repozytorium i ścieżki pliku za pomocą konfiguracji. Testy muszą używać izolowanego, tymczasowego katalogu albo repozytorium w pamięci.
  - Dowód DI: ten sam service działa z obiema implementacjami bez zmiany swojego kodu; wybór i składanie zależności odbywa się poza service. Kontrakt i wywołujący muszą poprawnie obsługiwać asynchroniczne I/O.

**Checkpoint:** Rozumiesz, co zwraca funkcja `async`, gdzie powinno być `await`, jak przechwycić odrzucony Promise i dlaczego integracja z systemem plików utrudnia testy, jeśli nie zadbasz o izolację.

**Uwaga:** Zapis do pojedynczego JSON wystarczy do edukacyjnej aplikacji uruchamianej lokalnie. Nie przedstawiaj tego w README jako rozwiązania odpornego na równoczesne zapisy wielu procesów.

### ETAP 5 — Testy jednostkowe (Vitest)

- [ ] **5.1** Skonfiguruj Vitest i pierwszy samodzielny test czystej funkcji.
  - Wskaż części Arrange–Act–Assert we własnym teście; nazwa opisuje zachowanie, a asercja wykrywa jego naruszenie. Nie wymaga się komentarzy AAA w każdym teście.
- [ ] **5.2** Przetestuj tworzenie issue: wartości domyślne, poprawne dane, ograniczenia pól.
  - Przed kodem sam zaprojektuj tabelę przypadków z wynikiem i uzasadnieniem: Equivalence Partitioning (klasy danych poprawnych i niepoprawnych) oraz Boundary Value Analysis (tytuł po trim: 2/3/100/101, opis: 1000/1001). Rozróżnij happy path, negative path i edge case. W unit sprawdzaj reguły należące do domeny; walidację surowego JSON sprawdzaj w 6.3, bez kopiowania identycznych testów między poziomami.
- [ ] **5.3** Przetestuj aktualizację: tylko wybrane pola, brak mutacji oryginalnego obiektu, zmiana `updatedAt`.
- [ ] **5.4** Przetestuj operacje serwisu z kontrolowanym repository (bez HTTP i bez prawdziwego pliku).
  - Wykorzystaj repository w pamięci jako fake i `vi.fn()` jako kontrolowaną zależność zwracającą ustalony wynik (stub) oraz rejestrującą wywołania. Dla jednej istotnej operacji sprawdź argumenty i liczbę wywołań; dla odrzuconej operacji repository sprawdź zachowanie service. Użyj `vi.spyOn()` do obserwacji jednej rzeczywistej metody i przywróć ją po teście. Wyjaśnij mock (oczekiwane interakcje), stub (ustalone odpowiedzi), spy (obserwacja) i fake (uproszczona działająca implementacja); jedno narzędzie może pełnić różne role. Asercje interakcji mają wynikać z odpowiedzialności service, nie z prywatnych szczegółów implementacji.
  - Testy asynchroniczne oczekują na wynik lub zwracają Promise do runnera, w tym dla asercji odrzucenia. Pokaż osobne deterministyczne scenariusze resolve i reject. W kontrolowanym ćwiczeniu pomiń `await` przy asercji asynchronicznej, rozpoznaj fałszywy sukces albo komunikat runnera i przywróć poprawny test; nie pozostawiaj wadliwego testu w zestawie.
- [ ] **5.5** Wprowadź czytelne fabryki danych testowych, zamiast wklejać ten sam obiekt do każdego testu.
- [ ] **5.6** Doprowadź testy do niezależności — kolejność uruchomienia nie może zmieniać wyniku.
  - Kontroluj czas i ID tam, gdzie wpływają na asercje; nie używaj oczekiwania przez sleep. Każdy test otrzymuje własny stan, spy/mocks są odpowiednio czyszczone lub przywracane. Sprawdź wybrany test osobno i cały zestaw, a dla JSON także sprzątanie katalogów tymczasowych. Wyjaśnij różnicę między czyszczeniem historii wywołań a przywróceniem oryginalnej metody.

**Checkpoint:** Potrafisz wyjaśnić `describe`, `it/test`, `expect`, `beforeEach`, fake/test double, happy path, negative path, boundary case.

### ETAP 6 — Testy integracyjne API (Vitest + Supertest)

- [ ] **6.1** Napisz pierwszy test `GET /health`, bez uruchamiania serwera ręcznie.
- [ ] **6.2** Napisz test `POST /issues`: poprawne body → `201`, wymagane pola i wartości domyślne.
- [ ] **6.3** Przetestuj błędy `POST`: brak tytułu, same spacje, za krótki/długi tytuł, niedozwolony priority, nieznane pola.
  - Rozszerz tabelę z 5.2 o klasy surowych danych HTTP, np. błędny typ pola, oraz sam dobierz reprezentantów. Zastosuj `test.each` do jednej jednorodnej grupy przypadków walidacji; każdy przypadek ma czytelną nazwę i sprawdzalny wynik. Uwzględnij wartości tuż poniżej, na i powyżej granic; nie parametryzuj na siłę różnych scenariuszy CRUD.
- [ ] **6.4** Przetestuj `GET /issues` i `GET /issues/:id`, również pustą listę, nieprawidłowe ID i brak istniejącego ID.
- [ ] **6.5** Przetestuj `PATCH`: zmiana części pól, pusty obiekt i niepoprawne wartości.
- [ ] **6.6** Przetestuj `DELETE`: `204`, brak body i `404` przy próbie usunięcia drugi raz.
- [ ] **6.7** Przetestuj filtrowanie po jednym filtrze, dwóch filtrach i niedozwolonym filtrze.
- [ ] **6.8** Napisz przynajmniej jeden pełny scenariusz CRUD: create → read → update → delete → read (`404`).
- [ ] **6.9** Sprawdź izolację danych testowych: każdy test zaczyna z ustalonym stanem, bez zależności od innych testów i od zewnętrznego API.
  - Kryteria odpowiedzi dla 6.1–6.8: sprawdzaj status i istotne wartości/typy oraz strukturę `data` lub `error`, a nie sam status. Dla odpowiedzi JSON sprawdź `Content-Type`, dla DELETE brak body. Pokaż 500 przez kontrolowane odrzucenie zależności i sprawdź brak stack trace. Błąd sieciowy klienta jest ćwiczony w 3.8, nie przez niestabilne połączenie w Supertest.

**Checkpoint:** Umiesz powiedzieć, co testuje jednostka, co testuje endpoint, dlaczego testy wymagają izolacji i czym różni się test negatywny od pozytywnego.

### ETAP 7 — GitHub Actions, jakość, diagnoza błędów

- [ ] **7.1** Dodaj skrypty: `dev`, `typecheck`, `lint`, `format:check`, `test`, `build` (jeśli stosujesz kompilację).
- [ ] **7.2** Przygotuj workflow GitHub Actions uruchamiany na `push` i `pull_request`. Użyj Node 24 i `npm ci`.
- [ ] **7.3** W CI uruchom: sprawdzanie typów, lint, format, testy i ewentualnie build.
- [ ] **7.4** Na osobnej gałęzi celowo wprowadź mały błąd wykrywany przez istniejący test i odtwórz go lokalnie. Sam odczytaj komunikat i stack trace, wskaż istotną ramkę własnego kodu, postaw hipotezę i użyj breakpointu w TS do sprawdzenia wartości podczas testu. Zapisz w opisie PR objaw, przyczynę i dowód naprawy. Pokaż nieudany run GitHub Actions na tej gałęzi: wskaż job, krok, komendę i fragment logu wyjaśniający błąd. Napraw błąd własnoręcznie, uzyskaj zielony run i dopiero wtedy wykonaj merge PR. Dowód obejmuje branch, małe commity, link do PR oraz czerwonego i zielonego runu; nie psuj celowo gałęzi domyślnej.
- [ ] **7.5** Sprawdź, czy repozytorium nie zawiera `node_modules`, lokalnego pliku z danymi, sekretów ani przypadkowych plików środowiskowych.

**Checkpoint:** Potrafisz wyjaśnić, co dzieje się w CI po `push`, jak odczytać log błędu i dlaczego „testy przechodzą u mnie” nie wystarcza.

### ETAP 8 — GitHub portfolio i przygotowanie do rozmowy

- [ ] **8.1** Napisz po angielsku czytelny `README.md`: po co jest projekt, stack, instalacja, uruchomienie, testy i przykłady requestów.
- [ ] **8.2** Dodaj w README tabelę endpointów, opis architektury i krótką sekcję **Testing strategy** z podziałem na unit i integration.
- [ ] **8.3** Dodaj **Design decisions & trade-offs**: dlaczego Express, repository pattern, JSON zamiast bazy i izolacja testów.
- [ ] **8.4** Dodaj **Known limitations** i **What I would improve next** — bez udawania, że to produkcyjny system.
- [ ] **8.5** Pokaż widoczny status CI, uporządkuj historię commitów i upewnij się, że świeży klon repozytorium można uruchomić wyłącznie według README.
- [ ] **8.6** Przygotuj 2-minutowy opis projektu po angielsku i samodzielnie odpowiedz na pytania z sekcji 7.
- [ ] **8.7** Dodaj krótką, uczciwą informację o użyciu AI: Codex dawał zadania, wskazówki i code review; kod implementowałeś samodzielnie, jeśli rzeczywiście tak było. Nie deklaruj „zero AI”.
- [ ] **8.8** Wykonaj końcowe zadanie samodzielności opisane poniżej. To konkretna weryfikacja istniejącego warunku dopisania małej zmiany i testów, nie nowy moduł.

**Zadanie 8.8 — jeden nowy filtr listy:** dodaj opcjonalny query parameter `titleContains` w istniejącym `GET /issues`. Wartość ma być pojedynczym stringiem, po trim długości 1–100 znaków; dopasowanie jest niewrażliwe na wielkość liter i szuka dosłownego fragmentu tytułu. Błędny typ, powtórzony parametr, pusty tekst i przekroczona długość oznaczają 400 w istniejącym formacie błędu. Filtr łączy się ze `status` i `priority` przez AND; brak parametru zachowuje obecne zachowanie, brak wyników daje 200 z pustą tablicą, kolejność dodawania pozostaje zachowana. Nie dodawaj paginacji, sortowania ani wyrażeń regularnych.

**Warunki przeprowadzenia 8.8:** mentor przed rozpoczęciem porównuje wymaganie z historią zadań/PR i ćwiczeń; samo przeczytanie specyfikacji nie jest wykonaniem zadania. Nie ćwiczymy identycznego filtra wcześniej. Jeżeli użytkownik już go implementował, przed próbą zastępujemy go jednym równie małym, niećwiczonym wymaganiem i zapisujemy jego kontrakt; nie zaliczamy znanej implementacji jako transferu.

**Kryteria 8.8:** użytkownik sam interpretuje wymagania, zapisuje plan i tabelę przypadków przed implementacją, wybiera moduły, implementuje zmianę oraz adekwatne unit/API tests, sam uruchamia sprawdzenia i diagnozuje błędy. Przedstawia diff, wyniki, wyjaśnienie decyzji, regresji i poziom pomocy. Jeśli nie napotka błędu, przeprowadza krótką kontrolowaną próbę z błędem w nowej zmianie i diagnozuje go, a następnie przywraca poprawne zachowanie. Oficjalna dokumentacja jest dozwolona; AI domyślnie dopiero robi końcowe review, bez oceny planu, listy przypadków, sygnatur ani kroków implementacji przed próbą. Pomoc na wyraźną prośbę jest dozwolona, ale odnotowana; po prowadzeniu krok po kroku dowód samodzielności wymaga kolejnej równie małej, nowej próby. Wszystkie wymagania kontraktu muszą być pokryte uzasadnionymi przypadkami, dotychczasowe testy i CI przechodzą, użytkownik sam wprowadza poprawki z review i potrafi wyjaśnić kod bez AI.

**Checkpoint:** Z pamięci umiesz wyjaśnić architekturę i testy oraz samodzielnie naprawić celowo wprowadzony błąd.

## 6. Minimalna matryca testów

Ta tabela mówi **co zweryfikować**, nie jak napisać test.

| Scenariusz  | Pozytywny                           | Negatywny / brzegowy                                    |
| ----------- | ----------------------------------- | ------------------------------------------------------- |
| Create      | poprawny issue, `201`, `id` i daty  | puste title, same spacje, 2/101 znaków, błędny priority |
| List        | pusta lista, lista po dodaniu       | filtr bez wyników, niedozwolony status                  |
| Get by ID   | istniejący issue                    | nieprawidłowy UUID, nieistniejący UUID                  |
| Update      | częściowa aktualizacja, zmiana daty | `{}`, niedozwolony status, brak issue                   |
| Delete      | `204`, potem `404`                  | brak issue, poprawny format odpowiedzi                  |
| Persistence | odczyt po restarcie                 | uszkodzony JSON, błędy I/O                              |
| Isolation   | test uruchamia się samodzielnie     | testy nie zależą od kolejności                          |

Nie traktuj samej liczby testów ani procentu coverage jako dowodu jakości. Ważniejsze są poprawne asercje, przypadki brzegowe i deterministyczność.

## 7. Pytania do rozmowy rekrutacyjnej

Na końcu spróbuj odpowiedzieć bez notatek:

1. Jak rozdzieliłeś logikę biznesową od warstwy HTTP i przechowywania danych? Co to dało testom?
2. Dlaczego TypeScript nie wystarcza do zweryfikowania danych przychodzących przez API? Do czego użyłeś Zod?
3. Czym różnią się Twoje testy jednostkowe od integracyjnych? Co właściwie weryfikuje każdy poziom?
4. Jak zapewniłeś niezależność testów od ich kolejności uruchomienia?
5. Co się stanie, gdy JSON jest uszkodzony lub zapis na dysku się nie uda?
6. Jak zdecydowałeś, jakie przypadki negatywne i brzegowe trzeba przetestować?
7. Jak działa CI, jakie komendy wykonuje i jaki problem pomaga wykryć?
8. Jak przeniósłbyś poznane wzorce do testów Playwright (fixtures, API requests, test isolation, asynchronous code)?
9. Jakie ograniczenia ma używanie pliku JSON w porównaniu z prawdziwą bazą danych?
10. Co zmieniłbyś w projekcie, gdyby miał obsługiwać tysiące użytkowników?

## 8. Warunki ukończenia — zielone światło do Playwrighta

Możesz przejść **w pełni do Playwrighta**, gdy spełniasz WSZYSTKIE poniższe warunki:

- [ ] Endpointy CRUD działają zgodnie z kontraktem, a błędy mają właściwe statusy.
- [ ] Samodzielnie wykorzystujesz `async/await`, `try/catch` i moduły TS.
- [ ] Potrafisz dopisać nową funkcję i test bez prowadzenia krok po kroku przez AI.
  - Dowód: zadanie 8.8 oraz praktyczne dowody umiejętności z matrycy w `AUDIT.md`; same odpowiedzi na quiz nie zastępują wykonania zadań.
- [ ] Masz działające unit + API integration tests i umiesz wyjaśnić 3 wybrane asercje.
- [ ] Testy są izolowane i deterministyczne.
- [ ] Pipeline GitHub Actions przechodzi na domyślnej gałęzi.
- [ ] README pozwala innej osobie uruchomić projekt od zera.
- [ ] Potrafisz opowiedzieć projekt na rozmowie rekrutacyjnej w 2–3 minuty.

**To nie jest obietnica gotowości do zatrudnienia.** To punkt, w którym dalszy rozwój TypeScriptu przez rozbudowę tego API daje mniejszy zwrot niż praktyka z Playwrightem.

## 9. BONUS — opcjonalne, nie blokują Playwrighta

- Paginacja i sortowanie listy issues.
- Śledzenie historii zmian statusu.
- OpenAPI/Swagger.
- Raport coverage z interpretacją luk, a nie wyłącznie procentem.
- Własny prosty frontend, który można później wykorzystać do testów Playwright.
- Zastąpienie JSON bazą danych.

Nie dodawaj tych funkcji, dopóki podstawowa część nie jest kompletna.

## 10. Jak pracować z Codexem

1. Utwórz puste repozytorium i dodaj do katalogu głównego wszystkie pięć plików `.md` z paczki; zacznij od `START_HERE.md`.
2. Otwórz repozytorium w Codexie.
3. Wyślij wiadomość: **`START`**. Codex powinien podać wyłącznie pierwsze małe zadanie.
4. Pracuj samodzielnie. Jeśli utkniesz, używaj stopniowo `WSKAZÓWKA 1`, `WSKAZÓWKA 2`, `WSKAZÓWKA 3`.
5. Po napisaniu kodu użyj **`REVIEW`** i samodzielnie popraw wykryte problemy.
6. Po weryfikacji odznacz zadanie w `PROJECT.md` i zapisz krótką notatkę w `PROGRESS.md` (samodzielnie albo poproś Codexa o aktualizację tych dwóch plików). Zrób sensowny commit.
7. Poproś o **`QUIZ`** po każdym etapie. Gdy odpowiedzi są niepewne, wróć do tej konkretnej luki.
8. Na końcu poproś o **`INTERVIEW`**.

**Zdanie, które warto zapamiętać:** celem nie jest to, żeby AI pomogło Ci skończyć repozytorium. Celem jest to, żebyś rozumiał każdą istotną decyzję i potrafił samodzielnie napisać kolejną funkcję oraz test.

---

### Polecana dokumentacja

- TypeScript Handbook: https://www.typescriptlang.org/docs/handbook/intro.html
- Node.js: https://nodejs.org/en/learn
- Express: https://expressjs.com/
- Zod: https://zod.dev/
- Vitest: https://vitest.dev/guide/
- Supertest: https://github.com/ladjs/supertest
- GitHub Actions: https://docs.github.com/en/actions
- Playwright (następny projekt): https://playwright.dev/docs/intro
