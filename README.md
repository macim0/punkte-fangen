# Punkte Fangen Einführung


## ~ @unplugged
Es soll ein Spiel programmiert werden.
Ziel des Spieles: Sammle so viele Punkte wie möglich ein, indem du den Calliope neigst.
![Hindernislauf](https://github.com/macim0/punkte-fangen/blob/master/punkte-fangen.gif?raw=true)


## Schritt 1: Erstelle eine Spielfigur
Als erstes erstellen wir uns eine ``||Variables: Variable||`` namens ``||Variables: Spielfigur||``. 
Diese kommt in den Block ``||basic: Beim Start|``.
```blocks
let Spielfigur: game.LedSprite = 0
```

## Schritt 2: Einen Sprite auf die Variable speichern
Im Bereich ``||game: Spiel||``, welcher unter ``|advanced: Fortgeschritten|`` zu finden ist, wird mit den sogenannten Sprites gearbeitet. 
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
Jetzt ist es an dir, dieses Tutorial zu verlassen und in den Editor zu wechseln. <br>
Füge dort eventuell einen weiteren Punkt dem Programm hinzu und lass diese ``||basic: Dauerhauft||`` und immer wieder neu auf der Anzeige, wenn du einen Punkt berührt hast. <br>
Überlege dir eine Bedingung, wann das Spiel vorbei ist und finde eine Möglichkeit Punkte zu verteilen. 




## Als Tutorial verwenden

Dieses Repository kann als **Tutorial** für MakeCode verwenden.

öffne dazu den Link: [https://makecode.calliope.cc/#tutorial:https://github.com/macim0/punkte-fangen]


> Diese Seite bei [https://macim0.github.io/punkte-fangen/](https://macim0.github.io/punkte-fangen/) öffnen


