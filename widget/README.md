# 🖥️ Widget na pulpit (Windows) — To-Do + Cel miesięczny

Widget pokazuje na pulpicie **listę to-do** i **cel miesięczny** z Twojego dashboardu. Odświeża się automatycznie, dopóki apka jest otwarta w przeglądarce/PWA.

> Działa na **Windows** z apką otwartą w **Chrome lub Edge** (na komputerze). Odświeża się tylko gdy apka jest otwarta — gdy ją zamkniesz, widget pokazuje ostatnie znane wartości.

## Jak to działa

1. Apka zapisuje na dysku mały plik `dashboard-widget.txt` (do folderu, który sam wybierasz).
2. **Rainmeter** czyta ten plik i rysuje widget na pulpicie.

## Instalacja krok po kroku

### 1. Włącz eksport w apce
- Otwórz dashboard na komputerze (Chrome/Edge) → **⚙️ Ustawienia → Widget na pulpit (Windows)**.
- Wybierz folder, w którym ma powstać plik (np. `Dokumenty\DashboardWidget`). Zapamiętaj tę ścieżkę.
- Apka od teraz zapisuje tam `dashboard-widget.txt` i odświeża go przy każdej zmianie.

### 2. Zainstaluj Rainmeter
- Pobierz i zainstaluj z **https://www.rainmeter.net/** (darmowe).

### 3. Dodaj skin
- Pobierz **`Dashboard.ini`** (przyciskiem w apce albo z tego folderu w repo).
- Wrzuć go do: `Dokumenty\Rainmeter\Skins\Dashboard\Dashboard.ini`
- Otwórz **`Dashboard.ini`** w Notatniku i w sekcji `[Variables]` ustaw ścieżkę:
  ```
  StatsFile=C:\Users\TWOJA_NAZWA\Documents\DashboardWidget\dashboard-widget.txt
  ```
  (wpisz pełną ścieżkę do pliku z kroku 1).
- W Rainmeterze: **Refresh all**, potem załaduj skin `Dashboard → Dashboard.ini`.

Gotowe — widget pojawi się na pulpicie. Możesz go przeciągnąć w dowolne miejsce.

## Dostosowanie
W sekcji `[Variables]` skinu możesz zmienić kolory (`cGold`, `cMint`, …) i czcionkę (`FontName`). Widget pokazuje do 8 zadań; resztę sygnalizuje linijka „+N więcej".

## Ograniczenia (uczciwie)
- Aktualizacja tylko gdy apka jest otwarta (to przeglądarka zapisuje plik).
- Zapis pliku działa w Chrome/Edge na komputerze (nie Firefox/Safari, nie na telefonie).
- Kolorowe emoji nie są renderowane przez Rainmeter — kategorie zadań pokazane są kolorową kropką.
