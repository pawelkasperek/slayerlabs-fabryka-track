# Weryfikacja — <nazwa zmiany>

Dokumenty: [spec.md](spec.md), [plan.md](plan.md), [tasks.md](tasks.md)

## Kontekst

- Data: <data wykonania>
- Weryfikujący: <osoba lub agent>
- Sprawdzana rewizja: <SHA oraz zmiany niecommitowane, jeśli są>
- Środowisko: <lokalne/CI, wersje narzędzi; bez sekretów>
- Zakres diffu: <pliki i zachowania objęte weryfikacją>

## Wyniki kryteriów

### AC-01 — <nazwa>

- Wynik: NOT RUN
- Metoda: <test lub obserwacja>
- Dowód: <polecenie, kod wyjścia, wynik, ewentualny link>
- Ograniczenia: <czego ten test nie dowodzi>

Dozwolone wyniki: `PASS`, `FAIL`, `BLOCKED`, `NOT RUN`.
Nie wpisuj `PASS` wyłącznie na podstawie przeczytania testu lub oczekiwanego zachowania.

## Pozostałe sprawdzenia

- Testy regresji: <polecenia, kody wyjścia i wyniki>
- Frontend / UI / język: <wynik lub nie dotyczy z uzasadnieniem>
- Kontrakty API/SDK/workerów: <wynik lub nie dotyczy z uzasadnieniem>
- Kontrola diffu i danych wrażliwych: <wynik>

## Niewykonane sprawdzenia i ryzyka

<Co pominięto, dlaczego, skutek i dalszy krok. Brak dostępu do GPU nie oznacza sukcesu testu GPU.>

## Decyzja o zakończeniu

- Gotowość: niepotwierdzona
- Wszystkie kryteria mają PASS: nie
- Wszystkie zadania ukończone: nie
- Znane ograniczenia: <lista lub brak>
- Status wdrożenia: nie wdrażano

Ustaw `Status: done` w specyfikacji tylko po spełnieniu bramki z
[docs/spec-flow.md](../../docs/spec-flow.md). Dla pliku w katalogu konkretnej zmiany
ta ścieżka pozostaje taka sama.
