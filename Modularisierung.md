# Modularisierung

- Funktionen auslagern
- erhöht wartbarkeit
- Wiederverwendbarkeit
- Compilierzeit wird geringer, da nur das geänderte Modul neu kompiliert werden muss

## 1. Programmierebene:
(potentiell Plattform spezifisch)

Hier werden die Programmteile händsch zusammengefügt wobei die name.c und name.h dateien jeweils zusammen gehören.
Funktionen sollten sinnvoll zusammen gefasst werden. **Keine** Artfremden Kreuzungen (z.b. Musik und Quersummenfunktion)

### main.c
```c
#include "ein_modul.h"

funktion_aus_modul();

```

### ein_modul.h
```c
#ifndef EIN_MODUL_H
#define EIN_MODUL_H

funktion_aus_modul(...);

#endif
```
- ```#ifndef``` = präprozessor sagen das dieses Modul nur einmal eingebungen werden muss, falls das Moul schon eingebunden wurde, wird alles bis ```#endif``` übersprungen
- ```funktion_aus_modul(...);``` = Bekanntmachen der Funktion im Modul "Funktionsprototyp" (Semikolon am ende)

### ein_modul.c
```c
#include "ein_modul.h"

funktion_aus_modul() {
    //Funktionscode
}
```
- ```#include "ein_modul.h"``` = einbinden der eigenen Bibliotheksdatei


## 2. Compilerebene:
(Plattformspezifisch)

aus dem Beispiel:
**ein_modul.c** und **ein_modul.h** wird eine Objekdatei ein_modul.o generiert
Aus **main.o** generiert der Compiler auch eine eigene Objektdatei **main.o**

## 3. Linkerebene:
(Plattformspezifisch)

Aus den Objektdateien **main.o** und **ein_modul.o** wird ein Programm generiert (zusammengefügt)