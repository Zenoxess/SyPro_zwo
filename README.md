# x64 Assembly "Hallo Welt" für Windows (mit NASM & GoLink)

Dieses Repository enthält ein "Hallo Welt"-Programm in 64-Bit Assembly (NASM), das speziell für Windows entwickelt wurde.  
Das Besondere an diesem Projekt ist, dass es **ohne externe Abhängigkeiten** wie Visual Studio oder die MSVC++ Build Tools auskommt.  
Alles, was du brauchst, ist [Visual Studio Code](https://code.visualstudio.com/).

---

## ✨ Besonderheiten

* **Keine externen Abhängigkeiten**: Kein Visual Studio, keine MSVC++ Build Tools. Einfach herunterladen und loslegen.  
* **Portable Build-Tools**: Der NASM-Compiler und der GoLink-Linker sind direkt im Repository enthalten.  
* **Einfacher Build-Prozess**: Ein vordefinierter VS Code Task automatisiert das Kompilieren und Linken.  
* **Ideal für Einsteiger**: Perfekt, um die Grundlagen von 64-Bit-Assembly unter Windows zu lernen, ohne sich mit komplexen Setups herumschlagen zu müssen.  

---

## 🚀 Erste Schritte: Vom ZIP zur lauffähigen .exe

Folge dieser Anleitung, um das Projekt in wenigen Minuten zum Laufen zu bringen.

### 1. Voraussetzungen

Stelle sicher, dass du [Visual Studio Code](https://code.visualstudio.com/) installiert hast.  
Mehr wird nicht benötigt!

### 2. Projekt öffnen

1. Klone dieses Repository oder lade es als ZIP-Datei herunter und entpacke es.  
2. Öffne Visual Studio Code.  
3. Gehe zu `Datei > Ordner öffnen...` und wähle den Projektordner aus.  

> **📌 Hinweis für ZIP-Downloads:**  
> Wenn du das Repository als ZIP-Datei herunterlädst, wird es oft in einem übergeordneten Ordner entpackt (z.B. `projektname-main`).  
> Stelle sicher, dass du den **inneren Ordner**, der die `.asm`-Datei und die anderen Projektdateien enthält, in Visual Studio Code öffnest.

---

### 3. Kompilieren und Ausführen

Der gesamte Build-Prozess ist automatisiert und mit einem einzigen Befehl startklar.

1. Öffne die Datei `hello64.asm`, um den Quellcode anzuzeigen.  
2. Drücke die Tastenkombination **`Strg + Umschalt + B`**, um den Build-Task zu starten.

Im VS Code-Terminal siehst du, wie das `make.bat`-Skript die folgenden Schritte ausführt:

#### **Kompilieren**
```shell
nasm -f win64 -Ox hello64.asm
```
# 🧠 Funktionsweise & Code-Erklärung

Das Programm zeigt eine einfache Windows-Messagebox an. Hier ist eine Erklärung der wichtigsten Teile des Codes in `hello64.asm`:
; --- Wichtige Abschnitte von hello64.asm ---

; Deklariert externe Funktionen aus den Windows-Bibliotheken,
; die wir verwenden möchten.
extern MessageBoxA
extern ExitProcess

section .data
    ; Hier definieren wir die Texte (Strings) für die MessageBox.
    ; "db" steht für "define byte". Die 0 am Ende markiert das String-Ende.
    title db 'Hallo Welt', 0
    text  db 'Dies ist eine 64-Bit-Nachricht!', 0

section .text
global Start ; Der Einsprungpunkt des Programms

Start:
    ; Die Windows x64 ABI (Application Binary Interface) erfordert,
    ; dass wir Platz auf dem Stack für die aufgerufene Funktion reservieren.
    sub rsp, 40
    -
    ; Argumente für MessageBoxA werden in Registern übergeben (nicht auf dem Stack).
    ; Reihenfolge: RCX, RDX, R8, R9
    mov rcx, 0          ; hWnd (Handle zum übergeordneten Fenster, 0 = kein übergeordnetes Fenster)
    mov rdx, text       ; lpText (Der anzuzeigende Text)
    mov r8, title       ; lpCaption (Der Fenstertitel)
    mov r9, 0           ; uType (Buttons, hier 0 für MB_OK)
    call MessageBoxA    ; Ruft die Funktion auf
    -
    ; Programm sauber beenden, um einen Absturz zu vermeiden.
    mov rcx, 0          ; Exit-Code (0 = Erfolg)
    call ExitProcess

# 💻 64-Bit-Assembly-Projekt

---

## 📁 Projektstruktur

| Datei / Ordner | Beschreibung |
| :--- | :--- |
| **`hello64.asm`** | Die Hauptdatei mit dem **64-Bit-Assembly-Code**. |
| **`make.bat`** | Ein einfaches **Batch-Skript**, das die Build-Befehle ausführt. |
| **`.vscode/tasks.json`** | Die Konfigurationsdatei, die den **Strg + Umschalt + B**-Befehl für **VS Code** definiert. |
| **`nasm.exe`** | Der portable **Netwide Assembler**. |
| **`golink.exe`** | Der portable **GoLink-Linker**. |

---

## 🔧 Fehlerbehebung (Troubleshooting)

| Problem | Lösung |
| :--- | :--- |
| Der Befehl **`Strg + Umschalt + B`** funktioniert nicht. | Stelle sicher, dass du den **gesamten Ordner** in VS Code geöffnet hast (**Datei > Ordner öffnen...**) und nicht nur die einzelne **`.asm`**-Datei. Nur so wird die **`.vscode/tasks.json`** geladen. |
| Mein Antivirenprogramm blockiert oder löscht die **`hello64.exe`**. | Das ist ein häufiges Problem bei selbst erstellten **`.exe`**-Dateien (**False Positive**). Füge eine **Ausnahme** für die **`hello64.exe`** oder den gesamten Projektordner in deinem Antivirenprogramm hinzu. |

---

## 📜 Lizenz

Dieses Projekt steht unter der **MIT-Lizenz**.

Du kannst den Code **frei verwenden, verändern und weitergeben**.
