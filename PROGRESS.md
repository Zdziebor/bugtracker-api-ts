# PROGRESS.md — dziennik nauki

> Projekt #2: BugTracker API + Automated Tests  
> Planowany start: **2026-10-12 (poniedziałek)**  
> Deadline: **2026-10-31**
> Stan: rozpoczęto przygotowanie repozytorium; brak dowodów ukończenia pozostałych etapów.

## Aktualny etap

- Etap: `0 — Fundament repozytorium`
- Najbliższe zadanie: `0.2` (wydane w rozmowie; wykonanie nieweryfikowane)
- Ostatnio potwierdzone w rozmowie: `0.1`; checkbox w `PROJECT.md` nie został jeszcze zsynchronizowany. Audyt specyfikacji nie odhacza zadań.
- Aktualne ryzyko: deadline 31.10.2026 przy 2 h dziennie daje 40 h od planowanego startu, mniej niż szacowany zakres; zobacz `ROADMAP.md`.

## Dziennik sesji

Dodawaj **jeden krótki wpis po sesji**. Nie musisz wpisywać czasu co do minuty; ważniejsze jest to, czego się nauczyłeś.

| Data | Zadania | Czego się nauczyłem | Pomoc AI (1–4) | Samodzielność (S0/S1/S2) | Co dalej |
|---|---|---|---|---|---|
| 2026-10-12 | — | Start projektu | — | — | Zadanie 0.1 |

Powyższy wpis pochodzi z szablonu i oznacza planowany start, nie dowód odbycia przyszłej sesji.

### Audyt specyfikacji — 2026-10-11

Przejrzano aktualne AGENTS/PROJECT/ROADMAP/PROGRESS. Specyfikacja miała CRUD, podstawy async, negatywne/graniczne testy i izolację, ale nie pełne praktyczne kryteria EP/BVA, doubles, współbieżności, fetch, debuggera i PR/CI. Włączono je do istniejących etapów oraz doprecyzowano końcową próbę 8.8. W odczytanych plikach brakowało zapisów wcześniejszych zmian OOP/DI; obowiązkowe klasy, konstruktory i DI zostały jawnie ujęte w 2.2/2.3/4.2/4.5. Nie przypisano nowych poziomów samodzielności ani zaliczeń; audyt wymagań nie jest weryfikacją umiejętności.

Dowody po faktycznym wykonaniu zadania zapisujemy w krótkim wpisie sesji: numer zadania, wynik/komenda lub link do PR/runu, przyczyna napotkanego błędu, zakres pomocy i następny krok. Dla 8.8 dodatkowo: potwierdzenie nowości wymagania, własny plan/tabela przypadków, wyniki i wyjaśnienie decyzji. Nie dodajemy drugiej checklisty umiejętności; mapowanie znajduje się w `AUDIT.md`.

**Samodzielność:** S0 = AI podało istotne kroki lub szkielet; S1 = mój pomysł + konkretne wskazówki; S2 = własny plan i implementacja, dokumentacja + review AI. Poziom to opis **sposobu wykonania zadania**, nie ocena użytkownika. Aktualizuj na żądanie, nie trzeba wpisywać codziennie.

## Luki do powtórki

| Temat | Co jest niejasne? | Jak sprawdzę, że rozumiem? |
|---|---|---|
| — | — | — |

## Samodzielne ćwiczenia kontrolne

Po użyciu `WSKAZÓWKA 3` lub `WSKAZÓWKA 4` Codex może zaproponować małe podobne ćwiczenie — zapisz rezultat tutaj, np. `bez podpowiedzi`.

## Checkpointy

- [ ] Rozumiem `tsc` / `tsx`, moduły, `strict` i konfigurację Node.
- [ ] Potrafię sam zrobić podstawową operację CRUD w TypeScript.
- [ ] Rozumiem `Promise`, `async/await`, `try/catch`.
- [ ] Potrafię sam zaprojektować endpoint i zweryfikować odpowiedź HTTP.
- [ ] Umiem napisać testy jednostkowe i integracyjne bez gotowca AI.
- [ ] Testy są izolowane, a GitHub Actions przechodzi.
- [ ] Potrafię opowiedzieć o projekcie i jego ograniczeniach po angielsku.

> `PROGRESS.md` nie zastępuje checklisty w `PROJECT.md`; zadania odhaczaj wyłącznie tam.
