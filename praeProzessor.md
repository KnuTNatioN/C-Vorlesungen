# Präprozessor

ist vor dem Compiler geschaltet
einbinden externer Dateien (+include)
ersetzungen (#define)
bedingte Compilierung (#ifdef)

beginnt immer mit #
geht je anweisung bis ende einer Zeile
mit backslash wird die Zeile erweitert \

### #include
```
#include <datei> sucht im Compiler default verzeichnis
#include "datei" sucht im aktuellen Verzeichnis
```

## Makros
#define name [ (Parameterliste) ] [wert]

Makros mit und ohne Parameter und mit oder ohne Ersetzungstext möglich

## Beispiel:

Vor Präprozessor:
```C
#define PI 3.141592
#define OR ||

if ((x < 10) OR (y < 10)) {
    z = PI;
}
```
Nach Präprozessor:
```C

//M_PI aus der math.h ist genauer/besser

if ((x < 10) || (y < 10)) {
    z = 3.141592;
}
```
