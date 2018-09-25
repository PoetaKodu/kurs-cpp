# Wstęp > Absolutne podstawy
### <div align="right">Kurs C++ `by Poeta Kodu`</div>

## Czym jest programowanie

Programowanie pozwala Ci określać, co krok po kroku ma wykonać program, który tworzysz. Może on się uruchamiać na komputerze, na telefonie, mikrokontrolerze, który np. steruje jakimś robotem, czy też na elektronice sprzętu AGD.

Dzięki programowaniu możesz korzystać z komputera, czytać na nim właśnie ten kurs w oknie przeglądarki czy przeglądać portale społecznościowe. Właściwie z programowaniem masz do czynienia, w każdej sytuacji, gdzie ustalasz dokładnie krok po kroku zachowanie czegoś, za pomocą poleceń.

Polecenia wydaje się przy użyciu języków programowania. Całość tak naprawdę sprowadza się do tego, żeby jakoś tym językiem przedstawić zamysł programisty. Programista wcześniej obmyśla plan jak ma coś działać, używając do tego jednego z ludzkich języków i następnie myśli, jak zapisać to samo za pomocą języka programowania. Ten kurs dotyczy języka `C++`. Charakteryzuje się on m.in. tym, że:

- **jest imperatywny** - programowanie w nim polega na wydawaniu kolejno pewnych poleceń
- **jest wysokopoziomowy** - składnia w dużym stopniu przypomina język ludzki (tu angielski), tak że całkiem łatwo jest mniej więcej zrozumieć zachowanie programu, nie znając nawet tego języka.
- **jest wieloplatformowy** - można programować w nim w taki sposób, by ten sam kod działał uruchamiany na różnych systemach operacyjnych, np. na Windowsie, Linuxie czy Androidzie.
- **jest ogólnego użytku** - można go używać do programowania gier, aplikacji biurowych, aplikacji mobilnych czy mikrokontrolerów

Programista zwykle zapisuje swój kod do osobnego pliku. Początkowo spotkasz się często z nazwą `Main.cpp`, lub innymi do niej podobnymi, co po prostu oznacza, że jest to plik główny programu (z ang. *main* oznacza *główny*) z kodem źródłowym napisanym w języku Cpp (`C++` = `C Plus Plus` = `Cpp`, lub czasem `CXX`).

## Uruchamianie napisanego kodu

Gdy napiszesz kod z poleceniami, będziesz mógł go uruchomić. Niech za przykład posłuży tzw. `Hello World!`, czyli program, który często symbolicznie pisze się, gdy uczysz się nowego języka programowania. Taka aplikacja po prostu wyświetla w dowolny sposób angielski tekst "Witaj świecie!". Tak będzie to wyglądało w języku C++:

```cpp
#include <iostream>

using std::cout;

int main()
{
	cout << "Hello World";
}
```

Na analizę tego kodu jeszcze przyjdzie czas. Na razie omówmy, co musisz zrobić, aby zobaczyć jak ten program działa. Komputer nie rozumie tego języka. Jeśli zaglądałeś kiedyś do zawartości plików wykonywalnych (na Windowsie np. `.exe` lub `.dll`), to pewnie zdziwiłeś się, bo jest to kompletnie niezrozumiałe dla człowieka.

![Plik wykonywalny otworzony notatnikiem][img executable-in-notepad]

Ale w takiej formie musisz dostarczyć swój kod komputerowi. To co widać u góry, to **skompilowany** kod. Kod przechodzi proces **kompilacji**, czyli tłumaczenia ze składni języka programowania na **kod maszynowy**. Dopiero wówczas może zostać uruchomiony. Można łatwo się domyślić, że narzędziem, które nam **skompiluje** kod jest **kompilator** (ang.: *compiler*).

![Proces kompilacji kodu źródłowego][img compilation]

Gdy już przejdziesz przez proces kompilacji, dostaniesz swoją gotową aplikację. W przypadku naszego "Hello World", oczekujemy że zobaczymy takie właśnie powitanie.

**Jeśli spróbujesz uruchomić tą aplikację, pojawi się czarna konsola, która najprawdopodobniej zdąży zniknąć zanim w ogóle ją zauważysz.**

Dzieje się tak dlatego, że program zaraz po zakończeniu swojego działania (czyli wyświetleniu napisu `Hello World`) zamyka się. Możesz zapobiec temu w prosty sposób - uruchamiając aplikację poprzez terminal, czy też konsolkę systemową. Warto o tym pamiętać w przyszłości. Tak wygląda wynik na moim komputerze:

![Wynik programu Hello World][img hello-world]

<!-- Next and previous lesson -->
<hr>
<p>
	Poprzednia lekcja lekcja:<br>
	<a href="Wstep.md">&lt;&lt;&lt; Wstęp</a>
</p>

<!-- Links and images -->
[img executable-in-notepad]: Images/ExecutableInNotepad.png
[img compilation]: Images/Compilation.png
[img hello-world]: Images/OutputHelloWorld.png