# ThmdPlayer - Aplikacja do Oglądania Filmów na Linux

ThmdPlayer to lekka aplikacja desktopowa do odtwarzania wideo na Linux, stworzona w C# przy użyciu .NET 8, AvaloniaUI i LibVLC.

## Funkcje

- **Odtwarzanie wideo**: Obsługa popularnych formatów wideo (MP4, MKV, AVI, MOV, WMV, FLV, WebM)
- **Playlista**: zapisuje i przywraca listę odtwarzania między uruchomieniami
- **Okno playlisty**: zapamiętuje rozmiar i pozycję okna playlisty
- **Okno kontrolne**: zapamiętuje rozmiar i pozycję paska sterowania
- **Kontrolki odtwarzania**: Play/Pause, Stop, poprzedni/następny
- **Pasek postępu**: podgląd i nawigacja w czasie odtwarzania
- **Regulacja głośności**: suwak głośności z natychmiastową aktualizacją
- **Obsługa napisów**: możliwość wczytywania plików z napisami

## Wymagania

- .NET 8.0 SDK
- Linux (Ubuntu, Debian, Fedora, Arch itp.)
- VLC Media Player z bibliotekami natywnymi LibVLC

## Instalacja VLC na Linux

### Ubuntu/Debian

```bash
sudo apt-get update
sudo apt-get install -y vlc libvlc-dev
```

### Fedora

```bash
sudo dnf install vlc libvlc-devel
```

### Arch Linux

```bash
sudo pacman -S vlc
```

## Instalacja .NET 8.0 na Linux

### Ubuntu/Debian

```bash
wget https://packages.microsoft.com/config/ubuntu/22.04/packages-microsoft-prod.deb -O packages-microsoft-prod.deb
sudo dpkg -i packages-microsoft-prod.deb
sudo apt-get update
sudo apt-get install -y dotnet-sdk-8.0
```

### Fedora

```bash
sudo dnf install dotnet-sdk-8.0
```

## Budowanie i Uruchamianie

### Krok 1: Przywracanie zależności

```bash
dotnet restore
```

### Krok 2: Budowanie projektu

```bash
dotnet build ThmdPlayer.csproj
```

### Krok 3: Uruchomienie aplikacji

```bash
dotnet run --project ThmdPlayer.csproj
```

## Użycie

1. **Otwórz plik wideo**: Kliknij przycisk "📁 Otwórz" i wybierz plik wideo
2. **Odtwarzanie/Pauza**: Użyj przycisku Play/Pause do sterowania odtwarzaniem
3. **Stop**: Kliknij przycisk "⏹ Stop" aby zatrzymać odtwarzanie
4. **Pasek postępu**: Przeciągnij suwak aby przejść do konkretnej części wideo
5. **Głośność**: Użyj suwaka, aby regulować poziom dźwięku
6. **Playlista**: Otwórz playlistę i dodaj pliki; aplikacja zapisze pozycję i rozmiar okna

## Struktura Projektu

```
ThmdPlayer/
├── Program.cs              # Punkt startowy aplikacji
├── App.axaml               # Definicja aplikacji XAML
├── App.axaml.cs            # Code-behind aplikacji
├── MainWindow.axaml        # Interfejs głównego okna
├── MainWindow.axaml.cs     # Logika głównego okna
├── ViewModels/
│   └── MainWindowViewModel.cs  # ViewModel dla MVVM
├── ThmdPlayer.csproj       # Plik projektu
└── README.md               # Dokumentacja
```

## Technologie

- **.NET 8.0**: Framework aplikacji
- **AvaloniaUI 11.0**: Cross-platform UI framework
- **LibVLCSharp**: Biblioteka do odtwarzania wideo
- **MVVM Pattern**: Czysta architektura UI

## Rozwiązywanie Problemów

### Nie można znaleźć biblioteki LibVLC
Upewnij się, że biblioteka LibVLC jest zainstalowana i że `dotnet restore` przebiegł pomyślnie.

```bash
dotnet restore
```

### Błąd: Brak dźwięku
Sprawdź ustawienia dźwięku systemowego i ustawienia głośności w aplikacji.

### Błąd: Format wideo nie jest obsługiwany
LibVLC obsługuje większość popularnych formatów. Jeśli format nie działa, spróbuj przekonwertować plik na MP4.

### Kompilacja do pojedynczego pliku wykonywalnego

```bash
dotnet publish -c Release -r linux-x64 --self-contained true -p:PublishSingleFile=true -p:IncludeNativeLibrariesForSelfExtract=true -o ./publish_path
```

## Licencja

Projekt jest dostępny do użytku edukacyjnego i osobistego.

## Autor

Softbery by Paweł Tobis

Aplikacja stworzona w C#, AvaloniaUI i LibVLC na platformie Linux.
