.

🚀 Erste Schritte: Vom ZIP zum lauffähigen Code
Hey! Damit du das Projekt bei dir zum Laufen bekommst, folge einfach diesen Schritten. Der Hauptunterschied zwischen dem Ordner, den du bekommen hast, und einem frisch geklonten GitHub-Repo ist, dass bei dir wahrscheinlich schon kompilierte Dateien (.obj, .exe) dabei sind. Die ignorieren wir aber erstmal und bauen alles neu.

1. Vorbereitung
Stell sicher, dass du Visual Studio Code installiert hast. Du brauchst keine zusätzlichen C++-Compiler oder riesige Visual Studio-Installationen, da alle notwendigen Tools (NASM-Compiler und GoLink-Linker) direkt in diesem Ordner enthalten sind.

2. Projekt in VS Code öffnen
Entpacke die ZIP-Datei, die du bekommen hast, in einen Ordner deiner Wahl.

Öffne Visual Studio Code und gehe zu Datei > Ordner öffnen.... Wähle den nasm-nonvc Ordner aus.

3. Code kompilieren und ausführen
Ich habe bereits alles so vorbereitet, dass du den Code mit einem einzigen Befehl bauen kannst.

Öffne die Datei hello64.asm, um den Code zu sehen.

Drücke die Tastenkombination Strg + Umschalt + B.

Daraufhin wird ein sogenannter "Task" ausgeführt. Im Terminalfenster unten siehst du, wie die make.bat-Datei aufgerufen wird.

Dieser Task macht zwei Dinge, wie in der make.bat definiert:

Kompilieren: nasm -f win64 -Ox hello64.asm – Der NASM-Compiler übersetzt deinen Assembly-Code (hello64.asm) in eine Objektdatei (hello64.obj).

Linken: golink.exe /entry:Start kernel32.dll user32.dll hello64.obj – Der GoLinker verbindet deine Objektdatei mit den notwendigen Windows-Bibliotheken (kernel32.dll und user32.dll), um eine ausführbare Datei (hello64.exe) zu erstellen.

Nachdem der Task durchgelaufen ist, findest du im Ordner eine neue hello64.exe. Du kannst sie direkt aus dem Explorer oder über das Terminal in VS Code (./hello64.exe) starten. Sie zeigt eine einfache Windows-Messagebox an.

📁 Wichtige Dateien im Projekt
hello64.asm: Das ist die Hauptdatei mit unserem 64-Bit Assembly-Code. Sie definiert, was das Programm tut – in diesem Fall eine simple Messagebox anzeigen.

make.bat: Ein einfaches Skript, das die Befehle zum Kompilieren und Linken enthält. So müssen wir das nicht jedes Mal von Hand ins Terminal tippen.

.vscode/tasks.json: Diese Datei konfiguriert Visual Studio Code so, dass es weiß, was zu tun ist, wenn du Strg + Umschalt + B drückst. Es sagt VS Code im Grunde nur: "Führe die make.bat aus".

nasm.exe und golink.exe: Das sind die eigentlichen Werkzeuge (Compiler und Linker), die wir brauchen. Sie sind direkt im Projektordner, damit du nichts extra installieren musst.

Viel Spaß beim Ausprobieren! Wenn etwas nicht klappt, sag einfach Bescheid.
