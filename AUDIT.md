# Końcowy audyt edukacyjny specyfikacji — 2026-10-11

Cel: ostatni projekt TypeScript przed Playwright + TypeScript, przygotowujący do dalszej nauki i pracy Junior Test Automation Engineer. Audyt obejmuje wymagania w AGENTS.md, PROJECT.md, ROADMAP.md i PROGRESS.md, a nie zaliczenie umiejętności użytkownika ani review działającej aplikacji.

## Wynik audytu stanu zastanego

- **Ćwiczone w dotychczasowych wymaganiach:** CRUD, model i typy, kontrolowane ID/czas (1.3), kontrakt repository i separacja warstw (2.1–2.3), HTTP i Zod (3.1–3.7), Promise/async i błędy I/O (4.1–4.5), happy/negative/boundary tests (5.2–5.4, 6.2–6.8), fixtures i izolacja (5.5–5.6, 6.9), CI i lokalne wykrywanie błędu (7.2–7.4).
- **Częściowe pokrycie:** graniczne dane były wymienione, ale bez samodzielnego EP/BVA; kontrolowane repository bez praktyki vi.fn/vi.spyOn; async bez kryteriów testowania odrzuceń i brakującego await; HTTP bez klienta fetch i jawnej kontroli headers; debugging/CI bez breakpointów i diagnozy faktycznie czerwonego runu. Końcowa samodzielność była deklarowanym warunkiem bez osobnego, sprawdzalnego zadania.
- **Brak jawnych zadań:** AAA, test.each, finally, Promise.all versus sekwencja, branch/PR/merge. W odczytanych plikach nie było także wcześniejszych zapisów o klasach, konstruktorach, OOP i DI ani deadline'u. Nie ma podstaw do odtworzenia ich dokładnego wcześniejszego brzmienia; zgodnie z bieżącą prośbą obowiązkowe OOP/DI i termin zostały wpisane jawnie.
- **Stan nauki:** 0.1 potwierdzono w rozmowie; 0.2 jest w toku. Dokumenty nie dowodzą opanowania dalszych umiejętności. Checkboxy nie zostały odhaczone w ramach audytu.

## Decyzje aktualizacji

Rozszerzono istniejące kryteria zamiast tworzyć drugi kurs. Klasy dotyczą repository i service, DI służy wymianie realnych zależności. AAA/EP/BVA/doubles ćwiczone są na istniejących testach; sprzątanie i współbieżność na jednym minićwiczeniu I/O. Jedna usterka w 7.4 służy równocześnie debuggingowi, Git i diagnozie CI. Nowe zadania to tylko mały klient fetch (3.8) i konkretyzacja istniejącego warunku transferu (8.8).

Walidacja domeny i surowego JSON mają różne odpowiedzialności: nie kopiujemy całej tej samej matrycy między unit a integration. Nie testujemy każdego prywatnego wywołania; interakcje doubles mają znaczenie dla kontraktu. Mechanizmy poznawane w minićwiczeniu nie muszą być później sztucznie dodawane do produkcyjnej logiki API.

Nie dodano Playwrighta, Allure, MCP, Reacta, Dockera, SQL, logowania, nowego dużego modułu ani implementacji aplikacji. Etapy pozostają 0–8. Wskazówki i review zachowano, z końcową próbą bez prowadzenia przed samodzielnym wykonaniem.

## Matryca: umiejętność → zadanie → sposób weryfikacji

To mapowanie kryteriów z PROJECT.md, nie druga checklista. Wszystkie poniższe umiejętności wymagają dowodu po wykonaniu, nie samej obecności w specyfikacji.

| Umiejętność | Zadanie | Sposób weryfikacji |
|---|---|---|
| Klasy, instancje, konstruktor, this, enkapsulacja | 2.2, 2.3, 4.2 | Własne klasy repository/service, dwie niezależne instancje, wyjaśnienie stanu i konstruktora |
| OOP: kompozycja i kontrakt | 2.1–2.3 | Service korzysta z kontraktu; użytkownik uzasadnia separację i kompozycję bez wymuszonego dziedziczenia |
| Dependency injection | 2.3, 4.5, 5.4 | Ten sam service działa z memory/JSON/test double bez zmiany kodu; zależności przekazane z zewnątrz |
| Equivalence Partitioning | 5.2, 6.3 | Samodzielna tabela klas danych, reprezentantów i oczekiwanych wyników przed testami |
| Boundary Value Analysis | 5.2, 6.3 | Przypadki 2/3/100/101 po trim oraz 1000/1001 dla opisu z uzasadnieniem poziomu testu |
| Happy path, negative path, edge cases | 5.2, 6.3–6.8 | Własne przykłady, przypisanie kategorii i asercje wykrywające naruszenie kontraktu |
| Arrange–Act–Assert | 5.1 | Wskazanie trzech części własnego testu i wyjaśnienie odpowiedzialności asercji |
| Samodzielne projektowanie testów | 5.2, 6.3, 8.8 | Tabela przed kodem; dobór danych i wyników przez użytkownika; w 8.8 bez wcześniejszej oceny AI |
| Testy parametryzowane test.each | 6.3 | Jedna jednorodna grupa walidacji z czytelnymi nazwami i niezależnymi przypadkami |
| Mock, stub, spy, fake — różnice | 5.4 | Wskazanie ról we własnych doubles i uzasadnienie ich wyboru; narzędzie nie determinuje roli |
| vi.fn() | 5.4 | Kontrolowany wynik zależności i rejestracja interakcji w teście service |
| vi.spyOn() | 5.4, 5.6 | Obserwacja rzeczywistej metody oraz przywrócenie jej po teście |
| Kontrola zależności, wywołania i argumenty | 1.3, 5.4 | Kontrolowane ID/czas, argumenty/liczba wywołań istotnej operacji, sukces i odrzucenie repository |
| Deterministyczność i izolacja | 5.6, 6.9 | Własny stan testu, kontrolowane ID/czas, cleanup doubles/katalogów, test osobno i w zestawie |
| Promise i async/await | 4.1–4.5 | Wyniki ćwiczenia I/O i repository JSON; wyjaśnienie wyniku funkcji async i zależności operacji |
| Odrzucone Promise | 4.1, 4.4, 5.4 | Obsłużony błąd I/O oraz test reject kontrolowanej zależności, bez cichej pustej bazy |
| try/catch/finally | 4.1 | Sukces i błąd z dowodem sprzątania w obu ścieżkach; uzasadnienie finally |
| Promise.all i sekwencja/współbieżność | 4.1 | Dwa niezależne odczyty obiema metodami, wyjaśnienie zależnych operacji i braku anulowania; bez pomiarów czasu jako asercji |
| Testowanie funkcji async i brak await | 5.4 | Test resolve/reject czeka na asercję; diagnoza i poprawa kontrolowanego pominięcia await |
| Podstawy HTTP, metody i statusy | 3.1–3.7 | Odczyt własnych request/response, wyjaśnienie 200/201/204/400/404/500 i przepływu HTTP |
| Body, query, path parameters i headers | 3.7 | Wskazanie elementów w requestach POST, GET po ID i filtrowanej liście |
| Content-Type i JSON | 3.7, 3.8, 6.9 | Wysłany nagłówek JSON, odczyt/sprawdzenie Content-Type odpowiedzi, brak parsowania pustego 204 |
| Walidacja odpowiedzi API | 6.2–6.9 | Status, struktura i istotne pola data/error, wartości domyślne, UUID/daty według kontraktu, brak body przy 204 |
| Błędy HTTP i sieciowe | 3.8, 6.9 | Różnica odpowiedzi 400/404 i odrzucenia fetch przy zatrzymanym serwerze; kontrolowany 500 bez stack trace |
| Natywny fetch jako klient | 3.8 | Lokalny POST i odczyt po ID, interpretacja ok/status/JSON, wyniki sukcesu i obu rodzajów błędów |
| Breakpointy VS Code i debugging TS | 0.3, 7.4 | Zatrzymanie w .ts, lokalna wartość/call stack/krok, potem sprawdzenie hipotezy podczas testu |
| Stack trace i komunikaty błędów | 7.4 | Własna ramka kodu, objaw → hipoteza → przyczyna → dowód naprawy w opisie PR |
| Samodzielna diagnoza testu | 7.4, 8.8 | Lokalna reprodukcja, sprawdzenie przyczyny, własna poprawka i ponowne przejście testu |
| Git branch, commit, PR, merge | 0.1, 7.4 | Osobna gałąź, spójne commity, PR z diagnozą, merge po zielonym CI |
| Nieudany pipeline GitHub Actions | 7.4 | Link do czerwonego i zielonego runu, identyfikacja job/krok/komenda/log oraz związku z poprawką |
| Transfer i wyjaśnienie decyzji | 8.8 | Sprawdzenie nowości wymagania, własny plan/implementacja/testy/debugging, diff i wyniki, końcowe review i wyjaśnienie bez AI |

## Termin i ograniczenia oceny

31.10.2026 pozostaje deadline'em. Przy 2 h codziennie od 12.10 dostępne jest 40 h. Nowy bazowy szacunek 52–82 h i 60–95 h z buforem oznacza konflikt czasu; szczegóły i założenia są w ROADMAP.md. Nie rozstrzygamy go przez usunięcie praktycznych zadań lub przyspieszenie zaliczeń.

O wcześniejszych zmianach OOP/DI wiadomo z bieżącej prośby, ale ich wersji nie ma w odczytanych dokumentach. Audyt zapewnia obowiązkowe pokrycie tych tematów, bez twierdzenia, że odtworzono nieznane szczegóły. Nowość zadania 8.8 zostanie ostatecznie zweryfikowana tuż przed próbą na podstawie rzeczywistej historii nauki.

Pełny diff czterech aktualizowanych dokumentów: `AUDIT_DIFF.md`. AUDIT.md i AUDIT_DIFF.md są nowymi artefaktami audytu; nie stanowią zadań implementacyjnych ani dokumentacji API.
