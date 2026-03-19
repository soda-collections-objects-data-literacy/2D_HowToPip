<!--

author: Mathias Zinnen (FAU/SODa)

comment: Einführung in die Umgebungsverwaltung mit Python und Pip
date: 2026-03-16
version: 0.0.1
email: mathias.zinnen@fau.de


mode: Textbook
dark: false
edit: https://github.com/soda-collections-objects-data-literacy/2D_HowToPip

link:       https://cdn.jsdelivr.net/gh/soda-collections-objects-data-literacy/OpenRefine-Beginner-Tutorial@main/theme.css
            https://fonts.googleapis.com/css?family=Noto+Sans


icon:       /res/SODa-Logo_Wort-Bild_RGB.png
logo:       /res/SODa-Logo_Wort-Bild_RGB.png

language: de

comment: Dieses Dokument ist einer Einführung zur Umgebungsverwaltung und zum Paketmanagement in Python. Es richtet sich insbesondere an Sammlungsverantwortliche mit geringen technischen Vorkenntnissen.

-->

# SODa Einführung in die Umgebungsverwaltung mit Python und Pip

Ob in der Digitalisierung, Objektforschung oder Texterfassung -- Open Source Software kann teure kommerzielle Angebote häufig ersetzen und sichert Daten- und Fähigkeitenautonomie. 
Dabei sind die Voraussetzungen die nötig sind, um solche Open Source Algorithmen auf lokalen Systemen lauffähig zu machen häufig geringer als erwartet. 
Dieses Tutorial soll die nötigen Grundlagen vermitteln, um das eigene System für die Ausführung solcher Algorithmen vorzubereiten. 
Nacheinander werden dazu der Umgang mit der Kommandozeile, die Installation einer lokalen Python Umgebung, die Umgebungsverwaltung und -Isolation mit venv, sowie das Paketmanagement mit Pip behandelt. 
Am Ende der Einheit sind Nutzer:innen in der Lage, mit wenig Aufwand Open Source Projekte von Plattformen wie GitHub oder Pip lokal auszuführen. 

Lernziele: 
- [Umgang mit der Kommandozeile](#3)
- [Installation einer Python Umgebung](#5)
- [Umgebungsverwaltung mit Venv](#6)
- [Paketmanagement mit Pip](#7)

Das Tutorial ist angelehnt an den SODa Workshop ["Python, GitHub, Pip & Co"]() sowie die einführenden Teile der Workshops zur [Objekt-]() und Texterkennung. 
Entsprechend der Zielsetzung des SODa Projekts stellen Sammlungsverantwortliche und mit Sammlungsdaten Forschende die primäre Zielgruppe dar, grundsätzlich kann das Tutorial aber natürlich von allen genutzt werden.
Der Quelltext ist auf GitHub [veröffentlicht]() und frei nachnutzbar. Über Verbesserungsvorschläge freuen wir uns sehr, egal ob per (Mail)[mailto:mathias.zinnen@fau.de] oder GitHub pull request. 

## Einführung


- Motivation: Warum lokale Python Umgebungen? 
  - Ökosystem auch ohne Code-Kenntnisse nutzen, Datenautonomie, Open Source, häufig lokale Lösungen ausreichend
  - Veröffentlichung weiterer, darauf aufbauender Tutorials geplant

Sobald es konkret wird unterscheiden sich die nötigen Schritte je nach Betriebssystem. Einfach das Kontextmenü für das jeweilige Betriebssystem ausklappen.
------------

## Kommandozeile

Hier kontext Erklären

### Kommandozeile öffnen
-----------------------

<details>
<summary>**Windows**</summary>

Probieren powershell zu öffnen. Falls es klappt -> done
Falls nicht -> powershell installieren 
Powershell öffnen
</details>

<details>
<summary>**MacOS**</summary>

Instructions MacOS
</details>

<details>
<summary>**Linux**</summary>

Je nach Distribution und Window Manager unterschiedlich. Unter Ubuntu 'ctrl+alt+t' drücken. 
</details>

### Navigation

Einheitlich für alle
Erklären was das CWD ist, wie funktionieren relative und absolute Pfade

### Tab Completion

### Command History und Repeat

### Quizfrage
Irgendwas in die Richtung: Was kommt raus wenn man einen Befehl eingibt

## Python Installieren
Betriebssystemabhängig

### Quizfrage
Irgendein Python Befehl eingeben: Was kommt raus?

## Virtuelle Umgebung Einrichten

Was sind Umgebungen, warum virtuell? 

Diagramme aus den Folien einfügen 

1. OS ist Umgebung für kompilierte Programme
2. Python ist Umgebung für Python scripte
3. Versionsabhängigkeiten 
4. Paketabhängigkeiten
5. Versionskonflikte
6. Venv to the rescue
7. Multi-Env, Multi-Python
8. Vergleichspunkte: Anaconda, Docker

### Quiz

## Pip Packages Installieren

## Open Source Projekte Finden

## CheatSheet
Große Tabelle mit allen Commands


## Impressum

SODa – Sammlungen, Objekte, Datenkompetenzen: https://sammlungen.io/
--------------------------------------------

--------------------------------------------

**Autoren:**

- Mathias Zinnen (mathias.zinnen@fau.de)

---

Version: 0.0.1
Datum: 2026-03-17
Repository: https://github.com/soda-collections-objects-data-literacy/2D_HowToPip

---


weitere Tutorials und Open Educational Resources: https://sammlungen.io/kb

---

gefördert durch:

![Finanziert von der Europäischen Union](img/FinanziertVonDerEU.jpg)

![Gefördert durch: Bundesministerium für Forschung, Technologie und Raumfahrt](img/BMFTR_de_Web_RGB_gef_durch.jpg)