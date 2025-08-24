# Workflow Configuration

## Główne zadanie
Gdy otrzymam prompt: "wykonaj prompt.md [repo], [TASK-ID]", wykonuję pełny workflow developmentu z wykorzystaniem Linear MCP oraz GitHub MCP i GitHub CLI

**Uwaga:** [AUR-06] to tylko przykład - każdy task ma własny unikalny identyfikator (np. AUR-01, AUR-05, AUR-45, DEV-12, etc.).

## Workflow kroków

### 1. Pobranie szczegółów taska
- Wykorzystuj MCP Linear do pobrania pełnych szczegółów taska [TASK-ID]
- Przeanalizuj wymagania, opis i acceptance criteria
- Upewnij się, że rozumiesz zakres pracy
- W przypadku błędów z MCP Linear - zgłoś problem do rozwiązania

### 2. Przygotowanie brancha
```bash
# Utworzenie i przełączenie na nowy branch
# Preferuj pobranie nazwy z MCP Linear jeśli dostępne
# W przeciwnym razie użyj formatu: task-id-slug-z-tytułu
# Przykład: dla "AUR-6" + "Dodanie 3 podtytułu" = aur-6-dodanie-3-podtytulu
git checkout -b [nazwa-z-linear-lub-wygenerowana]
```

### 3. Implementacja i pierwszy commit
- Rozpocznij implementację zgodnie z wymaganiami taska
- Po pierwszej wersji kodu wykonaj commit:
```bash
git add .
git commit -m "Initial implementation - krótki opis"
git push origin [nazwa-brancha]
```

### 4. Utworzenie Pull Request
Natychmiast po pierwszym push wykonaj:
```bash
gh pr create --draft --title "[TASK-ID] - [tytuł taska z Linear]" --body "[wygenerowany opis na podstawie taska Linear]"
```

**Ważne:** Title MUSI zawierać identyfikator taska (np. AUR-06, DEV-12) dla automatycznego połączenia z GitHub.

### 5. Iteracyjna praca
Po każdej zmianie/poprawce:
- czekam czy poprawki są zaakceptowane. Jeżeli tak to wykonam commit i push do gita:
```bash
git add .
git commit -m "Krótki, opisowy komunikat zmian"
git push origin [nazwa-brancha]
```

### 6. Zakończenie
- Czekam na potwierdzenie zakończenia pracy od użytkownika
- Na żądanie wykonuję merge do main lub użytkownik robi to ręcznie

## Format commitów
Wszystkie commity używają prostego formatu:
- Krótki, opisowy komunikat (bez prefiksu TASK-ID)
- Przykład: `Add user authentication logic`
- Przykład: `Fix validation error handling`
- Przykład: `Update user interface components`

## Format Pull Request
- **Title:** `[TASK-ID] - [dokładny tytuł z Linear]`
- **Body:** Wygenerowany opis zawierający:
  - Cel taska
  - Główne zmiany
  - Acceptance criteria
  - Link do taska Linear (jeśli dostępny)

## Wymagane narzędzia
- MCP Linear (do pobierania szczegółów tasków)
- MCP GitHub (dodatkowe funkcjonalności GitHub)
- GitHub CLI (`gh`)
- Git

**Uwaga:** Wszystkie dependencies są już zainstalowane i skonfigurowane.

## Naming Convention - Branch
- **Preferowane:** Pobierz nazwę brancha z MCP Linear (jeśli dostępne)
- **Fallback:** Wygeneruj z ID i tytułu taska w formacie:
  - Przykład: `AUR-6` + `Dodanie 3 podtytułu` → `aur-6-dodanie-3-podtytulu`
  - Zasady: lowercase, kebab-case, cyfry bez zer wiodących
## Uwagi
- PR jest tworzony jako draft na początku
- Branch name generowany z Linear lub według wzorca: `task-id-slug-z-tytułu`
- Nie wykonuję merge bez wyraźnej prośby użytkownika
- W przypadku błędów z MCP lub GitHub CLI - zgłaszam problem do rozwiązania
