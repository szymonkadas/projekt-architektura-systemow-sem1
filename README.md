Projekt Symulatora Instrukcji Procesora 8086 w React.js
Cel Projektu:
Celem projektu jest stworzenie aplikacji w React.js, która symuluje działanie dwóch instrukcji procesora 8086: MOV oraz XCHG, dla rejestrów AX, BX, CX, i DX. 
Użytkownik będzie mógł wprowadzać wartości w postaci szesnastkowej (HEX) do tych rejestrów i obserwować działanie wspomnianych instrukcji.
Wymagania Funkcjonalne:
1.	Interfejs Użytkownika:
Aplikacja powinna posiadać prosty i intuicyjny interfejs, który pozwala na:
•	Wprowadzanie wartości do rejestrów AX, BX, CX, DX w formacie szesnastkowym.
•	Wyświetlanie aktualnych wartości rejestrów.
•	Wykonanie instrukcji MOV i XCHG poprzez interaktywne przyciski.
•	Resetowanie wartości rejestrów do stanu początkowego.
2.	Instrukcja MOV:
•	Symulacja instrukcji MOV, która kopiuje wartość z jednego rejestru do drugiego.
•	Interakcje obejmujące wszystkie pary rejestrów: AX, BX, CX, DX.
3.	Instrukcja XCHG:
•	Symulacja instrukcji XCHG, która wymienia wartości dwóch rejestrów.
•	Interakcje obejmujące wszystkie pary rejestrów: AX, BX, CX, DX.
 
Podłoże teoretyczne symulacji instrukcji MOV XCHG procesora 8086:
Wstęp
Procesor 8086 jest 16-bitowym mikroprocesorem stworzonym przez firmę Intel wprowadzonym na rynek w 1978 roku. Jest znany z tego, że stanowił podstawę rozwoju rodziny procesorów x86, która stała się standardem w komputerach osobistych. Projektowany był głównie do obsługi języka asemblera i niskopoziomowych operacji wykonywanych bezpośrednio na rejestrach procesora.
Rejestry Procesora 8086
Procesor 8086 posiada zestaw rejestrów, które można podzielić na kilka kategorii: dane, wskaźniki i indeksy oraz segmenty. W kontekście naszego projektu interesują nas jedynie rejestry danych:
1.	AX (Accumulator Register):
Rejestr akumulatora, często używany do operacji arytmetycznych, logicznych oraz przechowywania danych tymczasowych.
2.	BX (Base Register):
Rejestr bazowy, używany głównie jako wskaźnik do danych w segmentach.
3.	CX (Count Register):
Rejestr licznikowy, używany do operacji iteracyjnych, jak pętle.
4.	DX (Data Register):
Rejestr danych, często używany w operacjach we/wy, arytmetyce rozszerzonej.
Każdy z tych rejestrów może przechowywać wartości 16-bitowe, co oznacza, że mogą one przyjmować wartości szesnastkowe w zakresie 0000 - FFFF.
Instrukcje MOV i XCHG
1.	MOV (Move):
•	Instrukcja MOV kopiuje wartość z jednego miejsca do drugiego. W przypadku rejestrów, instrukcja ta jest używana do przenoszenia danych między rejestrami.
•	Składnia: MOV dokąd, skąd
•	Przykład: MOV AX, BX – kopiuje wartość z rejestru BX do rejestru AX.
2.	XCHG (Exchange):
•	Instrukcja XCHG wymienia wartości dwóch operandów. Dla rejestrów oznacza to zamianę wartości między dwoma rejestrami.
•	Składnia: XCHG dokąd, skąd
•	Przykład: XCHG AX, BX – wymienia wartości między rejestrami AX i BX.
 
Architektura Aplikacji:
Aplikacja wspiera się typescriptem, reactem etc
Logika działań zostanie zrealizowana przy użyciu klasy Emulator o następującej strukturze: 
```
typescript
``` 
Warstwa wizualna opiera się na komponentach w React.js które tworzą strukturę html.
To wszystko ze wsparciem kaskadowych arkuszy stylów które zapewnią znośny wygląd.
Opis później gdy będzie kod
 
Jak uruchomić:
instrukcje uruchomienia projektu z archiwum, najlepiej rzucić zbuildowany projekt.

