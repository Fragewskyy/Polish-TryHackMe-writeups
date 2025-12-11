# Source
## Zadanie

Enumerate and root the box attached to this task. Can you discover the source of the disruption and leverage it to take control?

## Kroki

Standardowo zaczynamy od nmapa.

![alt text](image.png)

Jak zazwyczaj SSH jest otwarte oraz mamy dodatkowo WebMin operujący na porcie 10000.

Użyjmy metasploitable aby znaleźć podatności dla tej aplikacji.

![alt text](image-5.png)

Wykorzystamy podatność z indeksem 11.

![alt text](image-2.png)

Ustawiamy parametry i używamy `exploit`.

![alt text](image-3.png)

Okazuje się że jesteśmy rootem więc od razu zgarniamy obie flagi ;)

![alt text](image-4.png)

![alt text](image-6.png)

## Flaga

User: **THM{SUPPLY_CHAIN_COMPROMISE}**
Root: **THM{UPDATE_YOUR_INSTALL}**