# Hindernislauf Einführung


## ~ @unplugged
Es soll ein Hindernislauf programmiert werden.
Ziel des Spieles: Sammle möglichst viele Punkte indem du mit den Tasten A und B den Hindernissen ausweichst, welche vom oberen Bildschirmrand nach unten bewegt werden.
![Hindernislauf](https://github.com/r00b1nh00d/Spiele_Programmieren_Lernen_Hindernislauf/blob/master/HindernislaufGIF.gif?raw=true)


## Schritt 1: Erstelle eine Spielfigur
Als erstes erstellen wir uns eine ``||Variables: Variable||`` namens ``||Variables: Spielfigur||``. 
Diese kommt in den Block ``||basic: Beim Start|``.
```blocks
let Spielfigur: game.LedSprite = 0
```

## Schritt 2: Einen Sprite auf die Variable speichern
Im Bereich ``||game: Spiel||`` was unter ``|advanced: Fortgeschritten|`` zu finden ist, wird mit den sogenannten Sprites gearbeitet. 
Diese Sprites sind wie Spielsteine oder Spielfiguren. Sie besitzen eine Position (eingeteilt in X von links nach recht und Y von oben nach unten),
 eine Blickrichtung, eine Helligkeit und sie können blinken.  <br>
Wir brauchen aus dem Bereich ``||game: Spiel||`` den Block ``||game: erzeuge Sprite an Position x y ||``. Dieser wird in den Block ``||Variables: Setze Variable auf||`` geschoben.
Jetzt sollte im Simulator eine LED in der Mitte des Calliope Displays leuchten.

```blocks 
let Spielfigur = game.createSprite(2, 2)
```

## Schritt 3: Bewegen der Spielfigur
Nun wollen wir die Spielfigur bewegen. 
Dazu benötigst du aus dem Bereich ``||Input: Eingabe mehr||`` den Block ``||Input: Rotation (°) rollen||``, 
``||math: runden||``,  ``||math: verteile 0 von niedrig 0 von hoch 1023 zu niedrig 0 zu hoch 4  ||`` und 
``||game: Sprite setze x auf 0 ||``. Nun muss ``||math: runden||`` in ``||game: Sprite setze x auf 0 ||`` geschoben werden.
Der Block ``||math: verteile 0 von niedrig 0 von hoch 1023 zu niedrig 0 zu hoch 4  ||`` muss in das ``||math: runden||`` eingefügt werden.
Abschließend wird ``||Input: Rotation (°) rollen||`` in das erste Feld des ``||math: verteile 0 von niedrig 0 von hoch 1023 zu niedrig 0 zu hoch 4  ||``
eingefügt und wir ändern die Werte "von niedrig" auf -32 und "von hoch" auf 32. <br>
Das gleiche muss für ``||game: Sprite setze y auf 0 ||`` gemacht werden. Hierfür benötigen wir ``||Input: Rotation (°) Winkel||``.

```blocks
basic.forever(function () {
    Spielfigur.set(LedSpriteProperty.X, Math.round(Math.map(input.rotation(Rotation.Roll), -32, 32, 0, 4)))
    Spielfigur.set(LedSpriteProperty.Y, Math.round(Math.map(input.rotation(Rotation.Pitch), -32, 32, 0, 4)))
})
let Spielfigur = game.createSprite(2, 2)
```

## Schritt 4: Der Punkt
Nun benötigen wir noch ein Ziel. Dafür erstellen wir eine neue Variable (``||Variables: Punkt||``) und erzeugen einen Sprite 
(``||game: erzeuge Sprite an Position x y ||``). Außerdem lassen wir das Ziel blinken, dafür ändern wir ``||game: Punkt setze x auf 0 ||``
auf ``||game: Punkt setze blinken auf 250 ||``. 

```blocks
basic.forever(function () {
    Spielfigur.set(LedSpriteProperty.X, Math.round(Math.map(input.rotation(Rotation.Roll), -32, 32, 0, 4)))
    Spielfigur.set(LedSpriteProperty.Y, Math.round(Math.map(input.rotation(Rotation.Pitch), -32, 32, 0, 4)))
})
let Spielfigur = game.createSprite(2, 2)
let Punkt = game.createSprite(2, 2)
Punkt.set(LedSpriteProperty.Blink, 250)
```

## Schritt 5: Der springende Punkt
Als letztes muss der Punkt wegspringen, wenn die Spielfigur ihn erreicht. Hierfür müssen wir erstmal erkennen, dass die Spielfigur und der Punkt
sich berühren. Dafür benötigen wir aus dem Bereich ``||logic: Logik||`` den Block ``||logic:Wenn dann||`` und aus dem ``||game: Spiele ||`` Bereich 
den Block ``||game: Sprite berührt ||``. Der zweite muss in den "Wenn"-Bereich eingefügt werden. Außerdem müssen die ``||Variables: Punkt||`` und 
``||Variables: Spielfigur||`` in die Bedingung eingefügt werden. <br>
In den "Dann"-Bereich (also wenn die Spielfigur den Punkt berührt) wird der ``||Variables: Punkt||`` auf eine zufällige neue Position gesetzt.
Hierfür müssen wir ``||math: wähle zufällige Zahl zwischen 0 und 4||`` in den Block ``||game: Sprite setze x auf 0 ||`` einsetzen. 


```blocks
basic.forever(function () {
    Spielfigur.set(LedSpriteProperty.X, Math.round(Math.map(input.rotation(Rotation.Roll), -32, 32, 0, 4)))
    Spielfigur.set(LedSpriteProperty.Y, Math.round(Math.map(input.rotation(Rotation.Pitch), -32, 32, 0, 4)))
    if (Spielfigur.isTouching(Punkt)) {
        Punkt.set(LedSpriteProperty.X, randint(0, 4))
        Punkt.set(LedSpriteProperty.Y, randint(0, 4))
    }
})
let Spielfigur = game.createSprite(2, 2)
let Punkt = game.createSprite(2, 2)
Punkt.set(LedSpriteProperty.Blink, 250)
```

## ~avatar avatar @unplugged
Unter : [https://github.com/r00b1nh00d/Spiele_Programmieren_Lernen_Hindernislauf/blob/master/KurzHilfeSpiele.pdf](https://github.com/r00b1nh00d/Spiele_Programmieren_Lernen_Hindernislauf/blob/master/KurzHilfeSpiele.pdf) <br>
findest du auch nochmal eine kurze Übersicht zu den Befehlen aus dem Bereich ``||game: Spiele||``. <br>
Jetzt ist es an dir dieses Tutorial zu verlassen und in den Editor zu wechseln. <br>
Füre dort die Hindernisse 1 bis 3 dem Programm hinzu und lass diese ``||basic: Dauerhauft||`` und immer wieder neu auf der Anzeige des @boardname@ von oben nach unten bewegen. <br>
Berührt ein Hindernis die Spielfigur ist das Spiel vorbei. Sind die Hindernisse am unteren Rand angelangt sollen sie erneut an ``||maths:zufälliger||`` Stelle auftauchen und ein Punkt vergeben werden. Über eine Zeiteinstellung mittels ``||basic:pausiere||`` kannst du die Schwierigkeit einstellen. 




## Als Tutorial verwenden

Dieses Repository kann als **Tutorial** für MakeCode verwenden.

öffne dazu den Link: [https://makecode.calliope.cc/#tutorial:https://github.com/macim0/Spiele_Programmieren_Lernen_Hindernislauf]


> Diese Seite bei [https://macim0.github.io/punkte-fangen/](https://macim0.github.io/punkte-fangen/) öffnen

## Als Erweiterung verwenden

Dieses Repository kann als **Erweiterung** in MakeCode hinzugefügt werden.

* öffne [https://makecode.calliope.cc/](https://makecode.calliope.cc/)
* klicke auf **Neues Projekt**
* klicke auf **Erweiterungen** unter dem Zahnrad-Menü
* nach **https://github.com/macim0/punkte-fangen** suchen und importieren

## Dieses Projekt bearbeiten ![Build Status Abzeichen](https://github.com/macim0/punkte-fangen/workflows/MakeCode/badge.svg)

Um dieses Repository in MakeCode zu bearbeiten.

* öffne [https://makecode.calliope.cc/](https://makecode.calliope.cc/)
* klicke auf **Importieren** und dann auf **Importiere URL**
* füge **https://github.com/macim0/punkte-fangen** ein und klicke auf Importieren

## Blockvorschau

Dieses Bild zeigt den Blockcode vom letzten Commit im Master an.
Die Aktualisierung dieses Bildes kann einige Minuten dauern.

![Eine gerenderte Ansicht der Blöcke](https://github.com/macim0/punkte-fangen/raw/master/.github/makecode/blocks.png)

#### Metadaten (verwendet für Suche, Rendering)

* for PXT/calliopemini
<script src="https://makecode.com/gh-pages-embed.js"></script><script>makeCodeRender("{{ site.makecode.home_url }}", "{{ site.github.owner_name }}/{{ site.github.repository_name }}");</script>
