# ROADMAP.md — mapa nauki (BugTracker API)

## Co jest celem?

To projekt #2, który rozpoczniesz **w poniedziałek 12 października 2026 r.**, po domknięciu `watchlist-ts`.

**Cel nie jest taki, by zostać backend developerem.** Masz nauczyć się samodzielnie pisać TypeScript i testy, rozumieć HTTP oraz pracować z błędami, żeby później przejść bez osobnego kursu na **Playwright + TypeScript**.

Pełny zakres oraz wszystkie podzadania (`0.1`–`8.7`) są zapisane w `PROJECT.md`. Ten dokument to wyłącznie mapa etapów. **Nie odhaczaj zadań tutaj — jedno źródło prawdy to `PROJECT.md`.**

## Etapy i orientacyjny nakład pracy

| Etap | Temat | Efekt etapu | Szacunkowo |
|---|---|---|---:|
| 0 | Repozytorium, Node i TS | Projekt uruchamia się i przechodzi typecheck | 2–4 h |
| 1 | Typy i model Issue | Tworzenie/aktualizacja obiektów, zasady domeny | 4–7 h |
| 2 | Repository i service | CRUD oraz filtry bez HTTP | 5–8 h |
| 3 | Express, HTTP, Zod | Działające endpointy REST i walidacja | 7–11 h |
| 4 | `async/await`, JSON | Odczyt/zapis danych i obsługa I/O | 5–9 h |
| 5 | Vitest — unit | Samodzielne testy logiki biznesowej | 6–9 h |
| 6 | Vitest + Supertest — API | Testy pozytywne, negatywne i CRUD E2E na poziomie API | 8–12 h |
| 7 | GitHub Actions | Automatyczne uruchamianie jakości i testów | 3–5 h |
| 8 | README i rozmowa | Portfolio, dokumentacja, świadome decyzje | 3–5 h |

**Bazowy szacunek: około 43–70 godzin.** Z dodatkowymi samodzielnymi próbami, powtórkami i ćwiczeniami transferowymi realnie może to być **50–85 godzin**, czyli około 25–43 dni przy 2 godzinach dziennie. Nie traktuj tego jako deadline. Nie rozszerzaj zakresu backendu tylko dlatego, że idzie wolniej.

## Jak będzie malało wsparcie AI?

- **Etapy 0–2:** Priorytet: nauczyć się układać *własny plan* zanim Codex poda sugestie. Wskazówki są normalne i dozwolone. Za pierwszym razem z nowym zagadnieniem możesz potrzebować przykładu na innych danych.
- **Etapy 3–4:** Nowe biblioteki i asynchroniczność — dozwolone objaśnienia mechanizmów oraz dokumentacja. Przy podobnych endpointach i operacjach stopniowo przejmuj projektowanie sygnatur i algorytmu.
- **Etapy 5–6:** Przy testach próbuj najpierw sam wymyślać przypadki, dane i asercje. Codex recenzuje; po pomocy 3–4 dostajesz krótkie ćwiczenie transferowe.
- **Etapy 7–8:** Nauka CI i dokumentacji — składni nowych narzędzi nie musisz pamiętać z głowy. Końcowy sprawdzian: samodzielnie zaplanuj i napisz jedną małą zmianę logiki API oraz test, a następnie wyjaśnij swoją implementację.

Nie opieraj przejścia do Playwrighta na zero-jedynkowym „nigdy nie korzystałem ze wskazówek”. Liczy się sprawdzalna samodzielność w **powtarzalnych, podstawowych zadaniach**. Nowsze narzędzia wymagają nauki i dokumentacji także u profesjonalistów.

## Kamienie milowe

- **Po etapie 2:** potrafisz zbudować logikę CRUD bez frameworka HTTP.
- **Po etapie 3:** umiesz wysłać request, odczytać response i wyjaśnić kody HTTP.
- **Po etapie 4:** rozumiesz `async/await`, Promise, `try/catch` i nie ukrywasz błędów I/O.
- **Po etapie 6:** testujesz API automatycznie i diagnozujesz porażki testów.
- **Po etapie 8:** masz repozytorium gotowe do pokazania rekruterowi i możesz rozpocząć projekt Playwright.

## Zasada priorytetów

1. **Obowiązkowe:** wszystkie zadania 0–8, testy i dokumentacja.
2. **Nieobowiązkowe:** dodatki `BONUS` opisane w `PROJECT.md`.
3. **Celowo pominięte:** frontend, baza SQL, Docker, Playwright, Allure, MCP i autoryzacja. Te technologie nie są potrzebne, żeby ukończyć projekt #2.

Jeśli ukończysz wszystkie wymagania i potrafisz samodzielnie wytłumaczyć rozwiązania, **nie rozbudowuj BugTrackera w nieskończoność**. Przejdź do przygotowanego projektu Playwright.

## Dla Codexa

- Czytaj sekcję etapu w `PROJECT.md` i wydawaj **jedno** najmniejsze nieukończone zadanie.
- Nie zastępuj zadań własnymi pomysłami ani nie przeskakuj etapów bez decyzji użytkownika.
- Po ukończeniu etapu przeprowadź krótki quiz i review, zanim przejdziesz dalej.
