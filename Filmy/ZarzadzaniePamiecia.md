# Zarządzanie pamięcią w C++

### Autorzy
- Główny: Paweł Syska (*Poeta Kodu*).
- Poprawki:
  - *uzupełnić listę osób, które wprowadzały poprawki do materiału*


Materiał przeznaczony na film na kanale Poeta Kodu. Zastrzegam sobie wyłączne prawo do użycia tego materiału w filmie.

Materiał zaczyna się tutaj:

## Czym jest pamięć operacyjna?

Pamięć operacyjna (czyli RAM) to miejsce na najróżniejsze dane dla programów, które aktualnie są uruchomione na komputerze. Kiedy, przykładowo, uruchamiamy grę, to jej "ładowanie" odnosi się właśnie do tego, że bierze ona dane, takie jak np. tekstury, modele, dźwięki **z dysku** i zapisuje je do znacznie szybszej pamięci operacyjnej. Każdemu programowi, a dokładniej procesowi, system operacyjny przydziela pulę pamięci, czyli tzw. pamięć wirtualną procesu. Kiedy program potrzebuje więcej miejsca, to wysyła odpowiednią prośbę do systemu operacyjnego, a kiedy dane miejsce nie jest już używane, to niejako mówi systemowi: "*tego miejsca już nie używam, rób z tym co chcesz*".

W sytuacji, kiedy na komputerze używamy większej liczby programów na raz, tej pamięci może zabraknąć. Niektórych barier się nie przeskoczy, bo ciężko jest oczekiwać, że na komputerze z zainstalowanymi... 2GB RAMu uruchomimy jednocześnie przeglądarkę, grę, film w tle i program do edycji filmów. Problemem jest jednak sytuacja, w której program używa zbyt dużo pamięci, bez szczególnej potrzeby, ze względu na to, że programista go źle zaprojektował. Weźmy na przykład taką prostą sytuację: gra strategiczna, w której możemy tworzyć nowe jednostki wojowników. W trakcie gry wiele jednostek jest tworzonych i część z nich np. umrze podczas walki. Wtedy taki wojownik powinien zostać usunięty z pamięci, bo już nie jest w grze używany. Jeśli programista nie umie poprawnie zarządzać pamięcią i nie będzie zwalniał jej po tym poległym wojowniku, to pamięć użyta przez grę będzie puchła... i puchła a w najgorszym wypadku zabraknie pamięci operacyjnej komputerowi i system pewnie automatycznie zamknie proces gry. Z sytuacjami, gdzie może nastąpić **wyciek pamięci** (bo tak właśnie się to nazywa) programiści spotykają się... stale i przez to jest to takie ważne. Bardziej szczegółowo, wyciek pamięci to sytuacja, w której niepotrzebna, nigdzie już nieużywana pamięć pozostaje zabrana przez proces a my tracimy ostatnią szansę, żeby ją zwolnić, bo nie mamy już żadnego "odnośnika" (czy, mówiąc bardziej po programistycznemu, wskaźnika) do tego, gdzie ta pamięć się znajduje, więc będzie ona sobie tak trwała, zaalokowana, nieużywana do końca życia procesu.

## Pamięć w języku C++

W C++ wyróżniamy cztery rodzaje alokacji pamięci. Każdy rodzaj odnosi się do tego, w jaki sposób i kiedy dane do tej pamięci trafiają i kiedy są z niej zwalniane. Po angielsku używa się określenia "**storage duration**" i oznacza to w uproszczeniu czas "życia" tego co trafia do pamięci (np. zmiennej czy obiektu). Istnieje:

- alokacja automatyczna
- alokacja statyczna
- alokacja w pamięci wątku
- alokacja dynamiczna

Obiekty zaalokowane statycznie istnieją przez cały czas życia programu a obiekty w pamięci wątku istnieją przez cały czas życia wątku. Nie chcę się dodatkowo na ten temat rozgadywać, bo to nie o te rodzaje storage duration musimy się specjalnie martwić, bo ta pamięć jest zarządzana automatycznie.

Warto jednak trochę powiedzieć o alokacji automatycznej. To właśnie z nią mamy przeważnie do czynienia. Kiedy po prostu tworzymy zmienne czy obiekty, w ten sposób, to pamięć przeznaczona dla nich jest automatycznie zwalniana, kiedy program wyjdzie poza blok kodu, w którym się znajdują. Zwykle alokacja automatyczna ma miejsce na stosie programu. Stos jest takim specjalnym typem pamięci, na który tymczasowo *wrzucamy* dane i zwykle wkrótce je *zdejmujemy*, więc nie musi być on zbyt duży, zwykle można się spodziewać, że jego rozmiar jest rzędu kilku megabajtów. Rozmiar stosu mozna sobie dostosować, ale to nie temat na ten film. Warto tutaj zauważyć, że zmienne są niszczone (zdejmowane ze stosu) w odwrotnej kolejności niż są tworzone. Ostatni który został wrzucony na stos, jest pierwszym, który zostaje z niego zdjęty, tzw. *LIFO* - z angielskiego "*last in, first out*". O ile nie jesteśmy jakimiś szaleńcami i nie alokujemy gigantycznych tablic na stosie na dłuższy czas, to nie mamy się czym martwić. W innym wypadku możemy spowodować tzw. "*stack overflow*", czyli przepełnienie stosu. Jeśli chcemy przechowywać duże ilości danych, jak np. całe tekstury, które zajmują czasem po kilkanaście czy kilkadziesiąt megabajtów, to z pomocą przychodzi nam kolejny rodzaj alokacji, o którym najwięcej trzeba powiedzieć... i jest to **alokacja dynamiczna**.

## Alokacja dynamiczna i jej ryzyko

Alokacja dynamiczna jest w całości powierzona programiście. To on manualnie, jawnie, samemu decyduje gdzie zaalokuje i gdzie zwolni pamięć... i to w jego interesie jest, żeby zadbać o to, by nie dopuścić do powstania wycieku pamięci. Daje to duże możliwości, ale też stwarza zagrożenie. Alokacji dynamicznej używa się np., gdy chcemy stworzyć tablicę o liczbie elementów, która nie jest znana już w momencie pisania kodu (w tzw. *compile-time*), czyli np. zależy od tego co użytkownik programu wpisze do konsoli. Pamiętajmy o tym, że taki zapis w C++ jest niedozwolony!

 <!-- Przykład: -->
```cpp
int n = 0;
std::cin >> n;
int tab[n]; // niedozwolone!
```
<!-- Koniec przykładu -->

Nie można utworzyć w ten sposób tablicy, której rozmiar nie jest znany w *compile-timie*. Musisz w tym przypadku zaalokować tablicę dynamicznie. Tablice w C++ jako tako nie mogą zmieniać swojego rozmiaru. Jeśli do Twojej tablicy, która aktualnie ma 5 elementów chcesz dodać kolejne 2, to będziesz musiał stworzyć nową, 7-mio elementową tablicę, skopiować 5 elementów z poprzedniej tablicy, a następnie możesz zrobić co chcesz z tymi dwoma nowymi. To stwarza potrzebę wielokrotnego alokowania i zwalniania pamięci dynamicznie. Może to wyglądać np. tak:

<!-- Przykład: -->
```cpp
// Tablica 5-ciu elementów:
int* tab = new int[5] {3, 2, 1, 5, 6};

// Ten fragment zwieksza rozmiar tablicy "tab" o 2.
{
	int* tabBigger = new int[7]; // Nowa, większa tablica
	// Kopiuje poprzednie elementy:
	for(int i = 0; i < 5; ++i)
		tabBigger[i] = tab[i];
	// Zwalniam poprzednią tablicę:
	delete[] tab;
	// Podmieniam wskazniki, teraz "tab" wskazuje na nową tablicę.
	tab = tabBigger;
}
// Robie co chce z nowymi elementami:
tab[5] = 8;
tab[6] = 10;

// Na koniec zwalniam tablice.
delete[] tab;
```
<!-- Koniec przykładu -->

Zapomnij w którymś z tych miejsc użyć `delete[]` i masz wyciek pamięci.

<!-- Chwila przerwy na analizę kodu. Jakaś zgrabna animacja. -->

No dobrze, ale teraz ktoś może się odezwać i powiedzieć:

> Przecież jak nie zapomnę tego zwolnić to wszystko będzie okej.

To jest bardzo naiwne podejście, które często jest spotykane wśród nowicjuszy, które ja też kiedyś przejawiałem. Osoba, która ma takie podejście **nie umie zarządzać pamięcią**. O ile w języku `C`, używając `malloc` oraz `free` taki kod byłby bezpieczny, o tyle podejście w `C++` całkowicie się zmieniło wraz z wprowadzeniem programowania obiektowego oraz mechanizmu wyjątków. W skrócie: obiekty (a raczej klasy) mają tzw. konstruktory i destruktory, czyli funkcje, które są wywoływane odpowiednio, bezpośrednio po utworzeniu oraz bezpośrednio przed usunięciem obiektu. Wyjątki to szczególne sytuacje w programie, kiedy coś poszło nie tak, np. nie ma pliku z teksturą... który miał być, a więc trzeba anulować wczytywanie tekstury i jakoś rozsądnie to rozwiązać, np. wstawiając w jej miejsce jakiś prosty kolor czy coś innego. No dobra, ale wyjątki mają to do siebie, że powodują wychodzenie kolejno z wykonywanych aktualnie funkcji, w dół "stosu wywołań funkcji", aż nie zostanie napotkany fragment kodu, który obsługuje wyjątek.
No i jeśli taki wyjątek nastąpi przykładowo... **tu**.

<!--  Przykład, gdzie nastąpi: -->
```cpp
// Tablica 5-ciu elementów:
int* tab = new int[5] {3, 2, 1, 5, 6};

// Ten fragment zwieksza rozmiar tablicy "tab" o 2.
{
	int* tabBigger = new int[7]; // Nowa, większa tablica
	// Kopiuje poprzednie elementy:
	for(int i = 0; i < 5; ++i)
		tabBigger[i] = tab[i];

	// Wyjątek następuje tutaj:
	throw std::runtime_error("jakis wyjatek");

	// Zwalniam poprzednią tablicę:
	delete[] tab;
	// Podmieniam wskazniki, teraz "tab" wskazuje na nową tablicę.
	tab = tabBigger;
}
// Robie co chce z nowymi elementami:
tab[5] = 8;
tab[6] = 10;

// Na koniec zwalniam tablice.
delete[] tab;
```
<!-- Koniec przykładu -->
To nasz program nigdy nie dojdzie do momentu, w którym zwalnia pamięć tablic, które zaalokował dynamicznie... no i mamy wyciek pamięci.

> Ale co Ty gadasz? Ja będę uważał.

No... Ty możesz nie rzucać samemu wyjątków, możesz uważać, że wszystko jest okej... ale biblioteki, z których korzystasz (**W TYM BIBLIOTEKA STANDARDOWA C++**) może rzucić wyjątek... i co wtedy? To **NIE** jest poprawne podejście do zarządzania pamięcią. Choćbyś nie wiem jak się starał, **NIE** jesteś w stanie przewidzieć wszystkich scenariuszy.

## Jak zarządzać poprawnie dynamiczną pamięcią?

Wspominałem o tym, że istnieją obiekty, które posiadają konstruktory i destruktory. W momencie rzucenia wyjątku, zanim program wyjdzie z aktualnie wykonywanej funkcji, wywoła destruktory wszystkich obiektów, które **zaalokowaliśmy automatycznie**, czyli tak jak zwykłe zmienne. Ten proces określa się po angielsku przez "*stack unwinding*". Żeby mieć 100-procentową pewność, że wszystko jest poprawnie zwalniane, korzysta się właśnie z tego faktu - zwalnianie każdej, dynamicznie zaalokowanej, pamięci powierzamy destruktorowi obiektu. Ta technika nosi nazwę "*RAII*", czyli po angielsku "*Resource Acquisition Is Initialization*" i oznacza to, że zarządzanie czasem życia zasobów alokowanych dynamicznie powierzamy konstruktorowi i destruktorowi obiektu. Należy zadbać o to, by **ZAWSZE** istniał co najmniej jeden obiekt, który jest jakby właścicielem pamięci, którą zwolni gdy sam będzie niszczony... czy to przez rzucenie wyjątku, czy przez zwykłe wyjście poza blok kodu, w którym został stworzony, czyli to o czym mówiłem na początku filmu, przy okazji alokacji automatycznej.

Przykładem poprawnie wykonanego RAII dla tablicy może być coś takiego:

<!-- Przykład RAII -->
```cpp
class DynamicArray
{
public:
	// Konstruktor:
	DynamicArray(int size_) {
		// Powinno się też użyć listy inicjalizacyjnej.
		ptr = new int[size_];
	}
	// Destruktor:
	~DynamicArray() {
		delete[] ptr;
	}

	int* ptr;
};
```
<!-- Koniec przykładu RAII -->

Wtedy nie musimy się martwić o to, że nasza tablica nie zostanie zwolniona w takim wypadku:

<!-- Przykład -->
```cpp
{
	DynamicArray arr(10);
	throw std::runtime_error("jakis wyjatek");
}
```
<!-- Koniec przykładu -->

W praktyce, w `DynamicArray` brakuje jeszcze paru rzeczy, ale w tym filmie możemy to pominąć... bo rada dla programistów C++ jest taka, żeby korzystać z kontenerów z biblioteki standardowej. Jeśli potrzebujesz tablicy o zmiennym rozmiarze, użyj `std::vector`. Oto porównanie wcześniejszego kodu z rzucaniem wyjątku i zmianą rozmiaru tablicy z kodem, który robi to samo... ale używa `std::vector` z biblioteki standardowej.

<!--  Przykład, gdzie nastąpi: -->
```cpp
// Na początku programu:
#include <vector>

// Tablica 5-ciu elementów:
std::vector<int> tab = {3, 2, 1, 5, 6};
// Dodaj liczbe 8 na koniec
tab.push_back(8);
// Dodaj liczbe 10 na koniec
tab.push_back(10);

// Mimo rzucenia wyjątku, wszystko jest ładnie zwalniane.
throw std::runtime_error("jakis wyjatek");

```
<!-- Koniec przykładu -->

Prawda, że prościej, łatwiej i przyjemniej? Nie używajcie zwykłych tablic.

## Dynamiczna alokacja i obiekty

Wiemy już co robić w przypadku tablic. A co jeśli chcemy stworzyć dynamicznie obiekt i mieć pewność, że zostanie poprawnie zwolniony? W tym wypadku również korzystamy z biblioteki standardowej i specjalnie przygotowanych inteligentnych wskaźników, po angielsku nazywanych *smart pointerami*. Smart pointery to specjalnie przygotowane klasy, tak jak wcześniej pokazane `DynamicArray`, które służą właśnie do tego, by automatycznie zarządzać zaalokowaną pamięcią. Trzeba teraz wprowadzić pojęcia:

- owning pointer (wskaźnik właściciel)
- non-owning pointer (wskaźnik niebędący właścicielem)

Wskaźnik właściciel to właśnie inteligentny wskaźnik, który jest używany głównie do kontrolowania czasu życia obiektu.
Wskaźnik niebędący właścicielem to zwykły wskaźnik taki jak znamy z C++, czyli mówiąc kolokwialnie "ten z gwiazdką".

W C++ istnieją dwa inteligentne wskaźniki i jeden "pomocniczy" inteligentny wskaźnik:

- `unique_ptr` - unikalny wskaźnik
- `shared_ptr` - wskaźnik współdzielony
- `weak_ptr` - "słaby" wskaźnik (pomocniczy)

`unique_ptr` jest zawsze **JEDYNYM**, unikalnym właścicielem obiektu. To czas życia `unique_ptr` decyduje o tym, ile będzie żył obiekt, na który wskazuje. Kiedy niszczony jest wskaźnik, to niszczony jest też obiekt. W zdecydowanej większości będziecie korzystać właśnie z tego typu smart pointera.

`shared_ptr` jest jednym z wielu wskaźników, które wspólnie odnoszą się do jednego obiektu w pamięci. Kiedy `shared_ptr` jest niszczony, to działa to na zasadzie "ostatni zamyka drzwi", czyli dopiero ostatni `shared_ptr` niszczy też obiekt, na który wskazywał. Jest on wolniejszy niż `unique_ptr`, jednak czasem niezbędny, np. gdy nasz program posiada wiele wątków, z których chcemy dostać się do jednego obiektu w pamięci, albo gdy np. mamy 10 modeli w grze, z których każdy korzysta z tej samej tekstury i chcemy, aby sama tekstura została zwolniona z pamięci, dopiero gdy ostatni model przestanie istnieć.

`weak_ptr` to słaby wskaźnik, który współpracuje z `shared_ptr`-ami. Nie bierze on udziału w metodzie "ostatni zamyka drzwi". Nawet jeśli do danego obiektu w pamięci będzie istniało jeszcze 100 `weak_ptr`-ów, to wciąż, ostatni `shared_ptr` zwolni po sobie obiekt. `weak_ptr` służy do tego, by móc sprawdzić, czy obiekt, na który wskazuje, jeszcze istnieje... i jeśli tak, to możemy użyć tego `weak_ptr`-a do stworzenia `shared_ptr`, żeby się odwołać do obiektu.

Każdy z tych wskaźników znajdzie swoje zastosowanie, które zaraz pokażę. Najpierw jednak kluczowa i najważniejsza zasada w zarządzaniu pamięcią z użyciem smart pointerów.
Inteligentne wskaźniki służą do kontrolowania czasu życia obiektu **i przede wszystkim do tego**. Mogła się pojawić wątpliwość, u kogoś z oglądających, że przecież skoro mamy jednego właściciela, w postaci `unique_ptr`, to jak ja przekażę ten wskaźnik do funkcji? W tym momencie...
 <!-- Tutaj pokazanie na moment wywołania funkcji  -->
 <!-- Przykład -->
```cpp
void addTen(std::unique_ptr<int> ptr_) {
		*ptr_ += 10;
}
int main() {
	std::unique_ptr<int> x = new int(20);
	// TUTAJ:
	addTen(x);
}
```
 <!--  -->
...wskaźnik będzie musiał zostać skopiowany, a więc będą istniały dwa unikalne wskaźniki do jednego obiektu w pamięci, co jest przecież zabronione. **I TO JEST PRAWDA**. Przy kompilacji tego kodu, dostaniemy błąd od kompilatora. Nie możemy skopiować `unique_ptr`. W tym wypadku mamy trzy wyjścia:

- przekazać surowy, zwykły wskaźnik do `int`-a, czyli "ten z gwiazdką" 
- przekazać referencję do `int`-a
- przenieść "odpowiedzialność" nad zaalokowanym `int`-em na wskaźnik `ptr_` w funkcji `addTen`.

<!-- Przykłady powyższej listy -->
<!-- Przykład 1 -->
```cpp
void addTen(int* ptr_) {
	 *ptr_ += 10;
}
int main() {
	std::unique_ptr<int> x = new int(20);
	// funkcja get() zwraca surowy wskaźnik
	addTen(x.get());
}
```
<!-- Przykład 2 -->
```cpp
void addTen(int& ref_) {
	 ref_ += 10;
}
int main() {
	std::unique_ptr<int> x = new int(20);
	// operator dereferencji (czyli *x), działa tak samo
	// jak na zwykłym wskaźniku
	addTen(*x);
}
```
<!-- Przykład 2 -->
```cpp
void addTen(std::unique_ptr<int> ptr_) {
	*ptr_ += 10;
}
int main() {
	std::unique_ptr<int> x = new int(20);
	// używamy std::move, aby przenieść "odpowiedzialność"
	addTen(std::move(x));
	// po wykonaniu tej funkcji "x" jest pustym wskaźnikiem.
}
```
<!-- Koniec przykładów -->

Musimy się liczyć z tym, z czym wiąże się użycie każdego z tych sposobów. Funkcja, która przyjmuje zwykły wskaźnik dopuszcza podanie pustego wskaźnika, czyli `nullptr`. Funkcja, która wymaga przeniesienia odpowiedzialności, już na pierwszy rzut oka mówi programiście, że to ona od teraz zajmie się zarządzaniem czasem życia obiektu. Najlepszym wyjściem tutaj będzie użycie referencji. Zadaniem tej funkcji jest zwiększenie wartości jakiegoś `int`-a o 10, więc od razu zakładamy, że taki `int` musi istnieć, więc nie pozwalamy na podanie `nullptr`-a. No i przede wszystkim, ta funkcja nic innego nie robi, więc nie potrzebna jest jej odpowiedzialność nad tym `int`-em.

Bardzo podobnie jest w przypadku `shared_ptr`-ów. Jeśli funkcja ma wykonać tylko jakąś operację na tym, do czego odnosi się `shared_ptr` to używamy referencji. Jeśli z jakiegoś powodu, ta rzecz może nie istnieć, to podajemy wskaźnik. Dopiero, jeśli funkcja zarządza czasem życia obiektu, podajemy tam odpowiedni, inteligentny wskaźnik. **Błędnym** jest przekonanie, że zwykłe, surowe wskaźniki zostały wyparte przez te inteligentne. Surowe wskaźniki **NIGDY** nie powinny być używane do zarządzania czasem życia obiektu, ale są idealne jako sposób do "dostania" się do obiektu, jego właściwości itd.

## Przykłady użycia unique_ptr

TODO

## Przykłady użycia shared_ptr

TODO

## Przykłady użycia weak_ptr

TODO

## Zakończenie

TODO