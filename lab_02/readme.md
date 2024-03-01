# Wprowadzenie do języka Python

## Lab 02

### 1. Typ łańcuchowy w Pythonie i klasa `str`. Omówienie wybranych aspektów.

> Dokumentacja: https://docs.python.org/3.11/library/stdtypes.html#str

Typ łańcuchowy jest chyba najbardziej powszechnym typem danych nie tylko w języku Python. Dane pobierane z plików, bez względu na ich postać są pierwotnie zapisane jako łańcuch znaków, a następnie mogą być skonwertowane na inny typ, np. numeryczny. Zapisanie danych do pliku wyjściowego również wymaga często ich rzutowania (zamiany typu) na typ `str`.

W etapie przygotowania i oczyszczania danych (ang. data cleaning, data mangling) bardzo często praca polega na wykorzystaniu metod i technik pracy z łańcuchami znaków.


#### 1.1 Wybrane własności klasy `str`.

Klasa `str` zapewnia konstruktor, który zwraca postać łańcuchową przekazanego obiektu. Każdy obiekt w Pythonie posiada taką postać, chociaż czasem to co uzyskamy na wyjściu nie zawsze jest pomocne. Dzieje się to z powodu dziedziczenia innych obiektów po klasie `object`, która dostarcza między innymi magicznej metody `__str__()`. 

Osoby zainteresowane zgłębianiem kodu źródłowego implementacji CPython odsyłam do: https://github.com/python/cpython

Technicznie przy wywołaniu `str(obiekt)` wywoływana jest metoda `__str__()` dla danego typu obiektu, a jeżeli tam nie została ona zaimplementowana to poprzez mechanizm dziedziczenia będzie kaskadowo poszukiwana metoda `__str__()` obiektu rodzica, aż do abstrakcyjnej ogólnej klasy `object`.

**Listing 1**
```python

# deklaracja typu str poprzez literał
artykul = """Recenzja "Władcy Pierścieni"."""
imie = 'Jan'
hobby = "piłka nożna"

# deklaracja typu str poprzez wykorzystanie konstruktora
lista_string = str(list[1, 2, 3])
int_string = str(5)
```

Powyższy fragment to tylko przykład różnych metod deklaracji, w trakcie zajęć będą stosowane apostrofy.


**Listing 2**
```python
# czy będzie jakaś różnica w oknie konsoli ?
print(str(5))
print(5)
print(int(5))
print(int(5).__str__())
```

Poniżej przedstawiony zostanie fragment kodu, a którym wykorzystane zostanie kilka wybranych metod dla klasy `str`. Dla pełnej listy odsyłam do oficjalnej dokumentacji.

**Listing 3**
```python
# 1. wczytujemy dane ze standardowego wejścia (tu przechwytujemy wejście z klawiatury w oknie konsoli)
sentence = input('Wpisz dowolne zdanie:\n')
# dane przechowywane są w postaci zmiennej typu str

# 2 - możemy usunąć ewentualne białe znaki na początku i końcu łańcucha.
sentence = sentence.strip()
# można ograniczyć się tylko do początku lub końca łańcucha używając odpowiednio metod
# lstrip() i rstrip()

# 3 - Jedną z metod jest metoda split, która dzieli łańcuch na części, a każda z nich jest
# zapisywana do listy w postaci łańcucha znaków bez uwzględnienia znaku separatora.
# Łańcuch zostanie podzielony i zliczone zostaną słowa (zakładają, że spacje jest separatorem)
words = sentence.split(' ')

"""
Można pominąć ' ' w tym przypadku i efekt będzie taki sam, ale to nie oznacza, że domyślnie
jest to po prostu spacja. 
Za dokumentacją:
If sep is not specified or is None, a different splitting algorithm is applied: runs of consecutive whitespace are regarded as a single separator, and the result will contain no empty strings at the start or end if the string has leading or trailing whitespace. Consequently, splitting an empty string or a string consisting of just whitespace with a None separator returns [].
"""

print('W podanym zdaniu jest ', len(words), ' słów.')

# 4 - możemy również sprawdzić, czy zdanie rozpoczyna się wielką literą
print('Czy zdanie rozpoczyna się wielką literą? -> ', words[0].istitle())

# 5 - lub czy zdanie rozpoczyna się znakiem alfabetycznym
print('Czy zdanie rozpoczyna się od litery? -> ',sentence[0].isalpha())

# 6 - teraz wczytamy inne wejście - oczekujemy podania liczby
num = input('Wpisz dowolną liczbę:\n')

print('Czy liczba jest liczbą całkowitą? -> ', num.isdigit())

# 7 - jak wprowadzone zostaną instrukcje warunkowe i pętle to będzie łatwiej :)
# sprawdzimy, czy wartość była podana jako docelowy float (separator . )
print('Czy liczba jest liczbą zmiennoprzecinkową? -> ', num.replace('.','',1).isdigit())

# 8 - dopełnimy liczbę poprzedzającymi zerami do 5 pozycji
# aktualnie zadziała tylko dla liczby całkowitej
print(num.zfill(5))
```

Ciąg tekstowy w Pythonie to tablica znaków co daje z miejsca wiele możliwości manipulacji i dostępu do składowych tego ciągu. Inna ważna cecha stringów to fakt, że po ich zadeklarowaniu nie możemy zmienić zadeklarowanych znaków ciągu, gdyż zmienne typu string są niemutowalne (ang. immutable). Oczywiście możemy nadpisać zmienną nową wartością, czyli zmienić wartość przez przypisanie.


**Listing 4**
```python
imie = 'Kowalski'
nazwisko = 'Jan'

# string to tablica znaków więc możemy odwołać się do jej elementów
print(imie[0])

# indeks elementu możemy również określać jako pozycja od końca ciągu
print(imie[-1])

# można również pobrać fragment ciągu (slice) określając jako indeks
# element początkowy i końcowy. Zwróć uwagę na wartość tych indeksów.
print(imie[0] + imie[-2] + imie[4:6])
# można również określic tylko jeden z dwóch indeksów
# co oznacza od elementu o indeksie 3 do końca łańcucha
print(imie + nazwisko[3:])

# ogólna postać slice
# [start:stop:step]
# wartości poszczególnych parametrów slice'a są pomijalne, ale
# musimy zapisywać drukropki, które informują mechanizm o tym
# które parametry zostaną uzyte z ich domyślnymi wartościami
# sprawdź działanie poniższych przykładów
print(imie[::2])
print(imie[-2])
print(imie[:-4:-1])
print(imie[::-1])

# inny sposób złączania ciągów
print(imie + ' ' + nazwisko)

# Elementów ciągu nie można zmieniać więc poniższa instrukcja zwróci błąd.
# nazwisko[0] = "P"

# Potwierdzeniem tego, że ciąg tekstowy jej również obiektem jest możliwość
# wykonania na nim metod dla tego typu zdefiniowanych. Metoda count() zlicza
# ilość wystąpień danego ciągu w wartości przechowywanej przez zmienną.
print(imie.count('z'))
# Co ciekawe w Pythonie możemy wywoływać funkcje dla danego obiektu już podczas deklaracji
# co na pierwszy rzut oka może wyglądać dość egzotycznie.
print('Jesteś szalona!'.count('a'))

# Potwierdzeniem niezmienności zadeklarowanego stringa może być również poniższy kod
print(imie.lower())
print(imie)

# Aby zwrócić długość ciągu tekstowego należy posłużyć się wbudowaną funkcją len()
print(len(nazwisko))
```


#### 1.2 Formatowanie łańcuchów znaków.

Formatowanie łańcuchów znaków polega na łączeniu wzorców tekstowych z wartościami innych typów.
Wiemy już, że możemy to zrobić poprzez uzycie funkcji `print()` np. `print('Adam ma ', 23 ,' lata')` i nie jest to najgorszy pomysł. Ma jednak pewne wady, a mianowicie nie mamy tutaj zbyt wielu możliwości określenia formatu, w jakim wartość niebędąca łańcuchem znaków zostanie wypisana, np. z dokładnością do n-znaków po przecinku, wyrównana do strony prawej lub lewej, itd. Z pomocą przychodzą techniki formatowania łańcuchów znaków przedstawione na listingu poniżej.

**Listing 5**
```python
# formatowanie znane z Pythona 2.x
wyznanie = 'Lubię %s' % 'Pythona'
print(wyznanie)
wonsz = 'Python'
print('Lubię %sa' % wonsz)

print('Lubię %s oraz %sa' % ('Pythona', wonsz))

# %s oznacza, że w miejsce tego znacznika będzie podstawiany ciąg tekstowy
# %i - to liczba całkowita
# %f - liczba rzeczywista lub inaczej zmiennoprzecinkowa
# %x lub %X - liczba całkowita zapisana w formie szesnastkowej

print('Używamy wersji Python %i' % 3)
print('A dokładniej Python %f' % 3.9)
print('Chociaż lepiej to zapisać jako Python %.1f' % 3.9)
print('A kolejną glówną wersją Pythona może być wersja %.4f' % 3.11111)
print('A może będzie to wersja %.1f ?' % 3.111)
print('A może jednak %.f ?' % 3.12)
wersja = 4
print('A %i w systemie szesnastkowym to %X' % (wersja, wersja))
print('A %i * %i szesnastkowo daje %X' % (wersja, wersja, wersja*wersja))

# Chociaż możliwości przy korzystaniu z mechanizmów powyżej są spore,
# to i kilka wad się również znajdzie. Trzeba pilnować zarówno liczby argumentów, jak
# i ich kolejności. Konieczne jest powielanie tej samej zmiennej, jeżeli kilka
# razy jest wykorzystywana w formatowanym ciągu. Spójrzmy na inne możliwości.

print('Lubię %(jezyk)s' % {'jezyk': 'Pythona'})
print('Lubię %(jezyk)s a czy Ty lubisz %(jezyk)s ?' % {'jezyk': 'Pythona'})
# wadą jest dość duża ilość dodatkowego kodu do napisania, ale nazwy zmiennych
# w ciągu pozwalają na ich szybką identyfikację i wielokrotne wykorzystanie w
# dowolnej kolejności

# poniżej kolejny sposób
print('Lubię język {1} oraz {0}'.format('Java', 'Python'))

# w nowej wersji języka Python możliwe jest również odwoływanie się do elementów kolekcji
# lub pól klasy
class Osoba:

    def __init__(self, imie, nazwisko):
        self.imie = imie
        self.nazwisko = nazwisko

jan = Osoba('Jan', 'Kowalski')

print('Tą osobą jest {0.imie} {0.nazwisko}'.format(jan))
```

W wersji 3.6 wprowadzono do języka Python pojęcie **„f-string”**, które nieco upraszcza formatowanie ciągów tekstowych. Jest to obecnie zalecana i szeroko stosowana metoda. Przykład poniżej.

**Listing 6**	
```python
import sys

# zapis jest skróconą postacią użycia funkcji .format()
imie = 'Marek'
print(f'Witaj {imie}!')
print(f'Wynik dodawania 33.33 oraz 66.67 to{33.33 + 66.67: .4f}')
print(f'Witaj {input()}!')
print(f'Korzystasz z Pythona w wersji {sys.version}.)
```

Po więcej przykładów związanych z formatowaniem łańcuchów można udać się pod poniższe adresy:

1.	https://docs.python.org/3/library/string.html#format-string-syntax
2.	https://pyformat.info/
3.	https://realpython.com/python-f-strings/


Kilka mniej oczywistych przykładów z wykorzystaniem właściwości typów `str`.

**Listing 7**
```python
# \r jest sekwencją sterującą (tu powrót karetki), sprawdź co to oznacza
print('elo\r', end='')
print('zero\r', end='')

# sekwencje sterujące są opisane tu:
# https://docs.python.org/3.11/reference/lexical_analysis.html#escape-sequences

# gdybyśmy jednak chcieli wypisać na konsoli łańcuch reprezentujący zarezerwowany 
# dla sekwencji sterującej możemy to zrobić wykorzystując łańcuch 'surowy' lub sekwencję escape (\\)

print('elo\\r', end='')
print(r'zero\r', end='')

# a dlaczego się to może przydać ? wypisz linie poniżej
print('\sciezka\rok\numer\task')
print(r'\sciezka\rok\numer\task')
print('\\sciezka\\rok\\numer\\task')

# można też wypisać znaki niestandardowe z tablicy Unicode
print("\u2764")
print("\u2765")
print("\U0001F602")

# tablica unicode w przyjaznej formie: https://symbl.cc/en/unicode/table/

```

**Zadania**

1. Napisz fragment kodu, który wczyta trzy zmienne z klawiatury:
   * linię danych rozdzielonych jakimś separatorem (spacja, średnik, itd.)
   * separator źródłowy
   * separator docelowy  
   
Następnie zaimplementuj z użyciem metod `split` oraz `join` podzielenie danych wejściowych pierwszym separatorem, połączenie i wypisanie danych połączonych drugim separatorem.
Czy można to zrobić prościej wykorzystując wbudowane metody?

2. Użyj funkcji `input()` aby pobrać łańcuch znaków z klawiatury i z użyciem wycinków (slice) wykonaj:
  * podziel łańcuch na dwie części, w miarę możliwości równe, ale jeżeli długość łańcucha jest nieparzysta, np. 11 znaków to pierwszy ma długość 5, a drugi 6. Wyświetl te łańcuchy w oknie konsoli.
  * wyświetl łańcuch składający się z co drugiego znaku licząc od końca łańcucha

3. Wyświetl na konsoli dowolny ciąg znaków i wykorzystaj wbudowane metody:
* `title()`, 
* `capitalize()`,
* `zfill()`,
* `upper()`,
* `count()`,
* `center()`.

4. Wprowadź z klawiatury dowolny łańcuch znaków i zapisz go do zmiennej. Następnie bazując na przykładzie poniżej zapisz również wyniki dla metod `isalpha(), isascii(), isprintable(), istitle(), isupper()`.
`wejscie = input()`
`print("Łańcuch {wejscie} isdecimal: {wejscie.isdecimal()}")`.

5. Przejdź na stronę https://pyformat.info/, a następnie zapisz w oddzielnym pliku .py i wykonaj 5 wybranych przykładów formatowania ciągów oznaczonego jako „New”, których nie było w przykładach z tego podrozdziału (np. z wyrównaniem do prawej lub lewej strony, ilością pozycji liczby, znakiem, wypełnieniem spacji itp.). Przerób zaprezentowane tam przykłady na postać z użyciem f-string.

6. Wykorzystując **listing 7** wypisz na konsoli 10 wybranych znaków niestandardowych (np. litery z alfabetu greckiego, symbole walut - (funt, bitcoin)) wypisując jednocześnie jego kod z tablicy unicode.