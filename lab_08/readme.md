 Wprowadzenie do języka Python

## Lab 08 - Tablice oraz widoki pamięci. Moduł `collections`.

### **1. Tablice.**

Wbudowany typ `list` jest często nadużywany przez programistów Pythona ze względu na swoją uniwersalność, ale nierzadko lepszym pomysłem jest użycie tablic, np. do przechowywania dużej ilości liczb.

Tablice są lekkie, podobnie jak w języku C. Definiuje się je podając kod literowy, oznaczający wybrany typ danych języka C. Tablica przechowuje bajty w spakowanej formie, co znacznie redukuje ilość zaalokowanej pamięci oraz czas wykonania operacji. Tablice są homogeniczne tzn., możemy przechowywać tylko jeden typ wartości na raz oraz w przeciwieństie do tablic z modułu `NumPy` ich rozmiar możemy dynamicznie zmieniać (tak jak listy). Poza tym `array` posiada niemal większość metod znanych z klasy `list` takie jak: `append`, `insert`, `extend`, `count`, `index` i inne.'

> Dokumentacja: https://docs.python.org/3.11/library/array.html


**_Listing 1_**
```python
import sys
from array import array

# tablica zawierająca wartości typu unsigned int
# inicjalny rozmiar = 0 elementów
tab = array('I')
print(len(tab))

# możemy dodać element na koniec tablicy
tab.append(1)
print(len(tab))

# użycie metody extend
tab.extend([2, 3, 4])
print(tab)
print(len(tab))

# poniższy fragment zgłosi błąd TypeError
# tab.extend([2, 3.0, 4])
# print(tab)
# print(len(tab))

# tablicę możemy również inicjować z istniejących obiektów
# z listy - wywołana zostanie metoda from list klasy array (patrz dokumentacja)
tab_from_list = array('I', [i for i in range(10)])
print(tab_from_list)

# z obiektu typu str - wywołana zostanie metoda fromunicode
tab_from_string = array('u', 'ABRACADABRA')
print(tab_from_string)
print(tab_from_string[4:6])
# wstawienie wartości z użyciem slice - typem obiektu wstawianego musi być również array
tab_from_string[4:6] = array('u', '_')
print(tab_from_string)

# z generatora
import random
tab_of_floats = array('f', (random.random() for _ in range(10)))
print(tab_of_floats)
# z ciekawości możemy porównać ilość zaalokowanej pamięci dla tablicy i listy tych samych wartości
# im więcej będzie wartości tym różnica będzie większa na korzyść tablicy
list_of_floats = [random.random() for _ in range(10)]
print(sys.getsizeof(tab_of_floats))
print(sys.getsizeof(list_of_floats))
```

Dzięki tablicom możemy w środowisku z ograniczonymi zasobami zmniejszyć ilość zaalokowanej pamięci. A jak wygląda czas niezbędny do zaalokowania tablicy i listy tych samych elementów ?

**_Listing 2_**
```python
# test czasu wykonania
from timeit import timeit
import random
setup = """
from array import array
import random
"""
stmt1 = """
tab_of_floats = array('f', [random.random() for _ in range(1_000_000)])
"""
stmt2 = """
list_of_floats = [random.random() for _ in range(1_000_000)]
"""

print(timeit(stmt1, setup, number=100))
print(timeit(stmt2, setup, number=100))
# wynik ?
```

Wynik pokazuje, że czas wykonania nie jest koniecznie po stronie tablic. Wartości mogą się różnić dla różnych typów wartości.

**Zadanie 1**  
Wykorzystując przykład z listingu 2 napisz kod, który przetestuje czas inicjowania tablicy znaków oraz wartości całkowitych (typ int i long) i porówna z czasem zainicjowania listy z takimi samymi wartościami.

**_Listing 3_**
```python
# zapisanie tablicy do pliku oraz jej wczytanie
tab_of_floats = array('f', [random.random() for _ in range(1_000_000)])

with open('floats_array.bin', 'wb') as file_arr:
    tab_of_floats.tofile(file_arr)

# wczytujemy ponownie dane do tablicy floatów
tab_of_floats_loaded = array('f')
file_arr  = open('floats_array.bin', 'rb')
tab_of_floats_loaded.fromfile(file_arr, 1_000_000)
file_arr.close()


# i analogiczna operacja dla listy
list_of_floats = [random.random() for _ in range(1_000_000)]
with open('floats_list.txt', 'w') as file_arr:
    file_arr.writelines('\n'.join([str(x) for x in list_of_floats]))

with open('floats_list.txt', 'r') as file_list:
    list_of_floats_loaded = file_list.readlines()

list_of_floats_loaded = [float(x.strip()) for x in list_of_floats_loaded]
print(list_of_floats_loaded[:10])
```

**Zadanie 2**  
Zmierz czas operacji zapisu i ładowania danych z tablicy i listy z listingu 3. Użyj do tego modułu `datetime`. Wnioski ?

Można oczywiście użyć bardziej wyrafinowanych narzędzi do serializacji obiektów Pythona i ich późniejszej deserializacji np. popularnego modułu `pikle`.

Innym ciekawym rozwiązaniem, które może się przydać przy pracy z dużą ilością obiektów jest klasa `memoryview` (widok pamięci). Jej powstanie zostało zaispirowane biblioteką NumPy.

**_Listing 4_**
```python
tab = array('I', range(1, 11))
print(tab)
# lokalizacja w pamięci
print(id(tab))

mem = memoryview(tab)
# lokalizacja w pamięci - inna, ale przecież to inny obiekt
print(id(mem))

# jednak elementy tablicy i memory view współdzielą pamięć
print(id(tab[0]))
print(id(mem[0]))

# nie wykonamy tego dla obiektów non byte
# print(mem.cast('I', [2, 5]))

tab = array('B', range(1, 11))
print(tab)
mem = memoryview(tab)
# jeżeli chcemy ten widok zmaterializować
print(mem.cast('B', [2, 5]).tolist())
```


### **2. Moduł `collections`.**

> Dokumentacja: https://docs.python.org/3.11/library/collections.html#module-collections

Moduł ten dostarcza kilka bardziej wyrafinowanych kolekcji. Jedną z nich jest klasa `deque`, która jest implementacją kolejki dwustronnej. Jej działanie można po części symulować z użyciem list, ale jednak nie jest to dokładnie to samo. Dodatkowo klasa `deque` jest lepiej zoptymalizowana w porównaniu do list.


**_Listing 5_**
```python
from collections import deque, namedtuple, Counter


def test_deque():
    kolejka = deque('Ala ma kota'.split())
    print(kolejka)

    kolejka.append('?')
    print(kolejka)

    kolejka.appendleft('Czy')
    print(kolejka)

    kolejka.rotate(2)
    print(kolejka)

    kolejka.rotate(-2)
    print(kolejka)


if __name__ == '__main__':
    test_deque()
```

Inna kolekcja, której przyjrzymy się bliżej to `namedtuple` czyli krotka nazwana. Jej użycie przypomina wykorzystanie programowania obiektowego do tworzenia struktur danych.

**_Listing 6_**
```python
def test_namedtuple():

    Person = namedtuple('Person', ['first_name', 'last_name', 'age', 'gender'])

    adam = Person('Adam', 'Malinowski', '32', 'Male')
    print(adam)
    print(adam.first_name)

    first_name, last_name, age, gender = adam

    print(first_name, last_name, age, gender)
    print(','.join(adam))

    # np. rekord z bazy danych
    record = ['Jan', 'Kowalski', '35', 'Male']
    jan = Person._make(record)
    print(jan)
```

Ostatnia z omawianych tutaj klas z modułu `collections` to `Counter`. Jest to podklasa klasy `dict` i służy do zliczania ilości obiektów hashowalnych.


**_Listing 7_**
```python
def test_counter():

    def print_c_stats(counter: Counter):
        print(counter)
        print(f"Elementy: {list(counter.elements())}")
        print(f"Najliczniejszy element: {counter.most_common(1)}")

    c_str = Counter('Jakieś długie zdanie z wieloma znakami.')
    c_dict = Counter({'red': 4, 'blue': 2})
    c_args = Counter(cats=4, dogs=8)

    print_c_stats(c_str)
    print_c_stats(c_dict)
    print_c_stats(c_args)
```

**Zadanie 3**  
Napisz kod, który porówna czas wykonania operacji append i append left na obiekcie typu `deque` oraz analogicznie append i insert(0) dla obiektu typu `list`.

**Zadanie 4**  
Wykorzystaj plik zamówienia.txt z lab 6 i załaduj część jego zawartości (kilka rekordów) do krotek nazwanych tak, że pola tej krotki są dynamicznie definiowane na podstawie wartości z pierwszego wiersza tego pliku (etykiety).

**Zadanie 5**  
Napisz funkcję, która z tablicy wartości liczbowych będzie zwracała 10% najwyższych wartości.

**Zadanie 6**  
Zdefiniuj funkcję o nazwie `create_kolo_fortuny(*args)`, która przyjmuje nieokreśloną listę argumentów pozycyjnych. Z tej listy argumentów tworzony jest obiekt typu `Counter`, a funkcja zwraca obiekt typu `deque` z elementami tegoż licznika.

**Zadanie 7**  
Korzystając z kodu umieszczonego poniżej oraz wykorzystując funkcję zdefiniowaną w zadaniu 6 napisz rozwiązanie, które będzie operowało na zwracanej kolejce z zadania 6, wykonując jej rotację, i wyświetlało tak jak w funkcji `spinit` aktualne wartości "koła fortuny", aż zatrzyma się na właściwym (można przyjąć, że będzie to pierwszy element kolejki). Wykonaj kilka obrotów kołem dla przetestowania kodu (wartości obrotu mogą być "na sztywno" lub losowane).

```python
def spinit(ticks: int):
    import time
    import numpy as np

    waits = np.logspace(0.0, 1.0, num=ticks) / ticks

    for tick in range(ticks):
        print(f'{tick}', end='')
        time.sleep(waits[tick])
        print('\r', end='')
```