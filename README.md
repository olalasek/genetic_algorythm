# genetic_algorythm

Olga Łasek s6054, 2020/2021, Sztuczna inteligencja – laboratorium, prow. Konrad Ożdżyński.
Dokumentacja 2 – Podstawowy algorytm genetyczny – wyszukiwanie maksimum funkcji.

1. Opis algorytmu genetycznego 
 Terminy:
    • Gen – najmniejsza część chromosomu
    • Chromosom – uporządkowany ciąg genów
    • Genotyp – struktura danych – jak reprezentujemy rozwiązanie
    • Osobnik – najprostsza jednostka podlegająca ewolucji
    • Fenotyp – znaczenie lub interpretacja tego rozwiązania
    • Populacja – zbiór rozwiązań
    • Selekcja – lepsze rozwiązania generowane są dzięki większej liczbie kopii ( w przypadku stałej liczby populacji lepsze rozwiązania z czasem dominują populację)
    • Zmiana :
        ◦ Mutacja – nagła zmiana materiału genetycznego
        ◦ Krzyżowanie – losowe przecięcie dwóch chromosomów w jednym punkcie i zamiana podzielonych części między chromosomami
    • Dopasowanie – funkcja celu – sprawdzanie jakości populacji
    • Losowanie populacji początkowej
    • Selekcja, czyli obliczanie funkcji przystosowania dla każdego osobnika, najlepiej przystosowane osobniki biorą udział w procesie reprodukcji 
    • Wybrane osobniki poddawane są operacjom ewolucyjnym:
            ▪ pierwszym krokiem jest krzyżowanie, wymiana materiału genetycznego pomiędzy rodzicami
            ▪ następnie przeprowadzana jest mutacja, czyli wprowadzenie drobnych losowych zmian.
    • Powstaje drugie (kolejne) pokolenie. Aby utrzymać stałą liczbę osobników w populacji, te najlepiej przystosowane ( wg funkcji przystosowania) są powielane, a najsłabsze usuwane. Jeżeli nie znaleziono dostatecznie dobrego rozwiązania, algorytm wraca do kroku drugiego.

2. Obliczenia

Dane do zadania:
Nr indeksu: 6054,  a = 5, b = 4
Zadana funkcja y = ax + b, y = 5x + 4
Pk – współczynnik krzyżowania = 0,8
Pm – współczynnik mutacji = 0,2
Liczba chromosomów = 6
Zakres x € <0,31> (5 bitów)

	I. Ustalenie puli początkowej chromosomów binarnych.
	
	Ch1 = 01000
	Ch2 = 00011
	Ch3 = 01110
	Ch4 = 11101
	Ch5 = 10001
	Ch6 = 11110
	
	II. Obliczenie fenotypów (wartości dziesiętnej chromosomów).
	
	Ch1 = 01000 = 8
	Ch2 = 00011 = 3
	Ch3 = 10101 = 21
	Ch4 = 11101 = 29
	Ch5 = 10001 = 17
	Ch6 = 11110 = 30

	III. Obliczanie wartości funkcji przystosowania
	
	f(ch1) = 5 * 8 + 4 = 44
	f(ch2) = 5 * 3 + 4 = 19
	f(ch2) = 5 * 21 + 4 = 109
	f(ch2) = 5 * 29 + 4 = 149
	f(ch2) = 5 * 17 + 4 = 89
	f(ch2) = 5 * 30 + 4 = 154

	IV. Selekcja chromosomów metodą koła ruletki
	
	Suma wartości wszystkich funkcji przystosowania.
	44 + 19 + 109 + 149 + 89 +154 =  564

	Wartość procentowa dla kolejnych chromosomów:

	f(ch1) % = (44/564)*100% = 7,8% (granatowy)
	f(ch2)% = (19/564)*100% = 3,37% (pomarańczowy)
	f(ch3)% = (109/564)*100% =19,33% (żółty)
	f(ch4)% = (149/564)*100% = 26,42% (zielony)
	f(ch5)% = (89/564)*100% = 15,78% (bordowy)
	f(ch6)% = (154/564)*100% = 27,3% (błękitny)
	Koło ruletki:




	Losowanie chromosomów z koła ruletki (pula po selekcji):

	Ch1 → Ch6 = 11110
	Ch2 → Ch4 = 11101
	Ch3 → Ch5 = 10001
	Ch4 → Ch6 = 11110
	Ch5 → Ch3 = 01110
	Ch6 → Ch4 = 11101

	V. Operacje genetyczne

	Krzyżowanie  - dobieramy kolejno chromosomy w pary
	Losowanie Pk oraz lokus (od 1 do n-1) dla każdej pary

	Ch1 – 0100|0							01001
				Pk = 0,5	lokus = 4 		krzyżowanie
	Ch2 – 0001|1 							00010


	Ch3 – 0111|0							01111
				Pk = 0,3	lokus = 4 		krzyżowanie
	Ch4 – 1110|1 							11100
	Ch5 – 100|01							10001
				Pk = 0,9	lokus = 3 		brak krzyżowania
	Ch6 – 111|10							11110

	Pula po krzyżowaniu:
	
	Ch1 = 01001
	Ch2 = 00010
	Ch3 = 01111
	Ch4 = 11100
	Ch5 = 10001
	Ch6 = 11110

	Mutacje – dla każdego chromosomu losujemy dwie liczby Pm i lokus.
	Mutacja to negacja bitu.

	Ch1 = 01011	Pm = 0,03	lokus = 1		mutacja

	Ch2 = 00010	Pm = 0,17	 lokus = 1		mutacja

	Ch3 = 01111	Pm = 0,35	lokus = 4		brak mutacji

	Ch4 = 11100	Pm = 0,11	lokus = 3		mutacja

	Ch5 = 10001	Pm = 0,46	lokus = 5		brak mutacji

	Ch6 = 11110	Pm = 0,93	lokus = 3		brak mutacji

	Pula po mutacji:

					fenotyp		f. przystosowania
	Ch1 = 11011		27			5 * 27 + 4 = 139 
	Ch2 = 10010		18			5 * 18 + 4 = 94 
	Ch3 = 01111		15			5 * 15 + 4 = 79
	Ch4 = 11000		24			5 * 24 + 4 = 124
	Ch5 = 10001		17			5 * 17 + 4 = 89
	Ch6 = 11110		30			5 * 30 + 4 = 154

	Suma funkcji przystosowania: 679
