### Projekt Symulatora Instrukcji Procesora 8086 w HTML i JavaScript
#### Cel Projektu:
Celem projektu jest stworzenie aplikacji w HTML i JavaScript, która symuluje działanie dwóch instrukcji procesora 8086: MOV oraz XCHG, dla rejestrów AX, BX, CX, DX. Użytkownik będzie mógł wprowadzać wartości w postaci szesnastkowej (HEX) do tych rejestrów i obserwować działanie wspomnianych instrukcji.
Stosowane są trzy tryby adresowania: bazowe, indeksowe, indeksowo-bazowe. Symulator ma na podstawie wprowadzonych wartości rejestrów BX, BP, DI, SI oraz offsetu (w kodzie szesnastkowym) wyliczać adres komórki pamięci, do której przesyłane są zawartości rejestrów AX, BX, CX lub DX.
Wymagania Funkcjonalne:
- **Interfejs Użytkownika:**
  Aplikacja powinna posiadać prosty i intuicyjny interfejs, który pozwala na:
  - Wprowadzanie wartości do rejestrów AX, BX, CX, DX, BX, BP, DI, SI i offsetu w formacie szesnastkowym.
  - Wyświetlanie aktualnych wartości rejestrów.
  - Wykonanie instrukcji MOV i XCHG poprzez interaktywne przyciski.
  - Resetowanie wartości rejestrów do stanu początkowego.
- **Instrukcja MOV:**
  - Symulacja instrukcji MOV, która kopiuje wartość z jednego rejestru do drugiego lub między rejestrami a pamięcią operacyjną za pomocą różnych trybów adresowania.
    - Tryby adresowania: bazowe, indeksowe, indeksowo-bazowe.
- **Instrukcja XCHG:**
  - Symulacja instrukcji XCHG, która wymienia wartości dwóch rejestrów.
  - Interakcje obejmujące wszystkie pary rejestrów: AX, BX, CX, DX.
  - **Dodatkowo:** Symulacja rozkazu XCHG dla przesyłania z pamięci operacyjnej do rejestrów AX, BX, CX i DX i z rejestrów do pamięci.
### Podłoże teoretyczne symulacji instrukcji MOV i XCHG Procesora 8086:
**Wstęp:**
Procesor 8086 jest 16-bitowym mikroprocesorem stworzonym przez firmę Intel wprowadzonym na rynek w 1978 roku. Jest znany z tego, że stanowił podstawę rozwoju rodziny procesorów x86, która stała się standardem w komputerach osobistych. Projektowany był głównie do obsługi języka asemblera i niskopoziomowych operacji wykonywanych bezpośrednio na rejestrach procesora.
**Rejestry Procesora 8086:**
Procesor 8086 posiada zestaw rejestrów, które można podzielić na kilka kategorii: dane, wskaźniki i indeksy oraz segmenty. W kontekście naszego projektu interesują nas jednak nie tylko rejestry danych, ale również pamięć operacyjna o czym później.
- **AX (Accumulator Register):**
  Rejestr akumulatora, często używany do operacji arytmetycznych, logicznych oraz przechowywania danych tymczasowych.
- **BX (Base Register):**
  Rejestr bazowy, używany głównie jako wskaźnik do danych w segmentach.
- **CX (Count Register):**
  Rejestr licznikowy, używany do operacji iteracyjnych, jak pętle.
- **DX (Data Register):**
  Rejestr danych, często używany w operacjach we/wy, arytmetyce rozszerzonej.
  Każdy z tych rejestrów może przechowywać wartości 16-bitowe, co oznacza, że mogą one przyjmować wartości szesnastkowe w zakresie 0000 - FFFF.
- **Rejestr BP:**
  Rejestr bazowy (BP) jest używany podobnie jak BX do bazowego adresowania komórek pamięci. Służy głównie do adresowania danych w stosie lub w strukturach danych.
- **Rejestr SI:**
  Rejestr SI (Source Index) jest używany jako wskaźnik źródłowy w operacjach przetwarzania danych. Może być używany zarówno w trybach indeksowego, jak i bazowo-indeksowego adresowania.
- **Offset:**
  Offset jest wartością bezpośrednią dodawaną do zawartości rejestrów bazowych lub indeksowych w celu obliczenia adresu efektywnego pamięci. Wartość offset jest podawana bezpośrednio przez programistę i może być używana do precyzyjnego określenia lokalizacji w pamięci.
- **Rejestr DI:**
  Rejestr DI (Destination Index) jest używany jako wskaźnik docelowy w operacjach przetwarzania danych. Podobnie jak SI, może być stosowany zarówno w trybach indeksowego, jak i bazowo-indeksowego adresowania.
**Pamięć operacyjna:**
Pamięć operacyjna w procesorze 8086 umożliwia przechowywanie i odczyt danych oraz adresów, które mogą być wykorzystane do bezpośrednich operacji z rejestrami. Symulator będzie obsługiwał przesyłanie wartości między rejestrami a pamięcią operacyjną.
#### Tryby Adresowania:
- **Tryb bazowy:**
  W trybie bazowym adres efektywny jest sumą wartości z rejestru bazowego (BX lub BP) oraz opcjonalnego offsetu. Przykład:
  \[ \text{Adres Efektywny} = BX + OFFSET \quad \text{lub} \quad BP + OFFSET \]
- **Tryb indeksowy:**
  W trybie indeksowym adres efektywny jest sumą wartości z rejestru indeksowego (SI lub DI) oraz opcjonalnego offsetu. Przykład:
  \[ \text{Adres Efektywny} = SI + OFFSET \quad \text{lub} \quad DI + OFFSET \]
- **Tryb bazowo-indeksowy:**
  W trybie bazowo-indeksowym adres efektywny jest sumą wartości z rejestru bazowego (BX lub BP), rejestru indeksowego (SI lub DI) oraz opcjonalnego offsetu. Przykład:
  \[ \text{Adres Efektywny} = BX + SI + OFFSET \quad \text{lub} \quad BP + DI + OFFSET \]
#### Wyjaśnienia i Przykłady Trybów Adresowania:
- **Tryb bazowy:**
  Przykład:
  - Rejestr BX = 0x1234
  - Offset = 0x0020
  - Adres efektywny: \[ \text{Adres Efektywny} = 0x1234 + 0x0020 = 0x1254 \]
- **Tryb indeksowy:**
  Przykład:
  - Rejestr SI = 0x5678
  - Offset = 0x0010
  - Adres efektywny: \[ \text{Adres Efektywny} = 0x5678 + 0x0010 = 0x5688 \]
- **Tryb bazowo-indeksowy:**
  Przykład:
  - Rejestr BX = 0x1234
  - Rejestr SI = 0x5678
  - Offset = 0x0004
  - Adres efektywny: \[ \text{Adres Efektywny} = 0x1234 + 0x5678 + 0x0004 = 0x68B0 \]
#### Instrukcje MOV i XCHG:
- **MOV (Move):**
    - Instrukcja MOV kopiuje wartość z jednego miejsca do drugiego. W przypadku rejestrów, instrukcja ta jest używana do przenoszenia danych między rejestrami oraz między rejestrami a pamięcią operacyjną.
    - Składnia: MOV dokąd, skąd
    - Przykład: MOV AX, BX – kopiuje wartość z rejestru BX do rejestru AX.
    - Przykład: MOV [5000h], AX – kopiuje wartość z rejestru AX do pamięci na adresie 5000h.
- **XCHG (Exchange):**
    - Instrukcja XCHG wymienia wartości dwóch operandów. Dla rejestrów oznacza to zamianę wartości między dwoma rejestrami.
    - Składnia: XCHG dokąd, skąd
    - Przykład: XCHG AX, BX – wymienia wartości między rejestrami AX i BX.
    - **Dodatkowo:** Symulacja rozkazu XCHG dla przesyłania z pamięci operacyjnej do rejestrów AX, BX, CX i DX i z rejestrów do pamięci.
### Architektura Strony:
- Warstwa wizualna oparta jest na HTML + CSS.
- Logika wypełniana funkcjami w JavaScript.
### Jak uruchomić:
- Instrukcje uruchomienia projektu z archiwum:
  - Kliknąć po prostu plik HTML.