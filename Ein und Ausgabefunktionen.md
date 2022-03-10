# Ein und Ausgabefunktionen

## Funktionen allgemein
- Wiederverwendbarer Code
- einfachere Wartung
- kürzerer Code
- 

### Benutzen von Funktionen 
- Aufruf über Namen (Bezeichner) der Funktion
- Funktionen können Parameter besitzen. Diese müssen beim Aufruf in Klammern angegeben werden:
    ```
    printf("hello world\n");
    ```
- Funktionen können Rückgabewerte besitzen:
    ```C
    double x, y = 3;
    x = sin(2);
    cos(y);
    ```
- Man kann die Rückgabewerte ignorieren


## stdio.h
- In der Datei stdio.h sind Ein und Ausgabefunktionen deffiniert
- Einbinden mit `` #include <stdio.h>``
- Operationen für Bildschirm- Ein- und Ausgabe, wie auch Dateioperationen
- Gehört zu den mitgelieferten Standardbibliotheken.


## putchar() und getchar()
- `` putchar `` Schreibt ein Bildschirm
- `` getchar `` ließt ein Zeichen von Tastatur
```C
int main()
{
    char ch;
    ch = getchar();
    putchar('X');
    return 0;
}
```

## printf()
- formatierte Ausgabe
- Rückgabewert: Anzahl der tatsächlich ausgegebenen Zeichen
- ``` int printf( formatstring [,parameter])```

```C
    #include <stdio.h>
    int alter;
    alter = 15;
    printf("Hand ist %d Jahre alt.\n", alter);
```

- Formatstring besteht aus Ausgabetext und/oder Formatanweisung
- Text wird unverändert ausgegeben
- Formatanweisungen bestehen aus Prozentzeichen ``%`` und Zeichen, die den Datentyp angeben.
- Die Formatierung wird durch den nächsten, noch nicht bearbeiteten Parameter von ``printf`` ersetzt.

```C
    #include <stdio.h>
    int a, b, c;
    a = 5;
    b = 7;
    c = a + b;
    printf("%d + %d = %d \n", a, b, c);
```

Formatanweisung | Erklärung
-----------     | -----------
%d, %i          | int (auch short, iunt und char); dezimal mit Vorzeichen
%u              | int, dezimal ohne Vorzeichen
%o              | int; oktal ohne Vorzeichen
%x, %X          | int; hexadezimal mit kleinen bzw. Großen Buchstaben
%c              | char; Zeichen (ein Buchstabe / eine Ziffer, ...)
%s              | char*; Zeichenkette bis Zeichen `\0` gelesen wird
%f, %e, %g      | Fließkommaschreibweise (e/E = Exponentenschreibweise klein/groß) float/double
%lf, %le, %lg   | Fließkommaschreibweise (e/E = Exponentenschreibweise klein/groß) float/double
%Lf, %Le, %Lg   | Fließkommaschreibweise (e/E = Exponentenschreibweise klein/groß) float/double

### Erweiterte Formatanweisung
- ermöglicht z.B.: numerische Werte, Spaltenweise auszugeben oder die Anzahl der Dezimalstellen zu begrenzen.
- Syntax:
    ``` %[flags][width][.perci]type ```
  - flags:
    - -: linksbündige Ausgabe
    - +: Vorzeichenausgabe auch bei positiven Zahlen
    - #: Alternative Darstellung (siehe man-page)
    - 0: Auffüllen mit Nummen für Breite
    - Leerzeichen: Leerzeichen vor positiver Zahl
  - width: maximage Breite der ausgeschriebenen variable inklusive auffüllung
    - wenn Ausgabe größer: Breitenangabe wird ignoriert
    - wenn Ausgabe kleiner: linksbündig werden Leerzeichen eingefügt
  - .perci: Anzahl der auszugebenen Dezimalstellen bei Fließkommazahlen
  - l: long-Version des Datentyps
  - type ist eine einfache Formatanweisung
    ```C
    printf("% 8d\n, 12343); /* ->   12343*/
    printf("% 8d\n, 225);   /* ->     225*/
    // % leerzeichen auffüllen;
    ´´´

## scanf()
- Dient formatierte Eingabe von Variablen
- Rückgabewert: Anzahl der eingelesenen Eingaben (evtl. Fehlerkorrektur)
- ``` int scanf( formatstring [,parameter])```
- Formatanweisung bestehen aus ``%`` Prozentzeichen und Zeichen, das den Datentyp der Eingabe angibt
- Whitespaces passen zu einem Leerraum jeder Größe
- Andere Zeichen passen nur zu sich selbst
```C
    int x;
    scanf("%d", &x);
    /*Das & Symbol sagt, übergebe die Speicheradresse, nicht den Inhalt des Speichers.*/
```
- Eingaben werden an die als Parameter übergebenen Adressen geschrieben, dh. vor den Variablennamen muss das Zeichen & geschrieben werden

Formatanweisung | Erklärung
-----------     | -----------
%d, %i          | int (auch short, iunt und char); dezimal mit Vorzeichen
%u              | int, dezimal ohne Vorzeichen
%o              | int; oktal ohne Vorzeichen
%x, %X          | int; hexadezimal mit kleinen bzw. Großen Buchstaben
%zu             | size_t (riesige INT)
%c              | char; Zeichen (ein Buchstabe / eine Ziffer, ...)
%s              | char*; Zeichenkette bis Zeichen `\0` gelesen wird
%f, %e, %g      | Fließkommaschreibweise (e/E = Exponentenschreibweise klein/groß) float/double
%lf, %le, %lg   | Fließkommaschreibweise (e/E = Exponentenschreibweise klein/groß) float/double
%Lf, %Le, %Lg   | Fließkommaschreibweise (e/E = Exponentenschreibweise klein/groß) float/double

- Syntax:
    `` %[*][width][lh]type
  - *: die Eingabe wird nur gelesen, aber keiner Variable zugewiesen
  - width: maximale Anzahl zu lesender Zeichen
    - l: long-Variable
    - h: short-Variable
  - type ist eine einfache Formatanweisung
    ```C
    int x, y;
    printf("Addition? ");
    scanf("%d plus %d ist", &x &y);
    printf("%d\n", x+y);
    ´´´