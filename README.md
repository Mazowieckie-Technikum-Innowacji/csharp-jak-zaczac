# Jak zacząć z C#: od instalacji do pierwszego programu

Krok po kroku dla początkujących: co zainstalować, jak napisać i uruchomić pierwszy program konsolowy,
jak go debugować i jak zapisać pracę w Gicie. Przewodnik jest przygotowany pod Windows i Visual Studio
(tak, jak pracujemy na lekcjach w Mazowieckim Technikum Innowacji), a na końcu jest też wersja z samym terminalem.

## Spis treści

1. [Co będzie potrzebne](#1-co-będzie-potrzebne)
2. [Instalacja](#2-instalacja)
3. [Pierwszy program w Visual Studio](#3-pierwszy-program-w-visual-studio)
4. [Wczytywanie danych z klawiatury](#4-wczytywanie-danych-z-klawiatury)
5. [Debugowanie: szukanie błędów krok po kroku](#5-debugowanie-szukanie-błędów-krok-po-kroku)
6. [Typowe problemy](#6-typowe-problemy)
7. [Zapisz pracę w Gicie](#7-zapisz-pracę-w-gicie)
8. [Wersja z samym terminalem](#8-wersja-z-samym-terminalem)
9. [Co dalej](#9-co-dalej)

## 1. Co będzie potrzebne

| Narzędzie | Do czego służy |
|---|---|
| **.NET SDK** | środowisko, które kompiluje i uruchamia programy w C# |
| **Visual Studio Community** (darmowe do nauki) | edytor i debugger |
| **Git** | zapisywanie historii zmian i wysyłanie pracy na GitHub |
| konto **GitHub** | miejsce na repozytoria (u nas: konto szkolne) |

## 2. Instalacja

1. **Visual Studio Community**: pobierz instalator ze strony https://visualstudio.microsoft.com, uruchom go i zaznacz pakiet
   (workload) **„Programowanie aplikacji klasycznych na platformie .NET"** (po angielsku *.NET desktop development*).
   Instalator pobierze też potrzebne wersje .NET.
2. **Git**: pobierz z https://git-scm.com/download/win i zainstaluj z domyślnymi ustawieniami.
3. **Sprawdzenie:** otwórz terminal (menu Start → *Terminal* albo *PowerShell*) i wpisz:

   ```
   dotnet --version
   git --version
   ```

   Oba polecenia powinny wypisać numer wersji. Jeśli komputer nie zna polecenia, zamknij terminal i otwórz go ponownie.
4. **Ustaw swoje imię i e-mail w Gicie** (raz):

   ```
   git config --global user.name "Imię Nazwisko"
   git config --global user.email "twoj.adres@przyklad.pl"
   ```

> Sam .NET SDK możesz zainstalować też osobno: https://dotnet.microsoft.com/download (wybierz wersję **LTS**).

## 3. Pierwszy program w Visual Studio

1. Uruchom Visual Studio i wybierz **Utwórz nowy projekt**.
2. Wybierz szablon **Aplikacja konsolowa** (*Console App*) dla języka **C#** i kliknij **Dalej**.
3. Nadaj nazwę (np. `Pierwszy`), wybierz folder i kliknij **Dalej**, a potem **Utwórz**
   (platforma docelowa: **.NET 8** albo nowsza).
4. W pliku `Program.cs` wpisz:

   ```csharp
   Console.WriteLine("Witaj, świecie!");
   ```

5. Uruchom program klawiszami **Ctrl+F5** (*Uruchom bez debugowania*). Okno konsoli pozostanie otwarte, aż naciśniesz klawisz.
   Klawisz **F5** uruchamia program z debugerem i okno konsoli może się od razu zamknąć po zakończeniu programu.

**Co się stało?** Visual Studio skompilowało Twój kod do programu i go uruchomiło. Wynik zobaczyłeś w oknie konsoli.

## 4. Wczytywanie danych z klawiatury

```csharp
Console.OutputEncoding = System.Text.Encoding.UTF8;   // żeby w konsoli działały polskie znaki

Console.WriteLine("Witaj, świecie!");

Console.Write("Jak masz na imię? ");
string imie = Console.ReadLine();
Console.WriteLine($"Cześć, {imie}!");

Console.Write("Podaj liczbę: ");
int liczba = int.Parse(Console.ReadLine());
Console.WriteLine($"Podwojona liczba: {liczba * 2}");
```

- `Console.Write` wypisuje tekst bez przejścia do nowej linii, `Console.WriteLine` z przejściem.
- `Console.ReadLine()` zawsze zwraca **tekst**. Żeby dostać liczbę, zamieniasz go: `int.Parse(...)`.
- `$"...{zmienna}..."` to **interpolacja**: wstawia wartość zmiennej do tekstu.
- Jeśli użytkownik wpisze coś, co nie jest liczbą, `int.Parse` zgłosi błąd (`FormatException`). Bezpieczniej:
  `int.TryParse(tekst, out int liczba)` (zwraca `true` albo `false`).

## 5. Debugowanie: szukanie błędów krok po kroku

Debugger pozwala zatrzymać program w wybranym miejscu i zobaczyć wartości zmiennych.

| Klawisz | Co robi |
|---|---|
| **F9** | ustaw lub usuń **punkt przerwania** (*breakpoint*) w linii, w której stoi kursor |
| **F5** | uruchom z debugerem (zatrzyma się na punkcie przerwania) |
| **F10** | wykonaj bieżącą linię i przejdź do następnej (nie wchodzi do metod) |
| **F11** | wejdź do metody wywoływanej w bieżącej linii |
| **Shift+F5** | zatrzymaj debugowanie |

Wartości zmiennych zobaczysz w oknach **Zmienne lokalne** (*Locals*) i **Auto** na dole ekranu albo po najechaniu myszą na nazwę zmiennej.

Ćwiczenie: ustaw punkt przerwania w linii `int liczba = int.Parse(...)`, uruchom program klawiszem **F5**, wpisz liczbę
i przejdź dalej klawiszem **F10**. Obserwuj, jak zmienia się wartość `liczba`.

## 6. Typowe problemy

| Objaw | Co zrobić |
|---|---|
| Okno konsoli znika od razu po uruchomieniu | uruchom **Ctrl+F5** zamiast F5, albo dodaj na końcu programu `Console.ReadKey();` |
| Zamiast polskich znaków widzisz „krzaczki" | dodaj na początku `Console.OutputEncoding = System.Text.Encoding.UTF8;` |
| Żółte ostrzeżenia o możliwej wartości `null` (CS8600, CS8604) | to **ostrzeżenia**, nie błędy. Program się uruchomi. Przy `Console.ReadLine()` są normalne |
| Czerwone błędy „CS…" i program się nie uruchamia | przeczytaj komunikat w oknie **Lista błędów**: wskazuje plik i numer linii. Dwukrotne kliknięcie przenosi do miejsca błędu |
| `FormatException` po wpisaniu litery zamiast liczby | użyj `int.TryParse` zamiast `int.Parse` |
| `dotnet` lub `git` „nie jest rozpoznawany" | zamknij i otwórz ponownie terminal. Jeśli nie pomaga, zainstaluj program jeszcze raz |

## 7. Zapisz pracę w Gicie

W folderze projektu najpierw dodaj plik `.gitignore`, który mówi Gitowi, czego nie zapisywać (foldery `bin/` i `obj/`):

```
dotnet new gitignore
```

Potem:

```
git init
git add .
git commit -m "Pierwszy program"
```

Jeśli pracujesz na repozytorium z zadania (z GitHuba), użyj `git clone`, `git add .`, `git commit` i `git push`.
Szczegóły i typowe problemy z Gitem: [git-podstawy](https://github.com/Mazowieckie-Technikum-Innowacji/materialy-programowanie/blob/main/git-podstawy.md).

## 8. Wersja z samym terminalem

Wystarczy zainstalowany .NET SDK (bez Visual Studio) i dowolny edytor, np. Visual Studio Code:

```
dotnet new console -n Pierwszy
cd Pierwszy
dotnet run
```

- `dotnet new console -n Pierwszy` tworzy folder z projektem,
- `dotnet run` kompiluje i uruchamia program,
- plik `Program.cs` otwierasz w edytorze i zmieniasz tak samo jak w Visual Studio.

## 9. Co dalej

- [Ściąga: metody `string` i `char`](https://github.com/Mazowieckie-Technikum-Innowacji/materialy-programowanie/blob/main/csharp-sciaga-string.md)
- [Snippety do Visual Studio](https://github.com/Mazowieckie-Technikum-Innowacji/materialy-programowanie/tree/main/snippety): skróty, które wstawiają gotowy kod (klasa, wczytywanie liczby, pętle, sortowanie)
- Dokumentacja C# Microsoftu po polsku: https://learn.microsoft.com/pl-pl/dotnet/csharp/

## Licencja

Treści: [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/deed.pl). Możesz je kopiować i przerabiać,
pod warunkiem podania źródła i udostępnienia przeróbek na tej samej licencji.
