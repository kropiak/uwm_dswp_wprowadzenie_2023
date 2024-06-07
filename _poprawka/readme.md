# Wprowadzenie do języka Python.
## Kolokwium 1

Rozwiązania zapisz w jednym pliku o następującej strukturze.
```python
def zadanie_1():
    pass


def zadanie_2():
    pass


def main():
    # zadanie_1() # jeżeli w danym momencie wywołanie nie jest potrzebne
    zadanie_2()


if __name__ == '__main__':
    main()
```

Plik nazywamy według wzorca `imie_nazwisko_wp_k1.py` i po wykonaniu zadań wysyłamy na adres kropiak@matman.uwm.edu.pl.


**Zadanie 1 (1 pkt)**  
Napisz funkcję, która:
* jako argument wejściowy przyjmuje dowolny słownik
* funkcja zwraca listę kluczy ze słownika, które są liczbami

**Zadanie 2 (1 pkt)**  
Napisz funkcję, która:
* jako argument przyjmuje dowwolny ciąg znaków
* zwraca ten ciąg, ale tak, że każdy jego element (wyraz) wypisany jest wspak (ale nie cały ciąg)

**Zadanie 3 (1 pkt)**  
Napisz funkcję, która:
* jako argument przyjmuje wartość całkowitoliczbową max (int) określającą maksymalny numer indeksu produktu oraz prefix
* funkcja zwraca listę kodów produktów (np. dla prefixu prod_ i max = 10, zwraca listę [prod_01, ..., prod_10])

**Zadanie 4 (1 pkt)**  
Napisz funkcję "zgadywankę". Uruchomienie funkcji losuje liczbę z przedziału 1 - 100 a następnie z uzycie pętli while pozwala na wprowadzanie wartości z klawiatury w celu jej odgadnięcia. Za każdym razem informuj uzytkownika czy podana liczba jest za mała czy za duża lub czy została odgadnięta. Zapisuj wszystkie podawane liczby i po wygraniu wypisz komunikaty : W próbie n podałeś k1. Nie zgdałeś. , a dla odgadnięcia W próbie n podałeś k.. Wygrałeś!.


