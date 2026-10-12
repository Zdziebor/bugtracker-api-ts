# ROADMAP.md — mapa nauki (BugTracker API)

## Co jest celem?

To projekt #2, który rozpoczniesz **w poniedziałek 12 października 2026 r.**, po domknięciu `watchlist-ts`.

**Cel nie jest taki, by zostać backend developerem.** Masz nauczyć się samodzielnie pisać TypeScript i testy, rozumieć HTTP oraz pracować z błędami, żeby później przejść bez osobnego kursu na **Playwright + TypeScript**.

Pełny zakres oraz wszystkie podzadania (`0.1`–`8.8`) są zapisane w `PROJECT.md`. Ten dokument to wyłącznie mapa etapów. **Nie odhaczaj zadań tutaj — jedno źródło prawdy to `PROJECT.md`.** Matryca umiejętności i dowodów znajduje się w `AUDIT.md`.

## Etapy i orientacyjny nakład pracy

| Etap | Temat                    | Efekt etapu                                                                 | Szacunkowo |
| ---- | ------------------------ | --------------------------------------------------------------------------- | ---------: |
| 0    | Repozytorium, Node i TS  | Projekt uruchamia się, przechodzi typecheck i zatrzymuje na breakpoincie TS |      2–4 h |
| 1    | Typy i model Issue       | Tworzenie/aktualizacja obiektów, zasady domeny                              |      4–7 h |
| 2    | Repository i service     | CRUD, klasy, konstruktory i DI przez kontrakt                               |      6–9 h |
| 3    | Express, HTTP, Zod       | Endpointy REST, walidacja i mały klient fetch                               |     8–12 h |
| 4    | `async/await`, JSON      | I/O, sprzątanie, odrzucenia i współbieżne niezależne odczyty                |     6–10 h |
| 5    | Vitest — unit            | AAA, EP/BVA, test doubles i testy async                                     |     8–12 h |
| 6    | Vitest + Supertest — API | Walidacja odpowiedzi, test.each, CRUD i izolacja                            |     9–13 h |
| 7    | GitHub Actions           | Debugging TS, diagnoza czerwonego CI, branch/PR/merge                       |      4–7 h |
| 8    | README i rozmowa         | Portfolio i praktyczna próba samodzielności                                 |      5–8 h |

**Deadline pozostaje 31.10.2026.** Od 12 do 31 października włącznie są 20 dni, czyli 40 h przy codziennych 2 h nauki (mniej przy dniach wolnych). Dotychczasowe 43–70 h już przekraczało ten budżet. Po audycie szacunek planistyczny sumy etapów to **52–82 h**, a z poprawkami, powtórkami i transferem **60–95 h**. To oszacowanie, nie zmierzony czas; nakład ponownie oceniamy po etapach 0–2.

**Konflikt:** przy 2 h dziennie pełna ścieżka do deadline'u nie jest realistycznym założeniem. Potrzebne byłoby średnio 2,6–4,1 h dziennie na bazowy zakres lub około 3–4,75 h z buforem. Nie zakładamy automatycznie, że użytkownik ma ten czas. Zachowujemy termin i wymagania, zgłaszamy ryzyko zamiast skreślać testy/OOP/debugging lub deklarować gotowość bez dowodów. Łączymy ćwiczenia z istniejącymi zadaniami, unikamy duplikatów, odkładamy wszystkie BONUS-y. Nie rozszerzaj zakresu backendu tylko dlatego, że idzie wolniej.

## Jak będzie malało wsparcie AI?

- **Etapy 0–2:** Priorytet: nauczyć się układać _własny plan_ zanim Codex poda sugestie. Wskazówki są normalne i dozwolone. Za pierwszym razem z nowym zagadnieniem możesz potrzebować przykładu na innych danych.
- **Etapy 3–4:** Nowe biblioteki i asynchroniczność — dozwolone objaśnienia mechanizmów oraz dokumentacja. Przy podobnych endpointach i operacjach stopniowo przejmuj projektowanie sygnatur i algorytmu.
- **Etapy 5–6:** Przy testach próbuj najpierw sam wymyślać przypadki, dane i asercje. Codex recenzuje; po pomocy 3–4 dostajesz krótkie ćwiczenie transferowe.
- **Etapy 7–8:** Nauka CI i dokumentacji — składni nowych narzędzi nie musisz pamiętać z głowy. Końcowy sprawdzian: samodzielnie zaplanuj i napisz jedną małą zmianę logiki API oraz test, a następnie wyjaśnij swoją implementację.

Nie opieraj przejścia do Playwrighta na zero-jedynkowym „nigdy nie korzystałem ze wskazówek”. Liczy się sprawdzalna samodzielność w **powtarzalnych, podstawowych zadaniach**. Nowsze narzędzia wymagają nauki i dokumentacji także u profesjonalistów.

## Kamienie milowe

- **Po etapie 2:** potrafisz zbudować logikę CRUD bez frameworka HTTP.
  Potrafisz też wyjaśnić klasę, instancję, konstruktor, enkapsulację i wstrzyknięcie zależności przez kontrakt.
- **Po etapie 3:** umiesz wysłać request, odczytać response i wyjaśnić kody HTTP.
- **Po etapie 4:** rozumiesz `async/await`, Promise, `try/catch` i nie ukrywasz błędów I/O.
  Pokazujesz sprzątanie w `finally` i uzasadniasz wybór między sekwencją a `Promise.all` bez współbieżnych zapisów do jednego JSON.
- **Po etapie 6:** testujesz API automatycznie i diagnozujesz porażki testów.
- **Po etapie 8:** masz repozytorium gotowe do pokazania rekruterowi i możesz rozpocząć projekt Playwright.
  Dowodem transferu jest 8.8 wykonane samodzielnie oraz praktyczne kryteria z `AUDIT.md`, a nie sam quiz.

## Zasada priorytetów

1. **Obowiązkowe:** wszystkie zadania 0–8, testy i dokumentacja.
2. **Nieobowiązkowe:** dodatki `BONUS` opisane w `PROJECT.md`.
3. **Celowo pominięte:** frontend, baza SQL, Docker, Playwright, Allure, MCP i autoryzacja. Te technologie nie są potrzebne, żeby ukończyć projekt #2.

Jeśli ukończysz wszystkie wymagania i potrafisz samodzielnie wytłumaczyć rozwiązania, **nie rozbudowuj BugTrackera w nieskończoność**. Przejdź do przygotowanego projektu Playwright.

## Dla Codexa

- Czytaj sekcję etapu w `PROJECT.md` i wydawaj **jedno** najmniejsze nieukończone zadanie.
- Nie zastępuj zadań własnymi pomysłami ani nie przeskakuj etapów bez decyzji użytkownika.
- Po ukończeniu etapu przeprowadź krótki quiz i review, zanim przejdziesz dalej.
