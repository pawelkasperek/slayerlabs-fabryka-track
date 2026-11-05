# Spec-flow: prowadzenie zmian

Repozytoryjny proces spec-driven: **specyfikacja → plan → zadania → implementacja → weryfikacja**.
Nie jest to biblioteka SpecFlow ani integracja z zewnętrznym narzędziem. Nie dodaje zależności,
nie uruchamia CI, treningu, infrastruktury ani wdrożenia.

## Zakres

Stosuj pełny proces dla zmian zachowania produktu, kontraktów API/SDK/workerów, danych,
autoryzacji, treningu, infrastruktury i kosztów. Dla literówek, formatowania i drobnych zmian
dokumentacji bez zmiany zachowania wystarczy opis zakresu i weryfikacji w podsumowaniu lub PR.
Nie zakładaj osobnej specyfikacji dla każdego pliku.

Dokumentacja zmiany może być po polsku lub angielsku. Treść produktowa strony pozostaje
angielska zgodnie z [AGENTS.md](../AGENTS.md).

## Katalog zmiany

Jedna logiczna zmiana ma jeden katalog `specs/YYYY-MM-DD-krotka-nazwa/`:

- `spec.md` — problem, zakres i mierzalne kryteria akceptacji.
- `plan.md` — projekt rozwiązania, ryzyka, testy i decyzja o akceptacji.
- `tasks.md` — małe zadania powiązane z kryteriami akceptacji.
- `verification.md` — rzeczywiste wyniki, dowody, ograniczenia i decyzja o zakończeniu.

Skopiuj cztery pliki z [specs/_templates/](../specs/_templates/) do nowego katalogu,
zachowując nazwy plików. Zastąp pola w nawiasach `<...>`. Nie edytuj szablonów jako dokumentów
konkretnej zmiany. Data oznacza początek pracy; nazwa katalogu pozostaje stabilna.

## Etapy i bramki

### 1. Rozpoznanie i specyfikacja

Najpierw przeczytaj właściwy kod, testy i dokumenty. W `spec.md` oddziel:
fakty potwierdzone ścieżkami do kodu, wnioski oraz niewiadome.
Opisz stan obecny i oczekiwany, zakres i wyłączenia. Nadaj kryteriom identyfikatory `AC-01`,
`AC-02` itd. Każde kryterium musi mieć obserwowalny wynik i sposób sprawdzenia.
Nie przedstawiaj architektury docelowej z dokumentacji jako wdrożonej implementacji.

**Bramka:** wymagania są zrozumiałe; nierozstrzygnięte pytania wpływające na bezpieczeństwo,
koszty lub poprawność blokują implementację.

### 2. Plan i akceptacja

W `plan.md` opisz zmieniane komponenty, kontrakty, alternatywy, kompatybilność,
migrację i rollback, jeżeli dotyczą zmiany. Dla GPU uwzględnij lifecycle i cleanup;
dla API — producenta i konsumenta payloadu, autoryzację i błędy.
Zapisz wybrane testy i odwołania do kryteriów.

**Bramka:** przedstaw specyfikację i plan użytkownikowi lub reviewerowi. Implementację zacznij
dopiero po jawnej akceptacji obejmującej obydwa dokumenty. Zapisz kto, kiedy i gdzie jej udzielił.
Agent nie może zatwierdzać własnego planu w imieniu użytkownika.
Polecenie „przygotuj spec/plan” nie oznacza zgody na implementację.

### 3. Zadania

Rozbij zaakceptowany plan w `tasks.md` na zadania `T-01`, `T-02` itd.,
powiązane z `AC-*`, plikami i sprawdzeniem wyniku. Uwzględnij testy regresji i aktualizację
dokumentacji. Kolejność powinna odzwierciedlać zależności.
Zaznaczaj zadanie jako ukończone dopiero po wykonaniu i sprawdzeniu.

### 4. Implementacja

Implementuj wyłącznie zaakceptowany zakres. Przy istotnej zmianie kontraktu, ryzyka lub zakresu:
wstrzymaj pracę, uaktualnij specyfikację i plan, zapisz zmianę decyzji i uzyskaj ponowną akceptację.
Sam brakujący szczegół wykonawczy nie wymaga rozbudowy dokumentacji, jeśli nie zmienia ustaleń.

Zgoda na implementację nie jest automatycznie zgodą na commit, push, deploy, migrację produkcji
ani uruchomienie płatnego GPU. Takie działania wymagają odpowiedniego polecenia lub jawnej zgody.
Nie zapisuj tokenów, sekretów, prywatnych danych ani nagłówków uwierzytelniania w dowodach.

### 5. Weryfikacja i zakończenie

W `verification.md` zapisz dla każdego `AC-*`: wynik, metodę, dowód i ograniczenia.
Wyniki: `PASS`, `FAIL`, `BLOCKED`, `NOT RUN`. Podaj dokładne polecenia, kontekst środowiska
i kody zakończenia. Test przeczytany, ale niewykonany, nie jest testem zakończonym sukcesem.

**Bramka:** zmiana jest `done` dopiero, gdy wszystkie kryteria mają `PASS`, zadania są ukończone,
a znane ograniczenia zostały zapisane. Jeśli wymagane sprawdzenie nie jest dostępne, pozostaw
zmianę `blocked` lub `in-progress`; zmniejszenie zakresu wymaga nowej akceptacji i aktualizacji AC.
Zapisz rewizję albo stan drzewa roboczego i diff, którego dotyczy weryfikacja.
Zakończenie implementacji nie oznacza wdrożenia na produkcję.

## Statusy

Pole `Status` w `spec.md` opisuje całą zmianę:

`draft → approved → in-progress → done`

`blocked` oznacza brak możliwości kontynuacji; zapisz powód i poprzedni etap.
`cancelled` oznacza świadomą rezygnację. Po wyjściu z blokady wróć do właściwego etapu;
istotne zmiany planu cofają status do `draft` do czasu ponownej akceptacji.

## Weryfikacja właściwa dla projektu

Dobieraj testy do zakresu. Nie uruchamiaj kosztownego treningu jako domyślnego smoke testu.

| Obszar | Sprawdzenie |
| --- | --- |
| Python / API | `uv run --extra server --extra test --extra eval --extra corpus python -m pytest` lub wybrane testy z `tests/` |
| SDK | Ten sam runner pytest z `sdk_tests/test_durability.py` oraz odpowiednimi testami klienta |
| Frontend | `npm --prefix frontend run build` |
| Logika frontendowa | `node --experimental-strip-types --test tests/*.test.mjs` |
| Treść i UI | Obejrzenie dotkniętych widoków, stanów błędów i języka interfejsu |
| GPU / runner | Testy kontraktów z mockowanym dostawcą, np. `tests/test_gpu_training.py`; test rzeczywistego GPU tylko za zgodą |
| Dokumentacja | Linki, ścieżki, zgodność z kodem i rozróżnienie implementacji od propozycji |

Polecenia wymagają przygotowanego środowiska; instalację opisuje [README](../README.md#start-locally).
Pełny CI jest w [.github/workflows/deploy.yml](../.github/workflows/deploy.yml).
Uruchamianie lokalnych testów nie uruchamia tego workflow; push do `main` może uruchomić deploy.

## Krótki prompt dla agenta

> Poprowadź zmianę `<opis>` według `docs/spec-flow.md`. Najpierw zbadaj kod, utwórz
> `specs/<data>-<nazwa>/spec.md` i `plan.md`, a następnie poczekaj na akceptację.
> Po akceptacji uzupełnij `tasks.md`, wykonaj zmianę i zapisz wyniki w `verification.md`.
> Nie wykonuj commita, push, deploy ani płatnych operacji bez osobnego polecenia.

To proces oparty na dokumentach i review, nie automatyczny mechanizm wymuszający bramki w CI.
