# enhanced_webui
## Enhanced WebUI Addon


Enhanced WebUI ergänzt die vertraute OpenCCU-Weboberfläche um Funktionen, die das Bearbeiten und Dokumentieren von Programmen erleichtern: Programmlogik per Drag and Drop sortieren, Skripte mit Autovervollständigung bearbeiten und einzelne Programmteile mit Infotexten versehen. Dazu kommen verbesserte Listen, eine mobile Ansicht und ein optionales Dark Theme.

Die Erweiterungen lassen sich einzeln einschalten. **Nach der Installation sind alle elf Funktionen deaktiviert.** Du kannst mit einer einzelnen Funktion beginnen und die Oberfläche Schritt für Schritt ausprobieren.

Das Addon wurde ausschließlich mit agentischer KI (GPT-6.1 Sol Medium-Hoch, Gemini 4 Argon) erstellt. Das Addon hat über 300 automatisierte Regressionstestfälle erfolgreich durchlaufen.
Händisch wurde das Addon auf einer Test CCU sowie später auf meiner Live CCU erfolgreich getestet. Logs wurden erfolgreich auf Warnungen und Fehler überprüft - keine Auffälligkeiten.

#### Dennoch: Die Nutzung dieses Addons erfolgt ausschließlich auf eigene Gefahr. Ich übernehme keinerlei Haftung für Schäden, Datenverlust oder Fehlfunktionen, die durch die Ausführung dieses Addons entstehen. Vor dem Aktivieren der Funktionen empfiehlt es sich stets ein Backup zu erstellen!

## Funktionen

- **Programmlogik sortieren:** Ganze „WENN“- und „SONST, WENN“-Zweige sowie Bedingungen, logische Gruppen und Aktivitäten per Drag and Drop verschieben. Der abschließende „SONST“-Zweig bleibt fest an seiner Position.
- **Erweiterter Skripteditor:** Vorschläge für ReGa-Funktionen, Methoden, lokale Variablen, Geräte, Kanäle und Systemvariablen. Dazu Einrückungslinien und Markierungen von Fehlerzeilen nach der vorhandenen Fehlerprüfung.
- **Infotexte in Programmen:** Zweige, Bedingungen und Aktivitäten direkt mit Erläuterungen versehen – bis zu 2000 Zeichen je Textfeld. Ein grünes i kennzeichnet vorhandenen Text. Programmname und Beschreibung lassen sich ebenfalls im Textdialog bearbeiten.
- **Favoriten sortieren:** Favoritenlisten und ihre Einträge per Drag and Drop umordnen. Die ursprünglichen Pfeiltasten bleiben verfügbar; am Listenrand wird beim Ziehen automatisch gescrollt.
- **Benutzerkonto verbessern:** Die Systemvariablen der Startseite per Drag and Drop sortieren. Der Benutzerkonto-Dialog passt in das Browserfenster und lässt sich unten rechts in der Größe verändern.
- **Programm-IDs anzeigen:** Die interne ID als zusätzliche Spalte in der Programmübersicht einblenden.
- **Speicherzeit anzeigen:** Die vom Addon erfasste letzte Speicherung eines Programms anzeigen. Vor der Erfassung liegende Änderungen bleiben „unbekannt“.
- **Filter und Listensortierung verbessern:** Bereits während der Eingabe suchen, mehrere Spalten einbeziehen, Suchspalten auswählen und den Suchbegriff mit einem Klick löschen. Ein Trichter kennzeichnet einen aktiven Filter. Programme lassen sich zusätzlich nach Aktivstatus filtern und nach Name, Beschreibung, ID oder erfasster Speicherzeit sortieren. Unterstützte weitere Listen umfassen unter anderem Geräte, Kanäle, Systemvariablen, Räume, Gewerke und die Favoritenübersicht.
- **Programme mit Infotexten drucken:** Eine zusätzliche Druckansicht ergänzt die beiden ursprünglichen Druckfunktionen. Dafür ist eine angepasste, kompatible Fassung des Addons **hm-print** mit Unterstützung für die Infotexte erforderlich. Die Versionsnummer allein ersetzt diesen Kompatibilitätsnachweis nicht.
- **Mobile Ansicht:** Kompakte Kopfleiste mit aufklappbarem Menü, drei Darstellungsgrößen und angepasste Skriptdialoge. Ein Vollbildschalter steht bei entsprechender Browserunterstützung zur Verfügung; breite Tabellen und die Fußleiste lassen sich seitlich verschieben.
- **Theme-Auswahl:** Zwischen Original und Dark wechseln. Der blaue Kopfbereich bleibt erhalten, dunkle Flächen werden abgestuft dargestellt. Die Einstellungsseite des Addons behält ihr helles Design.

## Programmlogik sortieren

Bei größeren Programmen ist die gewünschte Reihenfolge oft erst nach dem Anlegen aller Bedingungen klar. Enhanced WebUI ergänzt dafür Greifpunkte im vorhandenen Programmeditor. So lassen sich Zweige samt ihren zugehörigen Bedingungen und Aktivitäten per Drag and Drop umordnen, ohne sie von Hand neu anzulegen.

<img width="505" height="454" alt="program_sorting" src="https://github.com/user-attachments/assets/5213157f-07e5-49c4-b972-1683ae5f6716" />

### Funktion

- Die Sortierung arbeitet **auf der Bearbeitungskopie des geöffneten Programms**. Der Server prüft, ob die betroffenen Elemente zu einer gültigen Editor-Arbeitskopie gehören.
- Für Bedingungen, Gruppen und Aktivitäten wird die Reihenfolge der vorhandenen Objektreferenzen geändert. Bei ganzen Zweigen werden native ReGa-Kopierfunktionen verwendet; Skripte und Zeitmodule werden nicht aus dem angezeigten Beschreibungstext neu erzeugt.
- Vor dem Schreiben werden IDs, erlaubte Reihenfolgen und die erwartete Ausgangsstruktur geprüft. Eine gültige Reihenfolge muss jedes betroffene Element genau einmal enthalten. Passt die Struktur nicht mehr, wird die Änderung abgewiesen.
- Nach dem Schreiben folgen Bestätigungsprüfungen. Bei Fehlern versucht die serverseitige Sortierlogik, den vorherigen Zustand wiederherzustellen. Eine unbestätigte Änderung wird als Fehler gemeldet und darf nicht einfach als erfolgreich behandelt werden.
- Die Darstellung wird anschließend über die vorhandenen Funktionen des WebUI-Editors neu geladen. Ein erfolgreicher Sortiervorgang bleibt mit einem Speicherhinweis sichtbar.

**Mit „OK“ wird das bearbeitete Programm gespeichert. Mit „Zurück“ wird die Programmbearbeitung einschließlich der noch nicht bestätigten Sortierungen verworfen.** Einen zusätzlichen Undo-Verlauf gibt es nicht.

Bedingungen bleiben in ihrer logischen Gruppe, Gruppen im selben Zweig und Aktivitäten in ihrer bisherigen Aktionsliste. Ein freies Verschieben zwischen unterschiedlichen Zweigen ist nicht vorgesehen. Der bedingungslose „SONST“-Abschluss bleibt am Ende; seine vorhandenen Aktivitäten können innerhalb dieser Liste sortiert werden.

### Die Reihenfolge ist Teil der Logik

Eine andere Zweigreihenfolge kann das Verhalten eines Programms bewusst verändern: Treffen mehrere Bedingungen zu, entscheidet der erste passende Zweig.

Beispiel: Zweig A prüft `Eingang >= 10`, Zweig B prüft `Eingang >= 20`. Bei einem Eingangswert von 25 passen beide. Steht A vor B, greift A; steht B vor A, greift B. Das ist der Grund, nach dem Umordnen passende Testwerte zu prüfen – auch wenn die zugehörigen Bedingungen, Skripte und Zeitmodule korrekt erhalten wurden.

## Erweiterter Skripteditor

Der Skripteditor wird sowohl unter **„Skript testen“** als auch beim Bearbeiten einer **Skript-Aktivität im Programm** ergänzt. Die vorhandenen Funktionen wie Syntax-Highlighting, Suche, Einrückung und Klammerhilfe bleiben verfügbar.

<img width="300" height="300" alt="scripteditor" src="https://github.com/user-attachments/assets/2010d688-a708-47d0-9c6e-724d60687450" />

- Vorschläge über **Strg+Leertaste** öffnen; in der mobilen Ansicht steht dafür auch eine Schaltfläche bereit. Mit den Pfeiltasten auswählen und mit Enter übernehmen.
- ReGa-Funktionen und Methoden werden durch einen lokalen Vorschlagskatalog ergänzt. Lokale Variablennamen werden aus dem bisher eingegebenen Skript ermittelt.
- Geräte, Kanäle und Systemvariablen werden über lesende Abfragen aus der angemeldeten Zentrale geladen. Bei Kanalvorschlägen erscheinen zusätzlich Gerätename, Adresse und Objekt-ID.
- Einrückungslinien machen verschachtelte Blöcke sichtbar. Im Dark Theme sind Kommentare farblich vom übrigen Code abgesetzt.
- Meldet die vorhandene Fehlerprüfung eine eindeutig zuordenbare Zeile, wird diese direkt im Code markiert. Meldungen ohne eindeutige Zeilenangabe werden nicht auf eine beliebige Codezeile übertragen.

Technisch wird der vorhandene CodeMirror-Editor um Vorschläge und Darstellungsfunktionen ergänzt. In der geprüften WebUI kommt CodeMirror 5.65.21 zum Einsatz. Das Addon bringt außerdem einen Adapter für seine alternative Editor-Einbindung mit; daraus ergibt sich keine pauschale Kompatibilitätszusage für andere WebUI-Versionen.

**Die Autovervollständigung führt keine Skripte aus.** Die Vorschläge sind eine Schreibhilfe, keine vollständige ReGa-Analyse und keine Prüfung der fachlichen Logik. Ausgeführt wird weiterhin über die vorhandenen WebUI-Funktionen. „Skript testen“ ist dabei kein isolierter Simulator: Ein ausgeführtes Skript kann echte Geräte und Systemvariablen verändern.

Nach dem Aktivieren dieser Funktion einen bereits geöffneten Skripteditor einmal schließen und neu öffnen.

## Infotexte und mobile Ansicht

Infotexte helfen, Entscheidungen direkt am betreffenden Programmteil festzuhalten: Warum steht ein Zweig zuerst? Weshalb wird eine Verzögerung verwendet? Welche Ausnahme soll die Bedingung abdecken?

<img width="348" height="248" alt="infotext" src="https://github.com/user-attachments/assets/12b64bff-081f-46b8-98f9-34d768c1a9e8" />
 
Die Texte werden in eigenen Metadaten des Addons gespeichert und nicht als zusätzliche ausführbare Skripte in die Programmlogik eingefügt. Die Speicherung der Infotexte erfolgt nach der nativen Programmspeicherung; eine dabei gemeldete Fehlermeldung sollte deshalb gesondert geprüft werden. Über **„Alle Infotexte aufklappen“** lassen sich die vorhandenen Erläuterungen gemeinsam anzeigen.

Die mobile Ansicht reduziert den Platzbedarf des Kopfbereichs und passt die Bedienung an kleinere Bildschirme an. Die gewohnte WebUI bleibt dabei erkennbar.

<img width="263" height="468" alt="mobile1" src="https://github.com/user-attachments/assets/99d0b419-ae83-4199-8c03-96ec04023e91" />
<img width="263" height="468" alt="mobile2" src="https://github.com/user-attachments/assets/b2b5299f-c926-452d-81c9-118e6d8d714e" />

## Favoritenlisten und Favoriten sortieren

Favoritenlisten und die darin enthaltenen Favoriten lassen sich über die zusätzlichen Greifpunkte per Drag and Drop verschieben. Die bisherigen Pfeiltasten bleiben erhalten und können parallel verwendet werden. Eine Einfügemarkierung zeigt die geplante Position.

Die Erweiterung verwendet die vorhandenen Favoritenobjekte. Vor einer Änderung wird die Ausgangsreihenfolge gelesen und beim Speichern mit der erwarteten Reihenfolge verglichen. Hat sich die Liste zwischenzeitlich verändert, soll die Sortierung nicht auf einem veralteten Stand weiterschreiben.

**Die Reihenfolge wird sofort gespeichert.** Anders als bei der Programmbearbeitung gibt es hier kein zusätzliches „OK“, mit dem der Vorgang erst bestätigt würde. Ein späteres „Zurück“ macht eine bereits gespeicherte Favoritensortierung nicht rückgängig.

## Benutzerkonto: Startseitenvariablen und Dialoggröße

Im Benutzerkonto-Dialog kann man nun, neben den bisherigen Pfeiltasten, die Systemvariablen auf der Startseite per Drag and Drop sortieren. Damit lässt sich beispielsweise eine häufig benötigte Statusvariable direkt an den Anfang der Liste verschieben.

Für die Reihenfolge werden nacheinander die vorhandenen nativen Sortierschritte verwendet. Der nächste Schritt beginnt erst, nachdem die erwartete Reihenfolge in der neu geladenen Tabelle sichtbar ist. Wird ein Schritt nicht bestätigt, hält die Erweiterung an. Bereits bestätigte Schritte bleiben gespeichert.

**Die Reihenfolge wird sofort gespeichert.** Die Sortierfunktion ändert weder die Werte der Systemvariablen noch Benutzername, Passwort oder Berechtigungen des Kontos.

Das Fenster kann zusätzlich über einen Ziehpunkt unten rechts in der Größe verändert werden.

## Programmübersicht: IDs und letzte Speicherung

Zwei unabhängig schaltbare Zusatzspalten helfen bei der Zuordnung von Programmen:

- **Programm-ID:** Zeigt die interne Objekt-ID. Sie ist beispielsweise beim Vergleichen mit ReGa-Skripten oder Diagnoseausgaben hilfreich.
- **Zuletzt gespeichert:** Zeigt die vom Addon erfasste letzte erfolgreiche WebUI-Speicherung des Programms. Diese Erfassung wird an den Abschluss des vorhandenen Speichervorgangs angebunden.

Für Programme ohne erfassten Speichervorgang steht „unbekannt“.

<img width="375" height="95" alt="id_savetimestamp" src="https://github.com/user-attachments/assets/d8c30fb1-54a1-44ab-8f4a-04c9518564a4" />

## Verbesserte Filter und Listensortierung

Eine zusätzliche Suchleiste ist in diversen Tabellen-Dialogen sichtbar (u.a. Programme oder Systemvariablen).

- **Live-Suche:** Bereits während der Eingabe wird nach dem Suchbegriff gesucht.
- **Spaltenübergreifend suchen:** In der Programmübersicht können Name, Beschreibung, Bedingungen und Aktivitäten gemeinsam durchsucht werden.
- **Suchbereich eingrenzen:** Über die Spaltenauswahl festlegen, welche unterstützten Spalten bei der Suche berücksichtigt werden sollen.
- **Programmstatus auswählen:** Alle Programme, nur aktive oder nur deaktivierte Programme anzeigen (Auswahl steht nur im Programm-Dialog).
- **Sortierrichtung erkennen:** Pfeilsymbole machen die auf- und absteigende Sortierung sichtbar.
- **Nach Programm-IDs und Speicherzeiten sortieren:** In der Programmübersicht lassen sich neben Name und Beschreibung auch die eingeblendete Programm-ID und die erfasste Speicherzeit verwenden. Unbekannte Speicherzeiten bleiben am Ende.

Die Funktion steht in den Systemvariablen-, Favoriten-, Geräte-, Kanal-, Raum- und Gewerkenamensdialogen zur Verfügung. Unter „Status und Bedienung“ können Geräte und die zugehörige Kanalliste getrennt gefiltert werden. Es handelt sich um eine Suche innerhalb der jeweils geladenen Liste, nicht um eine globale Suche durch sämtliche Konfigurationsdaten der Zentrale.

## Programme einschließlich Infotexten drucken

Voraussetzung für diese Funktion ist eine angepasste, kompatible Version des Addons **hm-print**. Das ursprüngliche [hm-print Addon](https://github.com/homematic-community/hm-print) unterstützt die neuen Infotexte nicht. Ist diese Version nicht installiert, so stehen lediglich die gewohnten Druckfunktionen **„Drucken“** und **„Drucken inkl. Interne“** zur Verfügung.

Ist die kompatible Version installiert, so öffnet die zusätzliche Schaltfläche **„Drucken mit Infotexten“** im Programm-Dialog eine Druckansicht in einem neuen Browser-Tab. Sie ergänzt die Programme um die separat gespeicherten Infotexte (siehe oben).

## Theme-Auswahl: Standard (hell) und dunkel

Nach Aktivierung der Theme-Auswahl in den Einstellungen des Addons erscheint **„Theme wechseln“** im Kopfbereich neben „Geräte anlernen“ (oben rechts). Die Auswahl zwischen Standard und Dunkel wird im jeweiligen Browser gespeichert. Verschiedene Browser können deshalb unterschiedliche Themes verwenden.

Das dunkele Theme passt helle Flächen, Menüs, Bedienelemente und unterstützte Dialoge an. Der blaue Kopfbereich bleibt erhalten.

Wird die Theme-Funktion deaktiviert oder das Addon deinstalliert, so verwendet das System wieder das helle Originaldesign. Die Theme-Auswahl ist rein optischer Natur und verändert keine Geräte-, Programm- oder Variablenwerte.

<img width="253" height="86" alt="theme1" src="https://github.com/user-attachments/assets/071ff27d-a196-4160-a8e5-e34a79934867" />
<img width="212" height="185" alt="theme2" src="https://github.com/user-attachments/assets/0567dc32-8c06-446c-8665-caa83f6d4e0c" />


*Alle Abbildungen wurden lokal mit dem Addon, Original-WebUI-Stilen und erfundenen Beispieldaten erstellt. Sie zeigen keine private Installation. Die Screenshots dienen der Funktionsdarstellung und sind kein Nachweis eines Live-Tests auf einer Zentrale.*

## Installation und erster Test

Vor dem Aktivieren der Funktionen empfiehlt es sich stets ein Backup zu erstellen!

1. Das Installationspaket `enhanced-webui-<Version>.tar.gz` aus den [Releases](https://github.com/unbox-digital-printing/enhanced_webui/releases) herunterladen. 
2. Das Paket unter **Einstellungen → Systemsteuerung → Zusatzsoftware** hochladen und installieren.
2.1. Die WebUI neu laden, am Desktop beispielsweise mit **Strg+F5**.
3. **Enhanced WebUI** in der Systemsteuerung öffnen oder in der Zusatzsoftwareverwaltung **„Einstellen“** wählen.
4. Gewünschte Funktion aktivieren und **„Einstellungen speichern“** anklicken.

**Alle Funktionen starten ausgeschaltet.** Die Schaltflächen „Alle aktivieren“ und „Alle deaktivieren“ ändern die Auswahl. Das abschließende Speichern übernimmt die Änderungen auf der Zentrale.

Für den Einstieg bieten sich unkritische Funktionen, wie Theme-Auswahl, mobile Ansicht und Infotexte an. Die Sortierung lässt sich anschließend an einer Kopie eines Programms (ggf. mit Dummy-Systemvariablen erproben). Prüfe die Kopie vor dem Speichern darauf, dass sie keine Geräteaktionen, Benachrichtigungen oder produktiven Skriptaufrufe enthält.

<details>
<summary>Einstellungsseite anzeigen</summary>

<img width="403" height="476" alt="image" src="https://github.com/user-attachments/assets/f60269b1-1b6e-47e3-b520-c211a1a47d34" />

*Die abgebildete Auswahl ist ein Beispiel. Nach der Installation sind alle Schalter aus.*

</details>

## Was wird wann gespeichert?

| Bereich | Speicherverhalten |
| --- | --- |
| Programmsortierung und Texte im Programmeditor | Die Programmbearbeitung über das originale „OK“ abschließen - mit „Zurück“ verwerfen. Infotexte werden separat durch das Addon gespeichert. |
| Favoriten und Favoritenlisten | Die Reihenfolge wird sofort gespeichert. |
| Systemvariablen-Reihenfolge im Benutzerkonto | Die Reihenfolge wird ohne Bestätigung durch „OK“ sofort gespeichert; verwendet werden bestätigte native Sortierschritte. |
| Addon-Einstellungen | Erst „Einstellungen speichern“ übernimmt die Auswahl. |
| Theme und mobile Darstellungsgröße | Die Auswahl wird im jeweiligen Browser gespeichert - die Funktionen müssen zentral aktiviert sein. |

## Einbindung, Abschalten und Deinstallation

Enhanced WebUI liegt unter `/usr/local/addons/ewebui`. Die Einbindung verwendet einen eigenen Lighttpd-Include. Originale WebUI-Skriptdateien werden unverändert durchgereicht und um den Lader der Erweiterung ergänzt. Die Installation verwendet einen geprüften, sanften Webserver-Reload und löst selbst keinen CCU-Neustart aus.

Serverseitige Änderungen über die Addon-Schnittstelle verlangen eine gültige Sitzung und Administratorrechte. Die Objektabfragen für Skriptvorschläge lesen Informationen.

Jede Funktion lässt sich wieder abschalten. Bei ausgeschalteten Schaltern bleiben der Einstellungszugang und die Prüfung der hm-print-Erreichbarkeit vorhanden.

Die Deinstallation erfolgt über die Zusatzsoftwareverwaltung. Eine bereits geladene Oberfläche erkennt die bestätigte Deinstallation über einen verbleibenden Status-Endpunkt und ruft die normale WebUI-Abmeldung auf. Das wird regelmäßig sowie bei Rückkehr zum Browserfenster geprüft. In inaktiven Tabs können Browser die Prüfung verzögern. Vorhandene Metadaten und Durchreich-Endpunkte werden bei der Deinstallation nicht vollständig entfernt.

## Voraussetzungen und Teststand

Dokumentationsstand: **Enhanced WebUI 1.0.0**.

Entwickelt im Umfeld von **[OpenCCU](https://github.com/OpenCCU) 3.89.11.20260919**. Die aktuellen lokalen Prüfungen verwenden Original-WebUI-CSS, Prototype und CodeMirror 5.65.21. Sie decken unter anderem Sortierabläufe mit nachgebildeten nativen Antworten, Touch-Bedienung, Dialoggrößen, Filter sowie Installation und Deinstallation ab.

Die Kombination aus nativen WebUI-Funktionen und strukturellen Prüfungen soll das Ausprobieren nachvollziehbar machen. Sie ist keine Garantie gegen Fehler. Insbesondere gibt es für die aktuelle Version keine pauschale Freigabe für andere Firmware-Versionen. Neue Funktionen daher zunächst mit Beispieldaten beziehungsweise Testprogrammen prüfen.

## Rückmeldungen

Fehler und Verbesserungsvorschläge können über die [Issues](https://github.com/unbox-digital-printing/enhanced_webui/issues) gemeldet werden. Hilfreich sind Addon-Version, OpenCCU-Version, Browser, betroffene Ansicht und eine kurze Beschreibung der Schritte. Screenshots bitte ohne Sitzungsadressen, Passwörter oder andere private Daten bereitstellen.

## Autor und Hinweise

(c) 2026 Stefan Kemper

Enhanced WebUI ist eine unabhängige Erweiterung der vorhandenen WebUI. Für mitgelieferte Fremdkomponenten gelten deren jeweilige Lizenzhinweise.

Die Nutzung dieses Addons erfolgt ausschließlich auf eigene Gefahr. Der Autor übernimmt keinerlei Haftung für Schäden, Datenverlust oder Fehlfunktionen, die durch die Ausführung dieses Addons entstehen.
