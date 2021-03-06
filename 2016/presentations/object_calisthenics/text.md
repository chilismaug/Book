# Object calisthenics

## Czym jest kalistenika?

Według definicji podanej przez Wikipedię, kalistenika to "aktywność fizyczna
polegająca na treningu siłowym opartym o ćwiczenia z wykorzystaniem własnej
masy ciała"&nbsp;[1]. Kiedy mówimy o kalistenice, najprościej jest zwizualizować
to pojęcie przywołując gladiatorów. Aż do XX wieku nie istniały siłownie -
żadnych bieżni mechanicznych, rowerów stacjonarnych, hantli. Był tylko
człowiek i masa jego ciała, którą mógł wykorzystać do ćwiczeń. Efektem takich
ćwiczeń, bez wykorzystania dodatkowego sprzętu, była czysta siła, a masa
mięśniowa stanowiła dodatkowy efekt uboczny - nie była celem samym w sobie.

Podobnie sprawa ma się z kalisteniką obiektową. Pod tym pojęciem kryją się
proste ćwiczenia. Zupełnie podstawowe reguły, które nie wymagają
nadzwyczajnych umiejętności, ani dodatkowych narzędzi. Celem jest poprawa
jakości kodu, pisanie kodu prostszego w utrzymaniu, prostszego w zrozumieniu,
możliwego do ponownego użycia oraz takiego, który można łatwo testować.

Kalistenika obiektowa została pierwotnie przedstawiona w eseju Jeffa Bay’a
i opublikowana w książce pt. *ThoughtWorks Anthology* [2]. Początkowo została
pomyślana z przeznaczeniem dla zastosowania w Javie, natomiast później
zaadaptowano ją na potrzeby innych języków programowania.

Dosyć popularnym powiedzeniem jest, że kod jest dużo częściej czytany niż
pisany. Dlatego tak ważne jest, by kod ten był łatwy do przeczytania,
zrozumienia, testowania i ponownego zastosowania w innym miejscu. O podobnym
celu jest mowa w *Czystym kodzie* [3] Roberta C. Martina.

Bez zbędnego przedłużania, zobaczmy konkretnie jakie reguły składają się na kalistenikę obiektową.

## 1. Nie używaj więcej niż jednego poziomu wcięcia na metodę.

Zbyt wiele zagnieżdżeń w ramach jednej funkcji lub metody źle wpływa na
czytelność i prostotę utrzymania. Wiele poziomów pętli i warunków sprawia, że
działamy na różnych poziomach abstrakcji, a to może oznaczać, że metoda robi
więcej niż jedną rzecz. To może nam również pokazać, że nazwa metody nie
odzwierciedla wprost celu metody. Przez to trudniej jest jej użyć ponownie
w innym miejscu, jak również przetestować.

Zupełnym przeciwieństwem jest kilku-, bądź kilkunastolinijkowa metoda, która
ma wyłącznie jedną odpowiedzialność - robi jedną rzecz, robi ją dobrze,
a dodatkowo jest adekwatnie nazwana. Dobra nazwa metody może znacznie ułatwić
zrozumienie jej celu w trakcie czytania kodu. Jeśli wiemy, co dokładnie jest
celem metody, to chętniej jej użyjemy w innym miejscu. Ponadto krótki kod,
który zmienia stan wyłącznie jednego obiektu i nie posiada efektów ubocznych,
jest łatwo testowalny.

## 2. Nie używaj słowa kluczowego `else`

Konstrukcja `if/else` jest obecna w prawie każdym języku programowania
i łatwo ją zrozumie nawet laik. Wielu z nas zna przypadek wielokrotnie
powtarzanych ciągów `if … elif … elif … else`. Trudno się je czyta, trudno
zrozumieć, częściej trudno zmodyfikować - a pokusa dopisania kolejnego `else`
jest ogromna. Tego typu sytuacje często prowadzą do duplikowania kodu oraz
wielu błędów.

Kilkoma rozwiązaniami pozwalającymi unikać takich konstrukcji są polimorfizm,
wzorzec strategii i wzorzec stanu. Kod, który korzysta z takiego podejścia,
znacznie łatwiej się czyta i jest łatwiejszy w utrzymaniu.

W najprostszym przypadku wystarczy, że sprawdzamy warunek w `if` i wychodzimy,
jeśli nie został on spełniony. Dzięki temu nie mamy w kodzie kilku możliwych
rozgałęzień. Reguła ta jest prostsza do przestrzegania, jeśli każda metoda
robi tylko jedną rzecz.

## 3. Prymitywne typy powinny być opakowane w klasy.

Powyższa zasada obowiązuje wyłącznie w sytuacji, gdy zmienna przekazuje
jakieś zachowanie. Do czasu Pythona 3.5 nie było możliwości, aby wymusić, by
metoda na poziomie składni przyjmowała konkretny typ zmiennej. Nawet jeśli
mamy dostępne tego typu udogodnienie, powyższa zasada ma sens.

Obowiązek poinformowania o intencjach metody spoczywa niejako na nazwie
metody. Jeśli zamiast integer przekażemy do metody obiekt klasy `Hour` lub
`Year`, już sama deklaracja metody jest czytelniejsza. Nie przekażemy przez
pomyłkę obiektu `Year`, gdy metoda spodziewa się od nas `Hour` lub odwrotnie,
co jest możliwe, gdy wymusimy wyłącznie typ `int`.

Tym samym dajemy programiście proste i czytelne API, które może nie wymagać
nawet wgłębiania się w kod implementacji. Co więcej, jeśli już mamy tego typu
klasy opakowujące typy proste, to jest to naturalne miejsce, by dodać kolejne
metody operujące na tych typach.

## 4. Tylko jedna kropka na linię.

(Nie dotyczy getterów i tzw. "Fluent interface".)
Celem tej zasady jest powstrzymanie programisty przed sięganiem zbyt głęboko
w implementację klas i tym samym łamaniem enkapsulacji. Jeśli w ramach jednej
linii odwołujemy się do dwóch różnych obiektów, to znaczy, że wiemy zbyt wiele
o innych obiektach.

Prawo Demeter [4] mówi nam, że metoda może odwołać się wyłącznie do metod należących do:

* tego samego obiektu;
* dowolnego parametru przekazanego do niej;
* dowolnego obiektu przez nią stworzonego;
* dowolnego składnika klasy, do której należy dana metoda.

Pomóc w przestrzeganiu Prawa Demeter może zasada "tell, don’t ask". W skrócie
polega to na bezpośrednim oddelegowaniu pewnego zadania do innego obiektu (bez
martwienia się o implementację) zamiast pobierania danych z kilku powiązanych obiektów.

## 5. Nie skracaj nazw.

Chodzi tutaj o wszelkie nazwy klas, metod i zmiennych. Najczęściej skracamy
nazwy dlatego, że pełna wersja jest zbyt długa, a musimy jej użyć wiele razy.
Zbyt długa nazwa może sugerować, że funkcja ma zbyt wiele odpowiedzialności
i stara się zrobić więcej niż jedną rzecz. Wielokrotne używanie tej samej
funkcji może z kolei być znakiem, że warto pokusić się o usunięcie
zduplikowanego kodu.

Warto zadbać o to, by nazwy klas i metod były krótkie i precyzyjne. Jeśli
funkcja ma jeden konkretny cel, to nazwanie jej w zwięzły sposób nie będzie
problemem. Należy również zwracać uwagę na kontekst, w jakim metoda będzie
używana. Załóżmy, że mamy klasę Order obsługującą zamówienia. Funkcja służąca
do wysyłki nie powinna się nazywać `ship_order()`, gdyż powtarzamy w ten
sposób nazwy. Zamiast tego wystarczy samo ship(), dzięki czemu wywołanie
order.ship() jest krótsze i czytelniejsze.

## 6. Encje powinny być małe.

W oryginalnych założeniach dla Javy była mowa o 15-20 liniach na metodę,
50 liniach w ramach klasy i do 10 klas w module. W przypadku Pythona możemy
te limity pozostawić na niezmienionym poziomie.

Limity te mają na celu wymuszenie trzymania się zasady jednej
odpowiedzialności. Jeśli w ramach metody/klasy chcemy zrobić zbyt wiele, jest
to jasny znak, że należy pomyśleć o osobnej metodzie/klasie do tego celu.
Dzięki temu klasy tworzą zwartą i zamkniętą całość.

W miarę jak klasy robią się mniejsze i mają mniejszą odpowiedzialność, okaże
się, że wszystkie klasy w ramach modułu są ze sobą logicznie powiązane i służą
osiągnięciu wspólnego celu. Moduły, podobnie jak klasy, powinny mieć konkretny cel.

## 7. Ograniczona liczba atrybutów w klasie.

Jeff Bay wspomina o limicie 2 atrybutów, taką też wartość możemy przyjąć dla
Pythona. Większość klas powinna być odpowiedzialna za stan jednej zmiennej,
ale w pewnych przypadkach potrzeba ich więcej. Dodanie każdej kolejnej
zmiennej (atrybutu) do klasy sprawia, że staje się ona mniej spójna. Zdaniem
Bay’a, jeśli chcemy mieć więcej atrybutów niż 2, to niemal na pewno jest sposób,
by część z nich wydzielić do osobnej klasy. Przykład poniżej:

 * Customer:
   * Name
     * FirstName - string
     * LastName - string
   * CustomerId - int

## 8. Używaj kolekcji pierwszej klasy.
Przez kolekcję pierwszej klasy rozumiemy nie posiadające dodatkowych
atrybutów, klasy operujące na kolekcjach. Jeśli mamy zbiór elementów i chcemy
na nich wykonywać operację, to musimy stworzyć do tego dedykowaną klasę. Każdy
typ kolekcji jest opakowany w swoją klasę. Dzięki temu zachowanie powiązane
z tą kolekcją jest w jednym miejscu.

## 9. Nie używaj akcesorów.

Nie chodzi tutaj bynajmniej o całkowity zakaz używania setterów i getterów.
Celem tej reguły jest to, by nie pobierać wartości z obiektu i na tej
podstawie podejmować jakichś decyzji. Prawidłowym podejściem jest pozwolić
klasie na wykonanie tej operacji. To wewnątrz klasy powinna się znajdować
logika, która opiera się wprost na atrybucie tej klasy. Wraca tutaj po raz
kolejny zasada "tell, don’t ask". Stosując tę regułę zachowujemy również
zasadę otwarte zamknięte (Open/closed principle z SOLID).

&nbsp;

Wszystkie 9 zasad, choć czasem bardzo restrykcyjnych, wymusza na programiście
enkapsulację i myślenie zorientowane na programowanie obiektowe. Aby lepiej
opanować przedstawione zasady, sugeruje się proste ćwiczenie: należy napisać
od postaw prostą aplikację do 1000 linii kodu bez łamania tych zasad.
Po zrealizowaniu takiego zadania od decyzji dewelopera zależeć będzie, których
zasad się trzymać, a które można nieco rozluźnić lub całkiem pominąć.

Kalistenika obiektowa to nie jest zbiór najlepszych praktyk i nie należy
przestrzegać ich rygorystycznie. W każdym przypadku można podać przykład,
gdzie stosowanie tych zasad sprawi, że końcowy kod będzie dużo gorszej
jakości. Najważniejsza jest bowiem praktyka i zdrowy rozsądek.

## Bibliografia

1. https://pl.wikipedia.org/wiki/Kalistenika
2. https://pragprog.com/book/twa/thoughtworks-anthology
3. https://www.goodreads.com/book/show/3735293-clean-code
4. https://pl.wikipedia.org/wiki/Prawo`_`Demeter
