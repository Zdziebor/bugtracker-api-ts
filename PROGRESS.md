# PROGRESS.md — dziennik nauki

> Projekt #2: BugTracker API + Automated Tests  
> Planowany start: **2026-10-12 (poniedziałek)**  
> Deadline: **2026-10-31**
> Stan: etap 0 zakończony i zweryfikowany w rozmowie; quiz zaliczony 2026-10-12.

## Aktualny etap

- Etap: `1 — Model domenowy i czysty TypeScript` (do rozpoczęcia)
- Najbliższe zadanie: `1.1`
- Ostatnio ukończone zadanie: `0.4`; checkboxy 0.1–0.4 zsynchronizowano na polecenie użytkownika.
- Aktualne ryzyko: deadline 31.10.2026 przy 2 h dziennie daje 40 h od planowanego startu, mniej niż szacowany zakres; zobacz `ROADMAP.md`.

## Dziennik sesji

Dodawaj **jeden krótki wpis po sesji**. Nie musisz wpisywać czasu co do minuty; ważniejsze jest to, czego się nauczyłeś.

| Data       | Zadania | Czego się nauczyłem | Pomoc AI (1–4) | Samodzielność (S0/S1/S2) | Co dalej    |
| ---------- | ------- | ------------------- | -------------- | ------------------------ | ----------- |
| 2026-10-11 | 0.1–0.2, początek 0.3 | Repozytorium i małe commity; lokalne zależności; package.json vs tsconfig.json; typecheck vs uruchomienie. Poprawiono uszkodzony opis i kodowanie README. | Konkretne komendy i objaśnienia | S1 | Dokończyć 0.3 |
| 2026-10-12 | Dokończenie 0.3, 0.4 i quiz etapu 0 | Kompilacja do build_files, uruchomienie JS przez Node, breakpoint/Variables/Call Stack/Step Over, source maps; Prettier vs ESLint; flat config i zgodność wersji zależności. | Do 4 — przykład układu konfiguracji ESLinta | 0.3: S1; 0.4: S0 (AI podało układ konfiguracji) | Zadanie 1.1 |

Dowody: review rzeczywistych plików; wyniki użytkownika dla dev, typecheck, build i Node; zrzut debuggera z testNumber = 10 oraz index.ts 4:1; lint wykrył celowo nieużywaną zmienną i przeszedł po jej usunięciu; format:check wykrył zły styl i ostatecznie zwrócił „All matched files use Prettier code style!”. Po zmianie TypeScriptu na linię 6.0 użytkownik potwierdził ponowne przejście typecheck/build. Quiz: poprawnie rozróżniono dev/typecheck, build/Node i Prettier/ESLint; doprecyzowano termin „kompilacja”. Nie uruchamiano sprawdzeń automatycznie ani nie potwierdzano pushu/CI.

### Audyt specyfikacji — 2026-10-11

Przejrzano aktualne AGENTS/PROJECT/ROADMAP/PROGRESS. Specyfikacja miała CRUD, podstawy async, negatywne/graniczne testy i izolację, ale nie pełne praktyczne kryteria EP/BVA, doubles, współbieżności, fetch, debuggera i PR/CI. Włączono je do istniejących etapów oraz doprecyzowano końcową próbę 8.8. W odczytanych plikach brakowało zapisów wcześniejszych zmian OOP/DI; obowiązkowe klasy, konstruktory i DI zostały jawnie ujęte w 2.2/2.3/4.2/4.5. Nie przypisano nowych poziomów samodzielności ani zaliczeń; audyt wymagań nie jest weryfikacją umiejętności.

Dowody po faktycznym wykonaniu zadania zapisujemy w krótkim wpisie sesji: numer zadania, wynik/komenda lub link do PR/runu, przyczyna napotkanego błędu, zakres pomocy i następny krok. Dla 8.8 dodatkowo: potwierdzenie nowości wymagania, własny plan/tabela przypadków, wyniki i wyjaśnienie decyzji. Nie dodajemy drugiej checklisty umiejętności; mapowanie znajduje się w `AUDIT.md`.

**Samodzielność:** S0 = AI podało istotne kroki lub szkielet; S1 = mój pomysł + konkretne wskazówki; S2 = własny plan i implementacja, dokumentacja + review AI. Poziom to opis **sposobu wykonania zadania**, nie ocena użytkownika. Aktualizuj na żądanie, nie trzeba wpisywać codziennie.

## Luki do powtórki

| Temat | Co jest niejasne? | Jak sprawdzę, że rozumiem? |
| ----- | ----------------- | -------------------------- |
| Zagnieżdżanie tablic i obiektów konfiguracji | Przy globalIgnores potrzebny był przykład pokazujący dwa elementy tablicy; rozumienie należy utrwalić w samodzielnym zadaniu. | Na nowych danych samodzielnie ułożyć tablicę zawierającą dwa obiekty i wyjaśnić nawiasy oraz przecinki. |
| Narzędzia i kompilacja | Początkowo mylono sprawdzanie typów, uruchamianie i kompilację; końcowy quiz był poprawny. | W kolejnym zadaniu samodzielnie wybrać dev/typecheck/build/lint i uzasadnić wybór. |

## Samodzielne ćwiczenia kontrolne

Po użyciu `WSKAZÓWKA 3` lub `WSKAZÓWKA 4` Codex może zaproponować małe podobne ćwiczenie — zapisz rezultat tutaj, np. `bez podpowiedzi`.

2026-10-12: po przykładzie konfiguracji ESLinta użytkownik wskazał bez dodatkowej podpowiedzi, że drugi wzorzec pomijanego folderu należy dodać do tablicy globalIgnores po przecinku. To sprawdzenie jednego elementu; pełne samodzielne układanie zagnieżdżonej konfiguracji pozostaje do utrwalenia.

## Checkpointy

- [ ] Rozumiem `tsc` / `tsx`, moduły, `strict` i konfigurację Node.
- [ ] Potrafię sam zrobić podstawową operację CRUD w TypeScript.
- [ ] Rozumiem `Promise`, `async/await`, `try/catch`.
- [ ] Potrafię sam zaprojektować endpoint i zweryfikować odpowiedź HTTP.
- [ ] Umiem napisać testy jednostkowe i integracyjne bez gotowca AI.
- [ ] Testy są izolowane, a GitHub Actions przechodzi.
- [ ] Potrafię opowiedzieć o projekcie i jego ograniczeniach po angielsku.

> `PROGRESS.md` nie zastępuje checklisty w `PROJECT.md`; zadania odhaczaj wyłącznie tam.
