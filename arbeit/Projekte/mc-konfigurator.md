RUN

sass --watch scss/konfigurator.scss build/css/konfigurator.css
OR
sass --watch scss/app.scss build/css/app.css

node tools/listener.js



- Sollen wir nicht wissen in welchem Land will ein Kund die Garage bauen?
 - Nein, wir können es mit P


- teils fadeout funktionert nicht [x]
- zurück Knopf soll opacity nicht die Farbe wechseln [x]
- FadeIn und Out soll nur den Inhalt und Titel wechseln [x]
- Progress bar soll langsamer wechseln [x]
- dynamish die Grösse von dem Fenster wechselt []
    - zu schwierig :/
- bug in Bildschirm contactForm [x]
- bug wenn ich zu schnell klicke [x]
- Die Zeichnung auf der letzten Folie soll nach recht verschieben werden. [x]
- Schmeiß das Check box auf dem ContactForm Bildshirm [x]
- Hinzufügt das Checkbox zu Formularseite [x]


Probleme mit zurück Knopf:
- wenn ich den Konfigurator eintrette mit nachvorne Knopf, gibt es keinen Name in Url []
- 


1. Offnen:
    1. der Konfigurator aufmachen, wenn es **noch nicht geöffnet wurde** 
        - Ein State wird zu dem History **mit URL parameter** hinzugefügt [x]
    2. der Konfigurator aufmachen, wenn es **schon geöffnet wurde** 
        - Ein State wird zu dem History **mit URL parameter** hinzugefügt [x]

2. Schlissen:
    1. wenn man das **Kreuz** oder **Außer** klickt
        - Ein State wird zum History **ohne URL parameter** hinzugefügt [x]

3. Bewegung nach vorne:
    1. nach vorne in Konfigurator
        - Das State wird zum **nächsten Bildshirm URL** geändert [x]

5. Nachvorne Knpopf im Browser:
    - wenn man den Konfigurator versucht, zu verlassen geht man zurück

4. Bewegung zurück (Beide züruck Knopf in dem Konfigurator und in Browser):
    - wenn der Konfigurator geöffnet ist
        1.  wenn es noch Schritte davor gibt
            - Das State wird zum **lätzten Bildshirm URL** geändert [x]
        2.  wenn es keinen Schritt davor gibt
            - Es kommt in History **ohne URL Parameter** zurück [x]
    - wenn der Konfigurator geschlossen ist
        3. kommen wir zu dem Konfigurator zurück
            -  Es kommt in History **mit einem Schritt URL Parameter** zurück [x]




TODO:
    - für die Großraumgaragen soll kein Schritt für die Schwingtor sein
    - die lange Frage zu den Architekt soll gelöscht werden
    - Wandfelder multichoice screen
    - In Form Bildschirm ist das Ort nicht geschickt 