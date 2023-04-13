# Wprowadzenie do języka Python

## Lab 07 - Wybrane funkcje wbudowane.

### **1. Wybrane funkcje wbudowane.**

Lista wszystkich funkcji wbudowanych znajduje się pod adresem: https://docs.python.org/3.10/library/functions.html

#### **1.1 Funkcja `zip`.**

**Sygnatura:**  
`zip(*iterables, strict=False)`

Funkcja `zip` iteruje przez przekazane __iterowalne__ i zwraca obiekt typu `zip iterator` zawierający krotki wartości.

**Listing 1**
```python
kolory = 'trefl pik karo kier'.split()
figury = list('JQKA')

for card in zip(figury, kolory):
    print(card)
```

```console
# output
('J', 'trefl')
('Q', 'pik')
('K', 'karo')
('A', 'kier')
```

Domyślnie argument `strict=False` co oznacza, że funkcja może przyjąć iterowalne o różnych liczebnościach, ale zwróci ilość krotek odpowiadającą najkrótszemu iterowalnemu.

**Listing 2**
```python
kolory = 'trefl pik karo kier'.split()
figury = list(range(2, 11)) + list('JQKA')

for card in zip(figury, kolory):
    print(card)
```

```console
# output
(2, 'trefl')
(3, 'pik')
(4, 'karo')
(5, 'kier')
```

Ustawienie parametru `strict=True` będzie rzucało wyjątek `ValueError`, który można następnie w kodzie obsłużyć.

#### **1.2 Funkcja `filter`.**

**Sygnatura:**  
`filter(function, iterable)`

Funkcja `filter` zwraca iterator z elementami z iterowalnego, dla których funkcja zwróciła wartość `True`.

**Listing 3**  
```python
lista = list(range(1, 11))

# możemy użyc funkcji anonimowej
print(list(filter(lambda x: x > 5, lista)))

# lub zdefiniowanej
def is_one_digit_number(num: int):
    return len(str(num)) < 2

print(list(filter(is_one_digit_number, lista)))
```
Co będzie wynikiem działania poniższego fragmentu kodu?
**Listing 4**  
```python
cyfry = filter(lambda x: x.isDigit(), 'hfysydf6s7dsd')
print(list(cyfry))
```

#### **1.3 Funkcje `any` oraz `all`.**

Funkcje `all` oraz `any` zwracają, odpowiednio, `True` jeżeli wszystkie elementy iterowalnego są `True` (lub iterowalny jest pusty) oraz jeżeli co najmniej jeden element iterowalnego jest `True`. Tutaj warto przypomnieć sobie jakie wartości są w Pythonie ewaluowane na `True` lub `False`.

**Listing 5**  
```python
nums = [0, 1, 2, 3]
print(any(nums))
print(all(nums))
print(any(filter(lambda x: x > 1, nums)))
```
Wyjaśnij wartości poniższego outputu.
```console
# output
True
False
True
```

#### **1.4 Funkcja `sorted`.**

**Sygnatura:**
`sorted(iterable, key=None, reverse=False)`

Funkcja `sorted` zwraca nową posortowaną listę z iterowalnego. Atrybut `key` pozwala na określenie klucza, na podstawie którego sortowanie ma się odbyć.

**Listing 6**

```python
# sortowanie listy
lista = [4, 5, 2, 3, 1, 0]
print(sorted(lista))
print(sorted(lista, key=lambda x: x % 2 == 0))

# sortowanie słownika
d = {'Alan': 10, 'Zenon': 5, 'Franek': 7}

# dumyślne sortowanie
print(sorted(d))
# sortowanie po wartości
print(sorted(d, key=lambda item: item[1]))
print(sorted(d.items(), key=lambda item: item[1]))
```

#### **1.5 Funkcja `map`.**

**Sygnatura:**
`map(function, iterable, ...)`

Funkcja `map` pozwala wykonać funkcję (również anonimową) na każdym elemencie przekazanych iterowalnych i zwraca iterator. Może przyjmować więcej argumentów, które są przekazywane do mapowanej funkcji.

**Listing 7**
```python
import math

lista = [2, 3, 4]
potegi = [2, 3]


power = map(lambda x: math.pow(x, 2), lista)
print(list(power))
# dynamiczne parametry - ile wywołań nastąpi ?
power = map(math.pow, lista, potegi)
print(list(power))
# z użyciem istniejącej funkcji
lancuch = map(str, lista)
print(list(lancuch))

# iterator jest oczywiście obiektem iterowalnym, więc możemy te funkcje zagnieżdżać
# co będzie wynikiem funkcji pritn(what) ?
what = sum(list(map(str.isdigit, map(str.upper, 'ud8s7u'))))
print(what)
```

**Zadania**

**Zadanie 1**  
Wykorzystując wbudowaną funkcję `isinstance` oraz `filter` napisz funkcję `extract_numbers(vals: list[Any]) -> list[int | float]`, która z podanej listy dowolnych obiektów odfiltruje tylko obiekty typu `int` oraz `float` i zwróci listę je zawierającą.

**Zadanie 2**  
Wykorzystując funkcję `sorted` i funkcję anonimową (lambda) posortuj listę wyrazów (wprowadzaną przez input) według ilości znaków w wyrazie malejąco.

**Zadanie 3**  
Wykorzystując funkcję `sorted` napisz funkcję, która będzie sortowała listę zawierająca wartości typu `int` oraz `str` (może wystąpić tylko jeden lub oba typy danych). Funkcja posiada atrybut domyślny `reversed=False`, który oznacza, że zwrócona lista będzie najpierw zawierała liczby posortowane rosnąco, a następnie łańcuchy znaków. Wartość `True` tego atrybutu oznaczać będzie w liście wyjściowej najpierw łańcuchy znaków, a później liczby.

**Zadanie 4**  
Przepisz (ale kod umieść w tym labie) zadanie 4 z labu 1, tak aby gdzie to możliwe użyć funkcji `map`.

**Zadanie 5**  
Napisz kod, który będzie sortował słownik postaci `{'Jan': [1, 3, 4, 7], ...}` na podstawie funkcji przekazanej jako argument, która będzie w stanie operować na liście wartości typu `int`. Wykorzystaj funkcje wbudowane `min, max, sum, abs`.








