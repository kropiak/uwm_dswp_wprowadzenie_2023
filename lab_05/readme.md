# Wprowadzenie do języka Python

## Lab 05 - Python comprehensions. Pisanie własnych funkcji.

### **1. Python comprehensions.**

W języku polskim nie istnieje jedno tłumaczenie `python comprehensions`, które uznaje się za jedyne słuszne. Można określać ten mechanizm jako mechanizm komprehencji, oryginalnej nazwy angielskiej lub, w zależności od typu zwracanej wartości, nazywać to wyrażeniem listowym, słownikowym itd.
W literaturze anglojęzycznej funkcjonują również pojęcia `listcomp`, `dictcomp` itd. Warto również wspomnieć, że oprócz listy, słownika czy zbioru produktem może być generator, który zostanie zwrócony z `wyrażenia generującego`.

Ogólna postać wyrażenia:
`[element_zwracany_lub_dodawany for element in iterowalny if warunek]`

**Listing 1**

```python
# zamiast pisać klasyczną pętlę for
lista = []
for element in range(5):
    if element > 0:
        lista.append(element * element)

# możemy zapisać w postaci wyrażenia listowego
lista = [element * element for element in range(5) if element > 0]
```
Jest to jeden z tzw. pythonizmów, czyli konstrukcji języka charakterystycznych dla Pythona.


Mamy zdefiniowane zbiory:

A={x^2: x&isin;<0,9>}  
B={1, 3, 9, 27,…, 3^5}  
C={x: x&isin;A i x jest liczbą nieparzystą}  

W Python zapiszemy to:

**Listing 2**

```python
A = {x ** 2 for x in range(10)}
B = {3 ** i for i in range(6)}
C = {x for x in A if x % 2 != 0}

print(A, B, C, sep='\n')
```

**Listing 3**

```python
# chcemy uzyskać liczby parzyste z podanego zakresu
# wersja z pętlą
liczby = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
lista = []

for i in liczby:
    if i % 2 == 0:
        lista.append(i)

print("Liczby parzyste uzyskane z wykorzystaniem pętli")
print(lista)

# wersja z Python comprehension
lista2 = [i for i in liczby if i % 2 == 0]
print(lista2)

# wykonanie operacji na każdym elemencie iterowalnego jest również częstym 
# zastosowaniem comprehencji
import math

bins = ['1110', '0010', '1000', '1111', '0101']
ints = [int(b, 2) for b in bins]
sqrts = [math.sqrt(x) for x in ints]

```

Wyrażenia te mogą być również zagnieżdżone o dodatkową pętlę, ale ich użycie pozostaje już do dyskusji, często przez utratę czytelności, która jest jednak ważnym elementem kodu pisanego w Pythonie.

**Listing 4**

```python
# zamiast pisać tak:
lista = []
for i in [1, 2, 3]:
   for j in [4, 5, 6]:
      if i != j:
          lista.append((i,j))
print(lista)

# można to zrobić krócej
lista2 = [(i,j) for i in [1, 2, 3] for j in [4, 5, 6] if i != j]
print(lista2)
```

Python comprehensions i słowniki.

**Listing 5**

```python
# słowniki i zamiana klucza z wartością
skroty = {"PZU": "Państwowy zakład Ubezpieczeń",
"ZUS": "Zakład Ubezpieczeń Społecznych",
"PKO": "Powszechna Kasa Oszczędności"}
odwrocone = {value: key for key, value in skroty.items()}

print("Oryginalny słownik")
print(skroty)
print("Słownik odwrócony")
print(odwrocone)
```

**Listing 5**

Wyrażenia generujące są uproszczoną wersją generatorów (temat generatorów zostanie poruszony przy okazji innego laboratorium).

```python
tekst = 'Alicja w krainie czarów.'
przeliteruj = (l for l in tekst)
print(type(przeliteruj)) # co będzie wyjściem ?
print(next(przeliteruj)) # co będzie wyjściem ?
tekst = 'No to zmiana tesktu w zmiennej.'
print(list(przeliteruj)) # co będzie wyjściem ?
print(next(przeliteruj)) # co będzie wyjściem ?
```

**Zadanie 1**  

Zdefiniuj następujące zbiory, wykorzystując Python comprehension:  
A = {1/x: x&isin;[1,10]}  
B = {1, 2, 4, 8,…, <img src="https://render.githubusercontent.com/render/math?math={2^10}">}  
C = {x: x&isin; B i x jest liczbą podzielną przez 4}  

**Zadanie 2**

Wygeneruj macierz (lista dwupoziomowa) losowych wartości (sprawdź pakiet **[random](https://docs.python.org/3.10/library/random.html)**) 4x4 i wykorzystując Python comprehension zdefiniuj listę, która będzie zawierała tylko elementy znajdujące się na głównej przekątnej.

**Zadanie 3**
Napisz wyrażenie generujące, które będzie zwracało krotkę dwuwartościową postaci: `('Ala', [65, 108, 97]), ('ma', [109, 97]), ('kota.', [107, 111, 116, 97, 46])` dla przykładowego zdania `Ala ma kota.` Dla każdego wyrazu z tekstu przekazanego jako argument wejściowy tego wyrażenia zwraca ten wyraz oraz listę wartości int odpowiadającą kodowi tego znaku z tablicy znaków (zobacz wbudowane `ord(), chr()`).


Mechanizm przedstawiony w tym podrozdziale jest bardzo przydatny, chociaż skomplikowane polecenia
mogą być wyzwaniem do zinterpretowania względem „tradycyjnego” podejścia. Więcej przykładów można
znaleźć w dokumentacji Pythona pod adresem https://docs.python.org/3.10/tutorial/datastructures.html#nested-list-comprehensions

### 2. Tworzenie nowych funkcji.

Ogólna definicja funkcji mówi, że jest to wydzielony blok kodu, który ma robić możliwie jak najmniej
rzeczy na raz, ale ma to robić dobrze. Jest to też niezbędny element metodologii DRY (Don’t Repeat Yourself), czyli tam, gdzie jakaś funkcjonalność będzie wykorzystywana wielokrotnie, możemy zastosować funkcję.


**Listing 6**
```python

def nazwa_funkcji(arg_pozycyjny, arg_domyslny=wartosc, *arg_4, **arg_5):
    instrukcje
    ...
    [return wartosc] # opcjonalne, brak oznacza zwrócenie None
```

Funkcję możemy wywoływać z argumentami lub bez, ale zawsze musimy używać nawiasów (nawet jak nie ma argumentów, wtedy nazywamy ją funkcją bezargumentową). Funkcja może nie zwracać żadnej wartości, może zwracać jedną lub wiele wartości, a w tym ostatnim przypadku wartości będą zwrócone jako krotka wartości.

**Listing 7**

Chcemy zdefiniować funkcję, która będzie obliczać pierwiastki równania kwadratowego:
```python
import math


def row_kwadratowe(a, b, c):
    delta = b**2 - 4 * a * c
    if (delta < 0):
        # brak pierwiastków
        return -1
    elif (delta == 0):
        # jeden pierwiastek
        x = (-b) / (2 * a)
        return x
    else:
        # równanie ma dwa pierwiastki
        x1 = (- b - math.sqrt(delta)) / (2 * a)
        x2 = (- b + math.sqrt(delta)) / (2 * a)
        return x1, x2

print(row_kwadratowe(6,1,3))
print(row_kwadratowe(1,2,1))
print(row_kwadratowe(1,4,1))
```


**Listing 8**
```python
# definiujemy funkcje z wartościami domyślnymi
import math


def dlugosc_odcinka(x1 = 0, y1 = 0, x2 = 0, y2 = 0):
    return math.sqrt((x2 - x1)**2 + (y2 - y1)**2)


# wywołujemy dla wartości domyślnych
print(dlugosc_odcinka())

# wywołujemy dla własnych podanych wartości
# są to argumenty pozycjne czyli ważna jest kolejnosć podania wartości
print(dlugosc_odcinka(1, 2, 3, 4))

# wywołujemy funkcje podając mieszane wartości
# dwie pierwsze są interpretowane jako x1 i y1 jak podano w definicji funkcji
print(dlugosc_odcinka(2, 2, y2 = 2, x2 = 1))

# wywołujemy funkcje pdoając wartości nie w kolejności
print(dlugosc_odcinka(y2 = 5, x1 = 2, y1 = 2, x2 = 6))

# wywołujemy funkcję podając tylko dwa argumenty a reszta domyślne
print(dlugosc_odcinka(x2 = 5, y2 = 5))
```

Sugerowanie typów w Pythonie (Python type hinting).

Począwszy od wersji 3.5 wprowadzono możliwość oznaczania zmiennych i funkcji typami oczekiwanymi co nawiązuje do notacji znanej z języków typowanych statycznie.

> Dokumentacja 1: https://peps.python.org/pep-0484/
> Dokumentacja 2: https://docs.python.org/3/library/typing.html
> Tutorial 1: https://realpython.com/python-type-checking/
> Tutorial 2: https://bulldogjob.pl/readme/nie-boj-sie-type-hints-w-pythonie (uwaga na wersję Pythona, o której mowa w artykule!)

Type hinting jest dość rozbudowanym zagadnieniem, które cały czas ewoluuje, więc wiedzę należy z każdą wersją Pythona aktualizować. Poniżej zostanie przedstawiony przykład z tylko niewielkim wykorzystaniem możliwości tego modułu.

**Listing 9**

```python
from typing import Union, Tuple


def dodaj(a: int, b: int) -> int:
    return a + b


def przywitaj(imie: str) -> None:
    print(f'Witaj {imie}!')


# domyślna wartość argumentu
def przywitaj_default(imie: str = 'Jan') -> None:
    print(f'Witaj {imie}!')


# definicja dopuszczalnych typów
Num = Union[int, float]
# lub
# Num = int | float
def fdodaj_multitype(a: Num, b: Num) -> Num:
    return a + b


# lub w formie skróconej - od wersji 3.10
def fdodaj(a: int | float, b: int | float) -> int | float:
    return a + b


# lub gdy zwracamy krotkę
# można też
# def daj_krotke(imie: str) -> Tuple(str, int): # wymagany import
# def daj_krotke(imie: str) -> tuple(str, int):
def daj_krotke(imie: str) -> (str, int):
    return imie, len(imie)


def main() -> None:
    print(dodaj(1, 2))
    przywitaj('Adam')
    przywitaj_default()
    print(fdodaj(1, 4))
    print(fdodaj_multitype(3.0, 3))
    print(daj_krotke('Eliasz'))


if __name__ == '__main__':
    main()
```


**Zadanie 4**  
Dodaj do funkcji z listingu 7 type hinting.

**Zadanie 5**  
Napisz funkcję, która:
* przyjmuje z klawiatury `n`, będące liczbą całkowitą
* wykonuje `n` rzutów kostką k6 i zwraca liste krotek wartości postaci
  `(oczka: 6, rzutów: i)` itd., gdzie zmienna i jest ilością rzutów dla tej liczby oczek. 
Dodaj odpowiedni type hinting.

**Listing 10**
```python
# symbol * oznacza dowolną ilość argumentów, które zostaną
# zapakowane do krotki
def ciag(* liczby):
    # jeżeli nie ma argumentów to
    if len(liczby) == 0:
        return 0.0
    else:
        return float(sum(liczby))

# wywołanie gdy brak argumentów
print(ciag())
# podajemy argumenty
print(ciag(1,2,3,4,5,6,7,8))
```
**Zadanie 6**

Wykorzystując poprzedni przykład z listingu 10 zdefiniuj funkcję, która będzie przyjmowała obiekty typu `str` jako wejście (dowolną liczbę), a będzie zwracała listę tych łańcuchów posortowaną alfabetycznie.

**Listing 11**
```python
# symbol ** spowoduje zapakowanie argumentów z kluczem do słownika
def to_lubie(**rzeczy):
    for cos in rzeczy:
        print(f'Lubię {cos}', end='')
        if len(rzeczy[cos]) > 0:
            print(f', takie jak {rzeczy[cos]}.')

to_lubie(slodycze="czekolada", rozrywka=["disco-polo", "moda na sukces"])
```
**Zadanie 7**

Napisz funkcję, która przyjmuje nieokreśloną liczbę wartości z kluczem. Funkcja przyjmuje argumenty w postaci: klucz to nazwa drużyny a wartość to ilość punktów, które drużyna zdobyła. Funkcja zlicza, ile jest wszystkich punktów razem i zwraca tę wartość.
