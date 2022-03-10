# Komandozeilenparameter

## Aufruf in Konsole:
```/home/user/programm.exe Para1 Para2 Para3 "Parameter wert"```

## Erklärung
Alle Parameter werden (bei Unix Systemen) mit Leerzeichen getrennt und als Strings übergeben.
Parameter inklusiver Leerzeichen müssen "escaped" werden.
- Manchmal möglich mit: ```parameter\ wert``` (durch das Backslash wird das Leerzeichen escaped und als Leerzeichen dem String angerechnet.)
- Sehr oft möglich mit: ```"Parameter wert"``` oder ```'Parameter wert'``` (Gänsefüsschen oder Ticks) Dadurch wird der String inklusive Leerzeichen gekapselt.

Partameter werden auch als Argumente bezeichnet.

## Beispiel
```c
//Doppelpointer!! (Array aus Pointern auf Zeichenketten)
int main(int argc, char *argv[])
int main(int argc, char **argv)
```

```argc``` Anzahl der Argumente (immer größer gleich 1)

```argv``` Zeiger auf Array von Zeigern auf Zeichenketten.
- ```argv[0]``` ist der Programmaufruf (im Beispiel ```/home/user/programm.exe```)
- ```argv[1]``` erstes Argument (im Beispiel ```Para1```)
- ```argv[2]``` zweiters Argument (im Beispiel ```Para2```)
- usw...
- ```argv[argc-1]``` letztes Argument (```"Parameter wert"```)


## passende Funktionen

```c
#include <stdlib.h>
a = atoi(argv[1]);
```
```atoi``` = array to Integer
```atof``` = array to float
