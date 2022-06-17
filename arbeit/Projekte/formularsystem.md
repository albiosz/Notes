HOW TO RUN?
	- frontend
		- Führ in git bash aus
	- backend
		- pipenv <- readme
		- Erstellt eine Datei .env und schreig da DEBUG=True


Backend

1. Ich kann die daten ohne login fetchen
- http://localhost:5000/forms/get_form/8319e8e5-02f6-493a-a72e-defe128cc3ad/11111
2.

Frage an Philip
- Wir haben ein Problem mit Cors. Ich kann nicht von meinem PC mit richtigen Daten anmelden.
	- Es gibt einen Fehler von Backend Seite [x]
		- RuntimeError: Cannot reopen a client instance, once it has been closed.
		- Es passiert nur auf der localhost Seite
	- Es gibt CORS fehler von Frontend Seite [x]
		- Es passiert nur auf der localhost Seite


- Was es passiert, was ich mit Debugger gesehen habe
	- Das Frontend schickt eine Anfrage an localhost:5000/get_token
	- Die Anfrage wird angenommen
	- Von Lokal Datenbank wird ein User genommen.
	- eine Anfrage an https://api.leadwiesel.de/

- Warum sind zwei Anfrage geschickt werden? [x]
	- Es gab eine auf Form und zweite auf Button
	- Es geht um die Umsetzung Eigenschaften, deswegen weiss ich nicht 

- Wie kann ich am Besten den System wechseln
	- Als ich jetzt denke, wäre es am Besten, um extra SCSS klasses hinzufügen und Genehmingungsystem zu verbesern



- forms.py @router.post("/sign_form/{form_id}/{zipcode}") <- da ist die Email mit Daten generiert
	- Ich muss irgendwie erkennen, ob ich mit Optima formular or Mc-Vetrieb handle


- Ich habe die Namen von den Dataien gewechselt, so passt es für beide Versionen aber ich weiß nicht genau wie dass pdf erstellt ist 


## DATENBANK VERKNÜPFUNG
- Pony verknupft python classes mit datenbank

get_form(form_id, zipcode, request: Request) <- erstellt und schickt einen pdf und eine Email

# Frontend
- was genau Webpack macht??
- dummy mc-vetrieb M:\WEB\_Produktionsfreigabe\Dummy MCV


Zu wechesln

Nur der Kode:
alt: OPTIMA, MC-VERTRIEB
logoPrint: ./img/logo-optima-print.png, logo-mcvertrieb-print.png

Stell die Frage:
Linie 10 faq - ./downloads/optima-faq-2022-02.pdf, MC-Vertrieb hat es gar nicht
Linie 11 mail - mailto:kundenservice@optima-garagen.de, mailto:test@mc-vertrieb.de

linie 94.1 impressum - https://www.optima-garagen.de/impressum/, https://www.mc-vertrieb.de/impressum.html, 
linie 94.2 dataProtection - https://www.optima-garagen.de/datenschutz/, https://www.mc-vertrieb.de/datenschutz.html, 



PROBLEME und TODO
Backend
- erstellt ein pipenv install Datei um die Dependencies automatisch herunterzuladen [x]
	- zeig Dustin [x]
- Ich darf nicht M:\WEB\_Produktionsfreigabe\Umsetzung.git clonen (git clone M:\WEB\_Produktionsfreigabe\Umsetzung.git) [x]
	- jetzt funktioniert es
- Ich kann jetzt nicht die Änderungen in git in WSL sehen [x]
	- jetzt funktioniert es
- Wie kann ich ein mock form in Weclapp generieren? <- Frag Dustin [x]
	- 	jetzt habe ich zwei Mocks
		- MC - AB60617-2020
		- Optima - AB-52382
- Wie kann ich makepdf.js überprüfen? Es funktioniert nicht, als ich gucke. [x]
	- puppeteer nimmt locahost nicht. Man muss die IP Adresse von einem PC geben z. B. 192.168.26.210[x]
- w0097824.kasserver.com:587 <- das Server funktioniert nicht [x]
	- auch die Emailadresse (abrufe@mc-vertrieb.de), die mir Peter gegeben funktioniert nicht
		- vielleicht mussen wir die neue Konto erstellen [x]
- wenn die Emails von mcvertreib geschickt werden, gibt es "Fragezeichen - ?" []
	- https://support.google.com/mail/answer/180707?hl=en&co=GENIE.Platform%3DAndroid
- Zeig Dustin die beide Webseite [x]
	- https://formulare.mc-vertrieb.de/_test/
	- https://formulare.optima-garagen.de/_test/
- der Domain zu erstellen [x]
- die Änderugnen in dem Datenbank []
	- Tenants
		- neue Spalte - email_config
			- sqlite3
			- .open /mnt/c/Users/a.szulc/d3-db.sqlite;
			- select * from tenants;
			- alter table tenants add email_config JSON;
			- edit Optima update tenants set email_config = '{"host":"smtp.strato.de:587","login":"kundenservice@optima-garagen.de","password":"123Optima_","sender":"OPTIMA Kundenservice <kundenservice@optima-garagen.de>"}' where tenant_id = 'optima';
			- add MC
				- insert into tenants (tenant_id, name, weclapp_config, email_config)	values('mcvertrieb', 'MC-Vertriebs', '{ "weclapp_key":"fa4b2639-aeef-43d1-8e31-f3000f310a14", "weclapp_orderno_field":"37869", "weclapp_trigger_internal_id":"6200039", "weclapp_trigger_set_after":"6200053", "weclapp_trigger_waiting":"6200052",   "weclapp_trigger_when":"6200051"}', '{"host":"w0097824.kasserver.com:587","login":"abrufe@mc-vertrieb.de","password":"ETgoebF36MU7wknJ","sender":"MC-Vertrieb Kundenservice <abrufe@mc-vertrieb.de>"}');

- das Password für email ist als ein Text geschikt. [x]
	- Jetzt ist es nicht nötig aber wenn wir dass email in d3 GUI wechseln werden, dann brauchen wir das Passwort da
	- in die erste Version werden wir keinen Passwort zeigen
- Zeig Dustin das Bug, dass man sofort nach dem Erzeugung nix mit dem Formular machen
	- fix in ReadyOrders.vue linie 49 [x]
- Soll mehr damit arbeiten und die zweite version entwickeln oder fokusieren wir zurest an der basis-Version? <- Eine Frage an Dustin [x]
	- am 10.06 deployen wir die erste Version
- log in der Email nach rechts [x]
- Produktionsfreigabe soll schwarz in der Email sein [x]
- Wie kann ich die Putty benutzen [x]
	- Klick auf "leadwiesel-appservers.ppk" in Formular Verzeichnung
	- in pageant wird einen neuen Schlussel hinzugefügt
	- dann kann ich mit Putty verbinden
- ordner für Entwürfe ist id von tenant [x]
- forms.py 221 nimm emails von Datenbank [x]
- faq in mc ausblenden [x]
- passwort nicht zeigen [x]

- **DEPLOYMENT**
- guck auf TODOs!!!!!!
	- emails für MC kommen an mich, für Optima kommen an Kunden
	- Produktionfreigabe für MC wechselt nicht

- frontend
 - npm run build
 - Dateien aus dist kopieren
- backend 
 - putty einlogen
 - die neue Dataie kopieren
 - die Verzeichnung '__pycache__' löschen
 - sudo systemctl restart uvicorn-d3 <- restart
 - sudo systemctl status uvicorn-d3 <- Überprüfen, ob das System funktioniert



**Frontend**
- es gibt einen Fehler, wenn ich eine neue Formular generiere. Kann ich dann die Knopfe nicht benutzen, gibt es einen Fehler auf der Frontend Seite [x]

**Weitere Entwicklung**

2. Version
- Mach hinzufügen und löschen von Tenants total in GUI möglich 
	- die Felder in Tenantsdetails editierbar
	- fügt ein Knopf in GUI zu löschen die Tenants

- mach auch die Dateien in GUI zu hinzufügen möglich und in der Datenbank speichern

- wechsel die Js script mit puppeteer zu python code

- forms.py linie 95.

**Frage an Peter**
- Wie soll das Entwurf für MC-Vertreibs aussehen? []
	- Ich habe die schon gut gemacht


**Frontend**
- http://localhost:1234/?8319e8e5-02f6-493a-a72e-defe128cc3ad/11111 - wie geht es, dass der Link ein Formular triggert. [x]
	- in mounted() von der Website wird es überprüft, ob in dem Link den Zip Code gibt [x]


Ich habe die daten von customAttributeDefinition genommen:
- api-key: fa4b2639-aeef-43d1-8e31-f3000f310a14
- Bauauftragsnummer-Feld: 37869
- Abrufversand-Feld: 6200039 <- customAttribute, name ProduktionsFreigabe, "attributeKey": "i5mtpjhr200t7j"

Felder von customAttribute - ProduktionsFreigabe:
	- Formular versenden: 6200051 <- 2. An Kunden versenden. - weclapp_config.weclapp_trigger_when **die Einträge werden aus Weclapp gefetcht**
	- Nach Versand setzen: 6200052 <- 3. Versandt. Warten auf Kunde.
	- Nach Freigabe: 6200053 <- 4. Freigabe erfolgt.



customAttributeDefinition
https://mcvertrieb.weclapp.com/webapp/api/v1/customAttributeDefinition




Test Weclapp Aufträge


Was ist schon gemacht:
- Emails sind von dem richtigen Entwurf erstellt
- das richtige Dokument ist als ein Anhang hinzugefügt
- eine neue Emailadresse, jetzt es ist test@mc-vertrieb.de
- das Email server funktioniert nicht auf dem port: 465. Port 587 ist verfügbar



ZU TESTEN
- schick einen Form ohne *_BZ_* datei [x]
	- Ein Kund bekommt eine Email, ohne Anhang



PDF erstellen: 



API description
**customers.py**
	Die Klasse sieht aus, als sie nicht benutzt ist.

**db.py**
	Hier stehen alle benutzte Entities.

**emails.py**
	Es ist keine API.

	- get_last_construction_drawing() <- Gibt die neuste Datei von WeClapp zurück, die regex ```/*_BZ*_/``` erfüllt. Wenn es keine solche Datei gibt, protokolliert es dass und schickt keine Datei

	- send_notification() <- Im Algemeinen, shickt es Emails. Es füllt einen Entwürf aus und, log zu dem SMTP Server und schickt die Email 

**events.py**
	- log() <- speichert die Logs in dem Datenbank

	- / <- gibt züruck die 20 neuste Log Einträge

**forms.py**

	- /ready_orders <- nimmt Aufträge aus Weclapp, deren das Produktionsfreigabe Feld (6200039, i5mtpjhr200t7j) gleich "2. An Kunden versenden" (6200051) ist.
	Die Einträge, die in der Datenbank in OpenForms sind, haben das "hasForm=true" und haben andere Knopfe.
	**Es mach keine Änderungen in WeClapp**

	- /resend_link <- schickt eine Email von email-abruf Template und fügt die neuste Dokument (nur ein) von Weclapp, die Regex *._BZ_.* erfüllt.
	**Es wechselt auch das Feld ProduktionsFreigabe zu 3. Versandt. Warten auf Kunde in WeClapp**

	- /generate_form <- erstellt in der Datenbank in OpenForms Tabelle, einen Eintrag mit den Daten von dem Kund und Formular Spezifikation. ID von dem Form wird automatisch generiert.
	**Es mach keine Änderungen in WeClapp**

	- /delete_form <- löscht die Form von der Datenbank
	**Es mach keine Änderungen in WeClapp**

	- /get_form/{form_id}/{zipcode} <- gibt die Form daten züruck
	**Es mach keine Änderungen in WeClapp**

	- /check_form



**DATENBANK KOPIEREN**
WSL -> WIN cp d3-db.sqlite /mnt/c/Users/a.szulc/
WIN -> WSL cp /mnt/c/Users/a.szulc/d3-db.sqlite .


**EMAIL**
{
   "host":"smtp.strato.de:587",
   "login":"kundenservice@optima-garagen.de",
   "password":"123Optima_",
   "sender":"OPTIMA Kundenservice <kundenservice@optima-garagen.de>"
}

{
   "host":"w0097824.kasserver.com:587",
   "login":"abrufe@mc-vertrieb.de",
   "password":"ETgoebF36MU7wknJ",
   "sender":"MC-Vertrieb Kundenservice <abrufe@mc-vertrieb.de>"
}

69483

8319e8e5-02f6-493a-a72e-defe128cc3ad


mcvertrieb - m.fiedler@it-mf.de

Backend adjusted to work also with MC


