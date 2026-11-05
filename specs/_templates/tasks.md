# Zadania — <nazwa zmiany>

Dokumenty: [spec.md](spec.md), [plan.md](plan.md), [verification.md](verification.md)

Twórz zadania dopiero na podstawie zaakceptowanego planu. Każde zadanie ma identyfikator,
zależności, zakres, powiązane kryteria i sposób potwierdzenia wykonania.
Dodaj kolejne kryteria i zadania według potrzeb.

## T-01 — Test regresji / kontraktu

- [ ] Ukończone
- Kryteria: AC-01
- Zależności: akceptacja planu
- Pliki: <testy>
- Działanie: <co sprawdzić>
- Potwierdzenie: <polecenie i wynik; przed i po poprawce, jeśli dotyczy>

## T-02 — Implementacja

- [ ] Ukończone
- Kryteria: AC-01
- Zależności: T-01
- Pliki: <implementacja>
- Działanie: <najmniejsza spójna zmiana>
- Potwierdzenie: <test lub kontrola wyniku>

## T-03 — Dokumentacja i weryfikacja

- [ ] Ukończone
- Kryteria: AC-01
- Zależności: T-02
- Pliki: <dokumentacja, verification.md>
- Działanie: <wybrane testy, UI i zgodność dokumentacji>
- Potwierdzenie: <dowody dla wszystkich AC; przegląd końcowego diffu>
