# Zarządzanie pamięcią w C++


## Czym jest pamięć operacyjna?

Pamięć operacyjna (czyli RAM) to miejsce na najróżniejsze dane dla programów, które aktualnie są uruchomione na komputerze. Kiedy, przykładowo, uruchamiamy grę, to jej "ładowanie" odnosi się właśnie do tego, że bierze ona dane, takie jak np. tekstury, modele, dźwięki **z dysku** i zapisuje je do znacznie szybszej pamięci operacyjnej. Każdemu programowi, a dokładniej procesowi, system operacyjny przydziela pulę pamięci, czyli tzw. pamięć wirtualną procesu. Kiedy program potrzebuje więcej miejsca, to wysyła odpowiednią prośbę do systemu operacyjnego, a kiedy dane miejsce nie jest już używane, to niejako mówi systemowi: "*tego miejsca już nie używam, rób z tym co chcesz*".

W sytuacji, kiedy na komputerze używamy większej liczby programów na raz, tej pamięci może zabraknąć. Niektórych barier się nie przeskoczy, bo ciężko jest oczekiwać, że na komputerze z zainstalowanymi... 2GB RAMu uruchomimy jednocześnie przeglądarkę, grę, film w tle i program do edycji filmów. Problemem jest jednak sytuacja, w której program używa zbyt dużo pamięci, bez szczególnej potrzeby, ze względu na to, że programista go źle zaprojektował. Weźmy na przykład taką prostą sytuację: gra strategiczna, w której możemy tworzyć nowe jednostki wojowników. W trakcie gry wiele jednostek jest tworzonych i część z nich np. umrze podczas walki. Wtedy taki wojownik powinien zostać usunięty z pamięci, bo już nie jest w grze używany. Jeśli programista nie umie poprawnie zarządzać pamięcią i nie będzie zwalniał jej po tym poległym wojowniku, to pamięć użyta przez grę będzie puchła... i puchła a w najgorszym wypadku zabraknie pamięci operacyjnej komputerowi i system pewnie automatycznie zamknie proces gry. Z sytuacjami, gdzie może nastąpić **wyciek pamięci** (bo tak właśnie się to nazywa) programiści spotykają się... stale i przez to jest to takie ważne. Bardziej szczegółowo, wyciek pamięci to sytuacja, w której niepotrzebna, nigdzie już nieużywana pamięć pozostaje w pamięci procesu a my tracimy ostatnią szansę, żeby ją zwolnić, bo nie mamy już żadnego "odnośnika" (czy, mówiąc bardziej po programistycznemu, wskaźnika) do tego, gdzie ta pamięć się znajduje, więc będzie ona sobie tak trwała, zaalokowana, nieużywana do końca życia procesu.

## Pamięć w języku C++

W C++ wyróżniamy cztery rodzaje alokacji pamięci. Każdy rodzaj odnosi się do tego, w jaki sposób i kiedy dane do tej pamięci trafiają i kiedy są z niej zwalniane. Po angielsku używa się określenia "**storage duration**" i oznacza to w uproszczeniu czas "życia" tego co trafia do pamięci (np. zmiennej czy obiektu). Istnieje:

- alokacja automatyczna
- alokacja statyczna
- alokacja w pamięci wątku
- alokacja dynamiczna

Obiekty zaalokowane statycznie istnieją przez cały czas życia programu a obiekty w pamięci wątku istnieją przez cały czas życia wątku. Nie chcę się dodatkowo na ten temat rozgadywać, bo to nie o te rodzaje storage duration musimy się specjalnie martwić, bo ta pamięć jest zarządzana automatycznie.

Warto jednak trochę powiedzieć o alokacji automatycznej. To właśnie z nią mamy przeważnie do czynienia. Kiedy po prostu tworzymy zmienne czy obiekty, w ten sposób, to pamięć przeznaczona dla nich jest automatycznie zwalniana, kiedy program wyjdzie poza blok kodu, w którym się znajdują. Zwykle alokacja automatyczna ma miejsce na stosie programu. Stos jest takim specjalnym typem pamięci, na który tymczasowo *wrzucamy* dane i zwykle wkrótce je *zdejmujemy*, więc nie musi być on zbyt duży, zwykle można się spodziewać, że jego rozmiar jest rzędu kilku megabajtów. Rozmiar stosu mozna sobie dostosować, ale to nie temat na ten film. Warto tutaj zauważyć, że zmienne są niszczone (zdejmowane ze stosu) w odwrotnej kolejności niż są tworzone. Ostatni który został wrzucony na stos, jest pierwszym, który zostaje z niego zdjęty, tzw. *LIFO* - z angielskiego "*last in, first out*". O ile nie jesteśmy jakimiś szaleńcami i nie alokujemy gigantycznych tablic na stosie na dłuższy czas, to nie mamy się czym martwić. W innym wypadku możemy spowodować tzw. "*stack overflow*", czyli przepełnienie stosu. Jeśli chcemy przechowywać duże ilości danych, jak np. całe tekstury, które zajmują czasem po kilkanaście czy kilkadziesiąt megabajtów, to z pomocą przychodzi nam kolejny rodzaj alokacji, o którym najwięcej trzeba powiedzieć... i jest to **alokacja dynamiczna**.

## Alokacja dynamiczna i jej ryzyko

Alokacja dynamiczna jest w całości powierzona programiście. To jego zadaniem jest zadbać o to, by we właściwym momencie zwolnić pamięć. Daje to duże możliwości, ale też stwarza zagrożenie właśnie w postaci wycieku pamięci. Alokacji dynamicznej używa się np., gdy chcemy stworzyć tablicę o liczbie elementów, która nie jest znana już w momencie pisania kodu (tzw. *compile-time*), czyli np. zależy od tego co użytkownik poda. Pamiętajmy o tym, że taki zapis w C++ jest niedozwolony!

 <!-- Przykład: -->
```cpp
int n = 0;
std::cin >> n;
int tab[n]; // niedozwolone!
```
<!-- Koniec przykładu -->

Musisz w tym przypadku zaalokować tablicę dynamicznie. Tablice w C++ jako tako nie mogą zmieniać swojego rozmiaru. Jeśli do Twojej tablicy, która aktualnie ma 5 elementów chcesz dodać kolejne 2, to będziesz musiał stworzyć nową, 7-mio elementową tablicę, skopiować 5 elementów z poprzedniej tablicy, a następnie możesz zrobić co chcesz z tymi dwoma nowymi. To stwarza potrzebę wielokrotnego alokowania i zwalniania pamięci dynamicznie. Może to wyglądać np. tak:

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

To jest bardzo naiwne podejście, które często jest spotykane wśród nowicjuszy, które ja też kiedyś przejawiałem. Osoba, która ma takie podejście **nie umie zarządzać pamięcią**. O ile w języku `C`, używając `malloc` oraz `free` taki kod byłby bezpieczny, o tyle podejście w `C++` całkowicie się zmieniło wraz z wprowadzeniem programowania obiektowego oraz mechanizmu wyjątków. W skrócie: obiekty mają tzw. konstruktory i destruktory, czyli funkcje, które są wywoływane odpowiednio, bezpośrednio po utworzeniu oraz bezpośrednio przed usunięciem obiektu. Wyjątki to szczególne sytuacje w programie, kiedy coś poszło nie tak, np. nie ma pliku z teksturą... który miał być, a więc trzeba anulować wczytywanie tekstury i jakoś rozsądnie to rozwiązać, np. wstawiając w jej miejsce jakiś prosty kolor czy coś innego. No dobra, ale wyjątki mają to do siebie, że powodują wychodzenie kolejno z wykonywanych aktualnie funkcji, w dół "stosu wywołań funkcji", aż nie zostanie napotkany fragment kodu, który obsługuje wyjątek.
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

Wspominałem o tym, że istnieją obiekty, które posiadają konstruktory i destruktory. W momencie rzucenia wyjątku, zanim program wyjdzie z aktualnie wykonywanej funkcji, wywoła destruktory wszystkich obiektów, które **zaalokowaliśmy automatycznie**, czyli tak jak zwykłe zmienne. Ten proces określa się po angielsku przez "*stack unwinding*". Żeby mieć 100-procentową pewność, że wszystko jest poprawnie zwalniane, korzysta się właśnie z tego faktu - zwalnianie każdej pamięci powierzamy destruktorowi obiektu. Ta technika nosi nazwę "*RAII*", czyli po angielsku "*Resource Acquisition Is Initialization*" i oznacza to, że zarządzanie czasem życia zasobów alokowanych dynamicznie powierzamy konstruktorowi i destruktorowi obiektu. Należy zadbać o to, by **ZAWSZE** istniał co najmniej jeden obiekt, który jest jakby właścicielem pamięci, którą zwolni gdy sam będzie niszczony... czy to przez rzucenie wyjątku, czy przez zwykłe wyjście poza blok kodu, w którym został stworzony, czyli to o czym mówiłem na początku filmu, przy okazji alokacji automatycznej.