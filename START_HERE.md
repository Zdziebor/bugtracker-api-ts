# START_HERE.md — BugTracker API / projekt #2

## Najpierw dokończ Watchlist

Rozpoczęcie projektu zaplanowane jest na **poniedziałek, 12 października 2026 r.** Nie ma potrzeby przełączać się wcześniej. Nie jest to automatyczne przypomnienie ani zadanie uruchamiane w tle.

## Co budujesz?

Będziesz stopniowo coraz samodzielniej tworzyć w **TypeScript** małe **REST API do zarządzania zgłoszeniami błędów**. Na końcu powstanie repozytorium zawierające:

- aplikację Node/Express z endpointami CRUD,
- walidację danych za pomocą Zod,
- asynchroniczny zapis/odczyt JSON i obsługę błędów,
- testy jednostkowe **Vitest** i integracyjne HTTP **Supertest**,
- workflow **GitHub Actions**, README i opis decyzji technicznych.

**Nie piszesz frontendu i nie zaczynasz jeszcze Playwrighta.** Allure, AI/MCP i testowanie interfejsu przyjdą w projekcie #3.

## Co znajduje się w tej paczce?

| Plik | Zastosowanie |
|---|---|
| `AGENTS.md` | Zasady pracy Codexa: mentor, brak automatycznych rozwiązań, 4 poziomy podpowiedzi |
| `PROJECT.md` | Wymagania, kontrakt API, szczegółowa checklista i kryteria ukończenia |
| `ROADMAP.md` | Etapy, szacowany nakład pracy i kamienie milowe |
| `PROGRESS.md` | Dziennik sesji i lista tematów do powtórki |
| `START_HERE.md` | Instrukcja rozpoczęcia |

## W poniedziałek — pierwszy start (bez generowania kodu przez AI)

1. Utwórz **nowe puste repozytorium** `bugtracker-api-ts` na GitHubie lub lokalnie (GitHub może zostać dodany w ramach zadania 0.1).
2. Skopiuj do jego katalogu głównego **wszystkie pięć plików** `.md` z tego zestawu.
3. Otwórz folder projektu w **Codexie** (CLI albo edytor).
4. Napisz do Codexa dokładnie: `START`.
5. Otrzymasz tylko **zadanie 0.1**. Najpierw spróbujesz zaplanować rozwiązanie; następnie wykonasz je z taką pomocą, jakiej potrzebujesz.
6. Jeśli utkniesz, użyj najpierw `WSKAZÓWKA 1`, a dopiero potem kolejnych poziomów.
7. Gdy skończysz, wpisz `REVIEW`. Dopiero po weryfikacji poproś o `ZAPISZ POSTĘP` i `DALEJ`.

## Komendy, które rozumie mentor

| Komenda | Efekt |
|---|---|
| `START` | Pierwsze najmniejsze zadanie |
| `DALEJ` | Następne zadanie, jeśli aktualne ukończone |
| `WSKAZÓWKA 1` | Pytanie naprowadzające |
| `WSKAZÓWKA 2` | Nazwa pojęcia/metody i dokumentacja |
| `WSKAZÓWKA 3` | Algorytm opisany krok po kroku, bez gotowego kodu |
| `WSKAZÓWKA 4` | Mały przykład na **innych danych** — tylko na Twoją prośbę |
| `MÓJ PLAN` | Codex recenzuje Twój pomysł przed pisaniem kodu, bez gotowej implementacji |
| `TRANSFER` | Małe podobne zadanie sprawdzające samodzielność |
| `REVIEW` | Ocena Twojego kodu i testów, bez edytowania plików |
| `DEBUG` | Pomoc w zrozumieniu błędu, nie automatyczne jego naprawienie |
| `QUIZ` | Trzy pytania sprawdzające z ostatniego etapu |
| `ZAPISZ POSTĘP` | Po Twojej zgodzie aktualizacja `PROJECT.md` i `PROGRESS.md` |
| `POSTĘP` | Pokaż, co już zrobione i co dalej |
| `INTERVIEW` | Symulacja rozmowy rekrutacyjnej o projekcie |

## Jak będzie działała pomoc?

Codex jest **mentorem, nie autorem gotowej aplikacji**. Możesz prosić o wskazówki, szkic pojęcia albo przykład na innych danych. Celem jest stopniowe ograniczanie podpowiedzi przy powtarzających się umiejętnościach, nie natychmiastowy zakaz pomocy. Domyślnie nie edytuje kodu, nie instaluje zależności i nie wykonuje za Ciebie zadań. Poziom pomocy wybierasz Ty. Jeśli Codex pokazuje za dużo gotowego kodu, napisz: `STOP — przypomnij AGENTS.md i wróć do wskazówek bez implementacji`.

## Kiedy przejść do Playwrighta?

Kiedy wykonasz kryteria w sekcji **„Warunki ukończenia — zielone światło do Playwrighta”** z `PROJECT.md` oraz będziesz umiał bez AI dodać nową drobną funkcjonalność i test. Nie czekaj na realizację dodatków `BONUS`.

**Planowana nauka:** około 43–70 godzin. Przy 2 godzinach w dzień nauki: około 22–35 dni. To szacunek, nie deadline.
