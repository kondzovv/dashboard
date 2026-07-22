# 🖥️ Widget na pulpit (Windows) — To-Do + Cel miesięczny

Dwa **osobne** widżety na pulpit — jeden z **listą to-do**, drugi z **celem miesięcznym** — wyglądem dopasowane do apki. Możesz je ustawić w różnych miejscach pulpitu. Odświeżają się automatycznie, dopóki apka jest otwarta w przeglądarce/PWA.

Pliki skinów: **`Dashboard-Todo.ini`** (lista zadań) i **`Dashboard-Cel.ini`** (cel miesięczny). Pobierz je z apki (Ustawienia → Widget na pulpit) albo z tego folderu.

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

### 3. Dodaj skiny (dwa osobne widżety)
- Pobierz **`Dashboard-Todo.ini`** i **`Dashboard-Cel.ini`** (przyciskami w apce albo z tego folderu).
- ⚠️ **Każdy skin musi być w OSOBNYM folderze** w `Dokumenty\Rainmeter\Skins\` — w Rainmeterze pliki `.ini` w tym samym folderze to warianty jednej konfiguracji i tylko jeden może być aktywny (dlatego włączenie jednego wyłącza drugi). Zrób np.:
  ```
  Dokumenty\Rainmeter\Skins\
    Kasa-Todo\Dashboard-Todo.ini
    Kasa-Cel\Dashboard-Cel.ini
  ```
- W Rainmeterze **Refresh all**, potem załaduj obie konfiguracje — pojawią się jako dwa niezależne widżety, które przeciągniesz gdzie chcesz.
- Jeśli w kroku 1 wybrałeś `C:\DashboardWidget` — **nic nie musisz zmieniać**, oba skiny już tam patrzą.
- Jeśli wybrałeś inny folder — w każdym `.ini` w `[Variables]` ustaw:
  ```
  StatsFile=C:\pełna\ścieżka\do\dashboard-widget.txt
  ```
- Gdy widget pokazuje instrukcję zamiast danych — nie widzi pliku: sprawdź `StatsFile` i czy eksport w apce jest włączony, potem prawy klik → **Refresh**.
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
