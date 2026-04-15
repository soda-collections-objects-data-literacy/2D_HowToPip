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

Ob in der Digitalisierung, Objektforschung oder Texterfassung -- Open Source Software kann teure kommerzielle Angebote häufig ersetzen. 
Dabei sind die Voraussetzungen die nötig sind, um solche Open Source Algorithmen auf lokalen Systemen lauffähig zu machen häufig geringer als erwartet. 
Dieses Tutorial soll die nötigen Grundlagen vermitteln, um das eigene System für die Ausführung der Algorithmen vorzubereiten. 
Nacheinander werden dazu der Umgang mit der Kommandozeile, die Installation einer lokalen Python Umgebung, die Umgebungsverwaltung und -Isolation mit venv, sowie das Paketmanagement mit Pip behandelt. 
Am Ende der Einheit sind Nutzer:innen in der Lage, mit wenig Aufwand Open Source Projekte von Plattformen wie GitHub oder Pip lokal auszuführen. 

Lernziele: 
- [Umgang mit der Kommandozeile](#3)
- [Installation einer Python Umgebung](#13)
- [Umgebungsverwaltung mit Venv](#19)
- [Paketmanagement mit Pip](#27)

Das Tutorial ist angelehnt an zwei SODa Präsenzworkshops: ["Python, GitHub, Pip & Co"](https://sammlungen.io/events/soda-workshop-python-github-pip-co) sowie die einführenden Teile des Workshops zur [Objekterkennung](https://sammlungen.io/events/workshop-automatisierte-objekterkennung-der-sammlungsarbeit). 
Entsprechend der Zielsetzung des SODa Projekts stellen Sammlungsverantwortliche und mit Sammlungsdaten Forschende die primäre Zielgruppe dar, grundsätzlich kann das Tutorial aber natürlich von allen genutzt werden.

Der Quelltext ist auf GitHub [veröffentlicht](https://github.com/soda-collections-objects-data-literacy/2D_HowToPip) und frei nachnutzbar. Über Feedback und Verbesserungsvorschläge, z.B. per [Mail](mailto:mathias.zinnen@fau.de), freuen wir uns sehr!
Insbesondere sind wir dankbar für Rückmeldungen falls die hier vorgestellten Anleitungen mit Ihrer Systemkonfiguration nicht funktionieren. Wir helfen gerne weiter und passen die OER dann dementsprechend an!

## Einführung

Warum sollte ich mir überhaupt die Mühe machen, mich in die Kommandozeile und Python Umgebungsverwaltung einzuarbeiten? Es gibt doch onlinedienste wie google colab, verschiedene Jupyterhubs oder den [SODa Semantic Coworking Space](https://sammlungen.io/semantic-coworking-space)? 
Es kommt darauf an, was man erreichen möchte. 

Um ein erstes Verständnis für Machine-Learning und Data Science Inhalte zu entwickeln, reicht es tatsächlich häufig aus, online verfügbare Notebooks durchzuarbeiten, ohne den notwendigen Code auf dem eigenen System ausführbar machen zu müssen. 
Ein gutes Beispiel dafür sind etwa die Online Workshops unserer Kolleg:innenen von [WiNoDa](https://winoda.de/), die ihre tollen Kurse und Workshop auf [YouTube](https://www.youtube.com/@WiNoDaKnowledgeLab) und häufig mit vorbereiteten Google Colab Notebooks unterstützen, so dass die Teilnehmer:innen die Lerninhalte direkt interaktiv ausprobieren können. 
Daneben kann zum Beispiel auch der momentan noch im Aufbau befindliche SODa Semantic Coworking Space verwendet werden, um Python auszuprobieren und programmatisch auf eigene WissKI Instanzen zugreifen zu können.

Hier verfolgen wir bewusst einen anderen Ansatz: Wer lernt, grundlegend mit der Kommandozeile umzugehen, sich mit der Umgebungsverwaltung und dem Paketmanagement grundsätzlich vertraut macht und vor allem lernt, das Ganze auf dem **eigenen** System einzurichten, gewinnt volle Autonomie über die eigenen Daten und digitalen Fähigkeiten. 
Diejenigen, die gelernt haben Quelloffene Software auf ihren eigenen System zu installieren, brauchen keine spontane Serviceabschaltung, keine Änderung des Geschäftsmodells oder veränderte politische Rahmenbedingungen zu fürchten.

Klar ist aber auch: Manchmal ist es einfach nicht möglich, die dafür nötige Zeit und personelle Ressourcen aufzubringen. Wir möchten aber dennoch dafür werben, sich wenn irgend möglich die Mühe zu machen und unterstützen mit dem SODa Helpdesk gerne bei Problemen in der Umsetzung.  

Aufbauend auf diesem Tutorial planen wir weitere Vertiefungsmodule, in denen Beispielprojekte lokal installiert und genutzt werden, etwa zur Objekterkennung mit YOLO, Textverarbeitung mit SpaCy, oder Texterkennung mit EasyOCR. 
Sobald es konkret wird unterscheiden sich die nötigen Schritte je nach Betriebssystem. Einfach das Kontextmenü für das jeweilige Betriebssystem ausklappen. 
Die pro Einheit erlernten Befehle sind jeweils noch einmal im Kapitel [TLDR](#35) kurz zusammengefasst. 

## Kommandozeile

![Symbolbild einer Kommandozeilenausgabe auf einer VT100](res/RT-11_help.jpg "Symbolbild einer Kommandozeilenausgabe auf einer VT100, Photo by [Autopilot](https://commons.wikimedia.org/wiki/User:Autopilot) via Wikimedia / [CC-BY-SA-3.0](https://commons.wikimedia.org/wiki/Category:CC-BY-SA-3.0)")

Die Kommandozeile (oft auch Terminal oder Konsole genannt) ist eine rein textbasierte Möglichkeit, mit dem eigenen Betriebssystem zu interagieren. 
Da die meisten modernen Betriebssysteme standardmäßig über grafische Oberflächen (mit Maus und Fenstern) gesteuert werden, kann man einen Computer jahrelang nutzen, ohne jemals mit der Kommandozeile in Berührung zu kommen. 

Für die Ausführung von Python-Skripten, das Installieren von Softwarepaketen oder die Automatisierung von Routineaufgaben ist die Kommandozeile jedoch das mächtigere und oft direktere Werkzeug. Im Folgenden schauen wir uns an, wie wir dieses Werkzeug aufrufen und uns darin bewegen.

### Kommandozeile öffnen
-----------------------
Der erste Schritt ist das Öffnen des entsprechenden Programms. Hier unterscheiden sich die konkreten Schritte je nach Betriebssystem. 

<details>
<summary>Windows (PowerShell)</summary>

> Unter Windows nutzen wir die **PowerShell**, da die sie mit der hier verwendeten Bash Syntax kompatibel ist.
> 1. Drücken Sie die Windows-Taste auf Ihrer Tastatur (oder klicken Sie unten in der Taskleiste auf das Start-Symbol / die Lupe).
> 2. Tippen Sie das Wort `powershell` ein.
> 3. Klicken Sie auf das Suchergebnis **Windows PowerShell**, um das Programm zu öffnen. Es öffnet sich ein Fenster mit einem meist blauen oder schwarzen Hintergrund und einem blinkenden Cursor.
Sollte die PowerShell nicht bereits installiert sein (kann bei älteren Windows Versionen der Fall sein), folgen Sie bitte den offiziellen [Installationsanweisungen](https://learn.microsoft.com/de-de/powershell/scripting/install/install-powershell-on-windows) von Microsoft.
</details>

<details>
<summary><b>MacOS (Terminal)</b></summary>

>Auf dem Mac ist die App **Terminal** bereits vorinstalliert.
> 1. Öffnen Sie die Spotlight-Suche. Drücken Sie dafür gleichzeitig die Tasten `[cmd] + [Leertaste]`.
> 2. Tippen Sie das Wort `Terminal` in das Suchfeld ein.
> 3. Drücken Sie `[Enter]` oder klicken Sie auf das Suchergebnis, um das Terminal zu starten. Ein Fenster mit weißem oder schwarzem Hintergrund und einem blinkenden Cursor öffnet sich.
</details>

<details>
<summary><b>Linux (Terminal)</b></summary>

> 1. In den meisten gängigen Linux-Distributionen (wie Ubuntu) können Sie das Terminal ganz einfach über die Tastenkombination `[Strg] + [Alt] + [T]` öffnen.
> 2. Alternativ finden Sie es im Anwendungsmenü unter dem Namen **Terminal** oder **Konsole**.
> 3. Sollten Sie eine andere Distribution als Ubuntu oder einen anderen Window Manager als Gnome verwenden, hegen wir den begründeten Verdacht, dass Sie wissen, wie man die Kommandozeile öffnet!

</details>

### Navigation und das Arbeitsverzeichnis

Sobald Sie die Kommandozeile geöffnet haben, befinden Sie sich immer an einem bestimmten virtuellen Ort auf Ihrem Computer. Das ist wie in einem physischen Gebäude. Sie befinden sich immer in einem konkreten Raum, auch wenn Sie theoretisch Schlüssel für das ganze Gebäude haben. 

Dieser "Raum" wird als Current Working Directory (CWD), also das aktuelle Arbeitsverzeichnis, bezeichnet. Das CWD bestimmt, an welchem Ort im Dateisystem Ihre Befehle ausgeführt werden. Wenn Sie beispielsweise den Befehl geben "Lege hier einen neuen Ordner an", passiert das genau in Ihrem CWD.

Um sich durch die Verzeichnisse zu bewegen, müssen Sie dem System den Weg beschreiben. Das tun wir über sogenannte Pfade, die entweder relativ oder absolut sein können.

**1. Absolute Pfade (Die vollständige Adresse)**
Ein absoluter Pfad ist wie eine exakte postalische Anschrift. Er beginnt immer ganz oben an der Wurzel Ihres Dateisystems (z.B. bei `C:\ ` unter Windows oder `/` bei MacOS/Linux) und beschreibt den exakten Weg bis zur Zieldatei. Ein absoluter Pfad funktioniert zeigt immer auf den gleichen Ort in ihrem Dateisystem, egal in welchem CWD Sie sich gerade befinden.
* Beispiel Windows: `C:\Benutzer\Name\Dokumente\Projekt`
* Beispiel Mac/Linux: `/Users/Name/Documents/Projekt`

**2. Relative Pfade (Die Wegbeschreibung von Ihrem Standort aus)**
Ein relativer Pfad ist wie die Anweisung "Gehe den Gang hinunter und nimm die zweite Tür links". Er geht immer von Ihrem aktuellen Arbeitsverzeichnis (CWD) aus.
* Wenn Sie im Ordner `Dokumente` sind und in den Unterordner `Projekt` möchten, reicht der relative Pfad: `Projekt` (oder `./Projekt`).
* Um einen Ordner nach oben zu gehen (quasi den aktuellen Raum zu verlassen und auf den Flur zu treten), nutzt man in der Kommandozeile immer zwei Punkte: `..`

#### Die wichtigsten Befehle zur Navigation

Probieren Sie doch direkt einmal in Ihrer geöffneten Kommandozeile aus, sich umzusehen:

* **Wo bin ich?** Geben Sie `pwd` (Mac/Linux) oder `Get-Location` (Windows PowerShell) ein und drücken Sie Enter. Das System zeigt Ihnen Ihr aktuelles CWD an.
* **Was ist hier?**
  Geben Sie `ls` ein und drücken Sie Enter. Das listet alle Dateien und Unterordner an Ihrem aktuellen Standort auf.
* **Wie wechsle ich den Raum?**
  Nutzen Sie den Befehl `cd` (change directory) gefolgt von einem Leerzeichen und dem Pfad. Zum Beispiel `cd Dokumente` (um in den Ordner Dokumente zu wechseln) oder `cd ..` (um einen Ordner nach oben zu gehen).

### Tipps & Tricks

Die Arbeit in der Kommandozeile wirkt anfangs oft mühsam, da jeder Buchstabe und jedes Leerzeichen exakt stimmen muss.
Zum Glück gibt es einfache Tricks, die Ihnen nicht nur den Großteil der Tipparbeit abnehmen, sondern auch frustrierende Tippfehler von vornherein verhindern.

#### Tab-Vervollständigung (Tab Completion)

Obwohl die Kommandozeile textbasiert ist, müssen sie bei weitem nicht alles selbst tippen. 
Hier kommt Ihr neuer bester Freund ins Spiel: Die Tabulatortaste (kurz Tab, befindet sich auf der Tastatur meist ganz links neben dem 'Q' und hat zwei entgegengesetzte Pfeile).

Wenn Sie anfangen, einen Ordner- oder Dateinamen einzutippen, und dann die Tab-Taste drücken, versucht die Kommandozeile, den Namen automatisch zu Ende zu schreiben. 

* Ein Beispiel: Stellen Sie sich vor, Sie haben einen Ordner namens `Sammlungsdaten_Export_2026`. Anstatt diesen langen Namen abzutippen (und sich dabei vielleicht zu vertippen), tippen Sie einfach `cd Samm` und drücken dann die `[Tab]`-Taste. 
* Die Kommandozeile vervollständigt den Befehl automatisch zu `cd Sammlungsdaten_Export_2026`.
* Gibt es mehrere Dateien, die mit "Samm" anfangen, können Sie die Tab-Taste mehrfach drücken, um durch die verschiedenen Möglichkeiten durchzuschalten.

Das funktioniert nicht nur für die Vervollständigung von Datei- und Ordnernamen, sondern auch zur automatischen Expansion von Kommandozeilenbefehlen. Auch andere Konsolenbefehle lassen sich automatisch vervollständigen, sobald genug Zeichen getippt sind, um das Kommando eindeutig zu identifizieren. Sollten noch nicht genug Zeichen getippt sein führt ein mehrmaliges Drücken der Tabulatortaste zu einer Anzeige der Optionen. Das ist sehr nützlich wenn man sich mal nicht genau an ein Kommando erinnern kann -- oder einfach keine Lust hat, so viel zu tippen! 


#### Befehlshistorie (Command History)

Niemand tippt gerne denselben langen Befehl zweimal ein. Auch hier nimmt Ihnen die Kommandozeile die Arbeit ab, denn sie merkt sich alle Befehle, die Sie in der aktuellen Sitzung eingegeben haben.

Um auf alte Befehle zuzugreifen, nutzen Sie einfach die **Pfeiltasten (Hoch und Runter)** auf Ihrer Tastatur:
* Drücken Sie die **Pfeil-nach-oben-Taste** (`[↑]`), um den zuletzt eingegebenen Befehl wieder aufzurufen.
* Drücken Sie sie mehrmals, um weiter in der Vergangenheit zurückzugehen.
* Sind Sie zu weit zurückgegangen? Mit der **Pfeil-nach-unten-Taste** (`[↓]`) springen Sie wieder einen Schritt vorwärts.

Sobald der gewünschte alte Befehl auf dem Bildschirm erscheint, können Sie ihn mit der `[Enter]`-Taste erneut ausführen oder ihn vorher mit der Löschen-Taste noch anpassen.

#### Ordner anlegen und löschen

Neben der reinen Navigation können Sie über die Kommandozeile natürlich auch Ihre Ordnerstruktur bearbeiten. Für unsere späteren Übungen ist es wichtig, dass Sie wissen, wie man neue "Räume" (Ordner) erschafft und wieder abreißt.

**1. Einen neuen Ordner anlegen (`mkdir`)**
Um in Ihrem aktuellen Arbeitsverzeichnis einen neuen Ordner zu erstellen, nutzen Sie den Befehl `mkdir` (steht für make directory), gefolgt von einem Leerzeichen und dem gewünschten Namen.
* Beispiel: `mkdir Projekt_Umgebungsverwaltung`
* Wenn Sie danach `ls` eingeben, werden Sie sehen, dass der neue Ordner aufgetaucht ist.

**2. Einen Ordner löschen (`rm`)**
Um Dateien oder ganze Ordner zu löschen, wird der Befehl `rm` (remove) verwendet. Da ein Ordner weitere Dateien enthalten kann, müssen wir der Kommandozeile sagen, dass sie den Ordner und seinen gesamten Inhalt (rekursiv) löschen soll. Dafür hängen wir ein `-r` an den Befehl an.
* Beispiel: `rm -r Projekt_Umgebungsverwaltung`
* **Achtung:** Wenn Sie Dateien oder Ordner über die Kommandozeile löschen, landen diese in der Regel nicht im Papierkorb, sondern verschwinden sofort unwiderruflich! Nutzen Sie diesen Befehl also mit Vorsicht.

### Weiterführende Kommandozeilen-Einführungen

In diesem Tutorial haben wir nur an der Oberfläche der Kommandozeile gekratzt. Wenn Sie lernen möchten, wie Sie zehntausende Dateien in Sekundenbruchteilen umbenennen, durchsuchen oder automatisierte Abläufe starten, finden Sie hier exzellente, speziell für Forschende und Geisteswissenschaftler:innen aufbereitete Einstiegshilfen und Vertiefungen:

* **[The Programming Historian](https://programminghistorian.org/):** Bietet hervorragende Einführungen, beispielsweise die (Introduction to the Windows Command Line with PowerShell)[https://programminghistorian.org/en/lessons/intro-to-powershell] oder (Introduction to the Bash Command Line)[https://programminghistorian.org/en/lessons/intro-to-bash].
* **[Library Carpentry - The UNIX Shell](https://librarycarpentry.org/lc-shell/):** Ein englischsprachiger, speziell für Bibliothekar:innen und Mitarbeitende an Sammlungen entwickelter Kurs. Er zeigt Schritt für Schritt die Zeitersparnis der Kommandozeile bei der täglichen Datenverarbeitung.
* **[Ubuntuusers Wiki (Shell)](https://wiki.ubuntuusers.de/Shell/Einf%C3%BChrung/):** Für Nutzer:innen von Linux (und in weiten Teilen auch Mac) bietet dieses verständliche, deutschsprachige Wiki einen Einstieg in die tiefere Funktionsweise des Terminals.

### Quiz: Kommandozeile

**Frage 1: Sie befinden sich aktuell im Verzeichnis `/Users/Forschung/Projekt_A`. Sie möchten in das parallel liegende Verzeichnis `/Users/Forschung/Archiv` wechseln. Welcher relative Befehl ist korrekt?**

[(X)] `cd ../Archiv`
[( )] `cd /Archiv`
[( )] `cd ./Archiv`
[( )] `cd .../Archiv`

**Frage 2: Was passiert exakt, wenn Sie den Befehl `rm -r ../Projekt` ausführen, während Ihr aktuelles Arbeitsverzeichnis (CWD) `/Dokumente/Projekt/Daten` lautet?**

[( )] Der Befehl schlägt fehl, da man keine Ordner löschen kann, in denen man sich gerade befindet.
[( )] Der Ordner "Projekt" wird in den Papierkorb verschoben.
[(X)] Der Ordner "Projekt" und all seine Inhalte (inklusive des Ordners "Daten", in dem Sie sich aktuell befinden) werden sofort und permanent gelöscht.
[( )] Es wird nur der leere Ordner "Projekt" gelöscht, da Dateien durch das Argument `-r` geschützt sind.

**Frage 3: Aus welchem spezifischen Grund wird im Tutorial für Windows-Nutzer die PowerShell anstelle der älteren Eingabeaufforderung (cmd) empfohlen?**

[( )] Weil sie als einziges Windows-Terminal absolute Pfade verarbeiten kann.
[(X)] Weil sie mit der Bash-Syntax kompatibel ist, wodurch die gleichen Befehle (wie `ls` oder `rm`) wie unter MacOS und Linux genutzt werden können.
[( )] Weil sie standardmäßig einen eingebauten Python-Interpreter besitzt.
[( )] Weil sie Befehle automatisch vervollständigt, ohne dass man die Tabulatortaste drücken muss.

**Frage 4: Sie tippen `cd Pr` und drücken die Tabulatortaste. Das Terminal vervollständigt den Begriff nicht und es scheint gar nichts zu passieren. Was ist laut Text die wahrscheinlichste Ursache?**

[( )] Tab-Vervollständigung funktioniert grundsätzlich nur bei der Eingabe von absoluten Pfaden.
[(X)] Die Buchstabenfolge "Pr" ist noch nicht eindeutig (es gibt im Ordner z.B. "Projekt" und "Privat"). Sie müssen Tab mehrmals drücken, um die Optionen durchzuschalten.
[( )] Die Tabulatortaste funktioniert nicht für Ordnernamen, sondern nur für ausführbare Dateien.
[( )] Sie haben weniger als die zwingend erforderlichen drei Zeichen getippt.

**Frage 5: Was bewirkt der Befehl `cd ./Projekt`, wenn Sie sich aktuell im Verzeichnis `~/Dokumente` befinden?**

[(X)] Er versucht, in einen Unterordner namens "Projekt" zu wechseln, der sich direkt in `~/Dokumente` befindet.
[( )] Er wirft eine Fehlermeldung, da ein einzelner Punkt in Dateipfaden unzulässig ist.
[( )] Er navigiert eine Verzeichnisebene nach oben und sucht dort nach "Projekt".
[( )] Er erstellt einen neuen Ordner "Projekt" und navigiert gleichzeitig hinein.

**Frage 6: Sie haben soeben 10 verschiedene Befehle in der Kommandozeile nacheinander ausgeführt. Sie drücken nun die Pfeil-nach-oben-Taste (`[↑]`) genau drei Mal. Da Sie zu weit zurückgegangen sind, drücken Sie danach einmal die Pfeil-nach-unten-Taste (`[↓]`). Welcher Befehl wird Ihnen nun in der Eingabezeile angezeigt?**

[( )] Der 7. Befehl, den Sie eingegeben haben.
[(X)] Der 9. Befehl, den Sie eingegeben haben.
[( )] Der 8. Befehl, den Sie eingegeben haben.
[( )] Die Historie wird gelöscht, die Zeile ist leer.

**Frage 7: Welcher der folgenden Pfade ist laut der Definition im Tutorial eindeutig ein "Absoluter Pfad"?**

[( )] `Dokumente/Projekt/Daten`
[( )] `../Users/Name/Documents`
[(X)] `/Users/Name/Documents/Projekt`
[( )] `./Projekt`
[(X)] `~/Users/Name/Documents/Projekt`

**Frage 8: Sie möchten in einem leeren Arbeitsverzeichnis einen neuen Ordner "Test" erstellen und sofort in diesen hineinwechseln. Welche Befehlsfolge ist dafür korrekt?**

[( )] Zuerst `cd Test`, dann `mkdir Test`
[(X)] Zuerst `mkdir Test`, dann `cd Test`
[( )] Ein einfaches `mkdir cd Test` reicht aus
[( )] Zuerst `mkdir Test`, dann `pwd Test`

**Frage 9: Was verdeutlicht die im Text verwendete Metapher des "Gebäudes und der konkreten Räume" in Bezug auf die Kommandozeile?**

[( )] Das Prinzip von Administratorenrechten, die einem "Schlüssel" für das gesamte System entsprechen.
[( )] Die Funktion der Tab-Vervollständigung, die einem automatisch die Türen öffnet.
[( )] Dass sich die Befehlshistorie wie ein Grundriss des Gebäudes verhält.
[(X)] Das Konzept des Current Working Directory (CWD), das als "Standort" den Ausgangspunkt für alle relativen Befehle festlegt.

**Frage 10: Warum ist es laut den Hinweisen im Text besonders riskant, den Befehl `rm -r` versehentlich mit einem absoluten Pfad auf die Wurzel des Systems (z.B. `/` oder `C:\`) auszuführen?**

[( )] Weil dies den Papierkorb des Betriebssystems restlos überfüllen und abstürzen lassen würde.
[(X)] Weil der Befehl das gesamte Betriebssystem permanent und ohne Backup löschen würde, da das `-r` Argument alle Unterordner einbezieht.
[( )] Weil dadurch die Kommandozeile ihre administrativen Rechte verliert.
[( )] Weil der Befehl dann die Tab-Vervollständigung für die aktuelle Sitzung dauerhaft blockiert.

## Python 

Python ist aktuell eine der beliebtesten Programmiersprachen der Welt. Besonders in der Wissenschaft, den Digital Humanities und bei der Arbeit mit großen Datenmengen (wie Sammlungsdaten) hat sie sich als Standard etabliert. Zwei Eigenschaften machen Python für unseren Anwendungszweck besonders interessant:

**1. Python ist eine interpretierte Sprache**
Bei vielen traditionellen Programmiersprachen (wie C++) wird der von Menschen geschriebene Code erst in ein fertiges, maschinenlesbares Programm übersetzt (kompiliert), bevor man es ausführen kann. Die fertige Datei (z.B. eine `.exe`) bringt dann alles mit, was sie zum Laufen braucht. 

Python funktioniert anders: Es ist eine interpretierte Sprache. Das bedeutet, der Programmcode bleibt als lesbarer Text erhalten. Er wird erst in dem Moment, in dem wir ihn starten, Zeile für Zeile von einem sogenannten Interpreter gelesen und direkt ausgeführt. 
Warum ist das wichtig? Weil ein Python-Skript (der Text) nicht für sich alleine lauffähig ist. Es bringt keinen eigenen Übersetzer mit. Um ein Python-Projekt von GitHub auf Ihrem Computer auszuführen, müssen wir also sicherstellen, dass auf unserem System der richtige Interpreter bereitsteht. Genau das macht das Thema Umgebungsverwaltung später so wichtig.

**2. Ein gigantisches Ökosystem an Paketen**
Niemand muss das Rad neu erfinden. Die weltweite Python-Community hat für fast jedes erdenkliche Problem bereits fertige Bausteine geschrieben, sogenannte Bibliotheken (Libraries) oder Pakete (Packages). Ob Sie Texte maschinell auswerten, automatische Objekterkennung in Bildern nutzen oder Metadaten aus Tabellen auslesen wollen: Es gibt dafür zehntausende vorgefertigte Pakete, die wir einfach in unser Projekt laden können. 

### Installation

Damit unser Computer Python-Code interpretieren kann, müssen wir Python zunächst installieren. Klappen Sie dafür die Anleitung für Ihr Betriebssystem auf:

<details>
<summary><b>Windows</b></summary>
> 1. Laden Sie den Python Install Manager von der offiziellen Website [Python.org](https://www.python.org/) herunter und führen Sie die Datei aus. Wichtig: Setzen Sie im allerersten Fenster des Installers unbedingt unten das Häkchen bei "Add Python to PATH"!
> 2. Um eine bestimmte installierte Version über das Terminal (PowerShell) aufzurufen, können Sie den Befehl `py -V:<VERSION>` nutzen, z.B. `py -V:3.11`.
</details>

<details>
<summary><b>MacOS</b></summary>

> Auf dem Mac empfehlen wir die Installation über die Kommandozeile, um spätere Versionen leichter verwalten zu können.
> 1. Öffnen Sie Ihr Terminal.
> 2. Falls Sie Homebrew (einen beliebten Paketmanager für Mac) noch nicht installiert haben, folgen Sie kurz den Anweisungen auf [brew.sh](https://brew.sh/).
> 3. Wir nutzen das Tool `pyenv` zur Verwaltung der Versionen. Geben Sie ein: `brew install pyenv` und drücken Sie Enter.
> 4. Installieren Sie nun Python (z.B. Version 3.11) mit dem Befehl: `pyenv install 3.11`
</details>

<details>
<summary><b>Linux (z.B. Ubuntu)</b></summary>

> Linux-Systeme bringen oft schon eine Python-Version mit oder lassen sich sehr einfach über den integrierten Paketmanager aktualisieren.
> 1. Öffnen Sie das Terminal.
> 2. Installieren Sie Python über den von ihnen verwendeten Paketmanager, z.B. unter ubuntu: `sudo apt update && sudo apt install python3`
</details>



Lassen Sie uns direkt überprüfen, ob die Installation erfolgreich war und Ihr Computer den Interpreter nun kennt. 
Öffnen Sie Ihre Kommandozeile und geben Sie folgenden Befehl ein (und drücken Sie Enter):

* Unter Windows: `python --version` (falls das nicht klappt, probieren Sie `py --version`)
* Unter Mac/Linux: `python3 --version` (oder auch `python --version`)

**Quiz: Erkennt die Kommandozeile Python?**

**Was wird Ihnen in der Kommandozeile als Antwort (Output) ausgegeben?**

[( )] "Command not found" oder "Der Befehl 'python' ist entweder falsch geschrieben oder konnte nicht gefunden werden."
[(X)] Ein Text wie "Python 3.11.x" (oder eine ähnliche Versionsnummer).
[( )] Es passiert gar nichts, der Cursor blinkt einfach in der nächsten Zeile weiter.


### Ein erstes Python-Skript ausführen

Nun, da der Python-Interpreter installiert und über die Kommandozeile erreichbar ist, wollen wir ihn auch nutzen. Wie zu Beginn des Kapitels erklärt, liest Python reine Textdateien (sogenannte Skripte, erkennbar an der Dateiendung `.py`) und führt die darin enthaltenen Befehle aus. 

Je nach Betriebssystem und Installation starten Sie Skripte, indem Sie in der Kommandozeile den entsprechenden Aufrufbefehl (`python`, `py` oder `python3`) gefolgt von einem Leerzeichen und dem Namen der Skript-Datei eingeben. 

Lassen Sie uns das direkt ausprobieren:

1. Öffnen Sie ein einfaches Texteditor-Programm (z.B. den vorinstallierten *Editor* bzw. *Notepad* unter Windows oder *TextEdit* auf dem Mac). Bitte nutzen Sie hierfür kein Word, da dieses versteckte Formatierungen speichert!
2. Tippen Sie exakt diese eine Zeile ein: 
   `print("Look ma, I can python!")`
3. Speichern Sie die Datei unter dem Namen `hello.py` in einem Ordner Ihrer Wahl (z.B. in einem neuen Ordner namens `Python_Test` in Ihren Dokumenten).
4. Öffnen Sie Ihre Kommandozeile und navigieren Sie mit dem `cd`-Befehl (den wir vorhin kennengelernt haben) in genau diesen Ordner. Zur Erinnerung: Mit der `[Tab]`-Taste geht das viel schneller!
5. Führen Sie das Skript nun aus. Tippen Sie dafür (je nach System):
   `python hello.py` (oder `python3 hello.py` bzw. `py hello.py`) und drücken Sie Enter.

Wenn alles geklappt hat, liest der Interpreter nun Ihre Datei und gibt den Text `Look ma, I can python!` direkt in Ihrer Kommandozeile aus. Herzlichen Glückwunsch zu Ihrem ersten laufenden Python-Skript!

### Optional: Eine zweite Python-Version installieren (Multi-Python)

Manche Open-Source-Projekte benötigen ganz bestimmte, oft ältere Python-Versionen (z.B. Python 3.9), da sie mit der allerneuesten Version nicht mehr kompatibel sind. 

Die gute Nachricht: Sie können problemlos mehrere Python-Versionen gleichzeitig auf Ihrem Computer installieren, ohne dass diese sich in die Quere kommen! Später lernen wir, wie wir mit `venv` gezielt auswählen, welche dieser Versionen für ein Projekt genutzt werden soll.

Wenn Sie dieses "Multi-Python"-Szenario später in unseren Übungen ausprobieren möchten, können Sie sich jetzt testweise eine zweite, ältere Version (z.B. Version 3.9) installieren. Klappen Sie dafür die Anleitung für Ihr System auf:

<details>
<summary><b>Windows</b></summary>

Unter Windows macht uns der sogenannte "Python Launcher" (der kleine Helfer `py`, der bei der Erstinstallation automatisch mitinstalliert wurde) das Leben sehr leicht.
1. Gehen Sie auf [python.org/downloads](https://www.python.org/downloads/) und scrollen Sie nach unten zu den älteren Releases.
2. Suchen Sie nach der gewünschten Version (z.B. 3.9.13) und laden Sie den Windows-Installer herunter.
3. Führen Sie die Installation genau wie beim ersten Mal durch (auch hier das Häkchen bei "Add Python to PATH" nicht vergessen!).
4. Der Python Launcher erkennt die neue Version automatisch. Sie können in der Kommandozeile nun einfach zwischen den Versionen wählen, indem Sie z.B. `py -3.9` oder `py -3.11` eingeben.
</details>

<details>
<summary><b>MacOS</b></summary>

Da wir auf dem Mac das Tool `pyenv` zur Installation genutzt haben, ist das Hinzufügen einer weiteren Version ein Kinderspiel.
1. Öffnen Sie Ihr Terminal.
2. Geben Sie den Befehl `pyenv install 3.9.18` (oder eine andere gewünschte Version) ein und drücken Sie Enter.
3. `pyenv` lädt die Version automatisch herunter und richtet sie parallel zu Ihrer bereits installierten Version ein.
4. Mit dem Befehl `pyenv versions` können Sie sich jederzeit eine Liste aller Python-Versionen anzeigen lassen, die nun auf Ihrem Mac zur Verfügung stehen.
</details>

<details>
<summary><b>Linux (z.B. Ubuntu)</b></summary>

Unter Linux nutzen wir einfach wieder den Paketmanager, um eine spezifische Version exakt neben die bestehende zu installieren.
1. Öffnen Sie das Terminal.
2. Geben Sie den Befehl für die gewünschte Version ein, z.B.: `sudo apt update && sudo apt install python3.9`
3. Nach der Installation können Sie diese spezifische Version in der Kommandozeile über den Befehl `python3.9` (statt nur `python3`) gezielt aufrufen.
</details>

### Weiterführende Python-Einführungen

Dieses Tutorial konzentriert sich gezielt auf die Umgebungsverwaltung und das Ausführen fremder Open-Source-Projekte. Wenn Sie auf den Geschmack gekommen sind und die Programmiersprache Python selbst von Grund auf lernen möchten, um eigene Skripte für Ihre Sammlungsdaten zu schreiben, empfehlen wir folgende kostenfreie Ressourcen:

* **[The Programming Historian](https://programminghistorian.org/en/lessons/?topic=python):** Exzellente, praxisnahe Tutorials, die speziell für Geistes- und Kulturwissenschaftler:innen sowie Archivar:innen geschrieben wurden (viele davon auch auf [Deutsch](https://programminghistorian.org/de/lernen/?topic=python) verfügbar).
* **[Offizielles Python-Tutorial](https://docs.python.org/de/3/tutorial/index.html):** Die offizielle Dokumentation ist mittlerweile sehr gut ins Deutsche übersetzt und bietet einen soliden Rundumschlag.
* **[W3Schools Python Tutorial](https://www.w3schools.com/python/):** Eine sehr einsteigerfreundliche, englischsprachige Seite, bei der Sie viele Konzepte direkt im Browser ausprobieren können.

### Quiz: Python 

**Frage 1: Warum ist das Thema "Umgebungsverwaltung" bei Python laut Text so viel relevanter als bei traditionellen, kompilierten Programmiersprachen wie C++?**

[( )] Weil Python-Programme zwingend eine grafische Benutzeroberfläche benötigen, die vom Betriebssystem simuliert werden muss.
[( )] Weil der Quellcode bei Python bei jeder Ausführung dauerhaft in Maschinencode (z.B. `.exe`) umgewandelt und auf der Festplatte gespeichert wird.
[(X)] Weil ein Python-Skript nur lesbarer Text ist, der keinen eigenen Übersetzer mitbringt, sondern exakt von der Laufzeitumgebung und den Paketen abhängt, die lokal auf dem System bereitstehen.
[( )] Weil Python-Pakete (Libraries) nach jeder Ausführung eines Skripts automatisch vom System gelöscht werden.

**Frage 2: Sie sollen für Ihr erstes Skript einen Editor öffnen. Warum warnt das Tutorial ausdrücklich davor, Textverarbeitungsprogramme wie Microsoft Word zum Schreiben von Python-Code zu verwenden?**

[(X)] Weil Word unsichtbare Formatierungen (wie Schriftarten, Zeilenabstände) in der Datei speichert, die kein reiner Text sind und an denen der Python-Interpreter beim Lesen scheitern würde.
[( )] Weil Word-Dokumente aus Lizenzgründen vom Python-Interpreter blockiert werden.
[( )] Weil Word die Dateiendung automatisch in `.exe` ändert und der Code somit kompiliert wird.
[( )] Weil Skripte, die in Word geschrieben wurden, nur mit Administratorrechten in der Kommandozeile ausgeführt werden dürfen.

**Frage 3: Ein Kollege nutzt Windows, hat Python heruntergeladen und installiert. Wenn er nun `python --version` im Terminal eingibt, meldet das System: "Der Befehl 'python' ist entweder falsch geschrieben oder konnte nicht gefunden werden." Was hat er höchstwahrscheinlich falsch gemacht?**

[( )] Er hat Python in der PowerShell statt in der älteren Eingabeaufforderung (cmd) aufgerufen.
[( )] Er hat vergessen, das Skript mit `pyenv install` zu aktivieren.
[( )] Er versucht ein Skript auszuführen, ohne dass eine `.py` Datei im aktuellen Verzeichnis (CWD) liegt.
[(X)] Er hat beim ersten Installationsfenster ganz unten das wichtige Häkchen bei "Add Python to PATH" nicht gesetzt, weshalb das Terminal nicht weiß, wo das Programm liegt.

**Frage 4 (Nur für Windows User): Sie nutzen Windows und haben testweise Python 3.9 neben einer neueren Version installiert. Wie lautet der spezifische Aufruf, um ein Skript (z.B. `hello.py`) über den "Python Launcher" gezielt mit der älteren Version 3.9 auszuführen?**

[( )] `python3.9 hello.py`
[(X)] `py -3.9 hello.py`
[( )] `python --version 3.9 hello.py`
[( )] `pyenv exec 3.9 hello.py`

**Frage 5 (nur für Mac User): Auf einem Mac nutzen Sie das Werkzeug `pyenv` für das "Multi-Python"-Szenario. Mit welchem konkreten Befehl können Sie sich anzeigen lassen, welche Python-Versionen Ihnen auf dem Mac nun insgesamt zur Verfügung stehen?**

[( )] `py -V:all`
[( )] `python3 --versions`
[(X)] `pyenv versions`
[( )] `brew list python`

## Umgebungsvirtualisierung

Bevor wir uns ansehen, wie wir Open-Source-Projekte lokal installieren, müssen wir ein zentrales Konzept verstehen: die Umgebung (Englisch: Environment). 

Was genau ist damit gemeint? Ähnlich wie eine Pflanze die richtige Erde, Temperatur und Luftfeuchtigkeit braucht, um zu wachsen, benötigt ein Softwareprogramm bestimmte Bedingungen, um fehlerfrei zu laufen. Diese Rahmenbedingungen nennen wir die Ausführungsumgebung.

**Das Betriebssystem als Umgebung für kompilierte Programme**
Bei klassischen, kompilierten Programmen (wie Ihrem Webbrowser oder einem Textverarbeitungsprogramm wie Microsoft Word) stellt das Betriebssystem (Windows, macOS, Linux) die Umgebung zur Verfügung. Das Programm kommuniziert direkt mit dem Betriebssystem, über sogenannte System Calls, um beispielsweise Speicherplatz anzufordern oder ein Fenster auf dem Bildschirm zu zeichnen. Das Programm bringt in der Regel alles andere, was es braucht, bereits in seinem Installationsordner mit.

**Python als Umgebung für Python-Skripte**
Für Python-Skripte reicht das Betriebssystem allein nicht aus. Wie wir im vorherigen Kapitel gelernt haben, bestehen Python-Programme nur aus für Menschen lesbarem Text. Die "Umgebung" für ein Python-Skript ist daher komplexer und besteht aus mehreren Schichten:
* Ganz unten liegt das Betriebssystem.
* Darauf liegt der Python-Interpreter (die sogenannte Python Runtime), der den Text liest und übersetzt.
* Darüber liegen die Python-Bibliotheken (Libraries / Pakete), also die externen Bausteine, die das Skript nutzt.

### Warum virtuell? Das Problem der Abhängigkeiten

Wenn wir nun anfangen, verschiedene Projekte von Plattformen wie GitHub herunterzuladen und auszuprobieren, stoßen wir sehr schnell auf drei große Herausforderungen:

**Versionsabhängigkeiten (Python-Version)**
Python entwickelt sich ständig weiter. Ein Skript, das 2020 geschrieben wurde, benötigt vielleicht exakt Python 3.8, weil bestimmte Befehle in der neueren Version 3.12 abgeschafft oder verändert wurden. 

**Paketabhängigkeiten (Dependencies)**
Fast kein modernes Skript kommt ohne externe Pakete aus. Ein Projekt zur Texterkennung braucht vielleicht die Pakete `numpy` und `spacy`. Diese müssen auf Ihrem Computer installiert sein, sonst bricht das Skript beim Start sofort mit einer Fehlermeldung ab.

**Versionskonflikte**
Hier liegt das größte Problem: Stellen Sie sich vor, Sie haben ein Projekt zur automatischen Bilderkennung für Ihre Sammlung heruntergeladen. Dieses Projekt benötigt das Paket `pandas` in der Version 1.0. 
Ein halbes Jahr später laden Sie ein brandneues Projekt zur Textanalyse herunter. Dieses verlangt zwingend `pandas` in der Version 2.0. 

Wenn Sie nun einfach alles zentral in Ihrer einzigen, systemweiten Python-Installation (Ihrer "globalen Umgebung") installieren, passiert Folgendes: Die Installation von Version 2.0 überschreibt die alte Version 1.0. Plötzlich funktioniert Ihr altes Bilderkennungsprojekt nicht mehr! Installieren Sie Version 1.0 wieder zurück, geht das neue Projekt kaputt. 

Um dieses Problem zu lösen, können die Python Umgebungen der jeweiligen Projekte voneinader isoliert werden. Das nennt man Umgebungsvirtualisierung.

### Venv verwenden

Anstatt alle Python-Pakete in einen einzigen, großen, systemweiten "Topf" zu werfen, geben wir jedem Projekt seinen eigenen, abgetrennten Bereich. 

Stellen Sie sich vor, Sie haben einen großen Garten (Ihr Betriebssystem). Anstatt alle Pflanzen kreuz und quer in dasselbe Beet zu setzen, wo sie sich gegenseitig das Wasser abgraben oder unterschiedliche Erde benötigen, setzen Sie jede Pflanze in ihren eigenen Blumentopf. 

Genau das ist eine virtuelle Umgebung (Virtual Environment).

Glücklicherweise hat Python seit Version 3.3 Python ein Werkzeug dafür direkt fest eingebaut: das Modul `venv`.

### Praxis: Mit virtuellen Umgebungen arbeiten

Es folgen ein paar praktische Übungen, um den Umgang mit `venv` zu lernen. Damit wir gefahrlos experimentieren können, ohne Ihr System unübersichtlich zu machen, legen wir zunächst einen dedizierten Übungsordner an.

Erinnern Sie sich an unsere Terminal-Befehle? Öffnen Sie Ihre Kommandozeile und geben Sie nacheinander Folgendes ein (nach jeder Zeile `[Enter]` drücken):

```bash
cd ~
mkdir SODA_Umgebungsverwaltung
cd SODA_Umgebungsverwaltung
```
(Zur Erinnerung: `cd ~` bringt Sie in Ihr Home-Verzeichnis, `mkdir` erstellt den neuen Ordner und das zweite `cd` wechselt direkt hinein.)

#### Übung 1: Ein Venv erstellen und aktivieren

Mit einem einfachen Befehl in der Kommandozeile weist das Modul `venv` Python an, einen neuen Ordner in Ihrem aktuellen Verzeichnis zu erstellen. Dieser Ordner enthält eine isolierte Kopie des Python-Interpreters und einen eigenen, leeren Platz für Pakete. 

Lassen Sie uns unsere erste Umgebung namens `venv1` erstellen. Tippen Sie dafür (je nach System):
* Windows: `python -m venv venv1` (oder `py -m venv venv1`)
* Mac/Linux: `python3 -m venv venv1`

Wenn Sie nun `ls`, sehen Sie, dass ein neuer Ordner namens `venv1` aufgetaucht ist. 
Die Umgebung existiert jetzt, aber sie ist noch nicht aktiv. Wir müssen unserem System erst explizit sagen: "Für alle Python befehle, die jetzt kommen, verwende die in diesem Ordner bereitgestellte Python Umgebung und ignoriere den Rest".

Klappen Sie die Anleitung für Ihr System auf und aktivieren Sie `venv1`:

<details>
<summary><b>Windows (PowerShell)</b></summary>

Geben Sie folgenden Befehl ein:
`.\venv1\Scripts\Activate.ps1`

*(Hinweis: Falls eine rote Fehlermeldung erscheint, dass das Ausführen von Skripten deaktiviert ist, müssen Sie dies einmalig erlauben. Öffnen Sie die PowerShell dafür als Administrator und geben Sie ein: `Set-ExecutionPolicy Unrestricted -Scope CurrentUser`, bestätigen Sie mit `J` und versuchen Sie die Aktivierung erneut.)*
</details>

<details>
<summary><b>MacOS / 🐧 Linux</b></summary>

Geben Sie folgenden Befehl ein:
`source venv1/bin/activate`
</details>

**Quiz: Woran erkennen Sie, dass die Umgebung erfolgreich aktiviert wurde?**

[( )] Ein neues Fenster mit einer grafischen Oberfläche öffnet sich.
[(X)] Ganz vorne in meiner Kommandozeile steht nun der Name der Umgebung in Klammern, also `(venv1)`.
[( )] Der Computer gibt einen kurzen Bestätigungston aus.

#### Übung 2: Zweites Venv erstellen und deaktivieren

Mit mehreren, voneinander isolierten Environments können Sie für jedes Forschungsprojekt eine eigene Umgebung erstellen. Versionskonflikte der verwendeten Packages werden damit automatisch vermieden. 

Lassen Sie uns eine zweite Umgebung anlegen. Bevor wir das tun, müssen wir die aktuelle Umgebung jedoch verlassen. 

Geben Sie in Ihr Terminal einfach dieses eine Wort ein:
```bash
deactivate
```
Das `(venv1)` am Anfang Ihrer Zeile verschwindet – Sie sind wieder in Ihrer normalen, globalen Systemumgebung.

Legen Sie nun analog zur ersten Übung ein zweites Environment an und aktivieren Sie es:
1. Erstellen: `python -m venv venv2` (bzw. `python3 ...`)
2. Aktivieren Sie es (denken Sie an den richtigen Pfad, diesmal mit `venv2`).

**Quiz: Umgebung aufräumen**
Was müssen Sie tun, wenn Sie das Projekt zu `venv2` nicht mehr benötigen und restlos von Ihrem Computer entfernen wollen?

[( )] Ich muss ein spezielles Python-Deinstallationsprogramm starten.
[( )] Ich tippe `python -m unvenv venv2`.
[(X)] Ich stelle sicher, dass die Umgebung deaktiviert ist, und dann lösche ich einfach den Ordner `venv2` von meiner Festplatte.

#### Übung 3: Drittes Venv mit einer anderen Python-Version erstellen

Wie in der Einführung gelernt, erfordern manche Projekte ältere oder spezifische Python-Versionen (Multi-Python). Wenn Sie auf Ihrem Betriebssystem mehrere Python-Versionen installiert haben (z.B. 3.9 und 3.12), können Sie beim Erstellen der virtuellen Umgebung gezielt angeben, welche Version als Basis für diesen speziellen "Blumentopf" dienen soll.

*(Hinweis: Für diese Übung setzen wir voraus, dass Sie eine zweite Python-Version auf Ihrem System installiert haben. Wie das geht, können Sie im Kapitel "Python > Installation" nachlesen).*

Um ein Venv mit einer bestimmten Version zu erstellen, rufen Sie einfach exakt diese Version auf, um den `venv`-Befehl auszuführen:

* **Windows:** `py -3.9 -m venv venv3` (ersetzen Sie 3.9 durch Ihre installierte Version)
* **Mac/Linux:** `python3.9 -m venv venv3` 

Aktivieren Sie nun Ihr neues `venv3` (denken Sie daran: bei Windows wieder über `.\venv3\Scripts\Activate.ps1`, bei Mac/Linux über `source venv3/bin/activate`).

**Quiz: Der Versions-Check**
Sie haben `venv3` erfolgreich aktiviert (das `(venv3)` steht vorne in der Zeile). Geben Sie nun einfach den Befehl `python --version` ein. Was fällt auf?

[( )] Er gibt einen Fehler aus, ich muss `python3.9 --version` tippen.
[(X)] Er gibt Version 3.9 (oder die von mir gewählte Version) aus, auch wenn mein System standardmäßig eigentlich eine neuere Version nutzt.
[( )] Er gibt die neueste Version aus, die auf meinem PC installiert ist.


### Alternativen: Conda und Docker

`venv` ist der Standardweg, der für 95 % der Anwendungsfälle in den Digital Humanities und der Datenarbeit völlig ausreicht. Sie werden in freier Wildbahn (vor allem in Forschungs-Papers oder auf GitHub) aber häufig auch über andere Begriffe stolpern, die wir hier kurz einordnen wollen:

**Conda (Anaconda / Miniconda)**
Conda ist ein alternativer, sehr mächtiger Paket- und Umgebungsmanager, der besonders in der Data-Science-Welt beliebt ist.
* Der Unterschied: Während `venv` nur Python-Pakete verwaltet, kann Conda auch systemnahe Bibliotheken (die z.B. in C oder C++ geschrieben sind) mitbringen. Außerdem kann Conda die Python-Basisversionen selbst herunterladen und verwalten. 
* Der Nachteil: Es ist deutlich "schwerfälliger" als `venv`, greift tiefer ins Betriebssystem ein und verlangt für die kommerzielle Nutzung (je nach Version) teils Lizenzen.

**Docker**
Docker spielt in einer ganz anderen Liga. Es virtualisiert nicht nur die Python-Umgebung, sondern gleich ein komplettes, minimales Betriebssystem in einem sogenannten "Container".
* Der Unterschied: Ein Docker-Container bringt vom simulierten Linux-System über Python bis hin zu den Paketen alles mit. Wenn ein Projekt in Docker läuft, läuft es theoretisch auf jedem Computer der Welt absolut identisch (selbst hier bestätigen Ausnahmen die Regel, siehe etwa die Einbindung von Grafikkarten in die Container).
* Der Nachteil: Docker ist für Anfänger deutlich komplexer zu erlernen, benötigt Zusatzsoftware und verbraucht mehr Speicherplatz und Arbeitsspeicher. 

**Weitere Tools (Poetry, uv, etc.)**
Daneben existiert eine Vielzahl an weiteren Tools zur Umgebungsvirtualisierung und zum Paketmanagement. Beliebt sind aktuell besonders [Poetry](https://python-poetry.org/) und das sehr schnelle [uv](https://docs.astral.sh/uv/), die das Management von Paket- und Versionsabhängigkeiten oft noch weiter von der reinen Dateisystem-Ebene abstrahieren. 

Wir beschränken uns hier dennoch ganz bewusst auf das leichtgewichtige, integrierte `venv`. Einerseits, weil keine weitere Software installiert werden muss und es im Regelfall völlig ausreicht. Andererseits, weil gerade im händischen Umgang mit `venv` die grundlegenden Zusammenhänge zwischen Programmumgebung, Dateisystem und Betriebssystem für Einsteiger:innen besonders gut klar und greifbar werden.

### Quiz: Umgebungsvirtualisierung 

**Frage 1: Was unterscheidet laut Text die Ausführungsumgebung eines klassischen, kompilierten Programms (wie Microsoft Word) von der eines Python-Skripts?**

[( )] Kompilierte Programme benötigen zwingend externe Bibliotheken, während Python-Skripte autark laufen.
[( )] Es gibt keinen Unterschied; beide kommunizieren ausschließlich über den Python-Interpreter mit der Hardware.
[(X)] Kompilierte Programme kommunizieren direkt über System Calls mit dem Betriebssystem, während Python-Skripte zusätzliche Schichten (den Interpreter und Python-Bibliotheken) über dem Betriebssystem benötigen.
[( )] Python-Skripte bringen alle benötigten Bausteine bereits in ihrem eigenen Installationsordner mit, während kompilierte Programme das nicht tun.

**Frage 2: Welches genaue Szenario beschreibt das im Text erklärte Problem der "Versionskonflikte"?**

[( )] Zwei unterschiedliche Betriebssysteme versuchen gleichzeitig auf dasselbe Python-Skript zuzugreifen.
[(X)] Projekt A benötigt Paket X in Version 1.0, Projekt B verlangt Paket X in Version 2.0. Bei einer globalen Installation überschreiben sich diese gegenseitig, wodurch eines der Projekte unweigerlich kaputtgeht.
[( )] Eine veraltete Python-Version (z.B. 3.8) kann nicht auf einem modernen Betriebssystem installiert werden.
[( )] GitHub blockiert den Download von Paketen, wenn deren Versionsnummern sich überschneiden.

**Frage 3: Was passiert auf Dateisystem-Ebene exakt, wenn Sie den Befehl `python -m venv venv1` ausführen?**

[( )] Das System lädt die neueste Python-Version aus dem Internet herunter und installiert sie global.
[( )] Es werden alle global installierten Pakete in ein Archiv gepackt, um Platz zu sparen.
[(X)] Es wird ein neuer Ordner erstellt, der eine isolierte Kopie des Python-Interpreters und einen eigenen, leeren Platz für Pakete enthält.
[( )] Die Umgebung wird erstellt und sofort automatisch für die aktuelle Sitzung aktiviert.

**Frage 4: Was ist der primäre technische Effekt, wenn Sie eine virtuelle Umgebung (z.B. über `source venv1/bin/activate` oder `.\venv1\Scripts\Activate.ps1`) aktivieren?**

[(X)] Sie weisen das System an, für alle folgenden Python-Befehle ausschließlich den Interpreter und die Pakete in diesem spezifischen Ordner zu verwenden und den Rest des Systems zu ignorieren.
[( )] Sie starten einen Hintergrunddienst, der automatisch fehlende Pakete von GitHub herunterlädt.
[( )] Sie kompilieren die Python-Textdateien in maschinenlesbaren Code.
[( )] Sie entziehen dem Betriebssystem die Rechte, auf den Projektordner zuzugreifen.

**Frage 5: Sie haben ein Projekt, das zwingend Python 3.9 benötigt. Auf Ihrem Rechner sind global Python 3.9 und 3.12 installiert. Sie erstellen die Umgebung korrekt mit `python3.9 -m venv venv_alt` und aktivieren sie. Was passiert, wenn Sie nun einfach den Befehl `python --version` eintippen?**

[( )] Das System wirft einen Fehler, da Sie zwingend `python3.9 --version` tippen müssen.
[( )] Das System greift auf die Standardversion des Betriebssystems (3.12) zu.
[( )] Das System fragt Sie über ein Pop-up, welche der beiden Versionen Sie nutzen möchten.
[(X)] Das System gibt Version 3.9 aus, da der simple Befehl `python` in einer aktiven Umgebung immer automatisch auf den isolierten Interpreter dieses Venvs umgeleitet wird.

**Frage 6: Wie entfernen Sie eine virtuelle Umgebung (z.B. `venv2`) mitsamt all ihren isolierten Paketen sauber und restlos von Ihrem Computer?**

[( )] Durch die Eingabe des Befehls `python -m unvenv venv2`.
[(X)] Indem Sie sicherstellen, dass die Umgebung deaktiviert ist, und dann einfach den Ordner `venv2` über das Dateisystem oder Terminal löschen.
[( )] Sie müssen das offizielle Python-Deinstallationsprogramm starten.
[( )] Durch die Eingabe von `deactivate --remove venv2`.

**Frage 7: Laut Text ist Conda ein mächtiger alternativer Umgebungsmanager. Welchen entscheidenden technischen Vorteil bietet Conda im Vergleich zum Standard-Tool `venv`?**

[( )] Conda ist direkt in Python eingebaut und benötigt keine zusätzliche Installation.
[(X)] Conda kann nicht nur reine Python-Pakete verwalten, sondern bringt auch systemnahe Bibliotheken (z.B. C/C++) mit und verwaltet die Python-Basisversionen selbst.
[( )] Conda verbraucht deutlich weniger Speicherplatz und Arbeitsspeicher als `venv`.
[( )] Conda abstrahiert die Paketverwaltung komplett vom Dateisystem.

**Frage 8: Warum wird Docker im Text als "in einer ganz anderen Liga spielend" beschrieben?**

[( )] Weil es ausschließlich für die Erstellung von grafischen Benutzeroberflächen gedacht ist.
[( )] Weil es Python-Skripte doppelt so schnell ausführt wie native Umgebungen.
[(X)] Weil es nicht nur die Python-Umgebung isoliert, sondern gleich ein komplettes, minimales Betriebssystem in einem Container virtualisiert.
[( )] Weil es als einziges Tool keine Ausnahmen bei der Portierbarkeit (wie z.B. bei Grafikkarten) zulässt.

**Frage 9: Das Tutorial erwähnt moderne, stark abstrahierende Tools wie Poetry oder uv. Aus welchem didaktischen Grund beschränkt sich dieser Kurs dennoch bewusst auf das integrierte Tool `venv`?**

[( )] Weil Poetry und uv kostenpflichtige Lizenzen erfordern.
[(X)] Weil der händische Umgang mit `venv` die grundlegenden Zusammenhänge zwischen Programmumgebung, Dateisystem und Betriebssystem für Einsteiger:innen besonders greifbar macht.
[( )] Weil `venv` das einzige Tool ist, das in den Digital Humanities verwendet wird.
[( )] Weil moderne Tools wie uv auf Windows-Systemen grundsätzlich nicht funktionieren.

**Frage 10: Der Text nutzt die Metapher eines Gartens. Wenn das Betriebssystem der Garten ist und die virtuelle Umgebung der Blumentopf – was repräsentieren dann logischerweise die "Nährstoffe" oder die "Erde", die exakt auf die Pflanze im Topf abgestimmt werden?**

[( )] Die globalen System Calls des Betriebssystems.
[(X)] Die spezifische Python-Version und die exakten Paket-Versionen (Dependencies), die isoliert im Ordner liegen.
[( )] Die Hardware des Computers (wie RAM oder Festplatte).
[( )] Der Quellcode von GitHub, der den Blumentopf herstellt.


## Paketmanagement mit Pip

Wir haben nun unseren isolierten "Blumentopf" (die virtuelle Umgebung) aufgestellt. Aber er ist noch leer. Er enthält bisher nur das absolute Minimum, nämlich den Python-Interpreter selbst. Wie bekommen wir nun die nützlichen Erweiterungen, die sogenannten Pakete (Packages), in unsere Umgebung?

Hier kommt Pip ins Spiel.

Pip steht (rekursiv) für "Pip Installs Packages" und ist der Standard-Paketmanager für Python. 
Stellen Sie sich Pip wie den App Store auf Ihrem Smartphone oder den zentralen Katalog einer großen Bibliothek vor. Wenn Sie ein bestimmtes Werkzeug für Ihre Forschungsarbeit brauchen (z.B. zur Textanalyse), müssen Sie dieses nicht mühsam manuell im Internet suchen, herunterladen und in die richtigen Ordner kopieren. 

Sie rufen einfach `pip` in der Kommandozeile auf und sagen ihm, was Sie brauchen. Pip verbindet sich dann automatisch mit dem Python Package Index (PyPI), einer zentralen Datenbank für Python-Software, lädt das Paket in der richtigen Version herunter und installiert es.

Wenn Ihre virtuelle Umgebung aktiviert ist (Sie erinnern sich: das `(venv1)` steht vorne in der Zeile), installiert Pip die neuen Pakete ausschließlich in diese Umgebung. Ihr restlicher Computer bleibt völlig unberührt.

### Übung: Pakete installieren und auflisten

Lassen Sie uns das direkt in der Praxis testen. Wir installieren ein Paket namens `cowsay` (eine sprechende Kuh), um den Prozess zu veranschaulichen.

**Schritt 1: Umgebung sicherstellen**
Stellen Sie sicher, dass Sie sich in Ihrer Kommandozeile in Ihrem Übungsordner `SODA_Umgebungsverwaltung` befinden und Ihr `venv1` aktiviert ist (das `(venv1)` muss sichtbar sein!). Falls nicht, aktivieren Sie es wieder (z.B. mit `source venv1/bin/activate` auf Mac/Linux oder `.\venv1\Scripts\Activate.ps1` unter Windows).

**Schritt 2: Das Paket installieren**
Geben Sie nun folgenden Befehl ein und drücken Sie Enter:
```bash
pip install cowsay
```
Sie werden sehen, wie sich Ihre Kommandozeile kurz mit dem Internet verbindet, einige Ladebalken anzeigt und am Ende idealerweise "Successfully installed cowsay..." meldet. 

**Schritt 3: Den Inhalt der Umgebung prüfen (`pip list`)**
Woher wissen wir, was alles in unserem aktuellen "Blumentopf" steckt? Dafür gibt es einen sehr nützlichen Befehl, den Sie im Alltag oft brauchen werden. Geben Sie ein:
```bash
pip list
```
Pip listet Ihnen nun tabellarisch alle installierten Pakete in dieser Umgebung auf. Sie sollten dort die Grundausstattung (wie `pip` selbst) und nun eben auch `cowsay` samt Versionsnummer sehen.

**Schritt 4: Das Paket nutzen**
Da das Paket nun in unserer Umgebung lebt, kann unser Python-Interpreter darauf zugreifen. Wir können die sprechende Kuh sogar direkt über die Kommandozeile aufrufen (da dieses spezielle Paket einen eigenen Kommandozeilenbefehl mitbringt). Tippen Sie:
```bash
cowsay "Hallo aus dem SODa Tutorial!"
```
Wenn alles geklappt hat, grüßt Sie nun eine kleine Kuh aus ASCII-Zeichen direkt im Terminal!

### Übung: Versionskonflikte auflösen

Auch mit korrekt aufgesetzter Python Umgebung und fehlerfreier Bedienung von pip geht manchmal etwas schief. Im Gegenteil, für fast alle, die sich regelmäßig im Python Ökosystem bewegen, sind Versionskonflikte treue Begleiter. Mit etwas Verständnis für die Mechanismen lassen sie sich allerdings häufig unkompliziert beheben. 

Oben haben Sie gelernt, wie Sie mit Hilfe von pip Pakete installieren können. Wenden Sie dieses Wissen nun an, um das Paket mit dem Namen "barplotme" zu installieren und versuchen Sie, das Programm zu starten, indem Sie den Befehl barplotme im Terminal eingeben. Was beobachten Sie?

### Übung: Fehlermeldung interpretieren
Wie Sie richtig erkannt haben, erscheint eine Fehlermeldung. Eine natürliche Reaktion besteht darin, das Projekt als "Funktioniert nicht" abzuhaken und sich mit etwas anderem zu beschäftigen. Doch wir sind stärker als dieses Verlangen! Wir schauen uns die Fehlermeldung an und versuchen zu verstehen, was schiefgelaufen ist und wie wir das Problem beheben könnten. 
Versuchen Sie doch einmal das Problem zu identifizieren. Vielleicht fällt Ihnen ja sogar eine Lösung ein. Falls Sie nicht weiterkommen, klappen Sie gerne den untenstehenden Tipp aus!

<details>
<summary>Tipp</summary>

Die Fehlermeldung weist Sie auf das Fehlen eines Paketes hin. Normalerweise werden alle notwendigen Abhängigkeiten mit pip Paketen mitgeliefert. Es kann allerdings vorkommen, dass besonders nachlässige Entwickler vergessen, die Abhängigkeiten zu spezifizieren. Dann müssen Sie selber aktiv werden. Versuchen Sie doch einmal, das in der Fehlermeldung genannte Paket per pip zu installieren.
<details>
<summary>Psst</summary>

Das fehlende Paket heißt "matplotlib".

Der Befehl um es zu installieren lautet 
`
pip install matplotlib
`
</details>

</details>

### Quiz: Paketmanagement

**Frage 1: Was passiert, wenn Sie vergessen, Ihr `venv` zu aktivieren, bevor Sie den Befehl `pip install cowsay` ausführen?**

[( )] Der Befehl schlägt sofort fehl und gibt eine Fehlermeldung aus, dass keine Umgebung gefunden wurde.
[( )] Pip erstellt automatisch im Hintergrund eine neue Umgebung und installiert das Paket dort.
[(X)] Das Paket wird global auf Ihrem Computer installiert und landet im großen, systemweiten "Topf".

**Frage 2: Welche Funktion hat das barplotme Paket, das Sie in der Übung installiert haben**

[( )] Es öffnet eine Oberfläche zur Erstellung verschiedener Diagramme.
[( )] Gar keine, es lässt sich nämlich nicht öffnen.
[(X)] Es zeichnet ein Balkendiagramm aus übergebenen Zahlen.

**Frage 3: Wofür steht die Abkürzung PyPI, mit der sich Pip bei der Installation verbindet?**

[(X)] Python Package Index
[( )] Python Programming Interface
[( )] Python Package Installer
[( )] Python Project Integration

**Frage 4: Sie führen den Befehl `pip list` in einer frisch erstellten und aktivierten Umgebung aus, *bevor* Sie eigene Pakete installieren. Was erwarten Sie als Ausgabe?**

[(X)] Eine kurze Liste, die nur die absolute Grundausstattung wie `pip` selbst anzeigt.
[( )] Eine komplett leere Tabelle, da noch nichts installiert wurde.
[( )] Eine Liste aller Pakete, die jemals auf diesem Computer heruntergeladen wurden.
[( )] Eine Fehlermeldung, da der Befehl nur funktioniert, wenn mindestens ein externes Paket installiert ist.

**Frage 5: Warum kam es bei der Installation von `barplotme` zu einer Fehlermeldung beim Starten, obwohl der `pip install`-Befehl selbst erfolgreich durchlief?**

[( )] Weil `barplotme` eine veraltete Python-Version benötigt.
[( )] Weil das Paket absichtlich als Virus programmiert wurde.
[(X)] Weil die Entwickler vergessen haben, eine benötigte Abhängigkeit (in diesem Fall `matplotlib`) in den Paketinformationen zu hinterlegen, sodass Pip sie nicht automatisch mitinstalliert hat.
[( )] Weil das Paket global installiert wurde und nicht in der virtuellen Umgebung.

## Open Source Projekte 

Wir können nun in der Kommandozeile navigieren, Python-Interpreter steuern, sichere Umgebungen (Venvs) anlegen und Pakete mit Pip installieren. Aber wo finden wir nun die versprochenen Open Source Projekte, die wir bei uns selbst installieren können um uns das Leben zu erleichtern?

Der Quellcode der Projekte selbst liegt meistens auf sogenannten Code Repositories. Von denen ist das von Microsoft betriebene GitHub das bekannteste, deswegen werden wir uns im Folgenden darauf konzentrieren. 

Im Sinne der Datenautonomie lohnt es sich allerdings darauf hinzuweisen, dass neben GitHub auch weitere, teilweise nichtkommerzielle Repositories wie [GitLab](https://about.gitlab.com/) oder [Codeberg](https://codeberg.org) existieren. Auch wenn sich aktuell GitHub als De-Facto Standard etabliert hat, ist die Existenz dieser Alternativen extrem wichtig, insbesondere angesichts aktueller politischer Entwicklungen in den USA.

### GitHub: Die Bibliothek für den Quellcode

[GitHub](https://github.com/) ist die weltweit größte Plattform zur Speicherung und gemeinsamen Entwicklung von Software. Neben dem Quellcode liegen dort insbesondere auch Anleitungen, wie die Software installiert und verwendet werden kann.

Der Name setzt sich aus zwei Teilen zusammen:
* Git: Das ist das eigentliche, unsichtbare Werkzeug (ein "Versionskontrollsystem"), das jede kleine Änderung am Code dokumentiert – ähnlich wie die "Änderungen nachverfolgen"-Funktion in Word, nur für hunderte Dateien gleichzeitig.
* Hub: Die zentrale Webseite, die diesen Code für alle Welt sichtbar und durchsuchbar macht.


#### Standardinstallation
Wenn Sie ein spannendes Projekt auf GitHub finden (z.B. ein Tool zur Datenbereinigung), scrollen Sie immer zuerst nach unten zur Datei `README.md`. Das ist die Bedienungsanleitung des Projekts. 

Im besten Fall sind die Projekte auf PyPI veröffentlicht und lassen sich einfach über pip installieren, dann lässt sich die Installationsanleitung häufig auf das Anlegen einer virtuellen Umgebung und die Installation des richtigen Pip Paketes herunterbrechen. 
Die Fähigkeiten dafür haben wir oben bereits erlernt: mit der Installation von [Cowsay](https://github.com/piuccio/cowsay) oder [barplotme](https://github.com/mathiaszinnen/barplotme), deren Quellcode und Installationsanweisungen auch jeweils über GitHub zugänglich sind.

#### Editierbare Installation 
Wenn das nicht der Fall sein sollte, oder der Code geändert werden soll, muss das Projekt auf den eigenen Rechner kopiert ("geklont") werden, um es lokal zu installieren. 
> Obacht! Für die folgenden Schritte ist eine Installation von Git nötig. Unter Linux und MacOS sollte Git vorinstalliert sein. Unter Windows können Sie der Installationsanleitung von [Git-for-Windows](https://git-scm.com/install/windows) folgen.
Als Beispiel nehmen wir das Barplotme Paket. Angenommen wir wünschen uns ein aussagekräftigeres Label für unseren Barplot als "Fancy Bar Plot" (schwer vorstellbar, aber hypothetisch denkbar), dann können wir das Paket mit Folgenden Kommandos im Terminal lokal installieren.
```bash
git clone 
cd 
pip install -e .
```
Das `-e` Argument hinter `pip install` macht die Installation `editable`, was bedeutet, dass Änderungen des Quellcodes im Projektordner direkt in die virtuelle Umgebung übernommen werden. Das `.` übernimmt die Funktion des Paketnames und verweist auf den aktuellen Ordner, der anstelle eines von PyPI heruntergeladenen Pakets als installiert werden soll.


Nun können wir den Code anpassen, etwa indem wir die `plot.py` Datei im Unterordner `src` (für source - Quellcode) ändern: Wenn wir dort in Zeile 13 die Zeichenkette 'Fancy Bar Plot' ersetzen, wird dementsprechend ein anderer Titel generiert. 
Probieren Sie es doch mal aus.

![barplot](res/barplot.png "Von dem Paket barplotme generiertes Balkendiagramm mit sehr gutem Label")

### Linklisten und Softwareübersichten
Aber woher bekomme ich nun die ganzen versprochenen Modelle? Auf GitHub liegen ja Millionen von Projekten, wie soll ich da den Überblick behalten?

#### Zum Einstieg Awesome Lists
![Awesome Logo](res/logo.svg "Awesome list of awesome lists logo, credit to Sindre Sorhus [awesome repository on GitHub](https://github.com/sindresorhus/awesome)" )
Verzagen Sie nicht, es gibt kuratierte Listen für alle möglichen Anwendungen von Bildverarbeitung und Maschinellem Lernen. Weil es so großartig ist, dass sich Menschen um die Kuration dieser Listen kümmern, heißen sie "awesome". Wenn Sie etwa nach Techniken zur automatischen Texterkennung (OCR) suchen, suchen Sie doch einfach mal "awesome ocr" auf der Suchmaschine ihrer Wahl. 

Zum Einstieg finden Sie hier eine massiv unvollständige Zusammenstellung von awesome Listen zu gängigen Themen in der Sammlungsdigitalisierung 

| Thema | Link | 
| --- | --- |
| OCR | https://github.com/zacharywhitley/awesome-ocr |
| Objekterkennung | https://github.com/XiongweiWu/Awesome-Object-Detection |
| Sprachverarbeitung | https://github.com/keon/awesome-nlp |
| LLMs | https://github.com/hannibal046/awesome-llm |

Auf GitHub findet sich sogar eine [Awesome Liste aller Awesome Listen](https://github.com/sindresorhus/awesome), stöbern Sie doch einfach mal herum. 

#### Für Experten: HuggingFace und andere Aggregatoren

Die aktuellsten und stärksten Algorithmen finden sich inzwischen vor allem auf [HuggingFace](https://huggingface.co/). 
Ein Klick auf Models zeigt Ihnen nach verschiedenen Anwendungen sortierte Algorithmen, die häufig mit Codebeispielen und Installationsanweisungen versehen sind. 
Der Einstieg ist etwas komplizierter und setzt meist Python Grundkenntnisse voraus, aber es lohnt sich, sich in das System einzuarbeiten. 

Speziell für die Bildverarbeitung empfehlen sich mit Microsofts [OpenMMLab](https://github.com/open-mmlab) Projekte. Allerdings ist die Einstiegshürde hier etwas höher als bei Huggingface. 
Etwas einfacher ist die Verwendung von [Ultralytics YOLO](https://docs.ultralytics.com/), einem Framework für verschiedene Bilderkennungsaufgaben, aber insbesondere zur Objektdetektion.
 
Wenden Sie sich vertrauensvoll an den SODa Helpdesk, wenn Sie Unterstützung benötigen -- wir helfen gerne!

### Quiz: Open Source Projekte 

Prüfen wir zum Abschluss, ob die Zusammenhänge zwischen den Plattformen, Werkzeugen und lokalen Installationen sitzen!

**Frage 1: Was genau bewirkt der Punkt (`.`) im Befehl `pip install -e .` während einer editierbaren Installation?**

[( )] Er zwingt Pip dazu, alle versteckten Dateien im Ordner mitzuinstallieren.
[(X)] Er verweist auf das aktuelle Verzeichnis, welches anstelle eines regulären PyPI-Pakets installiert werden soll.
[( )] Er steht für "everything" und installiert automatisch alle Pakete, die das Projekt benötigt.
[( )] Er deaktiviert die Versionskontrolle von Git für diesen spezifischen Installationsvorgang.


**Frage 2: Sie haben das Paket "barplotme" via `pip install -e .` installiert. Anschließend ändern Sie im Quellcode ein Text-Label ab. Was ist der nächste zwingende Schritt, damit das Python-Skript den neuen Titel ausgibt?**

[( )] Sie müssen das Paket mit `pip uninstall` entfernen und danach neu installieren.
[( )] Sie müssen den Befehl `pip install -e .` noch einmal ausführen, um die Änderung zu kompilieren.
[(X)] Gar nichts. Da das Paket "editable" installiert wurde, wird die Änderung im Quellcode bei der nächsten Ausführung sofort wirksam.
[( )] Sie müssen die Änderung zuerst mit Git bestätigen und ins Internet hochladen, bevor Pip sie erkennt.



**Frage 3: Warum wird im Text explizit auf Alternativen wie GitLab oder Codeberg hingewiesen, obwohl sich GitHub als De-Facto-Standard etabliert hat?**

[( )] Weil GitHub ausschließlich für proprietäre (geschlossene) Software genutzt werden darf.
[(X)] Um Aspekte der Datenautonomie angesichts kommerzieller und politischer Entwicklungen zu betonen.
[( )] Weil die Editierbare Installation auf GitHub technisch blockiert wird.
[( )] Weil große KI-Modelle von HuggingFace nur über Codeberg heruntergeladen werden können.



**Frage 4: Welche der folgenden Aussagen beschreibt das Verhältnis zwischen Git und GitHub am präzisesten?**

[( )] Git ist die Programmiersprache, in der die Projekte geschrieben sind, und GitHub ist der Server, der sie ausführt.
[( )] Git ist die zentrale Webseite für Open Source, während GitHub das Tool auf dem lokalen Rechner ist.
[(X)] Git dokumentiert lokale Code-Änderungen als Versionskontrollsystem, GitHub macht diese Dateien global im Netz sichtbar und durchsuchbar.
[( )] Beide Begriffe sind Synonyme für dasselbe Microsoft-Produkt zur Paketverwaltung.



**Frage 5: Sie suchen nach bewährten Open-Source-Tools zur automatischen Spracherkennung. Was ist laut Text der effizienteste erste Suchansatz?**

[(X)] Eine Suchmaschine nach Begriffen wie "awesome speech recognition" durchsuchen.
[( )] Den Suchbegriff `pip install speech` auf gut Glück im Terminal eingeben.
[( )] Die Datei `README.md` auf der Startseite von GitHub lesen.
[( )] Den Quellcode von "cowsay" auf GitHub analysieren.



**Frage 6: In welchem Fall ist eine "Editierbare Installation" (inkl. lokalem Klonen via Git) einer regulären Standardinstallation (direkt über Pip) zwingend vorzuziehen?**

[( )] Wenn Sie sicherstellen wollen, dass keine schädliche Software installiert wird.
[(X)] Wenn das Paket nicht auf PyPI verfügbar ist oder Sie die interne Funktionsweise des Codes selbst umschreiben möchten.
[( )] Wenn Sie Speicherplatz auf Ihrer Festplatte sparen möchten.
[( )] Wenn Sie das Paket in einer virtuellen Umgebung (Venv) nutzen wollen.


**Frage 7: Welche wesentliche Neuerung brachte die Plattform "Hugging Face" in das Open-Source-Ökosystem, wodurch sie sich von klassischen Code-Repositories unterscheidet?**

[( )] Sie erlaubt als erste Plattform das lokale Klonen von Projekten via Git.
[(X)] Sie ist ein Hub speziell für maschinelles Lernen, auf dem neben dem Code vor allem die riesigen, fertig trainierten KI-Modelle ("Gehirne") gehostet werden.
[( )] Sie bietet grafische Benutzeroberflächen an, sodass man für KI-Modelle keine Python-Kenntnisse mehr benötigt.
[( )] Sie löst das PyPI-Register komplett ab und ist der neue Standard für alle Pip-Installationen.


**Frage 8: Wie ordnet der Text die beiden Frameworks "OpenMMLab" und "Ultralytics YOLO" bezüglich ihrer Nutzungshürde für Bildverarbeitung ein?**

[( )] OpenMMLab gilt als deutlich einfacher und ist speziell für absolute Programmieranfänger konzipiert.
[( )] Beide Tools können komplett ohne Terminal bedient werden.
[( )] YOLO ist ausschließlich für Textverarbeitung gedacht, während OpenMMLab Bilder verarbeitet.
[(X)] OpenMMLab erfordert eine etwas höhere Einarbeitungszeit, während Ultralytics YOLO als einsteigerfreundlichere Alternative für Objektdetektion empfohlen wird.

**Frage 9: Welche Voraussetzung muss auf einem Windows-Rechner zwingend erfüllt sein, bevor Sie den Befehl `git clone` erfolgreich nutzen können?**

[( )] Sie müssen zuvor mit `pip install git` das Paket aus dem PyPI-Register laden.
[(X)] Das eigenständige Werkzeug "Git" muss auf dem Betriebssystem vorab installiert sein (z.B. via Git-for-Windows).
[( )] Sie müssen zwingend auf GitHub eingeloggt sein.
[( )] Die virtuelle Umgebung (Venv) muss zwingend vorher aktiviert werden.


**Frage 10: Ein Forschungstool ist offiziell über PyPI ("Standardinstallation") verfügbar. Was bedeutet dies konkret für Ihren Workflow?**

[(X)] Sie sparen sich den manuellen Download via `git clone` und können das Tool direkt über einen einfachen Pip-Befehl in Ihr Venv laden.
[( )] Sie müssen den Quellcode nach dem Klonen nicht mehr selbst kompilieren.
[( )] Das Tool kann nicht in einer virtuellen Umgebung installiert werden, sondern erfordert Root-Rechte.
[( )] Die `README.md` Datei fehlt bei diesen Projekten grundsätzlich.


## TLDR
Terminal
------------
Starten, je nach Betriebssystem

<details>
<summary>Windows</summary>
1. Powershell [Installieren](https://learn.microsoft.com/de-de/powershell/scripting/install/install-powershell?view=powershell-7.6) 
2. Im Startmenü `Powershell` eingeben.
</details>

<details>
<summary>MacOS</summary>
1. Spotlight Suche öffnen, z.B. mit Tastenkombination `[cmd] + [Leertaste]` 
2. `Terminal` eigeben
</details>

<details>
<summary>Linux</summary>
- Unter Ubuntu mit Gnome/KDE Tastenkombination `[Strg] + [Alt] + [T]`
- Alle anderen: RTFM
</details>

**Navigieren**

| Befehl | Beschreibung |
| --- | --- | 
| ls `<dir>` | Zeige Dateien in `<dir>` |
| cd `<dir>` | Wechsel in Verzeichnis `<dir>` |
| mkdir `<name>` | Lege Verzeichnis `<name>` an |
| mv `<old>` `<new>` | Benenne Datei `<old>` in `<new>` um, bei Eingabe von Pfaden wird die Datei verschoben |
| rm `<datei>` | entferne Datei `<datei>`, `-r` für Verzeichnisse |
| cp `<datei>` `<pfad>` | Kopiere `<datei>` nach `<pfad>`, `-r` für Verzeichnisse |

| Pfad | Beschreibung |
| --- | --- |
| Beginnend `/`, `~` oder Laufwerkbezeichnung (windows) | Absoluter Pfad |
| sonst | Relativer Pfad |
| `.` | Aktuelles Verzeichnis |
| `..` | Elternverzeichnis |
| `~` | Home-Verzeichnis |
| `/` | Wurzelverzeichnis|


Python
---------

Installieren, je nach Betriebssystem 
<details>
<summary>Windows</summary>
1. Python install manager von [Python.org](https://www.python.org/) herunterladen. 
2. Im terminal: `py -V:<VERSION>`, z.B. `py -V:3.11`  
</details>
<details>
<summary>MacOS</summary>
1. [Homebrew]() installieren
2. Pyenv installieren: `brew install pyenv`
3. Im terminal: `pyenv install <VERSION>`, z.B. `pyenv install 3.11`
</details>
<details>
<summary>Linux</summary>
Installation über Systemweiten Paketmanager, z.B. `apt-get install python3.11`
</details>


Venv
---------
Umgebung erstellen mit `python -m venv <PFAD>`, z.B. `python -m venv .venv`. 
Aktivieren, je nach Betriebssystem:
<details>
<summary>Windows</summary>
`<PFAD>/Scripts/Activate.ps1`, z.B. `.venv/Scripts/Activate.ps1`
</details>
<details>
<summary>MacOS/Linux</summary>
`source <PFAD>/bin/activate`, z.B. `source venv.bin/activate`
</details>


Pip
---------
| Befehl | Beschreibung |
| ---- | ---- |
| `pip install <PACKAGE>` | Installiert das Paket <PACKAGE> im aktivierten venv, z.B. `pip install cowsay` |
| `pip list` | Gibt alle installierten Pakete des aktiven venv aus |




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

License: CC-BY 4.0

---


weitere Tutorials und Open Educational Resources: https://sammlungen.io/kb

---

![Finanziert von der Europäischen Union](res/FinanziertVonDerEU.jpg)

![Gefördert durch: Bundesministerium für Forschung, Technologie und Raumfahrt](res/BMFTR_de_Web_RGB_gef_durch.jpg)