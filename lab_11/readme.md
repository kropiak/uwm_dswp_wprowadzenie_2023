Wprowadzenie do języka Python

## Lab 11 - Omówienie wybranych modułów wbudowanych języka Python. Część 2.


### **1. Moduł `re`.**

> Dokumentacja: https://docs.python.org/3.10/library/re.html
> Tutorial: https://docs.python.org/3.10/howto/regex.html#regex-howto

Moduł `re` pozwala na wykorzystanie wyrażeń regularnych z użyciem języka Python. Wyrażenia regularne pozwalają w uniwersalny bardzo elastyczny sposób określać wzorce, które mogą jednocześnie określać wiele reguł, które poszukiwany łańcuch znaków musi spełniać. 

Specjalne znaczniki i ich znaczenie w wyrażeniu.

| Znacznik | Opis |
|--|----------------------------------------------------------------------------------------------------------|
| `.` | Kropka zastępuje dowolny jeden znak poza znakiem nowej linii (w trybie DOTALL również znak nowej linii). 
| `^` | Ten znak oznacza wyszukiwanie sekwencji rozpoczynającej się od podanego wzorca (rozpoczyna się od ...).  |
| `$` | Ten znak powoduje dopasowanie wzorca na końcu sekwencji (kończy się na...)                               
| `?` | Poprzedzający element jest opcjonalny i dopasowany co najwyżej jeden raz.                                
| `*` | Poprzedzający element będzie dopasowany zero lub więcej razy. Nazywane dopełnieniem Kleene'a.            
| `+` | Poprzedzający element będzie dopasowany jeden lub więcej razy.                                           
| `{n}` | Poprzedzający element pasuje dokładnie n razy.                                                           
| `{n,}` | Poprzedzający element pasuje n lub więcej razy.                                                          
| `{,m}` | Poprzedzający element pasuje co najwyżej m razy. Jest to rozszerzenie GNU.                               
| `{n,m}` | Poprzedzający element pasuje co najmniej n razy, ale nie więcej niż m razy. 
| `'\'` | Znak ucieczki (escape). Powoduje potraktowanie kolejnego znaku dosłownie, bez jego specjalnego znaczenia. Należy pamiętać, że bez używania surowych stringów w Pythonie również uzywamy znaku `'\'` jako znaku ucieczki, więc trzeba go podawać podwójnie lub co wygodniejsze, używać łańcuchów znaków w trybie surowym (raw).
| `[]` | Symbol pozwalający na określenie zbioru wartości. Wyrażenie `[abc]` oznacza `a` lub `b` lub `c`. Możemy również określać zakresy wartości, np. `[0-9]` oznacza wszystkie cyfry od 0 do 9. Jeżeli określenie zbioru jest dość trudne ze względu na jego liczebność możemy poszukać dopełnienia zbioru: `[^abc]` - wszystkie znaki oprócz a, b lub c.
|`'|'`| Określa alternatywę dla podanych wzorców.
|`\d`| Określa cyfrę dziesiętną.
|`\D| Określa dowolny znak nie będący cyfrą dziesiętną
|`\s`| Określa znak niedrukowalny (\t\n\r\f\v)
|`\S`| Określa dowolny znak nie będący znakiem niedrukowalnym.
|`\w`| Określa znak odpowiadający zbiorowi `str.isalnum()` oraz znak `_`
|`\W`| Określa zbiór, który jest dopełnieniem zbioru `\w`
|`\Z`| Dopasowanie tylko na końcu łańcucha znaków.
|`\A`| Dopasowanie tylko na początku łańcucha.

Pozostałe elementy znajdują się w dokumentacji.

**_Listing 1_**
```python
import re

# konwersja wzorca w formie tekstu na obiekt wyrażenia regularnego
digits = re.compile('[0-9]')

# użycie różnych funkcji odnajdowania wartości pasujących do wzorca
# 1. Lista wartości, które spełniają wzorzec
print(re.findall(digits, '7s76dfy7syd7yyf7d'))
# 2. obiekt iteratora z wartościami dopasowanymi
print(re.finditer(digits, '7s76dfy7syd7yyf7d'))
# 3. zwraca obiekt Match, jeżeli na początku łańcucha odnaleziono dopasowanie
print(re.match(digits, '7s76dfy7syd7yyf7d'))
# 4. lub None, jeżeli dopasowania nie odnaleziono
print(re.match(digits, 's76dfy7syd7yyf7d'))
# 5. zwracany jest obiekt Match, jeżeli cały łańcuch spełnia wzorzec lub None w innym przypadku
print(re.fullmatch(digits, '7s76dfy7syd7yyf7d'))

# przykład innego wzorca
fval = re.compile(r'[0-9\s]+[.,][0-9]+')

print(re.findall(fval, '1 435.34343'))
print(re.findall(fval, 'etrt 1 435.34343 tert'))
print(re.findall(fval, '1 435,34343'))
print(re.findall(fval, '1435.0'))

# output
# ['7', '7', '6', '7', '7', '7']
# <callable_iterator object at 0x0000020BF58C7C40>
# <re.Match object; span=(0, 1), match='7'>
# None
# None
# ['1 435.34343']
# [' 1 435.34343']
# ['1 435,34343']
# ['1435.0']
```

### **2. Moduł `pickle`.**

>Dokumentacja: https://docs.python.org/3.10/library/pickle.html

Moduł `pickle` jest binarnym protokołem, który pozwala na serializację i deserializację obiektów języka Python.

**_Listing 2_**
```python
import pickle


my_dict = {'imie': 'Robert', 'nazwisko': 'Lewandowski', 'klub': 'FC Barcelona', 'pozycja': 'napastnik'}

# serializacja
with open('picled_dict', 'wb') as file:
    pickle.dump(my_dict, file)

# deserializacja
with open('picled_dict', 'rb') as file:
    loaded = pickle.load(file)

print(type(loaded))
print(loaded)
```


**Zadania**  

**Zadanie 1**  
Napisz wyrażenia regularne przeszukując plik `strings.txt` i znajdź:
* wszystkie liczby
* wszystkie liczby co najmniej 3 cyfrowe
* wszystkie adresy IPv4
* wszystkie wyrazy rozpoczynające się od wielkiej litery
* wszystkie linie z pliku, które mają co najmniej 4 wyrazy
* wszystkie adresy url

**Zadanie 2**  
Zapisz do pliku lokalnego zawartość przykładowego logu: https://github.com/elastic/examples/blob/master/Machine%20Learning/Security%20Analytics%20Recipes/suspicious_login_activity/data/auth.log

Następnie napisz 'parser', wykorzystując wyrażenia regularne tam, gdzie to możliwe, aby wyciągać z każdej linii datę, adres ip, użytkownika lub usługę i komunikat.
Zapisz do pliku csv datę w formacie RRRR-MM-DD HH:mm:ss, adres ip w formacie z kropkami, usługę/użytkownika bez PID (to wartość numeryczna wewnątrz []) i komunikat z cytowaniem (quoting dla csv).

**Zadanie 3**  
Napisz definicję dowolnej klasy bazując na poprzednich labach. Stwórz jej instancję i zapisz za pomocą modułu `pickle` do pliku binarnego. Załaduj ponownie jej stan.

**Zadanie 4** 
Stwórz listę kilku instancji obiektów z zadania 3 i ponownie serializuj listę obiektów do pliku i ją ponownie odczytać do tej samej postaci.
