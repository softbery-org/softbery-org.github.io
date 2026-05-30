# Changes

## [3.05.1215] - 2026-05-30

### Pomijanie intra i outra

- **Per-plikowe ustawienia pomijania** — `SkipIntroSeconds` i `SkipOutroSeconds` w `PlaylistItem`
- **Automatyczne pomijanie intra** — po rozpoczęciu odtwarzania odtwarzacz przeskakuje do zadanego czasu (sekundy)
- **Automatyczne pomijanie outra** — gdy pozycja osiągnie początek outra, odtwarzacz automatycznie przechodzi do następnego pliku
- **Auto-detect intra/outra** — przycisk "Auto-detect" w oknie playlisty analizuje wideo przez `ffmpeg` używając wielu metod: `blackdetect` (czarne segmenty), `silencedetect` (spadek głośności audio), `freezedetect` (statyczne klatki), `scenedetect` (zmiany scen) — łącząc wyniki dla najlepszej precyzji
- **Kopiowanie na wszystkie odcinki** — przycisk "Zastosuj na wszystkie" kopiuje ustawienia `SkipIntroSeconds`/`SkipOutroSeconds` ze zaznaczonego elementu na całą playlistę (przydatne dla seriali z tym samym openingiem/endingiem)
- **UI w oknie playlisty** — pola tekstowe "Intro (s)" i "Outro (s)" + przyciski "Ustaw pomiń" / "Auto-detect" / "Zastosuj na wszystkie" dla zaznaczonego elementu
- Ustawienia są zapisywane i przywracane w `config.json` wraz z pozostałymi danymi playlisty

### Naprawy

- **Crash przy pomijaniu outra** — `OnNextClick` wywoływane z VLC thread jest teraz dispatchowane na UI thread przez `Dispatcher.UIThread.Post`

## [3.05.1214] - 2026-05-30

### Skróty klawiszowe i nawigacja

- **Spacja** — play/pause
- **Strzałki** — lewo/prawo: przeskok ±10s, góra/dół: zmiana głośności ±5
- **F** — fullscreen, **Escape** — wyjście z fullscreen
- **N** — następny plik, **P** — poprzedni plik
- **M** — wyciszenie (mute)

### Tryb pełnoekranowy i zawsze na wierzchu

- Fullscreen ukrywa pasek `BottomBar` i ramki okna; mysz w dolnej części przywraca UI
- Przycisk **"Zawsze na wierzchu"** / **"Wyłącz pin"** w `MainWindow`

### Zarządzanie playlistą

- **Drag & drop** plików i folderów do okna playlisty
- **Przesuń w górę / w dół** w menu kontekstowym do ręcznej zmiany kolejności
- **Pole wyszukiwania** nad playlistą — auto-scroll do pierwszego pasującego elementu

### Odtwarzanie i napisy

- **Prędkość odtwarzania** — cykliczny przycisk 1x → 1.5x → 2x → 0.5x
- **Wznawianie pozycji** per plik — zapisywane w `ResumePosition` w `PlaylistItem`
- **Auto-ładowanie napisów** — automatyczne wczytanie `.srt` o tej samej nazwie co wideo
- **Synchronizacja napisów** — przyciski +/- 0.5s w panelu sterowania
- **Wybór ścieżki audio** — przycisk "Audio" w `MainWindow` do cyklicznego przełączania ścieżek

### Inne

- **Tryb Mini Player** — przycisk zmniejsza okno do 400x280, ukrywa pasek dolny; ponowne kliknięcie przywraca
- **Obsługa błędów** — komunikat gdy plik nie istnieje przy próbie odtworzenia

## [3.05.1208] - 2026-05-30

### Tryby odtwarzania

- Dodano cykliczny przycisk trybów odtwarzania w `ControlBarWindow` z ikoną i tekstem aktualnego trybu
- Obsługiwane tryby: **Wszystkie** (odtwarza kolejno, zatrzymuje na końcu), **Jeden** (zatrzymuje po zakończeniu), **Powtórz** (pętla całej listy), **Kolejka** (odtwarza z kolejki)
- `GetNext()` i `GetPrevious()` w `PlaylistViewModel` respektują aktywny tryb
- `OnEndReached` w `MainWindow` dispatchuje na UI thread, eliminując deadlock przy zmianie pliku

### Kolejka odtwarzania

- Dodano kolejkę odtwarzania (`_queueItems`) do `PlaylistViewModel`
- Elementy w kolejce mają widoczny numer (pomarańczowy okrągły badge) w playliście
- Przycisk **"Dodaj do kolejki"** w oknie playlisty — dodaje zaznaczone elementy
- Przycisk **"Wyczyść kolejkę"** — usuwa wszystko z kolejki i resetuje numery
- Menu kontekstowe (prawy przycisk myszy): Odtwórz / Dodaj do kolejki / Usuń z kolejki / Usuń z listy

### UI playlisty

- Ikona głośnika (zielona) obok nazwy aktualnie odtwarzanego pliku — widoczna niezależnie od zaznaczenia
- Zaznaczenie i auto-scroll aktualnie odtwarzanego wiersza przy każdej zmianie pliku
- Wielokrotne zaznaczanie (`SelectionMode="Multiple"`) z obsługą klawisza Delete
- Przycisk **"Dodaj folder"** — dodaje wideo z folderu i podfolderów

### Panel sterowania

- Wyświetlanie nazwy aktualnie odtwarzanego pliku nad suwakiem postępu
- Czas aktualny i całkowity obok suwaka

## [3.05.1147] - 2026-05-29

- Dodano skrypt `build.sh` do automatycznej kompilacji aplikacji
- Skrypt kompiluje aplikację do jednego pliku z numerem wersji w nazwie (np. `thmd-ver.3.05.1145`)
- Automatyczna instalacja VLC jeśli nie jest zainstalowane w systemie
- Tworzenie samo-rozpakowującego się instalatora `.run` zawierającego aplikację i biblioteki VLC

## [3.05.1115] - 2026-05-26

- Dodano okno `About` dostępne z przycisku w sekcji Controls Area
- Dodano `version.txt` oraz automatyczne podbijanie numeru wersji przy każdej kompilacji

## [3.05.1113] - 2026-05-26

- Zmieniono nazwę projektu na `ThmdPlayer`
- Zaktualizowano plik projektu `ThmdPlayer.csproj` i dokumentację `README.md`
- Naprawiono przywracanie playlisty po ponownym otwarciu aplikacji
- Dodano zapisywanie i przywracanie rozmiaru oraz pozycji okien `PlaylistWindow` i `ControlBarWindow`
- Poprawiono mechanizm zapisu konfiguracji okien, aby pozycje/rozmiary były zapisywane przy każdej zmianie
- Poprawiono zarządzanie konfiguracją playlisty i zapisywanie pustej listy po wyczyszczeniu
