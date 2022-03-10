# Datei operationen:

##
1. Öffnen bzw. erzeugen einer Datei
2. Lese- Schreibzugriffe
3. Schließen der Datei


### Öffnen
```C
include <stdio.h>

FILE* fopen(filename, mode[ext]);

```
filename: Dateiname (inkl. Pfad)

mode: Bearbeitungsmodus

- "r"   Öffnen zum Lesen
- "w"   Öffnen zum schreiben (löscht bestehende Datei mit gleichem Namen)
- "a"   Öffnen zum Schreiben (anhänghen, wenn Datei bereits vorhanden)
- "r+"  Öffnen bestehender Datei zum Verändern (lesen und schreiben)
- "w+"  Erzeugen neuer Datei zum Verändern (lesen und schreiben, löscht vorhandene gleichnamige Datei)
- "a+"  Öffnen einer Datei zum Ändern am Ende

[ext] = b   Datei im Binärmodus bzw Byte Modus geöffnet
- zb.:    Bild, Sound

[ext] = t   Datei im Textdatei Modus (systemabhängige Konvertierungen)
- zb.:    JSON oder anders menschen lesbare Dateien

Rückgabewerte:
    NULL bei Fehler
    Zeiger FILE* (Pointer)


### Schreiben und Lesen

```int putc(int c, FILE f*)```

```int getc(FILE f*)```

```int fprintf(FILE *f, const char *format, ....)```
- Kanäle, formatierter String mit %d Variablen, Variable für %d

inf fscanf(FILE *f, const char *format, ....)
- Eingabefunktion liefert bei Dateiende EOF



### Schließen einer Datei

```int fclose (FILE f*)```
- Puffer wird zuende gespeichert
- Danach kein Zugriff mehr


### Kanäle (stdin, stdout, stderr, FILE)
kein wirklicher Unterschied zwischen Bildschirm und Dateiein-/ausgabe
- stdin:    Standardeingabekanal
- stdout:   Standardausgabekanal
- stderr:   Standardfehlerkanal

Fehler sollten mit fprintf gemeldet werden
- fprintf(stderr, Fehlermeldung);


### Weitere Funktionen:

``` int puts(char *s);```
- schreibt die Zeichenkette s und einen Nachfolgenden Zeilenumbruch auf den Bildschirm
- Rückgabewert: EOF bei Ehler, nichtnegativ sonst

``` int fputs(char *s, FILE *stream);```
- schreibt die Zeichenkette s ohne das Abschlusszeichen '\0' in eine Datei
- Rückgabewert: EOF bei Ehler, nichtnegativ sonst

``` int fgets(char *s, int size, FILE *stream);```
- liest bis zum Zeilenende/-wechsel  oder EOF, maximal aber size-1 Zeichen, aus einer Datei, speichert sie in eiune Zeichenkette und hängt \0 an
  - \n wird nicht ersetzt
