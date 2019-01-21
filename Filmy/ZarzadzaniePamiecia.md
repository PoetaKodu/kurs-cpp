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

## Alokacja dynamiczna



