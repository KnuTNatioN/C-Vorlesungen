# Dynamische Speicherverwaltung
```C
#include <stdio.h>
```
## Funktionsanforderungen an Speicher
- während der Laufzeit Speicher anfordern und freigeben
- Läuft über den Heap (Ram/Auslagerungsdatei auf Festplatte)

## Speicherarten:
### - Programmspeicher

### - Globaler Speicher
- Speicher wird bei Programmstart angelegt und erst bei Programmende wieder freigegeben.
- Speicherung von globalen und Statischen Variablen

### - Stack
- Wird bei Bedarf erzeugt und freigegeben
- Speicherung von Funktionsargumenten und nichtstatischen lokane Variablen
- Interne Realisierung als Stack(Stapel)
- Gesamtspeicherbereich für Stack wird bei Programmstart reserviert
- Wenn Stack bei Funktionsaufruf voll, dann Programmabbruch (Stack Overflow)

### - Heap
(Groß und unstrukturiert)
- Zugriff nur über Zeiger
- Nicht automatisch verwaltet
- Hier arbeitet _calloc, malloc, realloc, free_

### Wichtige Elemente:
```C
#include <stdlib.h>
size_t s = sizeof(char) = 1
size = in Byte
count = #/* reserviert size * count */
ptr = Pointer auf erstes Element des Speichers

 sizeof /*Rückgabe des Speicherverbrauchs eines elements*/
 void* malloc(size_t size);
 void* calloc(size_t count, size_t size);
 void* realloc(void* ptr, size_t size);
 
 void* free(void* ptr);
 ```

----------

## sizeof()
### Größe von ()

```C
#include <stdlib.h>
**** size;
printf("%zu", sizeof(size));/* gibt größe von size in Byte zurück */
/* "%zu" weil size_t */
```
- mehr ist nicht sicher definiert! (alles andere hängt vom Compiler und Plattform an)
- berücksichtigt Speicherausrichtung? (gibt eventuell mehr zurück, entsprechend dem Prozessor Verwaltung)
- Rückgabe = [unsigned size_t]
- keine Seiteneffekt ausführung (sizeof(p++)) [-> kein ausgeführetes Aufaddieren! nur vereechnet ohne auswirkung!]

----------

## NULL
### Speicherstelle die immer null zurück gibt
```C
if(wert == NULL) {
    /* irgendetwas... */
```
- entspricht 0 und bedeutet "keine gültige Adresse"
- initialwert für Zeiger
- Dereferenzierung NICHT möglich
- benutzt bei Ende von Listen

## void *
### untypisierter Zeiger
- zu allen anderen zeigern kompatibel

----------

## malloc
### "memory" alloc
```C
#include <stdlib.h>
void *malloc(size_t size)
```
- Reserviert Speicher der Größe _size_ in Byte
- Speicher wird NICHT initialisiert
- Rückgabe:
  - Zeiger auf Anfang des Blocks
  - NULL wenn Fehler bei reservierung (z.B. 1GB gewollt, kein 1GB frei) [-> muss geprüft werden!]
### Beispiel:
```C
#include <stdlib.h>
int main() {
    char* buf = malloc(4 * sizeof(char));
    /* gibt einen Pointer auf deinen Speicherbereich mit der (hier)4-fachen größe von Char, zurück */
    if(buf ==NULL) {
        /*error handling*/
        fprintf(stderr, "Fehler: Konnte Speicher nicht reservieren. \n");
        return 1;
    }
    printf("%p\n", buf);
    return 0;
}
```

----------

## calloc
### "cleaned" alloc
```C
#include <stdlib.h>
void *malloc(size_t count, size_t size)
```
- count = Anzahl der Feldelemente
- size = Größe eines Feldelements
- Reserviert Speicher der Größe _size_ * _count_ in Byte
- Speicher wird mit 0 initialisiert
- Rückgabe:
  - Zeiger auf Anfang des Blocks
  - NULL wenn Fehler bei reservierung (z.B. 1GB gewollt, kein 1GB frei) [-> muss geprüft werden!]
### Beispiel:
```C
#include <stdlib.h>
int main() {
    char* buf = calloc(4, sizeof(char));
    /* gibt einen Pointer auf deinen Speicherbereich mit der 4fachen größe von Char, zurück */
    if(buf ==NULL) {
        /*error handling*/
        fprintf(stderr, "Fehler: Konnte Speicher nicht reservieren. \n");
        return 1;
    }
    printf("%p\n", buf);
    return 0;
}
```

----------

## free
### Freigabe von Speicher
```C
#include <stdlib.h>
void free(void *ptr);
```
- Dynamischer Speicher MUSS wieder freigegeben werden [-> memory Leak]
- automatisches Freigeben erst bei __Programmende__
- Undefiniertes Verhalten:
  - ptr noch nicht reserviert
  - ptr wurde bereits freigegeben

### Beispiel
```C
#include <stdlib.h>
int main() {
    char* buf = calloc(4, sizeof(char));
    /* Bereich wurde reserviert/allokiert */
    free(buf);
    /* Bereich wurde wieder freigegeben */
    /* "buf" zeigt aber IMMER noch auf die Stelle*/
    /* [-> buf = NULL;] */
}
```

----------

## realloc
### erlaubt, Größe von Speicher zu ändern
```C
#include <stdlib.h>
void* realloc (void* ptr, size_t size);
```
- Verändert die Größe von _ptr_ auf neue Größe _size_
- Rückgabe:
  - Zeiger auf Anfang des vergrößerten/verkleinerten Feldes
  - NULL wenn Fehler bei reservierung [-> muss geprüft werden!]

### Beispiel "in der Mitte erweitern"
```C
#include <stdlib.h>
int main() {
    char* buf = malloc(4*sizeof(char));
    /*bsp: buf = abcd */
    char* buf = realloc(buf, 5*sizeof(char));
    /*bsp: buf = abcd_ */

    memmove(&buf[insertPosition+1], %buf[insertPosition], sizeof(int) * (n-insertPosition))
    /*bsp: buf = ab_cd*/ /* @insertPosition=2*/
}
```

----------

## Beispiele:

#### Strukturierte Kundenliste
```C
#include <stdlib.h>
typedef struct s_kunde {
    char name[64];
    datum erster_einkauf;
} kunde;
int kundenanzahl;
scanf("%d", &kundenanzahl);

kunde *meine_kundenliste = calloc(kundenanzahl, sizeof(kunde));
if(meine_kundenliste == NULL) {
    fprintf(stderr, "Zu wenig Speicher!\n");
    exit(EXIT_FAILURE);
}
/*...*/
meine_kundenliste[i].erster_einkauf.jahr = 2002;
/*...*/
free(meine_kundenliste);
```


### __Vergrößerung eines Feldes__ _(von Hand)_
### hinten dran hängen
#### Vorgehen:
1. Erzeugen eines neuen größeren Feldes
2. Kopieren der Elemente vom alten uns neue Feld (von Anfang an auffüllen) _for_-schleife oder _memcpy_
3. Speicher freigeben _free_
4. Zeiger vom ersten Feld auf das neue Feld _a=b;_

### in der Mitte erweitern:
Gegeben:    Feld _A_ mit _n_ Elementen

Ziel:       Einfügen von Element _e_ an Index _i_\
A: _[affe, hamster, hund, katze]_ -> A: _[affe, hamster, __maus__, hund, katze]_

#### Vorgehen:
1. Erzeuge mit _calloc_ Feld b mit n+1 Elementen
2. Kopiere die Elemente A: _[affe, hamster, i-1]_ nach B: _[0, ..., i-1]_
3. Kopiere die Elemente A: _[i, ..., n-1]_ nach B: _[i+1, ..., n]_
4. Seite B:_[ i ]_ = e;
5. Speicher für Feld _A_ freigeben
6. Setze Zeiger neu auf Beginn des neuen Feldess _A = B_

```C
#include <stdlib.h>

void printTHEarray(int* array, site_t n) {
    for(size_t i = 0; i < n; i++) {
        if(i > 0) {
            printf(", ");
        }
        printf("%d\n", array[i]);
    }
    printf(" (n=%zu)\n",n);
}

int main() {
    size_t n = 10;
    int* Array = calloc(n, sizeof(int));
    if(array == NULL) {
        fprintf(stderr, "Error: Could not reserve memory.\n");
        return 1;
    }
/* Test Data */
    for(size_t i = 0; i < n; i++) {
        Array[i] = (int)i;
    }
/* VORHER */
    printf("Vorher");
    printTHEarray(Array, n);


/* Ask User what and where: */
    int insertElement;
    size_t insertPosition;

    printf("What to insert: ");
    scanf("%i", &insertElement);

    printf("Where to insert: ");
    scanf("%zu", &insertPosition);

    if(insertPosition > n) {
        fprintf(stderr, "Error: Invalid Position.\n");+
        return 1;
    }

/* Create new larger Array */
    int* newArray = calloc(n+1, sizeof(int));
    if(Array == NULL) {
        fprintf(stderr, "Error: Could not reserve memory.\n");
        return 1;
    }
{Entweder:
/* Copy Data with gap and store newElement in gap*/
    for(size_t i = 0; i < insertPosition; i++) {
        newArray[i] = Array[i]
    }

    for(size_t i = insertPosition; i < n; i++) {
        newArray[i+1] = Array[i]
    }
}
{ODER:
        memcpy(newArray, array, sizeof(int)*insertPosition);
        /* #include <string.h> */
        memcpy(&newArray[insertPosition + 1], &array[insertPosition], sizeof(int)* (n - insertPosition));
}
    newArray[insertPosition] = insertElement;
/* Free old Space */
    free(Array);
    n++;
    Array = newArray;

/* NACHHER */
    printf("Nachher");
    printTHEarray(array, n);
    
    free(array);
    return 0;
}
```
