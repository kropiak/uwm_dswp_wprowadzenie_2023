Wprowadzenie do języka Python

## Lab 10 - Omówienie wybranych modułów wbudowanych języka Python. Część 1.


### **1. Moduł `os`.**

> Dokumentacja: https://docs.python.org/3.10/library/os.html#module-os

Moduł `os` jest przydatnym modułem w przypadku, kiedy potrzebujemy skomunikować się bezpośrednio z systemem operacyjnym, na którym program zostanie uruchomiony. Komunikacja pośrednia odbywa się poprzez mechanizmy zarządzania dostępem do pamięci, zarówno dyskowej, jak i operacyjnej oraz procesora. Jeżeli istnieje potrzeba odczytu, ustawienia zmiennych środowiskowych czy operacji w systemie plików, moduł `os` będzie bardzo przydatny również ze względu na abstrakcję, która pozwala na napisanie jednolitego kodu, który będzie działał w różnych systemach operacyjnych (np. ścieżki do zasobów, lokalizacja zmiennych środowiskowych).

W poniższych przykładach zostały wybrane tylko niektóre z możliwości tego modułu.

**_Listing 1_**
```python
import os
# przydatny moduł typu "pretty print"
import pprint

# wypisanie wszystkich zmiennych
variables = os.environ
pprint.pprint(dict(variables), width = 1)

# wypisanie typu systemu operacyjnego
print(os.name)
# odwołanie do konkretnej zmiennej środowiskowej
print(f'Witaj {os.environ["username"]}')
# lub tak
print(os.getenv("username"))

# ustawienie zmiennej tylko dla tego procesu
# zmiany nie zostaną również zapisane na stałe
os.environ['test'] = 'testowa_zmienna'
print(os.environ['test'])

for path in os.environ['PATH'].split(';'):
    print(path)
```

Przykłady wykorzystania modułu `os` do pracy w systemie plików.

**_Listing 2_**
```python
# odczytanie listy zasobów w bieżącym folderze (domyślna ścieżka)
print(os.listdir())
# tylko foldery
dirs = [resource for resource in os.listdir() if os.path.isdir(os.path.join(resource))]
print(dirs)

# ścieżka do bieżącego folderu
print(os.getcwd())

# utworzenie folderu w bieżącej lokalizacji
try:
    dirname = 'TEMP_DIR'
    os.mkdir(dirname)
    print(f'Utworzono folder: {os.path.join(os.getcwd(), dirname)}')

except OSError as e:
    print(e)


# przykład budowania ścieżki sprawdzenia, czy zasób istnieje
# (są też inne możliwości np. sprawdzenie uprawniień do zapisu, odczytu itp.)
BASE_DIR = os.path.join(os.getcwd(), 'TEMP')
if os.path.exists(BASE_DIR):
    print('Folder bazowy istnieje')
else:
    print('Folder bazowy nie istnieje. Utworzyć(y/n)?')
    answer = input()
    if answer.lower() == 'y':
        try:
            os.mkdir(BASE_DIR)
            print(f'Utworzono folder: {BASE_DIR}')
            # i "przechodzimy" do tego folderu
            os.chdir(BASE_DIR)
            print(f'Bieżący folder to: {os.getcwd()}')
        except OSError as e:
            print(e)
    else:
        print('Folder bazowy nie został utworzony.')

    # przejście przez strukturę katalogów poczynając od folderu startowego (topdown)
    for root, dirs, files in os.walk(os.getcwd()):
        print(root)
        print('    ', files)

```

Istnieje jeszcze szereg innych funkcji, które pozwalają np. na zmianę nazwy zasobu, usunięcie zasobu itp., ale po szczegóły odsyłam do dokumentacji.

### **2. Moduł `time` oraz `datetime`.**

> Dokumentacja moduł time: https://docs.python.org/3.10/library/time.html

> Dokumentacja moduł datetime: https://docs.python.org/3.10/library/datetime.html

> Dokumentacja moduł zoneinfo: https://docs.python.org/3/library/zoneinfo.html

Może być konieczne zainstalowanie pakietu `tzdata` (pip install tzdata).

Oba moduły służą do pracy z datą i czasem umożliwiając odczytywanie, tworzenie i konwersję tych wartości. Korzystając z gotowych funkcji możemy uniknąć problemów związanych z ręcznym kontrolowaniem ilości dni w miesiącu, lat przestępnych, stref czasowych oraz łatwe obliczanie interwałów między datami.

**_Listing 3_**
```python
import time
from datetime import datetime, timezone, timedelta
from zoneinfo import ZoneInfo, available_timezones

# pobranie bieżącego czasu
now = time.time()

print(now)
now_local = time.localtime(now)
print(time.asctime(now_local))

# wyświetlenie bieżącego czasu w danym miejscu (strefa czasowa)
print(datetime.now(ZoneInfo('Europe/Madrid')))

# lista dostępnych stref czasowych
available_timezones()

# wykorzystując timedelta możemy dość łatwo operować na datach w przód lub w tył
data_wystawienia = datetime.now().date()
print(f'Data wystawienia: {data_wystawienia}')
print(f'Termin płatności: {data_wystawienia + timedelta(days=14)}')

print(f'3 dni wcześniej to {data_wystawienia - timedelta(days=3)}')

# konwersja daty zapisanej w postaci łańcucha znaków do obiektu datetime
# kody dla formatu: https://docs.python.org/3.10/library/datetime.html#strftime-and-strptime-format-codes
print(datetime.strptime('2023/03/23', '%Y/%m/%d'))
# data ze znacznika czasu (timestamp)
print(datetime.fromtimestamp(time.time()))

```

**Zadania**

**Zadanie 1**  
Napisz funkcję, która będzie przyjmowała listę ścieżek do folderów. Następnie iterując przez listę sprawdzaj, czy dana ścieżka istnieje i jeżeli nie to twórz wszystkie niezbędne foldery (i podfoldery). Sprawdź możliwość metody `makedirs` z modułu `os`.

**Zadanie 2**  
Napisz funkcję, która odczyta wszystkie pliki .txt z podanego folderu i podfolderów (testuj na zasobie dane_do_lab_10.zip) i scali ich zawartość do jednego pliku .csv, pomijając duplikujące się nagłówki występujące w plikach.

**Zadanie 3**  
Napisz skrypt, który będzie pytał użytkownika o czas (format HH:MM:SS), który następnie zostanie wyświetlony dla 4 poniższych miejsc (stref czasowych): Tokyo, Waszyngton, Sydney, Londyn.

**Zadanie 4**  
Napisz funkcję, która dla podanej daty wyświetli wiek w postaci:
Dzisiaj masz X lat, Y miesięcy i Z dni. Do twoich kolejnych urodzin pozostało N dni.

**Zadanie 5**  
Napisz funkcję, która:
* przyjmuje następujące argumenty: nazwa pliku, indeks kolumny z datą, format źródłowy i docelowy.
Odczytaj plik z zadania 2 i skonwertuj datę na format 'RRRR-MM-DD'. Zapisz plik pod inną nazwą.
