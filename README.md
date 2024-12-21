### Projekt Symulatora Instrukcji Procesora 8086 w HTML i JavaScript

#### Cel Projektu:

Celem projektu jest stworzenie aplikacji w HTML i JavaScript, która symuluje działanie dwóch instrukcji procesora 8086: MOV oraz XCHG, dla rejestrów AX, BX, CX, DX. Użytkownik będzie mógł wprowadzać wartości w postaci szesnastkowej (HEX) do tych rejestrów i obserwować działanie wspomnianych instrukcji. Dodatkowo aplikacja umożliwi symulację instrukcji PUSH i POP oraz obsługę trzech trybów adresowania: bazowego, indeksowego, indeksowo-bazowego.

#### Wymagania Funkcjonalne:

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
  - **Dodatkowo:** Symulacja rozkazu XCHG dla przesyłania z pamięci operacyjnej do rejestrów AX, BX, CX i DX oraz z rejestrów do pamięci.

- **Instrukcja PUSH i POP:**

  - **Dodatkowo:** Symulacja rozkazów PUSH i POP w odniesieniu do rejestrów AX, BX, CX i DX.

#### Podłoże teoretyczne symulacji instrukcji MOV, XCHG, PUSH i POP Procesora 8086:

**Wstęp:**
Procesor 8086 jest 16-bitowym mikroprocesorem stworzonym przez firmę Intel wprowadzonym na rynek w 1978 roku. Jest znany z tego, że stanowił podstawę rozwoju rodziny procesorów x86, która stała się standardem w komputerach osobistych. Projektowany był głównie do obsługi języka asemblera i niskopoziomowych operacji wykonywanych bezpośrednio na rejestrach procesora.

**Rejestry Procesora 8086:**
Procesor 8086 posiada zestaw rejestrów, które można podzielić na kilka kategorii: dane, wskaźniki i indeksy oraz segmenty. W kontekście naszego projektu interesują nas jednak nie tylko rejestry danych, ale również pamięć operacyjna.

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

  - Rejestr BX = 0x1234
  - Offset = 0x0020
  - Adres efektywny: 0x1234 + 0x0020 = 0x1254

- **Tryb indeksowy:**
  W trybie indeksowym adres efektywny jest sumą wartości z rejestru indeksowego (SI lub DI) oraz opcjonalnego offsetu. Przykład:

  - Rejestr SI = 0x5678
  - Offset = 0x0010
  - Adres efektywny: 0x5678 + 0x0010 = 0x5688

- **Tryb bazowo-indeksowy:**
  W trybie bazowo-indeksowym adres efektywny jest sumą wartości z rejestru bazowego (BX lub BP), rejestru indeksowego (SI lub DI) oraz opcjonalnego offsetu. Przykład:

  - Rejestr BX = 0x1234
  - Rejestr SI = 0x5678
  - Offset = 0x0004
  - Adres efektywny: 0x1234 + 0x5678 + 0x0004 = 0x68B0

#### Instrukcje MOV, XCHG, PUSH i POP:

- **MOV (Move):**

  - Instrukcja MOV kopiuje wartość z jednego miejsca do drugiego. W przypadku rejestrów, instrukcja ta jest używana do przenoszenia danych między rejestrami oraz między rejestrami a pamięcią operacyjną.
  - Składnia: MOV dokąd, skąd
  - Przykład: MOV AX, BX – kopiuje wartość z rejestru BX do rejestru AX.
  - Przykład: MOV [5000h], AX – kopiuje wartość z rejestru AX do pamięci na adresie 5000h.

- **XCHG (Exchange):**

  - Instrukcja XCHG wymienia wartości dwóch operandów. Dla rejestrów oznacza to zamianę wartości między dwoma rejestrami.
  - Składnia: XCHG dokąd, skąd
  - Przykład: XCHG AX, BX – wymienia wartości między rejestrami AX i BX.
  - **Dodatkowo:** Symulacja rozkazu XCHG dla przesyłania z pamięci operacyjnej do rejestrów AX, BX, CX i DX oraz z rejestrów do pamięci.

- **PUSH i POP:**

  Instrukcje PUSH i POP służą do zarządzania danymi na stosie, który jest strukturą danych typu LIFO (Last In, First Out). W procesorze 8086 stos znajduje się w pamięci operacyjnej, a jego górę wskazuje rejestr SP (Stack Pointer).

  - **PUSH:** Instrukcja ta zapisuje wartość rejestru na stosie. Wartość rejestru SP (Stack Pointer) zostaje najpierw zmniejszona o 2 (ponieważ 8086 operuje na słowach 16-bitowych), a następnie wartość rejestru jest kopiowana na adres wskazywany przez SP.
    - Przykład: PUSH AX – zmniejsza SP o 2 i zapisuje wartość rejestru AX na stosie.
  
  - **POP:** Instrukcja ta pobiera wartość ze stosu do rejestru. Najpierw odczytywana jest wartość z adresu wskazywanego przez SP, a następnie SP jest zwiększany o 2.
    - Przykład: POP AX – odczytuje wartość z adresu wskazywanego przez SP do rejestru AX i zwiększa SP o 2.

  - **Działanie stosu:** Stos w procesorze 8086 działa w pamięci segmentowej. Segment stosu jest określany przez rejestr SS (Stack Segment), a rejestr SP przechowuje offset w segmencie. Gdy dane są umieszczane na stosie (PUSH), wskaźnik SP przesuwa się w dół pamięci (do niższych adresów), a gdy dane są pobierane (POP), przesuwa się w górę (do wyższych adresów).

  - Dodatkowo: Symulacja rozkazów PUSH i POP w odniesieniu do rejestrów AX, BX, CX i DX.

#### Architektura Strony:

- Warstwa wizualna oparta jest na HTML + CSS.
- Logika wypełniana funkcjami w JavaScript.

#### Jak uruchomić:

- Instrukcje uruchomienia projektu z archiwum:
  - Rozpakować dane z archiwum, po czym uruchomić plik html (kliknąć 2 krotnie, powinno uruchomić w domyślnej przeglądarce)

