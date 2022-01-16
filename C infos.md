## Allgemein:
Pseudocode sieht fast aus wie echter Code, aber dient nur der verständnis.

## C:
Semicolon kommt immer am Ende einer __Anweisung__


## Zeichensatz der Sprache **C**:
Erstmal eine reine TextDatei.
- Alphanumerische Zeichen: *a, A, b, B,..., 1,2,3...*
- Zeichen zur Strukturierung: *{} () ;*
- Leer- und Trennzeichen: Leerzeichen, Tabulatoren, Zeilenwechsel
  - **Tabulatoren vermeiden**


- **Kommentare** sind Erläuterungen zum Code und helfen dem Verständnis
  - einzeilig mit **//**
  - mehrzeilig, eingeschlossen **/**  *kommentar*  **/**
    - dürfen nicht verschachtelt werden


- **Literale** sind feste Werte die im Programm verwendet werden:
  - Ganzzahlen zb.: 123
  - Kommazahlen mit Dezimalpunkt zb.:  14.3 (Amerikanische Notation Dezimalpunkt, nicht komma)
  - Einzelnes Zeichen eingeschlossen in '' Ticks zb.: 'A'
  - Zeichenketten / Strings/Texte, eingesclossen in "" zB.: "Hallo"


- **Operatoren**
  - [] () . -> ? : , sizeof ++ -- & * + - / % ~ ! << >> <> <= => == != ^ | && || *= /= += -= <<= >>= &= ^= |= = (Trennung mit leerzeichen)
  - Präprozessoranweisungen / Makros: eingeleitet mit #
  - (zb. #include ist eine Präprozessoranweisung und fügt dem Code eine Bibliothek hinzu)


- **Schlüsselwörter** haben spezielle Bedeutung in der Sprache C
  - auto, break, case, char, const, contunie, default, do
  - double, else, enum, extern, float, for, goto, if
  - int, long, register, return, short, signed, sizeof, static
  - struxct, switch, typedef, union, unsigned, void, volatile, while


- **Bezeichner** sind Namen zur eindeutigen Identifikation von Objekten
  - Regeln:
  1. Bezeichner bestehen aus Buchstaben (a-z, A-Z), Ziffern und dem Zeichen_, wobei das erste Zeichen keine Ziffer sein darf.
  2. Sie dürfen beliebig lang sein (intern mindestens 31 Zeichen Signifikant).
  3. Case Sensitiv (A != a)
  4. Unicode-  Zeichen (Ü, ß, á) vermeiden!
  5. Schlüsselwörter nicht als Bezeichner verwenden.

---

## Variablen und Datentypen
- Variable ist ein Logischer Speicherplatz, uzm Werte, Zwischenergebnisse, Benutzereingaben, ect zu speichern
  - Hält dinge fest,. mit denen man Arbeiten will

- C ist **Streng** Typisiert -> jede Variable muss von einem bestimmten Datentyp sein und behält diesen, solange sie existiert.
- Variablen müssen zu allererste deklariert werden.
  - Name [=Bezeichner] und Datentyp muss *festgelegt* werden, bevor wir mit der Variable arbeiten können.

### Datentypen:
**Elementar**
char    ein  Byte oder Zeichen          'A'     65
int     ganze Zahl                      1234    -1234
float   einfach genaue Gleitpunktzahl   3.45f
double  doppelt genaue Gleitpunktzahl   3.45

**Varianten**
short (int)         geringerer Speicherbedarf / Wertebereich
long (int)          höherer Speicherbedarf / Wertebereich
signed / unsigned  Variable mit/ohne Vorzeichen (für char, int, short)
long double         besonders genaue Gleitpunktvariable

in der Regel sind erstmal ALLE Variablen signed (also Negativ und Positiv)

### Literale
- Dezimal
  - 1234 ist vom Typ *int*
  - 1234l und 1234L sind vom Typ *long int*
  - 1234u und 1234U sind vom Typ *unsigned int*
  - 1234ul und 1234UL sind vom Typ *unsigned long int*
  - 123456789 ist vom Typ *long int*
- mit Dezimalpunkt:
  - 1.234 ist double
  - 1.234f und 1.234F sind float
  - 1.234l und 1.234L sind long double
- mit Exponenten:
  - das e steht für *10 hoch*
  - 1234e-3 ist double und bedeutet 1234*10^-3, also 1.234 (1,234)
  - 1.234e2f ist float und bedeutet 1.2324*10^2, entspricht 123.4 (123,4)
- Einzelne Zeichen in einfachen Anführungszeichen
  - zB.: 'a'
  - Entspricht numerischen Wert des Zeichend im Zeichensatz der Maschine
  - '7' != 7  (i.d.R. ACSII)
- Zeichenletten in doppelten Anführungszeichen
  - zB.: "Hello World"
- Sonderzeichen: (Steuerzeichen)
  - \a    Klingelzeichen
  - \b    Backspace
  - \d    Seitenvorschub
  - \n    Zeilenumbruch
  - \r    Wagenrücklauf
  - \v    vertikaler Tabulator
  - \\    Gegenschrägstrich
  - \?    Fragezeichen
  - \'    Anführungszeichen
  - \"    Doppeltes Anführungszeichen
  - \ooo  Zeichen mit oktalem Wert
  - \xxhh Zeichen mit hexadezimalem Wert

- Zuweisung
  > int wert, n = 1;
- Grundrechenarten +,-,*,/
  > wert = + 1;
- Punkt vor Strichrechnung Klammern sind möglich!
  > wert = 5* (n + 3) - 4;
- Modulo *Rest von Ganzzahldoivision):* **%**
  > a= 18;
  >
  > b=7;
  >
  > c= a % b; //4


## Konstanten
- Schlüsselwort *const* vor Variablendeklaration
  - erzeigt eine Variable die **NICHT GEÄNDERT* werden kann
> const double PI = 3.14159265;
> 
> ...
> 
> printf(PI = %g\n", PI);

- Makro-Substitution mit *#define*
  - Ersetzung des definierten Konstantennamens dirch den festgelegten Wert während der Übersetzung
> define PI = 3.14159265;
> 
> ...
> 
> printf(PI = %g\n", PI);


---
## Zeiger:
- Der Speicher ist (bei von Neumann) eine unendliche zeile an Speicherstellen.

- Eine Speicherstelle ist ein byte und kann 256 verschiedene zustände halten.

- Zeiger zeigt immer auf eine Speicherstelle.

- Beispielsweise belegt eine Variable des typs character 2 Speicherstellen.

- Der Zeiger zeigt dann auf die erste der beiden Adressen.

- Bei 4byte würde der Zeiger ebenfalls auf die erste Adresse zeigen.