# Diff audytu edukacyjnego

Zmiany specyfikacji względem HEAD oraz nowy raport AUDIT.md. Ten plik jest artefaktem podglądu diffu.

```diff
diff --git a/AGENTS.md b/AGENTS.md
index 1103410..58cb2de 100644
--- a/AGENTS.md
+++ b/AGENTS.md
@@ -81,11 +81,14 @@ Po komunikacie „REVIEW”:
 - Nie twierdź, że plik, test lub CI działa, jeśli tego nie sprawdzono.

 ## Granice projektu
+- Obowiązkowe klasy, konstruktory, enkapsulacja i dependency injection ćwiczymy w repository i service zgodnie z `PROJECT.md`; nie narzucaj dziedziczenia ani kontenera DI. Nie dodawaj mechanizmu tylko po to, by pojawił się w kodzie.
+- Deadline głównej ścieżki to 31.10.2026. Jeśli dostępny czas nie wystarcza, pokaż konflikt i oszacowanie z `ROADMAP.md`; nie usuwaj ważnych umiejętności ani nie zaliczaj ich bez dowodów.
 - Wymagania podstawowe są w `PROJECT.md` — nie dokładaj nowych frameworków i funkcji bez potrzeby.
 - Nie buduj frontendu, logowania, bazy SQL, Dockera ani mikroserwisów w ramach obowiązkowej części projektu.
 - Rozszerzenia `BONUS` można zaproponować dopiero po skończeniu głównej ścieżki; **nie blokują przejścia do Playwrighta**.

 ## Odnotowywanie postępów
+- Matryca w `AUDIT.md` mapuje wymagania na zadania i dowody, ale nie jest drugą checklistą. Odróżniaj obecność tematu w specyfikacji od jego praktycznego opanowania.
 - `PROJECT.md` jest **jedyną checklistą ukończenia** zadań; `PROGRESS.md` jest krótkim dziennikiem sesji i blockerów.
 - Nie oznaczaj zadania jako ukończonego bez pokazania przez użytkownika wyników lub przeprowadzenia uzgodnionych sprawdzeń.
 - Domyślnie nie edytuj nawet plików `.md`. Na polecenie `ZAPISZ POSTĘP` możesz zaktualizować **wyłącznie** checkbox w `PROJECT.md` i dziennik `PROGRESS.md`, jeśli użytkownik potwierdzi, że chce tej aktualizacji.
@@ -103,3 +106,10 @@ Po komunikacie „REVIEW”:

 ## Pierwsza odpowiedź Codexa
 Gdy użytkownik napisze `START`, krótko potwierdź cel i podaj wyłącznie **zadanie `0.1` z `PROJECT.md`, bez komend tworzących całą aplikację i bez gotowego kodu.
+
+## Końcowa próba samodzielności (8.8)
+
+- Przed próbą sprawdź historię zadań i ćwiczeń, aby wymaganie nie powtarzało identycznego rozwiązania. Nie ujawniaj rozwiązania przy audycie specyfikacji.
+- Użytkownik sam zapisuje plan i przypadki. W tym jednym zadaniu nie oceniaj ich przed samodzielną próbą; review wykonuj na końcu. Oficjalna dokumentacja jest dozwolona, stopniowane wskazówki pozostają dostępne wyłącznie na prośbę.
+- Sprawdź interpretację wymagań, implementację, projekt testów, deterministyczność, debugging i wyjaśnienie decyzji, nie tylko zielone testy. Poprawki pisze użytkownik.
+- Zanotuj zakres pomocy; po prowadzeniu krok po kroku zaproponuj równie mały, nowy transfer zamiast twierdzić, że próba dowiodła samodzielności.
diff --git a/PROGRESS.md b/PROGRESS.md
index 2262f7c..2a5716f 100644
--- a/PROGRESS.md
+++ b/PROGRESS.md
@@ -2,14 +2,15 @@

 > Projekt #2: BugTracker API + Automated Tests
 > Planowany start: **2026-10-12 (poniedziałek)**
-> **Stan początkowy:** nie rozpoczęto
+> Deadline: **2026-10-31**
+> Stan: rozpoczęto przygotowanie repozytorium; brak dowodów ukończenia pozostałych etapów.

 ## Aktualny etap

 - Etap: `0 — Fundament repozytorium`
-- Najbliższe zadanie: `0.1`
-- Ostatnio ukończone zadanie: brak
-- Aktualny problem / blocker: brak
+- Najbliższe zadanie: `0.2` (wydane w rozmowie; wykonanie nieweryfikowane)
+- Ostatnio potwierdzone w rozmowie: `0.1`; checkbox w `PROJECT.md` nie został jeszcze zsynchronizowany. Audyt specyfikacji nie odhacza zadań.
+- Aktualne ryzyko: deadline 31.10.2026 przy 2 h dziennie daje 40 h od planowanego startu, mniej niż szacowany zakres; zobacz `ROADMAP.md`.

 ## Dziennik sesji

@@ -19,6 +20,14 @@ Dodawaj **jeden krótki wpis po sesji**. Nie musisz wpisywać czasu co do minuty
 |---|---|---|---|---|---|
 | 2026-10-12 | — | Start projektu | — | — | Zadanie 0.1 |

+Powyższy wpis pochodzi z szablonu i oznacza planowany start, nie dowód odbycia przyszłej sesji.
+
+### Audyt specyfikacji — 2026-10-11
+
+Przejrzano aktualne AGENTS/PROJECT/ROADMAP/PROGRESS. Specyfikacja miała CRUD, podstawy async, negatywne/graniczne testy i izolację, ale nie pełne praktyczne kryteria EP/BVA, doubles, współbieżności, fetch, debuggera i PR/CI. Włączono je do istniejących etapów oraz doprecyzowano końcową próbę 8.8. W odczytanych plikach brakowało zapisów wcześniejszych zmian OOP/DI; obowiązkowe klasy, konstruktory i DI zostały jawnie ujęte w 2.2/2.3/4.2/4.5. Nie przypisano nowych poziomów samodzielności ani zaliczeń; audyt wymagań nie jest weryfikacją umiejętności.
+
+Dowody po faktycznym wykonaniu zadania zapisujemy w krótkim wpisie sesji: numer zadania, wynik/komenda lub link do PR/runu, przyczyna napotkanego błędu, zakres pomocy i następny krok. Dla 8.8 dodatkowo: potwierdzenie nowości wymagania, własny plan/tabela przypadków, wyniki i wyjaśnienie decyzji. Nie dodajemy drugiej checklisty umiejętności; mapowanie znajduje się w `AUDIT.md`.
+
 **Samodzielność:** S0 = AI podało istotne kroki lub szkielet; S1 = mój pomysł + konkretne wskazówki; S2 = własny plan i implementacja, dokumentacja + review AI. Poziom to opis **sposobu wykonania zadania**, nie ocena użytkownika. Aktualizuj na żądanie, nie trzeba wpisywać codziennie.

 ## Luki do powtórki
diff --git a/PROJECT.md b/PROJECT.md
index 61e65f3..3d5fa2d 100644
--- a/PROJECT.md
+++ b/PROJECT.md
@@ -2,6 +2,7 @@

 > **Projekt #2: TypeScript → testowanie API → Playwright**
 > Status: do rozpoczęcia — **poniedziałek, 12.10.2026**
+> Deadline głównej ścieżki: **31.10.2026**; konflikt dostępnego czasu opisano w `ROADMAP.md`.
 > Język kodu/README: English | Wskazówki mentora: polski

 ## 1. Po co budujesz ten projekt?
@@ -150,6 +151,8 @@ bugtracker-api-ts/

 **Zasada architektoniczna:** route obsługuje HTTP, service logikę, repository zapis/odczyt. Test integracyjny nie może wymagać ręcznego uruchamiania serwera w osobnym terminalu.

+**Obowiązkowe OOP i dependency injection:** repository w pamięci, repository JSON i service implementuj jako klasy. Konstruktor inicjalizuje stan i przyjmuje potrzebne zależności; service zależy od kontraktu repository, nie od jego konkretnej implementacji. Połączenie zależności wykonuj w miejscu składania aplikacji, a w testach podmieniaj je bez zmiany service. Wyjaśnij różnicę między klasą a instancją, rolę konstruktora, `this`, enkapsulację i kompozycję. Funkcje domenowe mogą pozostać czyste. Nie wymagamy dziedziczenia, kontenera DI, dekoratorów ani klas dla każdej funkcji.
+
 ## 5. Backlog — ucz się etapami

 Codex ma dawać Ci **po jednym podzadaniu**, a nie wszystko za jednym razem. Checkbox zaznaczaj dopiero po samodzielnym wykonaniu i weryfikacji.
@@ -159,6 +162,7 @@ Codex ma dawać Ci **po jednym podzadaniu**, a nie wszystko za jednym razem. Che
 - [ ] **0.1** Załóż publiczne repozytorium `bugtracker-api-ts`, dodaj ten `PROJECT.md` i `AGENTS.md`. Ustal, jak będziesz robić małe commity.
 - [ ] **0.2** Zainicjuj Node + TypeScript. Skonfiguruj `strict: true`, `.gitignore` i skrypt sprawdzania typów. Wyjaśnij, po co są `tsconfig.json` i `package.json`.
 - [ ] **0.3** Stwórz minimalne działające wejście do aplikacji. Uruchom projekt lokalnie i sprawdź kompilację.
+  - Weryfikacja debugowania TS: w VS Code zatrzymaj wykonanie na breakpoincie w pliku `.ts`, obejrzyj wartość lokalną i call stack oraz wykonaj krok. Wyjaśnij, jak debugger trafia do źródła TS (w tym rolę source maps, jeśli używasz kompilacji). Nie wystarczy sam plik konfiguracji debuggera.
 - [ ] **0.4** Dodaj podstawowe zasady formatowania i sprawdzania jakości kodu. Nie dodawaj jeszcze żadnej funkcji biznesowej.

 **Checkpoint:** Umiesz bez AI wyjaśnić różnicę między `tsc`, uruchamianiem JS/TS i `npm scripts`.
@@ -175,8 +179,8 @@ Codex ma dawać Ci **po jednym podzadaniu**, a nie wszystko za jednym razem. Che
 ### ETAP 2 — Warstwa przechowywania i logika CRUD

 - [ ] **2.1** Zaprojektuj prosty kontrakt repository dla operacji: `create`, `findAll`, `findById`, `update`, `delete`.
-- [ ] **2.2** Zaimplementuj repozytorium trzymające zgłoszenia w pamięci. Nie ujawniaj przypadkowo mutowalnego wewnętrznego stanu.
-- [ ] **2.3** Zaimplementuj operacje usługi: dodaj, pobierz jedno, pobierz wszystkie, aktualizuj, usuń.
+- [ ] **2.2** Zaimplementuj jako klasę repozytorium trzymające zgłoszenia w pamięci, zgodnie z kontraktem 2.1. Konstruktor inicjalizuje niezależny stan każdej instancji. Nie ujawniaj przypadkowo mutowalnego wewnętrznego stanu; pokaż, że zmiana danych jednej instancji nie zmienia drugiej.
+- [ ] **2.3** Zaimplementuj jako klasę operacje usługi: dodaj, pobierz jedno, pobierz wszystkie, aktualizuj, usuń. Wstrzyknij repository przez konstruktor i uzasadnij zależność od kontraktu. Wskaż miejsce składania zależności; nie twórz konkretnego repository wewnątrz service.
 - [ ] **2.4** Dodaj filtrowanie po `status` i `priority`. Zastanów się, co powinno się stać, gdy brak wyników.
 - [ ] **2.5** Wymyśl trzy sytuacje, w których warstwa logiki musi obsłużyć brak zgłoszenia lub błędne dane.

@@ -191,16 +195,20 @@ Codex ma dawać Ci **po jednym podzadaniu**, a nie wszystko za jednym razem. Che
 - [ ] **3.5** Dodaj spójne kody i komunikaty błędów (`400`, `404`, `500`). Nie zwracaj stack trace.
 - [ ] **3.6** Dodaj walidację i filtrowanie `GET /issues?status=...&priority=...`.
 - [ ] **3.7** Ręcznie przetestuj API (np. Postman, Insomnia albo `curl`) dla co najmniej jednego poprawnego i jednego błędnego scenariusza każdej operacji.
+  - Na własnych requestach wskaż metodę, URL, path parameters, query parameters, headers i body; wyjaśnij przepływ request–response oraz różnicę między błędem HTTP a brakiem odpowiedzi wskutek błędu sieciowego. Pokaż request z `Content-Type: application/json`, odczytaj status i nagłówki odpowiedzi oraz porównaj jej JSON z kontraktem (dla 204 sprawdź brak body).
+- [ ] **3.8** Napisz niewielki skrypt kliencki z natywnym `fetch()` do lokalnego API, bez nowej biblioteki i bez frontendu. Wyślij poprawny POST z nagłówkiem JSON i odczytaj utworzone zgłoszenie po ID; pokaż osobno odpowiedź HTTP 400/404 i błąd połączenia przy zatrzymanym lokalnym serwerze. Kryteria: interpretujesz status/`ok`, sprawdzasz istotne pola odpowiedzi, obsługujesz błąd HTTP oraz odrzucenie Promise, oczekujesz na zakończenie operacji i wyjaśniasz, dlaczego odpowiedź 404 sama w sobie nie oznacza odrzucenia Promise przez `fetch`. To pojedyncze ćwiczenie manualne, nie drugi zestaw testów ani wymaganie uruchamiania serwera dla Supertest.

 **Checkpoint:** Umiesz wyjaśnić, kiedy HTTP zwraca `200`, `201`, `204`, `400`, `404`, `500`, po co jest middleware i dlaczego typy TS nie walidują body HTTP.

 ### ETAP 4 — `async/await` i trwały zapis do JSON

 - [ ] **4.1** Poznaj `Promise`, `async/await` oraz `try/catch` na samodzielnym minićwiczeniu z `fs/promises`.
-- [ ] **4.2** Dodaj drugi typ repository zapisujący dane w lokalnym pliku JSON asynchronicznie, bez `readFileSync` i `writeFileSync`.
+  - W jednym minićwiczeniu użyj tymczasowego katalogu: obsłuż sukces oraz odrzucenie Promise i zapewnij sprzątanie w `finally` w obu przypadkach. Porównaj sekwencyjny odczyt dwóch niezależnych plików z `Promise.all`; uzasadnij, które operacje zależne muszą pozostać sekwencyjne. Nie wykonuj współbieżnych zapisów do tego samego pliku. Wyjaśnij, że odrzucenie `Promise.all` nie anuluje innych rozpoczętych operacji; sprzątanie nie może z nimi konkurować. Wskaż na swoim przykładzie skutek pominięcia `await` i popraw go. Dowód: wynik obu odczytów, obsłużony błąd, posprzątany katalog i wyjaśnienie kolejności; bez testów opartych na czasie wykonania.
+- [ ] **4.2** Dodaj klasę repository JSON zgodną z tym samym kontraktem co repository w pamięci, zapisującą dane asynchronicznie, bez `readFileSync` i `writeFileSync`. Konstruktor przyjmuje potrzebną konfigurację, np. ścieżkę. Nie duplikuj logiki biznesowej service.
 - [ ] **4.3** Obsłuż uruchomienie bez istniejącego pliku (pusta baza) i odczyt już zapisanych zgłoszeń po restarcie aplikacji.
 - [ ] **4.4** Obsłuż uszkodzony JSON i błąd odczytu/zapisu w sposób jawny; nie zamieniaj uszkodzonego pliku po cichu na pustą listę.
 - [ ] **4.5** Dodaj możliwość wyboru repozytorium i ścieżki pliku za pomocą konfiguracji. Testy muszą używać izolowanego, tymczasowego katalogu albo repozytorium w pamięci.
+  - Dowód DI: ten sam service działa z obiema implementacjami bez zmiany swojego kodu; wybór i składanie zależności odbywa się poza service. Kontrakt i wywołujący muszą poprawnie obsługiwać asynchroniczne I/O.

 **Checkpoint:** Rozumiesz, co zwraca funkcja `async`, gdzie powinno być `await`, jak przechwycić odrzucony Promise i dlaczego integracja z systemem plików utrudnia testy, jeśli nie zadbasz o izolację.

@@ -209,11 +217,16 @@ Codex ma dawać Ci **po jednym podzadaniu**, a nie wszystko za jednym razem. Che
 ### ETAP 5 — Testy jednostkowe (Vitest)

 - [ ] **5.1** Skonfiguruj Vitest i pierwszy samodzielny test czystej funkcji.
+  - Wskaż części Arrange–Act–Assert we własnym teście; nazwa opisuje zachowanie, a asercja wykrywa jego naruszenie. Nie wymaga się komentarzy AAA w każdym teście.
 - [ ] **5.2** Przetestuj tworzenie issue: wartości domyślne, poprawne dane, ograniczenia pól.
+  - Przed kodem sam zaprojektuj tabelę przypadków z wynikiem i uzasadnieniem: Equivalence Partitioning (klasy danych poprawnych i niepoprawnych) oraz Boundary Value Analysis (tytuł po trim: 2/3/100/101, opis: 1000/1001). Rozróżnij happy path, negative path i edge case. W unit sprawdzaj reguły należące do domeny; walidację surowego JSON sprawdzaj w 6.3, bez kopiowania identycznych testów między poziomami.
 - [ ] **5.3** Przetestuj aktualizację: tylko wybrane pola, brak mutacji oryginalnego obiektu, zmiana `updatedAt`.
 - [ ] **5.4** Przetestuj operacje serwisu z kontrolowanym repository (bez HTTP i bez prawdziwego pliku).
+  - Wykorzystaj repository w pamięci jako fake i `vi.fn()` jako kontrolowaną zależność zwracającą ustalony wynik (stub) oraz rejestrującą wywołania. Dla jednej istotnej operacji sprawdź argumenty i liczbę wywołań; dla odrzuconej operacji repository sprawdź zachowanie service. Użyj `vi.spyOn()` do obserwacji jednej rzeczywistej metody i przywróć ją po teście. Wyjaśnij mock (oczekiwane interakcje), stub (ustalone odpowiedzi), spy (obserwacja) i fake (uproszczona działająca implementacja); jedno narzędzie może pełnić różne role. Asercje interakcji mają wynikać z odpowiedzialności service, nie z prywatnych szczegółów implementacji.
+  - Testy asynchroniczne oczekują na wynik lub zwracają Promise do runnera, w tym dla asercji odrzucenia. Pokaż osobne deterministyczne scenariusze resolve i reject. W kontrolowanym ćwiczeniu pomiń `await` przy asercji asynchronicznej, rozpoznaj fałszywy sukces albo komunikat runnera i przywróć poprawny test; nie pozostawiaj wadliwego testu w zestawie.
 - [ ] **5.5** Wprowadź czytelne fabryki danych testowych, zamiast wklejać ten sam obiekt do każdego testu.
 - [ ] **5.6** Doprowadź testy do niezależności — kolejność uruchomienia nie może zmieniać wyniku.
+  - Kontroluj czas i ID tam, gdzie wpływają na asercje; nie używaj oczekiwania przez sleep. Każdy test otrzymuje własny stan, spy/mocks są odpowiednio czyszczone lub przywracane. Sprawdź wybrany test osobno i cały zestaw, a dla JSON także sprzątanie katalogów tymczasowych. Wyjaśnij różnicę między czyszczeniem historii wywołań a przywróceniem oryginalnej metody.

 **Checkpoint:** Potrafisz wyjaśnić `describe`, `it/test`, `expect`, `beforeEach`, fake/test double, happy path, negative path, boundary case.

@@ -222,12 +235,14 @@ Codex ma dawać Ci **po jednym podzadaniu**, a nie wszystko za jednym razem. Che
 - [ ] **6.1** Napisz pierwszy test `GET /health`, bez uruchamiania serwera ręcznie.
 - [ ] **6.2** Napisz test `POST /issues`: poprawne body → `201`, wymagane pola i wartości domyślne.
 - [ ] **6.3** Przetestuj błędy `POST`: brak tytułu, same spacje, za krótki/długi tytuł, niedozwolony priority, nieznane pola.
+  - Rozszerz tabelę z 5.2 o klasy surowych danych HTTP, np. błędny typ pola, oraz sam dobierz reprezentantów. Zastosuj `test.each` do jednej jednorodnej grupy przypadków walidacji; każdy przypadek ma czytelną nazwę i sprawdzalny wynik. Uwzględnij wartości tuż poniżej, na i powyżej granic; nie parametryzuj na siłę różnych scenariuszy CRUD.
 - [ ] **6.4** Przetestuj `GET /issues` i `GET /issues/:id`, również pustą listę, nieprawidłowe ID i brak istniejącego ID.
 - [ ] **6.5** Przetestuj `PATCH`: zmiana części pól, pusty obiekt i niepoprawne wartości.
 - [ ] **6.6** Przetestuj `DELETE`: `204`, brak body i `404` przy próbie usunięcia drugi raz.
 - [ ] **6.7** Przetestuj filtrowanie po jednym filtrze, dwóch filtrach i niedozwolonym filtrze.
 - [ ] **6.8** Napisz przynajmniej jeden pełny scenariusz CRUD: create → read → update → delete → read (`404`).
 - [ ] **6.9** Sprawdź izolację danych testowych: każdy test zaczyna z ustalonym stanem, bez zależności od innych testów i od zewnętrznego API.
+  - Kryteria odpowiedzi dla 6.1–6.8: sprawdzaj status i istotne wartości/typy oraz strukturę `data` lub `error`, a nie sam status. Dla odpowiedzi JSON sprawdź `Content-Type`, dla DELETE brak body. Pokaż 500 przez kontrolowane odrzucenie zależności i sprawdź brak stack trace. Błąd sieciowy klienta jest ćwiczony w 3.8, nie przez niestabilne połączenie w Supertest.

 **Checkpoint:** Umiesz powiedzieć, co testuje jednostka, co testuje endpoint, dlaczego testy wymagają izolacji i czym różni się test negatywny od pozytywnego.

@@ -236,7 +251,7 @@ Codex ma dawać Ci **po jednym podzadaniu**, a nie wszystko za jednym razem. Che
 - [ ] **7.1** Dodaj skrypty: `dev`, `typecheck`, `lint`, `format:check`, `test`, `build` (jeśli stosujesz kompilację).
 - [ ] **7.2** Przygotuj workflow GitHub Actions uruchamiany na `push` i `pull_request`. Użyj Node 24 i `npm ci`.
 - [ ] **7.3** W CI uruchom: sprawdzanie typów, lint, format, testy i ewentualnie build.
-- [ ] **7.4** Celowo wprowadź lokalnie prosty błąd i zobacz, który test/check go wykrywa. Następnie cofnij błąd.
+- [ ] **7.4** Na osobnej gałęzi celowo wprowadź mały błąd wykrywany przez istniejący test i odtwórz go lokalnie. Sam odczytaj komunikat i stack trace, wskaż istotną ramkę własnego kodu, postaw hipotezę i użyj breakpointu w TS do sprawdzenia wartości podczas testu. Zapisz w opisie PR objaw, przyczynę i dowód naprawy. Pokaż nieudany run GitHub Actions na tej gałęzi: wskaż job, krok, komendę i fragment logu wyjaśniający błąd. Napraw błąd własnoręcznie, uzyskaj zielony run i dopiero wtedy wykonaj merge PR. Dowód obejmuje branch, małe commity, link do PR oraz czerwonego i zielonego runu; nie psuj celowo gałęzi domyślnej.
 - [ ] **7.5** Sprawdź, czy repozytorium nie zawiera `node_modules`, lokalnego pliku z danymi, sekretów ani przypadkowych plików środowiskowych.

 **Checkpoint:** Potrafisz wyjaśnić, co dzieje się w CI po `push`, jak odczytać log błędu i dlaczego „testy przechodzą u mnie” nie wystarcza.
@@ -250,6 +265,13 @@ Codex ma dawać Ci **po jednym podzadaniu**, a nie wszystko za jednym razem. Che
 - [ ] **8.5** Pokaż widoczny status CI, uporządkuj historię commitów i upewnij się, że świeży klon repozytorium można uruchomić wyłącznie według README.
 - [ ] **8.6** Przygotuj 2-minutowy opis projektu po angielsku i samodzielnie odpowiedz na pytania z sekcji 7.
 - [ ] **8.7** Dodaj krótką, uczciwą informację o użyciu AI: Codex dawał zadania, wskazówki i code review; kod implementowałeś samodzielnie, jeśli rzeczywiście tak było. Nie deklaruj „zero AI”.
+- [ ] **8.8** Wykonaj końcowe zadanie samodzielności opisane poniżej. To konkretna weryfikacja istniejącego warunku dopisania małej zmiany i testów, nie nowy moduł.
+
+**Zadanie 8.8 — jeden nowy filtr listy:** dodaj opcjonalny query parameter `titleContains` w istniejącym `GET /issues`. Wartość ma być pojedynczym stringiem, po trim długości 1–100 znaków; dopasowanie jest niewrażliwe na wielkość liter i szuka dosłownego fragmentu tytułu. Błędny typ, powtórzony parametr, pusty tekst i przekroczona długość oznaczają 400 w istniejącym formacie błędu. Filtr łączy się ze `status` i `priority` przez AND; brak parametru zachowuje obecne zachowanie, brak wyników daje 200 z pustą tablicą, kolejność dodawania pozostaje zachowana. Nie dodawaj paginacji, sortowania ani wyrażeń regularnych.
+
+**Warunki przeprowadzenia 8.8:** mentor przed rozpoczęciem porównuje wymaganie z historią zadań/PR i ćwiczeń; samo przeczytanie specyfikacji nie jest wykonaniem zadania. Nie ćwiczymy identycznego filtra wcześniej. Jeżeli użytkownik już go implementował, przed próbą zastępujemy go jednym równie małym, niećwiczonym wymaganiem i zapisujemy jego kontrakt; nie zaliczamy znanej implementacji jako transferu.
+
+**Kryteria 8.8:** użytkownik sam interpretuje wymagania, zapisuje plan i tabelę przypadków przed implementacją, wybiera moduły, implementuje zmianę oraz adekwatne unit/API tests, sam uruchamia sprawdzenia i diagnozuje błędy. Przedstawia diff, wyniki, wyjaśnienie decyzji, regresji i poziom pomocy. Jeśli nie napotka błędu, przeprowadza krótką kontrolowaną próbę z błędem w nowej zmianie i diagnozuje go, a następnie przywraca poprawne zachowanie. Oficjalna dokumentacja jest dozwolona; AI domyślnie dopiero robi końcowe review, bez oceny planu, listy przypadków, sygnatur ani kroków implementacji przed próbą. Pomoc na wyraźną prośbę jest dozwolona, ale odnotowana; po prowadzeniu krok po kroku dowód samodzielności wymaga kolejnej równie małej, nowej próby. Wszystkie wymagania kontraktu muszą być pokryte uzasadnionymi przypadkami, dotychczasowe testy i CI przechodzą, użytkownik sam wprowadza poprawki z review i potrafi wyjaśnić kod bez AI.

 **Checkpoint:** Z pamięci umiesz wyjaśnić architekturę i testy oraz samodzielnie naprawić celowo wprowadzony błąd.

@@ -291,6 +313,7 @@ Możesz przejść **w pełni do Playwrighta**, gdy spełniasz WSZYSTKIE poniższ
 - [ ] Endpointy CRUD działają zgodnie z kontraktem, a błędy mają właściwe statusy.
 - [ ] Samodzielnie wykorzystujesz `async/await`, `try/catch` i moduły TS.
 - [ ] Potrafisz dopisać nową funkcję i test bez prowadzenia krok po kroku przez AI.
+  - Dowód: zadanie 8.8 oraz praktyczne dowody umiejętności z matrycy w `AUDIT.md`; same odpowiedzi na quiz nie zastępują wykonania zadań.
 - [ ] Masz działające unit + API integration tests i umiesz wyjaśnić 3 wybrane asercje.
 - [ ] Testy są izolowane i deterministyczne.
 - [ ] Pipeline GitHub Actions przechodzi na domyślnej gałęzi.
diff --git a/ROADMAP.md b/ROADMAP.md
index dfe196a..bc9fd8f 100644
--- a/ROADMAP.md
+++ b/ROADMAP.md
@@ -6,23 +6,25 @@ To projekt #2, który rozpoczniesz **w poniedziałek 12 października 2026 r.**,

 **Cel nie jest taki, by zostać backend developerem.** Masz nauczyć się samodzielnie pisać TypeScript i testy, rozumieć HTTP oraz pracować z błędami, żeby później przejść bez osobnego kursu na **Playwright + TypeScript**.

-Pełny zakres oraz wszystkie podzadania (`0.1`–`8.7`) są zapisane w `PROJECT.md`. Ten dokument to wyłącznie mapa etapów. **Nie odhaczaj zadań tutaj — jedno źródło prawdy to `PROJECT.md`.**
+Pełny zakres oraz wszystkie podzadania (`0.1`–`8.8`) są zapisane w `PROJECT.md`. Ten dokument to wyłącznie mapa etapów. **Nie odhaczaj zadań tutaj — jedno źródło prawdy to `PROJECT.md`.** Matryca umiejętności i dowodów znajduje się w `AUDIT.md`.

 ## Etapy i orientacyjny nakład pracy

 | Etap | Temat | Efekt etapu | Szacunkowo |
 |---|---|---|---:|
-| 0 | Repozytorium, Node i TS | Projekt uruchamia się i przechodzi typecheck | 2–4 h |
+| 0 | Repozytorium, Node i TS | Projekt uruchamia się, przechodzi typecheck i zatrzymuje na breakpoincie TS | 2–4 h |
 | 1 | Typy i model Issue | Tworzenie/aktualizacja obiektów, zasady domeny | 4–7 h |
-| 2 | Repository i service | CRUD oraz filtry bez HTTP | 5–8 h |
-| 3 | Express, HTTP, Zod | Działające endpointy REST i walidacja | 7–11 h |
-| 4 | `async/await`, JSON | Odczyt/zapis danych i obsługa I/O | 5–9 h |
-| 5 | Vitest — unit | Samodzielne testy logiki biznesowej | 6–9 h |
-| 6 | Vitest + Supertest — API | Testy pozytywne, negatywne i CRUD E2E na poziomie API | 8–12 h |
-| 7 | GitHub Actions | Automatyczne uruchamianie jakości i testów | 3–5 h |
-| 8 | README i rozmowa | Portfolio, dokumentacja, świadome decyzje | 3–5 h |
+| 2 | Repository i service | CRUD, klasy, konstruktory i DI przez kontrakt | 6–9 h |
+| 3 | Express, HTTP, Zod | Endpointy REST, walidacja i mały klient fetch | 8–12 h |
+| 4 | `async/await`, JSON | I/O, sprzątanie, odrzucenia i współbieżne niezależne odczyty | 6–10 h |
+| 5 | Vitest — unit | AAA, EP/BVA, test doubles i testy async | 8–12 h |
+| 6 | Vitest + Supertest — API | Walidacja odpowiedzi, test.each, CRUD i izolacja | 9–13 h |
+| 7 | GitHub Actions | Debugging TS, diagnoza czerwonego CI, branch/PR/merge | 4–7 h |
+| 8 | README i rozmowa | Portfolio i praktyczna próba samodzielności | 5–8 h |

-**Bazowy szacunek: około 43–70 godzin.** Z dodatkowymi samodzielnymi próbami, powtórkami i ćwiczeniami transferowymi realnie może to być **50–85 godzin**, czyli około 25–43 dni przy 2 godzinach dziennie. Nie traktuj tego jako deadline. Nie rozszerzaj zakresu backendu tylko dlatego, że idzie wolniej.
+**Deadline pozostaje 31.10.2026.** Od 12 do 31 października włącznie są 20 dni, czyli 40 h przy codziennych 2 h nauki (mniej przy dniach wolnych). Dotychczasowe 43–70 h już przekraczało ten budżet. Po audycie szacunek planistyczny sumy etapów to **52–82 h**, a z poprawkami, powtórkami i transferem **60–95 h**. To oszacowanie, nie zmierzony czas; nakład ponownie oceniamy po etapach 0–2.
+
+**Konflikt:** przy 2 h dziennie pełna ścieżka do deadline'u nie jest realistycznym założeniem. Potrzebne byłoby średnio 2,6–4,1 h dziennie na bazowy zakres lub około 3–4,75 h z buforem. Nie zakładamy automatycznie, że użytkownik ma ten czas. Zachowujemy termin i wymagania, zgłaszamy ryzyko zamiast skreślać testy/OOP/debugging lub deklarować gotowość bez dowodów. Łączymy ćwiczenia z istniejącymi zadaniami, unikamy duplikatów, odkładamy wszystkie BONUS-y. Nie rozszerzaj zakresu backendu tylko dlatego, że idzie wolniej.

 ## Jak będzie malało wsparcie AI?

@@ -36,10 +38,13 @@ Nie opieraj przejścia do Playwrighta na zero-jedynkowym „nigdy nie korzystał
 ## Kamienie milowe

 - **Po etapie 2:** potrafisz zbudować logikę CRUD bez frameworka HTTP.
+  Potrafisz też wyjaśnić klasę, instancję, konstruktor, enkapsulację i wstrzyknięcie zależności przez kontrakt.
 - **Po etapie 3:** umiesz wysłać request, odczytać response i wyjaśnić kody HTTP.
 - **Po etapie 4:** rozumiesz `async/await`, Promise, `try/catch` i nie ukrywasz błędów I/O.
+  Pokazujesz sprzątanie w `finally` i uzasadniasz wybór między sekwencją a `Promise.all` bez współbieżnych zapisów do jednego JSON.
 - **Po etapie 6:** testujesz API automatycznie i diagnozujesz porażki testów.
 - **Po etapie 8:** masz repozytorium gotowe do pokazania rekruterowi i możesz rozpocząć projekt Playwright.
+  Dowodem transferu jest 8.8 wykonane samodzielnie oraz praktyczne kryteria z `AUDIT.md`, a nie sam quiz.

 ## Zasada priorytetów

diff --git a/AUDIT.md b/AUDIT.md
new file mode 100644
index 0000000..a4de6f3
--- /dev/null
+++ b/AUDIT.md
@@ -0,0 +1,64 @@
+# Końcowy audyt edukacyjny specyfikacji — 2026-10-11
+
+Cel: ostatni projekt TypeScript przed Playwright + TypeScript, przygotowujący do dalszej nauki i pracy Junior Test Automation Engineer. Audyt obejmuje wymagania w AGENTS.md, PROJECT.md, ROADMAP.md i PROGRESS.md, a nie zaliczenie umiejętności użytkownika ani review działającej aplikacji.
+
+## Wynik audytu stanu zastanego
+
+- **Ćwiczone w dotychczasowych wymaganiach:** CRUD, model i typy, kontrolowane ID/czas (1.3), kontrakt repository i separacja warstw (2.1–2.3), HTTP i Zod (3.1–3.7), Promise/async i błędy I/O (4.1–4.5), happy/negative/boundary tests (5.2–5.4, 6.2–6.8), fixtures i izolacja (5.5–5.6, 6.9), CI i lokalne wykrywanie błędu (7.2–7.4).
+- **Częściowe pokrycie:** graniczne dane były wymienione, ale bez samodzielnego EP/BVA; kontrolowane repository bez praktyki vi.fn/vi.spyOn; async bez kryteriów testowania odrzuceń i brakującego await; HTTP bez klienta fetch i jawnej kontroli headers; debugging/CI bez breakpointów i diagnozy faktycznie czerwonego runu. Końcowa samodzielność była deklarowanym warunkiem bez osobnego, sprawdzalnego zadania.
+- **Brak jawnych zadań:** AAA, test.each, finally, Promise.all versus sekwencja, branch/PR/merge. W odczytanych plikach nie było także wcześniejszych zapisów o klasach, konstruktorach, OOP i DI ani deadline'u. Nie ma podstaw do odtworzenia ich dokładnego wcześniejszego brzmienia; zgodnie z bieżącą prośbą obowiązkowe OOP/DI i termin zostały wpisane jawnie.
+- **Stan nauki:** 0.1 potwierdzono w rozmowie; 0.2 jest w toku. Dokumenty nie dowodzą opanowania dalszych umiejętności. Checkboxy nie zostały odhaczone w ramach audytu.
+
+## Decyzje aktualizacji
+
+Rozszerzono istniejące kryteria zamiast tworzyć drugi kurs. Klasy dotyczą repository i service, DI służy wymianie realnych zależności. AAA/EP/BVA/doubles ćwiczone są na istniejących testach; sprzątanie i współbieżność na jednym minićwiczeniu I/O. Jedna usterka w 7.4 służy równocześnie debuggingowi, Git i diagnozie CI. Nowe zadania to tylko mały klient fetch (3.8) i konkretyzacja istniejącego warunku transferu (8.8).
+
+Walidacja domeny i surowego JSON mają różne odpowiedzialności: nie kopiujemy całej tej samej matrycy między unit a integration. Nie testujemy każdego prywatnego wywołania; interakcje doubles mają znaczenie dla kontraktu. Mechanizmy poznawane w minićwiczeniu nie muszą być później sztucznie dodawane do produkcyjnej logiki API.
+
+Nie dodano Playwrighta, Allure, MCP, Reacta, Dockera, SQL, logowania, nowego dużego modułu ani implementacji aplikacji. Etapy pozostają 0–8. Wskazówki i review zachowano, z końcową próbą bez prowadzenia przed samodzielnym wykonaniem.
+
+## Matryca: umiejętność → zadanie → sposób weryfikacji
+
+To mapowanie kryteriów z PROJECT.md, nie druga checklista. Wszystkie poniższe umiejętności wymagają dowodu po wykonaniu, nie samej obecności w specyfikacji.
+
+| Umiejętność | Zadanie | Sposób weryfikacji |
+|---|---|---|
+| Klasy, instancje, konstruktor, this, enkapsulacja | 2.2, 2.3, 4.2 | Własne klasy repository/service, dwie niezależne instancje, wyjaśnienie stanu i konstruktora |
+| OOP: kompozycja i kontrakt | 2.1–2.3 | Service korzysta z kontraktu; użytkownik uzasadnia separację i kompozycję bez wymuszonego dziedziczenia |
+| Dependency injection | 2.3, 4.5, 5.4 | Ten sam service działa z memory/JSON/test double bez zmiany kodu; zależności przekazane z zewnątrz |
+| Equivalence Partitioning | 5.2, 6.3 | Samodzielna tabela klas danych, reprezentantów i oczekiwanych wyników przed testami |
+| Boundary Value Analysis | 5.2, 6.3 | Przypadki 2/3/100/101 po trim oraz 1000/1001 dla opisu z uzasadnieniem poziomu testu |
+| Happy path, negative path, edge cases | 5.2, 6.3–6.8 | Własne przykłady, przypisanie kategorii i asercje wykrywające naruszenie kontraktu |
+| Arrange–Act–Assert | 5.1 | Wskazanie trzech części własnego testu i wyjaśnienie odpowiedzialności asercji |
+| Samodzielne projektowanie testów | 5.2, 6.3, 8.8 | Tabela przed kodem; dobór danych i wyników przez użytkownika; w 8.8 bez wcześniejszej oceny AI |
+| Testy parametryzowane test.each | 6.3 | Jedna jednorodna grupa walidacji z czytelnymi nazwami i niezależnymi przypadkami |
+| Mock, stub, spy, fake — różnice | 5.4 | Wskazanie ról we własnych doubles i uzasadnienie ich wyboru; narzędzie nie determinuje roli |
+| vi.fn() | 5.4 | Kontrolowany wynik zależności i rejestracja interakcji w teście service |
+| vi.spyOn() | 5.4, 5.6 | Obserwacja rzeczywistej metody oraz przywrócenie jej po teście |
+| Kontrola zależności, wywołania i argumenty | 1.3, 5.4 | Kontrolowane ID/czas, argumenty/liczba wywołań istotnej operacji, sukces i odrzucenie repository |
+| Deterministyczność i izolacja | 5.6, 6.9 | Własny stan testu, kontrolowane ID/czas, cleanup doubles/katalogów, test osobno i w zestawie |
+| Promise i async/await | 4.1–4.5 | Wyniki ćwiczenia I/O i repository JSON; wyjaśnienie wyniku funkcji async i zależności operacji |
+| Odrzucone Promise | 4.1, 4.4, 5.4 | Obsłużony błąd I/O oraz test reject kontrolowanej zależności, bez cichej pustej bazy |
+| try/catch/finally | 4.1 | Sukces i błąd z dowodem sprzątania w obu ścieżkach; uzasadnienie finally |
+| Promise.all i sekwencja/współbieżność | 4.1 | Dwa niezależne odczyty obiema metodami, wyjaśnienie zależnych operacji i braku anulowania; bez pomiarów czasu jako asercji |
+| Testowanie funkcji async i brak await | 5.4 | Test resolve/reject czeka na asercję; diagnoza i poprawa kontrolowanego pominięcia await |
+| Podstawy HTTP, metody i statusy | 3.1–3.7 | Odczyt własnych request/response, wyjaśnienie 200/201/204/400/404/500 i przepływu HTTP |
+| Body, query, path parameters i headers | 3.7 | Wskazanie elementów w requestach POST, GET po ID i filtrowanej liście |
+| Content-Type i JSON | 3.7, 3.8, 6.9 | Wysłany nagłówek JSON, odczyt/sprawdzenie Content-Type odpowiedzi, brak parsowania pustego 204 |
+| Walidacja odpowiedzi API | 6.2–6.9 | Status, struktura i istotne pola data/error, wartości domyślne, UUID/daty według kontraktu, brak body przy 204 |
+| Błędy HTTP i sieciowe | 3.8, 6.9 | Różnica odpowiedzi 400/404 i odrzucenia fetch przy zatrzymanym serwerze; kontrolowany 500 bez stack trace |
+| Natywny fetch jako klient | 3.8 | Lokalny POST i odczyt po ID, interpretacja ok/status/JSON, wyniki sukcesu i obu rodzajów błędów |
+| Breakpointy VS Code i debugging TS | 0.3, 7.4 | Zatrzymanie w .ts, lokalna wartość/call stack/krok, potem sprawdzenie hipotezy podczas testu |
+| Stack trace i komunikaty błędów | 7.4 | Własna ramka kodu, objaw → hipoteza → przyczyna → dowód naprawy w opisie PR |
+| Samodzielna diagnoza testu | 7.4, 8.8 | Lokalna reprodukcja, sprawdzenie przyczyny, własna poprawka i ponowne przejście testu |
+| Git branch, commit, PR, merge | 0.1, 7.4 | Osobna gałąź, spójne commity, PR z diagnozą, merge po zielonym CI |
+| Nieudany pipeline GitHub Actions | 7.4 | Link do czerwonego i zielonego runu, identyfikacja job/krok/komenda/log oraz związku z poprawką |
+| Transfer i wyjaśnienie decyzji | 8.8 | Sprawdzenie nowości wymagania, własny plan/implementacja/testy/debugging, diff i wyniki, końcowe review i wyjaśnienie bez AI |
+
+## Termin i ograniczenia oceny
+
+31.10.2026 pozostaje deadline'em. Przy 2 h codziennie od 12.10 dostępne jest 40 h. Nowy bazowy szacunek 52–82 h i 60–95 h z buforem oznacza konflikt czasu; szczegóły i założenia są w ROADMAP.md. Nie rozstrzygamy go przez usunięcie praktycznych zadań lub przyspieszenie zaliczeń.
+
+O wcześniejszych zmianach OOP/DI wiadomo z bieżącej prośby, ale ich wersji nie ma w odczytanych dokumentach. Audyt zapewnia obowiązkowe pokrycie tych tematów, bez twierdzenia, że odtworzono nieznane szczegóły. Nowość zadania 8.8 zostanie ostatecznie zweryfikowana tuż przed próbą na podstawie rzeczywistej historii nauki.
+
+Pełny diff czterech aktualizowanych dokumentów: `AUDIT_DIFF.md`. AUDIT.md i AUDIT_DIFF.md są nowymi artefaktami audytu; nie stanowią zadań implementacyjnych ani dokumentacji API.
```
