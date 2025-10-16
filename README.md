# 💬 x64 Assembly „Hallo Welt“ für Windows (NASM + GoLink)

Dieses Repository enthält ein minimalistisches **„Hallo Welt“**-Programm in 64-Bit-Assembly (NASM), speziell für **Windows**.  
Das Projekt kommt **komplett ohne Visual Studio oder MSVC++ Build Tools** aus – alles Nötige ist bereits enthalten.  
Du brauchst nur **[Visual Studio Code](https://code.visualstudio.com/)**.

---

## ✨ Features

✅ **Keine externen Abhängigkeiten** – kein Visual Studio, keine komplizierten Toolchains  
✅ **Portable Build-Tools** – NASM & GoLink sind bereits im Projekt enthalten  
✅ **Einfacher Build-Prozess** – automatisiertes Kompilieren über einen VS Code-Task  
✅ **Ideal für Einsteiger** – perfekt zum Lernen von 64-Bit-Assembly unter Windows  

---

## 🚀 Schnellstart: Vom ZIP zur lauffähigen `.exe`

### 1️⃣ Voraussetzungen

* Installiere **[Visual Studio Code](https://code.visualstudio.com/)**  
* Keine weiteren Tools nötig – alles andere ist im Repo  

---

### 2️⃣ Projekt öffnen

1. Repository klonen **oder** ZIP herunterladen und entpacken  
2. In **VS Code** öffnen:  
   `Datei → Ordner öffnen...` → wähle den Projektordner  
3. (Wichtig bei ZIP-Downloads):  
   Öffne **den inneren Ordner**, der die `.asm`-Datei und die Build-Tools enthält  
   *(z. B. `projektname-main/hello64.asm`)*  

---

### 3️⃣ Kompilieren & Ausführen

1. Öffne `hello64.asm`  
2. Starte den Build-Task mit **`Strg + Umschalt + B`**  
3. Im Terminal siehst du, wie `make.bat` automatisch kompiliert und linkt:

#### 🛠️ Kompilieren
```shell
nasm -f win64 -Ox hello64.asm
```

---

## 🧠 Code-Erklärung

Das Programm zeigt eine einfache Windows-**MessageBox** an.  
Hier sind die wichtigsten Codeabschnitte aus `hello64.asm`:

```asm
; Externe Windows-Funktionen deklarieren
extern MessageBoxA
extern ExitProcess

section .data
    title db 'Hallo Welt', 0
    text  db 'Dies ist eine 64-Bit-Nachricht!', 0

section .text
global Start

Start:
    sub rsp, 40             ; Stack für Aufruf vorbereiten
    mov rcx, 0              ; hWnd = kein übergeordnetes Fenster
    mov rdx, text           ; lpText
    mov r8,  title          ; lpCaption
    mov r9,  0              ; uType = MB_OK
    call MessageBoxA
    mov rcx, 0              ; Exit-Code
    call ExitProcess
```

---

## 💻 Projektstruktur

| Datei / Ordner | Beschreibung |
| :-------------- | :------------ |
| `hello64.asm` | Haupt-Assembly-Datei |
| `make.bat` | Batch-Skript zum Kompilieren & Linken |
| `.vscode/tasks.json` | VS Code-Task-Konfiguration |
| `nasm.exe` | Portabler **Netwide Assembler** |
| `golink.exe` | Portabler **GoLink-Linker** |

---

## 🧩 Fehlerbehebung

| Problem | Lösung |
| :------- | :------ |
| **Build-Task funktioniert nicht** | Stelle sicher, dass du den gesamten **Ordner** in VS Code geöffnet hast (nicht nur die `.asm`-Datei). |
| **Antivirus blockiert `hello64.exe`** | Häufig ein **False Positive**. Füge eine Ausnahme für die Datei oder den Ordner hinzu. |

---

## 📜 Lizenz

Dieses Projekt steht unter der **MIT-Lizenz**.  
Du darfst den Code **frei verwenden, anpassen und weitergeben**.
