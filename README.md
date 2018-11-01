Mario Fentler 5CHIT  
Übung vom 25.10.2018  
# syt5-gk912-visualisierung

__Ziel__ dieser Übung ist es __ein übersichtliches HMI zu erstellen__, auf dem der Mitarbeiter im vorbeigehen sehen kann, wie der Zustand der Maschine ist.  

Unter __HMI__ versteht man ein "Human Maschine Interface"

## __Vorraussetzung__
- Codesys
- Übung 1 Tankentleerung (auf dieser Übung wird weiter aufgebaut)

## __Aufgabenstellung__
Teste Programm und Visualisierung nach jeder Teilaufgabe ausführlich auf korrekte Funktion. Alle ursprünglichen Funktionen dürfen durch Änderungen nicht „beschädigt“ werden.  
Entscheide an welcher Stelle des Projektes Programmänderungen sinnvoll unterzubringen sind und begründe deine Entscheidung im Protokoll.

## __Aufgabendurchführung__
### __Visualisierungen erstellen__
Um eine Visualisierung zu erstellen -> __Rechte Maustaste__ auf __Application__ -> __Objekt hinzufügen__ -> __Visualisierung__.  
Daraufhin muss man einen Namen vergeben und das Visualisierungsfenster wird geöffnet.  

__!Wichtig!__ (Objektbibliotheken auf aktiv setzen, um schon vordefinierte Objekte zu haben)

### __Task1__
_"Erzeuge eine Visualisierung mit drei Schaltergrafiken für S1,S2,S3 und einer gelben Signallampe für V5. Diese soll leuchten, wenn V5 geöffnet ist und nicht leuchten wenn V5 geschlossen ist._  
_Die Visualisierungen sollen für einen Bildschirm mit 1024x768px gestaltet werden und „selbsterklärend“ sein, d.h. Gestaltung und Beschriftungen sollen dem Anwender des HMI helfen die Tankanlage einfach bedienen zu können."_

Die __Größe der Visualisierung__ lässt sich mit einem Doppelklick auf "TargetVisu" und dann unter den Skalierungsoptionen einstellen.  

Um die Aufgabe zu lösen werden 3 Kippschalter aus der __Objekt Bibliothek__ auf der rechten Seite gewählt (Lampen/Schalter/Bilder Section).  
<p align="center">
<img src="images/objektBib.png" alt="Objektbibliothek"/>
</p>

In den __Einstellungen__ wählt man dann als __Variable__ die Variable s1, für den Schalter, aus dem Programm aus.
<p align="center">
<img src="images/schalter_einst.PNG" alt="Einstellungsmöglichkeiten am Kippschalter"/>
</p>
Nachdem man die 3 Schalter und die LED für die Visualisierung des Ventil5 gesetzt hat und die Applikation dann ausführt, kann man sehen, dass die LED leuchtet sobald ein Schalter umgeschaltet wird.  
<p align="center">
<img src="images/erg_vis1.png" alt="Schaltung1 visualisiert"/>
</p>

### __Task2__
_Erweitere die Visualisierung um einen Taster, der den Sensor S7 (Überlauf) simulieren soll,  sowie um ein Standardisiertes Ventilsymbol für V9 (Einlaufventil), das bei geöffnetem Ventil grün und bei geschlossenem Ventil weiß angezeigt wird (Rand ist immer schwarz)._

Dazu wählt man aus der Objektbibliothek (siehe Bild) einen Taster aus (in diesem Beispiel wird zwecks der Überprüfung ein weiterer Kippschalter genommen). Diesem weist man die __Überlaufssensorvariable s7__ zu.  

__Damit das funktioniert__ muss zuerst der Code aus dem strukturierten Text File von der Vorübung __entfernt werden__. Denn dieser überprüft ob die Maximalwasserhöhe erreicht ist und setzt die Variable dementsprechend.  

Als Symbol für das Einlaufventil V9 wird ein Polygon verwendet, das im __aktiven__ Zustand __grün__ und im __passiven__ Zustand __weiß__ gefüllt sein soll. Der Rand soll immer Schwarz sein. (alle 8 Sekunden für 5 Sekunden aktiv außer Überlaufsensor s7 aktiv)  

Dem Polygon weißt man die Variable unter "__Filter/Eingabe__"  und die Farben über "__Filter/Farben__" zu.

<p align="center">
<img src="images/visual2.png" alt="Visualisierung2"/>
</p>

### __Task3__
_Um den Füllstand des Tanks zu visualisieren müssen im Projekt Kenngrößen nachgerüstet werden. Diese sollen sich in der Visualisierung bearbeiten lassen:_  

- __die Tankkapazität (in l):__  
einstellbar mit Eingabefeld zwischen 50 und 500 l  
- __die Füllgeschwindigkeit (in l/s):__  
einstellbar mit Schieberegler zwischen 10 und 40 l/s  
- __die Entleerungsgeschwindigkeit (in l/s):__  
einstellbar mit Schieberegler zwischen 8 und 20 l/s  

Für diesen Task müssen ein Eingabefeld und zwei Schieberegler zur HMI hinzugefügt werden. Diese findet man unter den __allgemeinen Steuerelementen__ (unsichtbare Eingabe und Schieberegler)  

#### __Schieberegler__
Bei den Schiebereglern kann man den Skalabegin und das Skalaende in den Einstellungen festlegen. Weiters kann man auch Einstellen, dass die Skala angezeigt wird.  
Die Regler können dann so aussehen:  
<p align="center">
<img src="images/schieberegler.png" alt="Schieberegler"/>
</p>

Um diese Regler in der Applikation zu verwenden muss man ihnen auch eine Variable zuweisen. Diese Variable wird im "TankManager" Programm hinzugefügt.  
Dieses Programm ist ein neues, welches das Befüllen und das Entleeren des Tanks für uns übernehmen soll.  

Die Variablen der Schieberegler sind __REAL__ Werte. Das sind Werte, mit denen man __Gleitkommazahlen__ darstellen kann.  

Als letzte Einstellung wird beim Schieberegler noch das Kästchen __"zum Klick springen"__ aktiviert, da man so die Userbility des Programms steigern kann.

#### __Eingabefeld__
Für das Eingabefeld wird ein __"unsichtbares Eingabefeld"__
ausgewählt. Man kann das leider nicht auf visible setzen.  
Aus diesem Grund habe ich als "Workaround" das Kästchen mit Linien eingerahmt.

In diesem Feld wird die Eigenschaft __"OnClick"__ konfiguriert. Dort wählt man folgende Optionen:  
<p align="center">
<img src="images/onClickEingabe.png" alt="OnClickEingabe"/>
</p>

__WICHTIG:__  
Man muss eine Variable zur Bearbeitung eingeben (diese wird zuerst auch noch im Programm deklariert). Ansonsten funktioniert es nicht. Um dann im laufenden Programm eine Eingabe zu machen klickt man in das Textfeld und gibt einen Wert zwischen Min(50) und Max(500) ein.  
Wenn der Wert größer oder kleiner ist, dann kann die Eingabe nicht gesetzt werden.  

Das kann dann so aussehen:  
<p align="center">
<img src="images/visualisierungEingaben.png" alt="Visualisierung Eingaben"/>
</p>

### __Task4__
_Der aktuelle Füllstand soll über ein Zeigerinstrument visualisiert werden (0 – Tankkapazität in l). Passe nun das Projekt so an, dass der aktuelle Füllstand korrekt aktualisiert wird, wenn Einlauf- und Entleerungsventile geöffnet/geschlossen werden._  
_Es darf idealisiert angenommen werden, dass die Ventile unmittelbar (in einem Zyklus) den Durchfluss beeinflussen (100% → 0 und umgekehrt)._

Das Zeigerelement ist unter dem Reiter __"Messgeräte"__ zu finden. Als Skala-Maximum wählt man die Variable für den __Maximalinhalt des Tanks__, die wir vorher erstellt haben.

Bei diesem Element gibt es die Option __"Variable"__ nicht. Stattdessen wird hier die Option __"Wert"__ verwendet. Dort gibt man eine Variable für den aktuellen Tankinhalt an, der dann durch den Zeiger visualisiert wird.  
Weiters kann man sich mit den Einstellungen von dem Zeigerelement spielen und auch dem __Maximum__ die Variable geben, die man im Eingabefeld "Tankkapazität" eingegeben hat.  
<p align="center">
<img src="images/zeiger.png" alt="Einstellungen am Zeigerobjekt"/>
</p>

Weiters wird in dem neuen Programm "TankManager" die Befüllungs- und Entleerungslogik eingebaut.

#### __Task4 - Programmierung__
Zunächst muss im "FillTank" Programm noch ein weiterer Timer eingebaut werden, der als __Trigger zum Befüllen/Entleeren des Tanks__ wirkt. Dieser schaltet alle 100ms auf True.  
Dieser Timer wird in ein __neues Netzwerk__ eingefügt (siehe Bild).  
<p align="center">
<img src="images/timer.png" alt="Neuer Timer"/>
</p>

Im "TankManager" wird jetzt der Code hinzugefügt, der die Ventile überprüft und gegebenenfalls den __Tank befüllt/entleert oder beides gleichzeitig__.

__Variablen des Programms:__

    PROGRAM TankManager
    VAR
        ventil9 : BOOL;
        ventil5 : BOOL;
        fillTankTimer : BOOL;
        
        maxTank : INT := 250;
        fuellGeschwindigkeit : REAL := 10;
        entleerGeschwindigkeit: REAL := 8;
        aktuellerTankInhalt : REAL := 0;
    END_VAR 

__Variablenzuweisung:__  
Um auf Variablen aus anderen Programmen zuzugreifen muss man es nach der Deklaration im Code machen, so wie im nachfolgenen Code-Snippet ersichtlich.  
Man kann die Variablen nicht direkt bei der Deklaration auf Werte aus anderen Programmen setzen, das funktioniert aus welchem Grund auch immer nicht.  

    ventil9 := Programm3_FillTank.v9;
    ventil5 := Programm4_EigenerFUP.Ventil5;
    fillTankTimer := Programm3_FillTank.fillTankTrigger;
__Tankbefüllung/Entleerung:__   
Hier wird mit IF/ELSE Statements der Zustand der Ventile abgefragt und dann gegebenenfalls die Aktionen durcheführt. Das geschieht __im Takt des Timers__, den wir gerade vorher erstellt haben.

    //Wenn nur das Einlaufventil(v9) geöffnet ist
    IF (ventil9 = TRUE AND fillTankTimer = TRUE AND NOT ventil5 = TRUE) THEN
        aktuellerTankInhalt := aktuellerTankInhalt + fuellGeschwindigkeit;
    ELSIF (ventil9 = TRUE AND ventil5 = TRUE AND fillTankTimer = TRUE) THEN
        IF (aktuellerTankinhalt + fuellGeschwindigkeit - entleerGeschwindigkeit < 0) THEN
            //Weniger als 0 geht nicht
            aktuellerTankInhalt := 0;
        ELSE
            aktuellerTankInhalt := aktuellerTankinhalt + fuellGeschwindigkeit - entleerGeschwindigkeit;
        END_IF
    ELSIF (ventil5 = TRUE AND fillTankTimer = TRUE AND NOT ventil9 = TRUE) THEN
        IF ((aktuellerTankinhalt - entleerGeschwindigkeit) < 0) THEN
            aktuellerTankinhalt := 0;
        ELSE
            aktuellerTankinhalt := aktuellerTankinhalt - entleerGeschwindigkeit;
        END_IF
    END_IF

### __Task5__
_Um den Überlauf zu simulieren, wird ein zweites „Überlaufsignal“ S8 eingeführt, das dann aktiviert wird, wenn der Tank zu 95% voll ist. Ein Überlauf wird signalisiert, wenn S7 (durch Taster simuliert) oder S8 melden. Ein Überlauf soll durch eine rote Signallampe visualisiert werden._

Dazu wird eine neue rote Lampe in die Visualisierung eingebaut. Diese bekommt als Variable "S8" für den Überlauf.  
Bei der wird dann der aktuelle Tankinhalt in relation zum maximalen Inhalt berechnet. Wenn das mehr als 95% sind oder der Überlaufsensor s7 true ist, dann Leuchtet die Lampe.

    IF(aktuellerTankInhalt >= maxTank/100*95) THEN
        s8 := TRUE;
    ELSE
        s8 := FALSE;
    END_IF

    IF(s8 = TRUE OR gvl.s7 = TRUE) THEN
        ueberlaufLampe := TRUE;
    ELSE
        ueberlaufLampe := FALSE;
    END_IF

### __Task6__
_Stelle den Tank visuell dar. Die Darstellung soll zu jedem Zeitpunkt den aktuellen Füllstand des Tanks grafisch maßstabsgetreu proportional wiedergeben. Befüllung und Entleerung sollen ebenso visuell ansprechend sichtbar gemacht werden._

Um den __Tankinhalt zu visualisieren__ werden zwei Rechtecke verwendet. Das eine, mit einer blauen Füllfarbe, die die Flüssigkeit im Tank realisieren soll.  
Den beiden Rechtecken wird ein __Y-Wert für die Relative Bewegung__ zugewiesen um die Größe der Rechtecke im Code bestimmen zu können.

- Rechteck 1: Y = __-__ maximaler Tankinhalt
- Rechteck 2: Y = __-__ aktueller Tankinhalt

Dabei ist zu beachten, dass die __Werte negiert werden müssen__ wie man oben entnehmen kann. Das muss man machen, damit das Rechteck __nach oben und nicht nach unten "wächst"__.  
<p align="center">
<img src="images/rechteck.png" alt="Einstellungen am Rechteck"/>
</p>

## __Ergebnis__
Die fertige Visualisierung kann dann so aussehen:  
<p align="center">
<img src="images/visFertig.png" alt="Visualisierung fertig"/>
</p>

## __Probleme und Lösungen__
- __Tankbefüllung/-entleerung:__  

Ich habe es sehr schwierig gefunden, den Tank richtig zu befüllen. Denn, wenn das Einlassventil 5 Sekunden lang offen ist und die Einlassgeschwindigkeit bei 10l/s liegt, dann sollte nach den 5 Sekunden ja auch 50 Liter im Tank sein.  
Das funktioniert aber nicht.

Grund dafür sind die Zeiten, die das Programm zum Berechnen, umschalten der Zustände, etc. braucht.  

Ich habe es nicht geschafft, dass die Werte genau sind. Sie sind aber angenähert zum richtigen Ergebnis.

- __Visualisierung des Tankinhalts:__

Zuerst wusste ich nicht ganz wie ich das machen sollte.  
Dann bin ich durch einen Tipp eines Mitschülers drauf gekommen, dass man das ganze mit 2 Rechtecken gut realisieren kann.

## __Quellen__
[1] https://infosys.beckhoff.com/index.php?content=../content/1031/tcplccontrol/html/tcplcctrl_iec_operators_overview.htm&id=8653966830076413975  
[2] https://infosys.beckhoff.de/index.php?content=../content/1031/tcplccontrol/html/tcplcctrl_languages%20st.htm&id=5754912264349492758  