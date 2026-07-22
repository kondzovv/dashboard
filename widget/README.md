# 🖥️ Widget na pulpit (Windows) — To-Do + Cel miesięczny

Widget pokazuje na pulpicie **listę to-do** i **cel miesięczny** z Twojego dashboardu. Odświeża się automatycznie, dopóki apka jest otwarta w przeglądarce/PWA.

> Działa na **Windows** z apką otwartą w **Chrome lub Edge** (na komputerze). Odświeża się tylko gdy apka jest otwarta — gdy ją zamkniesz, widget pokazuje ostatnie znane wartości.

## Jak to działa

1. Apka zapisuje na dysku mały plik `dashboard-widget.txt` (do folderu, który sam wybierasz).
2. **Rainmeter** czyta ten plik i rysuje widget na pulpicie.

## Instalacja krok po kroku

### 1. Włącz eksport w apce
- Otwórz dashboard na komputerze (Chrome/Edge) → **⚙️ Ustawienia → Widget na pulpit (Windows)**.
- **Najprościej:** utwórz folder `C:\DashboardWidget` i wybierz właśnie jego — wtedy skin działa bez żadnych zmian (jego domyślny `StatsFile` już wskazuje ten folder).
- Apka od teraz zapisuje tam `dashboard-widget.txt` i odświeża go przy każdej zmianie.

### 2. Zainstaluj Rainmeter
- Pobierz i zainstaluj z **https://www.rainmeter.net/** (darmowe).

### 3. Dodaj skin
- Pobierz **`Dashboard.ini`** (przyciskiem w apce albo z tego folderu w repo).
- Wrzuć go do: `Dokumenty\Rainmeter\Skins\Dashboard\Dashboard.ini`
- Jeśli w kroku 1 wybrałeś `C:\DashboardWidget` — **nic nie musisz zmieniać**, skin już tam patrzy.
- Jeśli wybrałeś inny folder — otwórz **`Dashboard.ini`** w Notatniku i w `[Variables]` ustaw:
  ```
  StatsFile=C:\pełna\ścieżka\do\dashboard-widget.txt
  ```
- Gdy widget pokazuje instrukcję zamiast danych — znaczy, że nie widzi pliku: sprawdź `StatsFile` i czy eksport w apce jest włączony, potem prawy klik na widget → **Refresh**.
- W Rainmeterze: **Refresh all**, potem załaduj skin `Dashboard → Dashboard.ini`.

Gotowe — widget pojawi się na pulpicie. Możesz go przeciągnąć w dowolne miejsce.

## Dostosowanie
W sekcji `[Variables]` skinu możesz zmienić kolory (`cGold`, `cMint`, …) i czcionkę (`FontName`). Widget pokazuje do 8 zadań; resztę sygnalizuje linijka „+N więcej".

## Autostart — żeby widget był zawsze aktualny (Edge)
Widget odświeża się tylko gdy apka działa. Żeby startowała sama z Windowsem:
1. W **Edge** otwórz stronę → zainstaluj jako apkę (ikona instalacji w pasku adresu, albo ⋯ → *Aplikacje → Zainstaluj tę witrynę jako aplikację*).
2. Wejdź na **`edge://apps`** → prawy klik na apce → włącz **„Uruchamiaj przy logowaniu do urządzenia"** (Start app when you sign in).
3. Od teraz apka startuje z systemem i w tle nadpisuje plik widgetu — okno możesz zminimalizować.

> Po restarcie systemu przeglądarka może raz poprosić o zgodę na zapis do folderu — kliknij **Zezwól**. W nowszym Edge zgoda potrafi być zapamiętana na stałe.

## Ograniczenia (uczciwie)
- Aktualizacja tylko gdy apka jest otwarta (to przeglądarka zapisuje plik).
- Zapis pliku działa w Chrome/Edge na komputerze (nie Firefox/Safari, nie na telefonie).
- Kolorowe emoji nie są renderowane przez Rainmeter — kategorie zadań pokazane są kolorową kropką.
