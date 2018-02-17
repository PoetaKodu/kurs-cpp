# Start | Lekcja 1
# C++ Speedrun [PL] - Wprowadzenie

Każdy chyba zna ten moment, w którym czytanie kursu lub jego oglądanie staje się bezmyślnym patrzeniem się w ekran a wszelkie informacje zdają się odbijać od nas z zaskakującą skutecznością. Wspominając swoje pierwsze próby programowania, myślę, że gdyby tylko udało mi się wtedy znaleźć odpowiednie materiały do nauczania, cały proces poznawania języka C++ poszedłby z górki. A Ty? Może Ty też teraz znajdujesz się w takiej sytuacji. A może po prostu chcesz uzupełnić swoją wiedzę. Jeśli czujesz, że coś nie do końca rozumiesz o co chodzi w tym C++-sie, lub gdy przychodzi co do czego nie jesteś w stanie zaprogramować konkretnej rzeczy to witaj na mojej skromnej stronie. Rozgość się tutaj i poszukaj tego, co Cie najbardziej interesuje. Jeśli dopiero zaczynasz naukę, to zacznij linijkę niżej.

## Parę słów o tym uroczym języku i o programowaniu

Gdyby ktoś, kto nie ma kompletnie wiedzy w tym temacie, mnie zapytał, czym jest w ogóle programowanie, to chyba opisałbym to tak:  
> **Programowanie to uczenie komputera rozwiązywania zadań, za pomocą prostych poleceń, które możemy mu wydawać.**

Dzięki latom kreatywnego działania programistów, stworzono dziesiątki języków programowania, dzięki którym możemy, w mniej lub bardziej przyjaznej dla nas formie przekazywać rozkazy do komputera. C++ jest, w mojej opinii, genialnym językiem a umiejętność jego prawidłowego stosowania jest według mnie samą przyjemnością.

C++ został opracowany przez Bjarne Stroustrupa w 1983 roku i jest wciąż prężnie rozwijany. Nazywany jest językiem ogólnego przeznaczenia: możemy w nim pisać wieloplatformowe aplikacje, gry czy programować mikrokontrolery.  

C++ jest językiem **kompilowanym do języka maszynowego**. Oznacza to, że w procesie `kompilacji` (czyli łączenia) kod, który napiszemy, zostanie przetłumaczony na, zrozumiały dla komputera, język maszynowy.

##  Środowiska i kompilatory

Do programowania w C++ będziemy potrzebowali na początek dwóch narzędzi:

 - *środowiska* (czyli IDE), po prostu edytora z różnymi fajnymi funkcjami
 - *kompilatora*, by móc z naszego kodu stworzyć aplikację wykonywalną
 
Ja osobiście pracuję w środowisku o nazwie Visual Studio, które zawiera już kompilator Microsoftu. Inne środowiska, którę moge Wam polecić to:

 - **Code Blocks** - bardzo proste IDE i łatwe do skonfigurowania. Nie ma ciemnego motywu, więc raczej nie nadaje się do długotrwałego kodowania. 
 - **QtCreator** - dobre IDE, które, jeśli ktoś lubi grzebać w ustawieniach, potrafi być bardzo przyjemne w użytkowaniu. Ze swojego doświadczenia raczej odradzam na początek, bo jest tam trochę zabawy z ustawieniami.
 
Przebieg instalacji tych środowisk wraz z kompilatorami będziecie mogli zobaczyć na filmach, które prowadzę na swoim kanale o nazwie **Poeta Kodu**.

A jaki kompilator wybrać?

Najrozsądniej teraz jest wybrać kompilator Microsoftu wraz z *Visual Studio*, jednak nie jest on wieloplatformowy. Jeśli zdecydowałeś się na jedno z alternatywnych IDE, to raczej będziesz zainteresowany instalacją jednego z dwóch następujących kompilatorów:

 - GCC (GNU Compiler Collection, kiedyś GNU C Compiler)
 - Clang

Oba stoją na podobnym poziomie, więc nie będę Wam zaprzątał głowy rzeczami technicznymi.

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
 
## Pisanie kodu!

Nareszcie przyszedł ten moment: pisanie kodu!  
Ostrzegam, że w pierwszych momentach będzie trochę "zaufaj, że tak zadziała", ale spokojnie, po chwili się wszystko wyklaruje.
Na początku nasze IDE wygeneruje nam początkowy kod, ale my go usuniemy. Wpisujemy coś takiego:

```cpp
#include <iostream>

int main()
{
	std::cout << "Witaj swiecie!";
}
```

**Kompilujemy program** (sposób przedstawiłem w wyżej przedstawionym filmie).  

