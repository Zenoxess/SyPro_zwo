Assembly "Hallo Welt" für Windows x64
Dieses Repository enthält ein kleines "Hallo Welt"-Programm, geschrieben in 64-Bit Assembly (NASM) für Windows. Es ist so konfiguriert, dass es direkt aus Visual Studio Code heraus kompiliert und ausgeführt werden kann, ohne dass zusätzliche Abhängigkeiten wie Visual Studio oder MSVC++ Build Tools erforderlich sind.

🚀 Erste Schritte: Vom ZIP zum lauffähigen Code
Diese Anleitung hilft dir, das Projekt schnell und einfach zum Laufen zu bringen.

1. Voraussetzungen
Stelle sicher, dass du Visual Studio Code installiert hast. Alle notwendigen Build-Tools (NASM-Compiler und GoLink-Linker) sind bereits in diesem Repository enthalten. 

2. Projekt öffnen
Klone dieses Repository oder lade es als ZIP-Datei herunter und entpacke es.

Öffne Visual Studio Code.

Gehe zu Datei > Ordner öffnen... und wähle den nasm-nonvc-Ordner aus. 

3. Kompilieren und Ausführen
Das Projekt ist mit einem vordefinierten VS Code Task ausgestattet, der den gesamten Build-Prozess automatisiert.

Öffne die Datei hello64.asm, um den Quellcode anzuzeigen. 

Drücke die Tastenkombination Strg + Umschalt + B, um den Build-Task zu starten. 

Im Terminalfenster siehst du, wie das make.bat-Skript ausgeführt wird.  Dieses Skript führt die folgenden zwei Schritte aus:


Kompilieren: Der NASM-Compiler übersetzt den Assembly-Code in eine Objektdatei (.obj). 

Shell

nasm -f win64 -Ox hello64.asm

Linken: Der GoLinker verbindet die Objektdatei mit den notwendigen Windows-Bibliotheken (kernel32.dll, user32.dll), um eine ausführbare Datei (.exe) zu erstellen. 

Shell

golink.exe /entry:Start kernel32.dll user32.dll hello64.obj
Nach erfolgreichem Build findest du die fertige hello64.exe im Projektverzeichnis.  Du kannst sie direkt per Doppelklick oder im VS Code-Terminal ausführen:

Shell

./hello64.exe
Das Programm zeigt eine einfache Windows-Messagebox an. 

📁 Projektstruktur

hello64.asm: Die Hauptdatei mit dem 64-Bit-Assembly-Code. 


make.bat: Ein einfaches Batch-Skript, das die Build-Befehle ausführt. 


.vscode/tasks.json: Die Konfigurationsdatei für den VS Code Build-Task. 


nasm.exe / golink.exe: Die portablen Build-Tools, die das Projekt autark machen.
