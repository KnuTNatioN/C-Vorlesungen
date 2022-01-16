# Compiler und Linker

## Compiler

### Symboltabelle
- Speichert alle verwendeten Symbole (Funktionsnamen, Variablennamen... und sorgt für die korrekte Zuordnung)

### Arbeitsschritte eines Compilers:
0. -> Quellprogramm

1. Lexikalische Analyse
   - Zerlegung in Folge von Symbolen (Namen, Literale, Schlüsselwörter...)
   - Überlesen bedeutungsloser Zeichen
   - Lexikalische Korrektheit
   - zB.: *(Variablen Name beginnt mit Zahl)*

2. Syntaktische Analyse
    - Prüfung auf syntaktische Korrektheit
    - Zerlegung der Symbolfolge des 1. Schritts in syntaktische Einheiten (Deklaration, Anweisungen, Ausdrücke...)
    - zB.: (Anweisungsende mit Semikolen ***C*** )
    - 
3. Semantische Analyse
   - Kontextabhängige Prüfung (sind aufgerufene Funktionen deklariert, Variablen deklariert ext.)

4. Zwischencodeerzeugung
   - Erzeugung der ersten Version des Ausgabeprogramms

5. Codeoptimierung (optional)
   - Der Maschinencode kann nach verschiedenen Kriterien optimiert werden (Laufzeit, Speicherbedarf...)

6. -> Objektdatei


### Compilertypen
- Prä- Compiler (textersetzung und einbindung von Header Dateien)
- Cross-compiler: Wird für andere Plattformen compiliert
  - zB.: (von PC auf Chip)
- Just-in-Time: Programm wird erst wärend der Ausführung des Programms übersetzt
  - zB.: (Integriert in einen Interpreter)
- Nachgeschalteter Assembler: Ist die Ausgabe des Compilers Assembler und nicht Maschinensprache, so muss ein Assemblierer nachgeschaltet werden
- Transpiler (source to source Compiler): Programm wird in andere Programmiersprache übersetzt (TypeScipt nach JavaScript)


## Linker

- Große Programme werden in Module aufgeteilt
  - möglicherweise verschiedene Personen bearbeiter werden
  - Eventuell unterschiedliche Programmiersprachen
- Jedes Modul wird mit einem Compiler in die Maschinensprache übersetzt, aber noch nicht als ausführbare Datei, sondern als Objektdatei.
- Die unterschiedlichen Objektdateiern werden dem Linker zu einer Datei zusammengefügt
- Dabei ist es zB. auch möglich, dass ein Modul, Funktionen eines anderen nutzt

## C-Programm
besteht zB. aus:
```
-> Compiler
=> Linker
main.c      -> main.o
point.c     -> point.o
geometry.c  -> geometry.o
line.c      -> line.o
*.o         => editor.exe
```