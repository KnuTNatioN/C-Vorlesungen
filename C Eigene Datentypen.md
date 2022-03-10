# Eigene Datentypen
```C
#include <stdio.h>
```
Komplexe Variablen bestehend aus einfachen Datentypen
Ziel: Bessere Lesbarkeit

## enum:
### Aufzählungszyp
```C
enum tier {hund, katze, maus} t;
t=hund;
```

```C
enum farbe {rot=55, blau};
enum farbe f;
f = blau;
```

## struct
### typedef
mit struct erstellt man eine neue Struktur
mit einem typedef davor bekommt die Struktur auch einen greifbaren namen
```C
typedef struct dude {
    char name[64];
    unsigned int alter;
    karre erster_einkauf;
} dude;

    dude varKnut; //neuer Kunde der ansprechbar über den Namen varKnut ist
    varKnut.alter = 31;    //zugriff auf knut alter und beschreibt in alter die Zahl 31

    varKnut.name; //(geht leider nicht!)
    strcpy(varKnut.name, "KnuT"); //kopiert den String "KnuT" an die Speicheradresse auf die varKnut.name zeigt (max 64 bytes).
    //karre bleibt leer, da dieser Datentyp auch irgendwie aufgebaut ein kann.

    dude varBob = { .name = "Robert ", .alter = 50 , .karre = "Ford-Rostlaube"};

    dude *zeigerBob = &varBob; //Zeiger auf Bob erstellt
    (*zeigerBob).alter = 20
```
Baut einen neuen Variablen typ mit dem Namen dude.
hier:   Name hat 64 Byte (63 Buchstaben und 1 end null)
        alter ist teil von dude 
        karre ist wiederum ein eigener Typ.


## union

mit Unions hat man zugriff auf einzelne bit. es werden entsprechend des Prozessors
```C
typedef union{
    float value;
    struct {
  /*+ 23Bit*/  unsigned int mantissaBit:23;   /* rest der 32bit ist mantisse 8Bit*/
  /*   8Bit*/  unsigned int biasedExponent:8; /* 255 zustaende 8Bit*/
  /*+  1Bit*/  unsigned int sign:1;           /* Vorzeichen 1Bit (1=negativ | 0=positiv*/
  /*= 32Bit*/ };
} max4B;



```
----------