# Start | Lekcja 1
# C++ Speedrun - Wprowadzenie

Kilka informacji rozpoczynających:

* **Dlaczego ten kurs?**  
Staram się w nim przedstawić *jak poprawnie programować*, a nie tak, żeby tylko zdać egzamin.
* **Czego się z tej lekcji dowiem?**  
Pokaże Ci, jak sprawnie rozpocząć programowanie w C++. Wytłumaczę też strukturę podstawowego programu.

Zapraszam do czytania.

## Parę słów o języku i o programowaniu

Gdyby ktoś, kto nie ma kompletnie wiedzy w tym temacie, mnie zapytał, czym jest w ogóle programowanie, to chyba opisałbym to tak:  
> **Programowanie to uczenie komputera rozwiązywania zadań, za pomocą prostych poleceń, które możemy mu wydawać.**

Dzięki latom kreatywnego działania programistów, stworzono dziesiątki języków programowania, dzięki którym możemy, w mniej lub bardziej przyjaznej dla nas formie, przekazywać rozkazy do komputera. C++ jest, w mojej opinii, genialnym językiem a umiejętność jego prawidłowego stosowania jest według mnie samą przyjemnością.

C++ został opracowany przez Bjarne Stroustrupa w 1983 roku i jest wciąż prężnie rozwijany. Nazywany jest językiem ogólnego przeznaczenia: możemy w nim pisać wieloplatformowe aplikacje, gry czy programować mikrokontrolery.  
C++ jest językiem **kompilowanym do języka maszynowego**. Oznacza to, że w procesie `kompilacji` (łączenia i tłumaczenia kodu przez narzędzie zwane *kompilatorem*) kod, który napiszemy, zostanie przetłumaczony na, zrozumiały dla komputera, język maszynowy.

##  Czego potrzebujemy?

Do programowania w C++ będziemy musieli posiadać dwa narzędzia:

- **środowisko** (ang.: IDE) - edytor z rozmaitymi funkcjami, ułatwiającymi pisanie kodu.  
Środowisko najczęściej zwalnia nas z ręcznej obsługi kompilatora, upraszczając jego polecenia do:

	|Polski                    |Angielski          | Znaczenie                                  |
	|:------------------------:|:-----------------:|:-------------------------------------------|
	|skompiluj (lub zbuduj)    |compile (build)    |przeprowadza cały proces kompilacji         |
	|skompiluj i uruchom       |compile and run    |kompiluje a potem uruchamia program wynikowy|
	|rekompiluj (lub przebuduj)|recompile (rebuild)|kompiluje wszystko od nowa<sup>[1]</sup>    |
	
	Warto jeszcze wspomnieć, że edytory takie jak Notatnik, [Notepad++](https://notepad-plus-plus.org/) czy [Atom](https://atom.io/) również mogą być środowiskami, chociaż pewnie wymagana będzie własnoręczna obsługa kompilatora.
	
- **kompilator** - przetwarza kod danego języka do postaci zrozumiałej dla komputera.
 
<sup>1</sup> - jeśli kod umieszczamy w więcej niż jednym pliku, to kompilator nie musi za każdym razem przerabiać wszystkich od nowa, tylko bierze pod uwage te, które zmodyfikowaliśmy od ostatniej kompilacji.

### Jakie środowisko wybrać?

Używając systemu operacyjnego Windows, najrozsądniej będzie teraz chyba użyć *Microsoft Visual Studio 2017*. Posiada darmową wersję, jest dostarczane razem z bardzo dobrym kompilatorem Microsoftu i znacznie ułatwia programowanie na każdym stopniu posiadanej wiedzy. Osoba, która dopiero zaczyna naukę, na pewno zakocha się w tych elementach:

* **Możliwość wyboru jednego z kilku motywów, w tym jedynego słusznego - ciemnego.**  
TODO: dodać screena
* **Obsługa wielu języków.**  
Chociaż jest dostępny język polski, to ja osobiście pracuję na wersji angielskiej, ponieważ szybciej rozpoznaje angielskie wersje terminów programistycznych. Tobie też to polecam, bo przy okazji poznasz dodatkową terminologię.
TODO: dodać screena
* **Wszystko co potrzebujesz do programowania zawarte w jednej aplikacji.**
* **Wszelkie ustawienia można po prostu "przeklikać".**  
To jest chyba decydujący argument za wyborem tego środowiska. Wiele innych środowisk wymaga już pewnego, czasem zdecydowanie zbyt dużego, obeznania w terminach programistycznych, komendach kompilatora oraz wiele wiele innych.

Niestety, posiada on też parę wad, które są konsekwencją powyższych wygód:

* **Duży, jak na środowisko + kompilator, rozmiar zajmowany na dysku.**  
Jeśli podczas instalacji wybierzesz tylko pakiet C++, to instalacja nie powinna przekroczyć 8 GB. Visual Studio jednak to nie tylko C++ - to również ogrom innych języków, pakietów itd. Jeśli zaznaczysz wszystkie pakiety na oślep, to wymagane miejsce na dysku może skoczyć do kilkudziesięciu gigabajtów.
* **Większe wymagania sprzętowe.**  
Chociaż nie są one ogromne, to na starszych laptopach czy komputerach środowisko może przycinać.
* **Wsparcie tylko dla systemu Windows.**
Visual Studio nie wspiera innych systemów, co linuksiarzom może zepsuć humor.  
**Uwaga!** *Visual Studio Code* ma się nijak do *Visual Studio 2017*, o którym jest mowa. VS Code jest multiplatformowy ale to całkowicie inne narzędzie.

Jeśli jednak z jakiegoś powodu nie możesz się na nie zdecydować, to oto inne środowiska, którę moge Wam polecić to:

- **Code Blocks** - bardzo proste, przystępne IDE, dostępne na różnych systemach operacyjnych. Doskonale nadaje się jako IDE, które można spakować na pendrive i korzystać z niego gdziekolwiek indziej.  
Charakterystyka:

	- Plusy:

		- Mało zajmuje.
		- Przenośne.
		- Instalacja trwa kilka minut.
		- Łatwe do skonfigurowania.
		- Wszelkie ustawienia projektu można przeklikać!
		- Obsługuje różne kompilatory.
	
	- Minusy:

		- **Nie ma ciemnego motywu**, więc raczej nie nadaje się do długotrwałego kodowania.
		- Nie posiada sprawdzania poprawności kodu w czasie rzeczywistym.
		- Słabe podpowiadanie *(ang.: auto completion)*
		- Nie posiada integracji z repozytorium Git, chociaż początkujący raczej nie zwrócą na to uwagi.
	
- **QtCreator** - dobre IDE, które, jeśli ktoś lubi grzebać w ustawieniach, potrafi być bardzo przyjemne w użytkowaniu. Ze swojego doświadczenia raczej odradzam na początek, bo jest tam trochę zabawy z ustawieniami.  
Charakterystyka:

	- Plusy:
	
		- Mało zajmuje.
		- Przenośne.
		- Instalacja trwa kilka minut.
		- Obsługuje różne kompilatory.
		- Dobrze podpowiada kod.
		- Posiada sprawdzanie poprawności kodu w czasie rzeczywistym.
		- Posiada ciemny motyw.
	
	- Minusy
		- **Ustawienie projektu sprowadzają się do ręcznego pisania skryptu, na podstawie którego QtCreator skorzysta z kompilatora!**
		
- **Eclipse**  
Brak mi informacji o tym IDE, chociaż słyszałem o nim wiele dobrych słów.
- **NetBeans**  
Podobnie jak u góry, chociaż mniej znane.
 
Przebieg instalacji tych środowisk wraz z kompilatorami będziecie mogli zobaczyć na filmach, które prowadzę na swoim kanale o nazwie **Poeta Kodu**.

### Jaki kompilator wybrać?

Najrozsądniej teraz jest wybrać kompilator Microsoftu wraz z *Visual Studio*, jednak nie jest on wieloplatformowy. Jeśli zdecydowałeś się na jedno z alternatywnych IDE, to raczej będziesz zainteresowany instalacją jednego z dwóch następujących kompilatorów:

- GCC (GNU Compiler Collection)
- Clang

Oba stoją na podobnym poziomie, więc nie będę Wam zaprzątał głowy rzeczami technicznymi.

### Czego na pewno NIE wybierać?

- [Dev-C++](dlaczego-nie-dev-cpp.md)
- [C++Builder](dlaczego-nie-cpp-builder.md)
- [Turbo C++](dlaczego-nie-turbo-cpp.md)

## Przygotowywanie środowiska pracy

Żeby nie zostawić nikogo na lodzie, bez żadnego środowiska czy kompilatora, pokażę Wam teraz, jak zainstalować Visual Studio oraz Code Blocks w prosty sposób tak, żeby móc przejść już do programowania.

### Instalacja Visual Studio

```diff
- TODO: dodać film lub screenshoty do poszczególnych podpunktów.
```

Po pierwsze - ostrzeżenie: Visual Studio jest dość obszernym środowiskiem, tak że instalacja jego może zająć nawet ponad godzinę, zależnie od naszego sprzętu.  

1. Wchodzimy na stronę: www.visualstudio.com  
Naszym celem jest pobranie środowiska dla systemu Windows, w wersji `Community` (czyli darmowej).
2. Po pobraniu odpalamy instalację i kierujemy się zgodnie z wytycznymi kreatora. Jest to czasochłonny proces, więc zwrócę jeszcze tylko uwagę na jedną rzecz:  
W pewnym momencie, będziemy mieli wybrać jakie pakiety z środowiska Visual Studio chcemy zainstalować. Nas interesuje tylko:
 
	* TODO: umiescic listę pakietów, które trzeba pobrać.
   
3. Warto jest szlifować angielski, więc instalujemy też angielski pakiet językowy. Ten krok jest ważny, nie pomijaj go.
4. Kiedy już Visual Studio zostanie zainstalowane, zmieniamy motyw na ciemny oraz język na angielski.
5. Teraz tworzymy nasz pierwszy projekt w kreatorze: wybieramy aplikację konsolową Windows.  
Nasz kod będziemy pisali w pliku main.cpp.
 
### Instalacja Code Blocks

1. Wchodzimy na stronę Code Blocksa, w dział download i pobieramy najnowszą wersję, **bez kompilatora**.  
[CodeBlocks](http://www.codeblocks.org/downloads/26)
2. Przechodzimy do pobrania kompilatora w paczce, która się nazywa `**MinGW-64**`.  
[MinGW-64](https://sourceforge.net/projects/mingw-w64/files/#readme)
3. Szukamy najnowszej paczki, czyli np.:  
`MinGW-w64 GCC 7.2.0 x86_64-win32-sjlj`
4. Musimy wypakować pliki. Teraz postępujemy już według filmu, w którym pokazałem cały proces instalacji wraz z wstępnym "oprowadzeniem" po środowisku.  
*Kliknij w obrazek poniżej by przejść do filmu.*  
[![Jak zainstalować Code Blocks?](http://img.youtube.com/vi/CETaETCm728/0.jpg)](http://www.youtube.com/watch?v=CETaETCm728)
 
## Rozpoczęcie programowania

Ostrzegam, że w pierwszych momentach będzie trochę "zaufaj, że tak zadziała", ale spokojnie: po chwili się wszystko wyklaruje. Na początku nasze IDE wygeneruje nam początkowy kod, ale my go usuniemy.  
Wpisujemy coś takiego:

```cpp
#include <iostream>

int main()
{
	std::cout << "Witaj swiecie!";
}
```

**Kompilujemy i uruchamiamy program** (zobacz na wyżej przedstawionym filmie).  
Co tu się właściwie stało? Nagle, przy uruchomieniu, pojawiła się czarna konsola znikąd i:

* w ciągu ułamka sekundy znikła  
*(efekt dla ręcznego uruchomienia programu lub środowiska Visual Studio)*
* w konsoli pojawił się tekst `Witaj swiecie!`, kilka linijek niżej parę innych informacji i konsolka czeka aż się ją zamknie  
*(efekt dla uruchamiania z poziomu Code Blocks - te kilka dodatkowych linijek to informacje statystyczne, które podaje nam Code::Blocks, na końcu też zatrzymuje działanie programu)*
 
Na razie nasz kod jest prawie pusty i dlatego też niewiele robi. Spójrzmy po kolei, co my tutaj mamy:

* Dodawanie zewnętrznych funkcjonalności:

	```cpp
	#include <iostream>
	```
	
	Ta linijka mówi dosłownie, żeby kompilator fizycznie znalazł plik o nazwie `iostream` gdzieś na dysku (prawdopodobnie znajduje się w jednym z podfolderów kompilatora), a następnie całą jego zawartość skopiował do pliku, w którym tą linijkę napisaliśmy - *main.cpp*  
	C++, w czystej formie, nie posiada wielu funkcjonalności, które fizycznie moglibyśmy zaobserwować. Możemy co prawda wykonywać mnóstwo operacji logicznych, arytmetycznych itp., ale nie zobaczymy ich wyniku.  
	Z pomocą przyszli nam programiści tzw. **biblioteki standardowej C++**, którzy zaprogramowali dla nas mnóstwo ciekawych narzędzi, z których możemy do woli korzystać. Tak właśnie jest z wejściem i wyjściem konsoli. Możemy za pomocą **wyjścia** *(ang.: output)* wyprowadzić dane (np. tekst) do konsolki i tym samym sprawić, że użytkownik to zobaczy. Aby zyskać właśnie dostęp do wejścia i wyjścia konsoli dołączamy *(ang.: include)* do kodu plik `iostream`. Nazwa *iostream* dosłownie jest zlepkiem angielskich wyrazów "*input/output stream*" czyli "*strumienie (danych) wejścia i wyjścia*".  
* Główna funkcja programu:

	```cpp
	int main()
	{
	}
	```
	
	TODO:
