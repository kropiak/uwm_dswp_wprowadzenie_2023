# Wprowadzenie do języka Python

## Lab 01

## 1. Wstęp
### **1.1 Historia języka Python**
 
Twórcą Pythona jest holender **Guido van Rossum**, a sama nazwa, co niektórych zapewne nie zdziwi, pochodzi od popularnego serialu BBC „Latający Cyrk Monty Pythona”. Prace nad pierwszym interpreterem Pythona rozpoczęły się w 1989 roku jako następcy języka ABC. Wszystkie wersje aż do wersji 1.2 powstawały w CWI (Centrum Matematyki i Informatyki) w Amsterdamie gdzie Guido wówczas pracował. Od wersji 2.1 Python był udostępniany jako projekt **Open Source** przez niedochodową organizację **Python Software Foundation (PSF)**. Obecnie nad rozwojem Pythona pracuje wiele osób, ale Guido wciąż jest zaangażowany w ten proces. **Update 2021**: Po sporach ze społecznością co do dalszego kierunku rozwoju języka Python Guido angażuje się już znacznie mniej w ten proces. 

Sam twórca w 1995 roku wyemigrował do USA gdzie w latach 2005 – 2013 pracował dla Google a następnie dla Dropbox'a (do października 2019 roku). We wspólnocie Pythona van Rossum pełnił do lipca 2018 roku funkcję Benevolent Dictator for Life (BDFL), co oznacza, że nadzorował rozwój języka, podejmując w razie konieczności ostateczne decyzje. W 2019 roku był jeszcze członkiem Python Steering Council, ale wycofał swoją kandydaturę na rok 2020. Po odejściu z Dropboxa ogłosił przejście na emeryturę, ale już w listopadzie 2020 ogłosił, że dołącza do firmy Microsoft, aby dalej rozwijać Pythona.
 
Ważnym momentem w historii Pythona było utworzenie drugiej głównej gałęzi – Pythona 3 w roku 2008. Od tego momentu wersja 2 oraz 3 były rozwijane oddzielnie, ale czas wersji 2 właściwie minął, o czym świadczy termin zakończenia wsparcia z dniem 12 kwietnia 2020 roku. Rozwój języka jest prowadzony przy wykorzystaniu **PEP (Python Enhancement Proposal)**. Dokumenty te to propozycje rozszerzeń lub zmian w języku w postaci artykułu, który jest poddawany pod dyskusję wśród programistów Pythona. Każdy dokument zawiera opis proponowanego rozwiązania, uzasadnienie oraz aktualny status. Po osiągnięciu konsensusu propozycje są przyjmowane lub odrzucane.

### **1.2. Wybrane cechy języka Python**

Python jest językiem **ogólnego przeznaczenia**, którego ideą przewodnią jest czytelność i klarowność kodu źródłowego. Standardową implementacją języka jest CPython (napisany w C), ale istnieją też inne, np. Jython (napisany w Javie), CLPython napisany w Common Lisp, IronPython (na platformę .NET) i PyPy napisany w Pythonie.

Python nie wymusza jednego stylu programowania, dając możliwość programowania obiektowego, programowania strukturalnego oraz programowania funkcyjnego.

Inne cechy języka Python:
* Typy sprawdzane są dynamicznie (w przeciwieństwie np. do Javy), 
* Do zarządzania pamięcią używany jest garbage collector, 
* Wszystkie wartości przekazywane są przez referencję, 
* Jest czasem kwalifikowany jako język skryptowy, 
* Nie ma enkapsulacji, jak to ma miejsce w C++ czy Javie, ale istnieją mechanizmy, które pozwalają na osiągnięcie podobnego efektu, 
* Możliwe jest tworzenie funkcji ze zmienną liczbą argumentów, 
* Możliwe jest tworzenie funkcji z argumentami o wartościach domyślnych. 

### **1.3. Python i data science.**

Python nie jest jedynym ani też jednoznacznie najlepszym językiem dla data science. Jego największym konkurentem w tej dziedzinie jest **R**, który od samego początku był tworzony z myślą o statystyce, która jak wiadomo w dziedzinie data science ma szerokie zastosowanie. Trwają niezliczone spory i porównania próbujące udowodnić wyższość jednego rozwiązania nad drugim. Skoro jednak będziemy zajmować się Pythonem przytoczę kilka jego zalet pod kątem data science:

* **Python jest językiem ogólnego przeznaczenia** co powoduje, że oprócz możliwości wykorzystania specjalistycznych bibliotek np. do budowy sztucznych sieci neuronowych, można bez konieczności integracji z innymi rozwiązaniami zbudować kompletną aplikację desktopową lub webową,

* **Python może być traktowany jako język skryptowy** co dodatkowo w połączeniu z np. Jupyter Notebook (dawniej IPython), pozwala na bardzo szybkie testowanie i prototypowanie poprzez pisanie kodu „na bieżąco”, co powoduje brak konieczności zapisywania kodu w pliku i jego późniejszego uruchamiania co znacznie przyspiesza proces stworzenia działającego prototypu,

* **Bogata paleta bardzo dobrej jakości bibliotek dla AI (Artificial Intelligence) i Data Science**. Za przykład mogą tutaj posłużyć **NumPy, Pandas, SciPy, matplotlib czy scikit-learn**, które jednak wykraczają poza zakres niniejszego przedmiotu.

* **Społeczność** – jako język ogólnego zastosowania społeczność Pythona jest bardzo duża co przekłada się na łatwość uzyskania odpowiedzi na pytania, sporą ilość dobrej dokumentacji oraz rozbudowaną listę bibliotek i dodatków.

## **2. Organizacja kodu według PEP8**

Jak zostało już wspomniane w punkcie 1 zmiany w specyfikacji języka odbywają się poprzez system PEP. Dokument o numerze PEP8 jest jedną (ale nie jedyną) propozycją organizacji kodu języka Python. Oryginalna treść dokumentu dostępna jest pod adresem https://www.python.org/dev/peps/pep-0008/.

Pod adresem https://realpython.com/python-pep8/ można znaleźć więcej przykładów z wyjaśnieniami jak stosować zalecenia PEP8 w praktyce oraz jakie narzędzia mogą nam w tym pomóc.

### **2.1. Wcięcia**

W kodzie języka Python nie znajdziemy znanych z PHP, Javy czy C# klamerek do separacji bloków kodu, określania ram ciała metody czy klasy lub zakresu operacji w pętli. Tutaj do tego celu służą odpowiednio umieszczone **wcięcia i puste linie** między w/w elementami. Dla osób, które nigdy wcześniej nie miały do czynienia z taką organizacją kodu może to być pewną nowością, ale dość szybko staje się zrozumiałe i intuicyjne.

**Listing 1**
```python
if score >= 100:
    print('Zwycięstwo !')
```

Każdy kolejny poziom zagnieżdżenia w bloku kodu poprzedza odstęp w postaci wielokrotności **4 spacji (pojedyncza wartość wcięcia)**. Dopuszczalne jest również stosowanie tabulatorów jako wcięć, ale zalecane są spacje a dodatkowo w wersji Python 3 użycie jednocześnie spacji i tabulatorów jako wcięć nie jest dozwolone. Zazwyczaj nie musimy się jednak martwić ręcznym wstawianiem wcięć, chyba że korzystamy z narzędzia do edycji kodu, które nie posiada wsparcia dla danego języka programowania.

Wcięcia używamy również w sytuacjach, w których linia kodu jest zbyt długa i powinna być złamana na większą ilość wierszy. Zalecana długość linii według PEP8 to 79 znaków.

**Listing 2**
```python
wyslane = wyslij_wiadomosc(e_mail_odbiorcy, temat,
                           wiadomosc)
```

W takim przypadku wcięcie sięga znaku otwarcia deklaracji listy atrybutów wywoływanej metody lub funkcji. Dopuszczalne są jednak odstępstwa od tej reguły pozwalające na zastosowanie mniejszego wcięcia dla kolejnych linii.

**Listing 3**
```python
wyslane = wyslij_wiadomosc(e_mail_odbiorcy,
    temat, wiadomosc)
```

Jednak sama dokumentacja mówi o tym, że jest to opcjonalne formatowanie, więc należy go używać tylko z konieczności a nie jako regułę.

Deklaracja zmiennych takich jak lista, tablica, krotka czy słownik dzięki wcięciom często poprawia ich czytelność co jest główną przyczyną, którą kierowano się określając reguły formatowania kodu w Pythonie.

**Listing 4**
```python
lista = [
    1, 2, 3,
    4, 5, 6,
]
```

W przypadku łamania linii i operatorów (np. arytmetycznych) obowiązuje zasada przenoszenia operatora do nowej linii.

**Listing 5**
```python
zysk = (przychod 
        - koszty 
        - podatki)
```

### **2.2. Puste linie**

Funkcje najwyższego rzędu oraz definicje klas oddzielamy od pozostałych bloków kodu dwiema pustymi liniami.

**Listing 6**
```python
def zrob_cos():
    return 'zrobione'


def tez_cos_zrob():
    return 'też zrobione'
```

Metody klas oraz funkcje lokalne oddzielone są natomiast pojedynczą pustą linią.

**Listing 7**
```python
class Osoba:

    def __init__(self, imie, nazwisko, plec):
        self.imie = imie
        self.nazwisko = nazwisko
        self.plec = plec

    def przedstaw_sie(self):
        print('Nazywam się {0} {1}'.format(self.imie, self.nazwisko))

    def moj_wiek(self):
        print('Moja płeć to: {0}.'.format(self.plec))


os = Osoba('Jan', 'Kowalski', 'mężczyzna')
os.przedstaw_sie()
os.moj_wiek()
```
**Listing 8**
```python
def funkcja_top_level():

    def funkcja_lokalna():
        pass

    def kolejna_funkcja_lokalna():
        pass
```

Pojedyncze puste linie mogą być również stosowane wewnątrz funkcji aby odseparować od siebie logiczne sekcje funkcji.

### **2.3. Organizacja importów**

Poszczególne instrukcje importu powinny być rozdzielone na oddzielne linie.
**Listing 9**
```python
# Tak
import os
import sys

# Nie
import sys, os
# Poprawny jest natomiast taki sposób definiowania importu:
from subprocess import Popen, PIPE
```

**Inne zasady dotyczące organizacji importów.**

Importy powinny być umieszczane na początku pliku tuż za ewentualnymi komentarzami dla modułu i elementami docstring. Kolejnośc importów ma również znaczenie. 

**Oto zalecany porządek:**
* import bibliotek standardowych
* import powiązanych bibliotek zewnętrznych (ang. third party imports)
* import lokalnych aplikacji/bibliotek**
  
Zalecane jest również dodawanie pustej linii po każdej z w/w grup importów. Jako, że Python umożliwia zarówno import całej biblioteki lub tylko wybranych jej modułów często trzeba dobrać odpowiedni sposób do sytuacji, ale z reguły zaleca się wykonywanie importu i dodanie aliasu lub import modułu zamiast konkretnej klasy z tego modułu co zmniejsza ryzyko wystąpienia konfliktów w przestrzeni nazw. Więcej informacji oraz przykłady znajdują się w rozdziale poświęconym zarządzaniu i importowi pakietów. 

Dobrym pomysłem na zdobycie wiedzy na temat dobrej organizacji kodu w naszych modułach jest zaglądanie do kodu źródłowego publicznie dostępnych, dobrej jakości modułów i bibliotek Pythona.

### **2.4. Konwencje nazewnicze**

Jest to moim zdaniem jedna z ważniejszych zasad do przyswojenia i pilnowania aż do wyrobienia nawyku. Warto zatem mieć pod ręką krótkie zestawienie:
* https://peps.python.org/pep-0008/#naming-conventions
* https://realpython.com/python-pep8/#naming-styles

Zasady co do zalecanego stylu są dość precyzyjne, ale dobranie odpowiedniej nazwy wymaga już nieco więcej wprawy i przemyślenia. Wykorzystanie jednoliterówych nazw dla zmiennych opisujących niewiadome w równaniu ma sens, ale użycie takiej samej zasady dla przechowania imienia, listy nazw produktów będzie znacznie utrudniało interpretację kodu i jego szybkie zrozumienie. Również autorowi i to po dość krótkiej przerwie w obcowaniu z tym kodem. Używanie zbyt długich nazw również ma swoje wady, które zamiast poprawienia czytelności zadziałają wręcz przeciwnie, lub zbyt często będą nas zmuszały do łamania pojedynczej linii kodu. Tu zalecany jest umiar. Warto również, mimo tego, że Python jest językiem typowanym dynamicznie, nawiązywać w jakiś stopniu do typu wartości, które zmienna przechowuje, np. `names_list lub list_of_names (typ list), has_permission lub is_valid (typ bool), number_of_digits word_count (typ numeryczny)`. To jest proces i dlatego warto wracać do swojego kodu po pewnym czasie i wykonywać **refaktoryzację** samodzielnie lub wykorzystać inne osoby w zespole do przeprowadzenia procesu **code review**.

### **2.5. Inne zalecenia**

Zmienne typu string można umieszczać zarówno w cudzysłowie lub w apostrofach, gdyż w przypadku Pythona nie ma to znaczenia. Natomiast PEP8 nie zaleca żonglowania tym zapisem i trzymania się jednej z opcji. Sytuacją, w której dozwolone jest użycie obu jednocześnie, jest ciąg tekstowy, który sam już zawiera cudzysłów lub apostrof – wtedy należy użyć innego niż w samym tekście, lub zastosować zapis, gdzie każdy specjalny znak będzie poprzedzony znakiem \\.

**Listing 10**
```python
artykul = 'Recenzja "Władcy Pierścieni".'

# Ale można również tak:
artykul = "Recenzja \"Władcy Pierścieni\"."

# lub tak
artykul = """Recenzja "Władcy Pierścieni"."""
```

> Spacje w wyrażeniach i definicjach są pożądane, ale nie należy ich nadużywać.

**Listing 11**
```python
dobrze:	zakupy(szynka[1], {jajka: 2})
	x = 1
	lista[index]
	lista[1:4]

źle: 	zakupy( szynka[ 1 ], { jajka: 2 } )
	x=1
	lista [index]
	lista[1: 4]
```
Wszystkie operatory binarne powinny być otoczone pojedynczą spacją.

## **3. Operatory oraz typy numeryczne.**
Zanim omówione zostaną typy danych, warto poznać kilka operatorów, które w powiązaniu ze zmiennymi są często używane.

**Listing 12**
```python
# operatory arytmetyczne

# operator dodawania
print(1 + 2)
# operator odejmowania
print(1 - 2)
# operator mnożenia
print(1 * 2)
# operator dzielenia z resztą
print(1 / 2)
# operator dzielenia bez reszty (dzielenie całkowite)
print(1 // 2)

# pamiętajmy o kolejności operacji arytmetycznych
suma = 1 + 2 * 3 / 4.0

# operatory przypisania
zmienna = "wartość" # przypisanie wartości do zmiennej
# są też skrócone postacie operatorów przypisania w połączeniu z innymi operatorami
suma = 10
suma += 1 
# to samo co
suma = suma + 1
# podobnie możemy używać operatorów -, *, /, //, **, % i operatorów bitowych (zachęcam do poczytania w dokumentacji)


# modulo czyli reszta z dzielenia
reszta = 12 % 5
# operator potęgowania
kwadrat = 5 ** 2
szescian = 5 ** 3

# operacje na zmiennych znakowych (string)
full_name = "Kowalski" + " " + "Jan"

# tak też można
spam = "SPAM " * 10
print(spam)


# operatory porównania
liczba1 = 1
liczba2 = 2
print(liczba1 > liczba2)
print(liczba1 < liczba2)
print(liczba1 <= liczba2)
print(liczba1 >= liczba2)
print(liczba1 == liczba2)
print(liczba1 != liczba2)

# powyższe porównania zwrócą wartości typu bool czyli True lub False

prawda = True
falsz = False

# operatory logiczne
print(prawda and falsz) # koniunkcja logiczna
print(prawda or falsz) # alternatywa logiczba
print(not prawda) # negacja
print(not not prawda) # podwójna negacja
print(bool(prawda or falsz)) # użycie metody bool(), która jest tutaj wywołaniem konstruktora klasy bool (więcej w kolejnych labach)

# operatory tożsamości (identity)
liczba = 1
liczba2 = liczba

print(liczba is liczba2)
print(liczba is not liczba2)

# operatory przynależności (membership)
lista = [1, 2, 3, 4]
print(1 in lista)
print(5 not in lista)

# operatory bitowe (zobacz: https://docs.python.org/3.10/library/stdtypes.html#bitwise-operations-on-integer-types)
x | y # logiczna alternatywy (ang. or) na x i y
x ^ y # logiczna alternatywa rozłączna na x i y
x & y # logiczna koniunkcja of x and y
x << n # x przesunięte w lewo o n bitów
x >> n # x przesunięte w prawo o n bitów
~x # przerzucanie bitów (negacja)

# operator przypisania := (nowość w Python 3.8.*)
# tutaj najpierw nowej zmiennej n przypisana zostaje wartość len(lista) a później
# dokonana zostaje ewaluacja tej zmiennej czy n > 10. Może to oszczędzić w niektórych
# przypadkach nieco miejsca na deklarację zmiennej, jeżeli potrzebna jest tylko w bardzo
# ograniczonym zakresie (ang. scope)
if (n := len(lista)) > 10:
    print(f"List is too long ({n} elements, expected <= 10)")
```

Python w bardziej złożonych wyrażeniach wykonuje działania w określonej kolejności:

1.	najpierw `**`
2.	następnie `*`, `/` oraz `%`
3.	a dopiero na końcu `+` i `-`

Informacje o epratorach, rozbite niestety w wielu podrodziałach, znajdują się w dokumencie opisującym wbudowane typy danych języka Python: https://docs.python.org/3.10/library/stdtypes.html. Do tego dokumentu będziemy jeszcze wracać.

Bardziej szczegółowe informacje na temat priorytetów operatorów można znaleźć tu: https://docs.python.org/3.10/reference/expressions.html#operator-summary


W Pythonie jako fałsz traktowane są:
* liczba zero (`0, 0.0, 0j` itp.)
* `False`
* `None`
* puste kolekcje (`[], (), {}, set()` itp.)
* puste łańcuchy znakowe
* w Pythonie 2 – obiekty posiadające metodę `__nonzero__()`, jeśli zwraca ona `False` lub `0`
* w Pythonie 3 – obiekty posiadające metodę `__bool__()`, jeśli zwraca ona `False`


Dwa główne typy liczbowe Pythona to liczba całkowita oraz rzeczywiste, czyli **int** i **float**. Jest jeszcze typ **complex**, który służy do przechowywania wartości liczb zespolonych, ale zapoznanie się z informacjami na jego temat pozostawiam czytelnikowi.

**Listing 13**
```python
calkowita = 5
calkowita_sep = 1 000 000  # również poprawny zapis, poprawiający czytelność
rzeczywista = 5.6
rzeczywista = float(56)

# powyższy sposób to rzutowanie (ang. casting) - konwersja jednego typu w inny o ile to możliwe
# poniżej kolejny przykład
liczba_str = '123'
liczba = int(liczba_str)
print(type(liczba))

# zmienne można również zadeklarować w jednej linii
# chociaż w praktyce ten zapis oznacza rozpakowanie krotki i zostanie przedstawiony w późniejszym czasie
a, b = 3, 4
```

Bibliotek standardowa zawiera również obiekt `Fraction`, który służy do przechowywania wartości w postaci ułamka zwykłego i przykład jego wykorzystania wygląda tak:

**Listing 14**
```python
from fractions import Fraction


ulamek = Fraction(2, 3)
print(ulamek)
ulamek = Fraction(100, 200)
print(ulamek)

# wyjście
# Fraction(2, 3)
# Fraction(1, 2) nastąpi automatyczne uproszczenie ułamka
```

Więcej informacji można znaleźć w dokumentacji: https://docs.python.org/3.11/library/fractions.html#fractions.Fraction

**Zadania**

0. Przygotuj repozytorium, w którym będziesz przechowywał/a rozwiązania zadań. Rozwiązania umieszczaj w podkatalogach, których nazwy będą postaci `lab_01, ...`. Zaproś prowadzącego do wglądu do w/w repozytorium.
1. Przestudiuj dokumentację opisującą typ `int` oraz `float` i napisz kod, w którym stworzysz po dwa obiekty typu int i float z użyciem różnych wartości dla konstruktorów tych typów (np. z inną podstawą niż domyślne 10 dla typu int).
2. Napisz kod, w którym wykorzystasz poniższe metody:
   * `int.bit_count()`
   * `float.is_integer()`
3. Sprawdź w dokumentacji (https://docs.python.org/3.11/library/functions.html#bin) działanie metody `bin`, a następnie wykonaj konwersję dowolnej liczby całkowitej na binarną i ponownie na całkowitą (sprawdź opis konstruktora klasy `int` w dokumentacji).
4. Przygotuj 4 przykłady kodu, który wykorzystuje operatory bitowe.
5. Wykorzystaj kod zamiany wartości `float` na wartość hex dostępną pod adresem https://docs.python.org/3.11/library/stdtypes.html#additional-methods-on-float i zapisz własny przykład konwersji wartości zmiennoprzecinkowej do postaci hex i ponownie do wartości typu float. Zapoznaj się również z kolejnym punktem tej dokumentacji o nazwie "Hashing of numeric types".