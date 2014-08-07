**KNXnet**
==========

KNXnet/1
--------

KNXnet/2
--------

KNXnet/3
--------

KNXnet/4
--------

KNXnet/IP
---------
KNXnet/IP/1
^^^^^^^^^^^
KNXnet/IP/2
^^^^^^^^^^^
KNXnet/IP Routing
^^^^^^^^^^^^^^^^^
KNXnet/IP Routing-Support
.........................

| **Allgemeines:**
| Beim Start wird automatisch ein KNX/IP routingfähiger IP-Router gesucht und gegebenenfalls im Log angezeigt. nomos liest die Mutlicast-Adresse des IP-Routers aus und tritt der entsprechenden Gruppe bei. 

| **Vorteil der Routing Variante:**
| Es können beliebig viele nomos Systeme gleichzeitig auf das KNXnet/IP-Device gleichberechtigt zugreifen. Die Konfigurationsdatei heisst knx.csv und wird im misc-Ordner abgelegt. In der knx.csv angelegte Adressen werden konvertiert, ggf. Actions ausgeführt und über den Broadcast Port ausgegeben.

|
| **Aufbau der Definitionstabelle:**

=======		===================
Typ:		csv Datei
Ort:		.\{projectPath}\misc\
Name:		knx.csv
Länge:		10000 Zeilen/Einträge
Event:		BC, Status
Export:		nein
Lizenz:		ja
=======		===================

| Die knx.csv besteht aus 3 Sektionen:

 * [CONFIG];			allgemeine Konfiguration der Interface Parameter
 * [DATAPOINTS];		Definition von Datenpunkten, die über KNXnet/IP empfangen und ausgewertet werden sollen.
 * [TABLE={NAME}];	Scan Definitionstabellen, Gruppenpollen 

|

**Aufbau:**

[CONFIG]; **Sektion**

 * ACTIVE;YES;
	| Schaltet den KNXnet/IP Support
	| „YES“ = ein,
	| „NO“ = aus

 * DEBUG;YES;
	| Schalter für
	| „YES“ = erweiterte Logausgaben (Busmonitor)
	| „NO“ = standard Logausgaben

 * ESF;{ESF File};
 	| Name der .esf-Datei in dem Ordner misc
	| (knx.esf = Default)

 * PHYSADDR;{Phys.Adresse};
	| Lokale Physikalische Absenderadresse, die mmh beim Versenden verwenden soll.

 * ADDRTYPE;{Adresstyp};
	| „2STEP“ = 2stufige Darstellung,
	| „3STEP“ = 3stufige Darstellung (Default)

 * DPTNAMES;YES;
	| Schaltet die Namen der Datenpunkte im Broadcast
	| „YES“ = ein (Default),
	| „NO“ = aus

 * MATCHLOCAL;YES;
	| Legt fest, ob die unter DATAPOINTS definierten Aktionen auch dann ausgeführt werden, wenn der Deamon selbst auf die Datenpunkte schreibt.
	| „YES“ = ein,
	| „NO“ = aus (Default)

 * INITSCAN;YES;
	| scannt die definierten Tabellen beim Engine-Start
	| „YES/ALL“ = ein,
	| „NO“ = aus (Default)

 * SENDRATE;{Telegr/s};
	| Begrenzt die Anzahl der Telegramme die pro Sekunde auf den Bus beschrieben werden. Der Puffer ist variabel und Burst fähig. „17“ (Default). Der hier eingestellte Wert gilt auch für den Abstand der Telegrammabfragen, die mit SCAN= initiert werden.

 * CONNECTIONTYPE;{Protokolltyp};
	| „ROUTING“ (default: ROUTING)
	| oder „TUNNELING“
	| oder“ TUNNELING_BRIDGE“

	**Spezifische Einstellungen für die Betriebsart „ROUTING“:**
		| CONNECTIONTYPE;ROUTING;
		| **Bei** CONNECTIONTYPE;ROUTING **wird folgender, zusätzlicher Schalter benötigt:**
		| MULTICAST_IP;{Multicast ADR};
		| Multicast IP des Gerätes Standard: {224.0.23.12} oder „AUTO“ für automatisches Suchen
		| (Default: AUTO)

|

[DATAPOINTS]; **Sektion**

 * {KNX/EIB Gruppenadresse};{Bedingung};{mmh-Sequenz};

  | In diesem Bereich können KNX Events direkt ausgewertet und entsprechende Aktionen eingeleitet werden.

  | **Erläuterungen:**

  | {KNX/EIB Gruppenadresse} Gruppenandresse im entsprechend eingestelltem ADDRTYPE
  | {Bedingung}	kann (entsprechend BAOS) folgende Zustände haben:

	* {Match-String}
		| der von KNX/IP übermittelte Wert muß mit {Match-String} übereinstimmen.

	* {#}
		| alle Werte starten das Script bzw. die Sequenz. Wenn *{Bedingung}* leer ist, wird '#' angenommen.

	* {mmh-Sequenz}
		| Auszuführende Kommandosequenz oder Scriptname, wenn *Bedingung* erfüllt. Kann als Platzhalter für den Wert '\#' 	beinhalten, bei Scripten wird der empfangene Wert als 	Argument übergeben

|

[TABLE={NAME}]; **Sektion** {NAME}
	definiert eine entsprechende Gruppe.
	Es können beliebig viele [TABLE={name}] Sektionen angelegt werden.
	Diese Namen werden bei der Ausführung der SCAN Befehle benötigt und im weiterem Verlauf genauer erklärt. 

	* {KNX/EIB Gruppenadresse};
 		| Gruppenadressen die gescannt werden soll. Es darf nur eine Gruppenadresse je Zeile eingetragen werden.

|

**Beispiele für die Definitionen [DATAPOINTS] Sektion:**

::

 8/1/4;1;<ITUNES><NEXT><PLAY></ITUNES>

| Bei Empfang der Adresse 8/1/4 mit dem Wert „1“ führt iTunes den internen Befehl „NEXT“ und PLAY aus. 
| Pro Adresse lassen sich mehrere Actions definieren, wenn unterschiedliche Match-Bedingungen angegeben werden. Bei identischen Match-Bedingungen pro Adresse wird nur die erste gefundene Action ausgeführt. 

|

::

 15/7/10;1;<SYS><SAY=on></SYS> oder 15/7/10;0;<SYS><SAY=off></SYS>

Führt nur bei Empfang einer logischen „1“ der Adresse 15/7/10 den Befehl ::

 <SYS><SAY=on></SYS>
 
aus.

Bei Empfang einer logischen „0“ wird nur der Befehl ::

 <SYS><SAY=off></SYS>

ausgeführt.

|

::

 8/1/7;#;<SYS><VOLSET=\#></SYS>;

Schreibt den empfangenen Wert auf die System Volume.

|

::

 5/2/8;DOWN,100;<SYS><VOLDN=5></SYS>;
 5/2/8;UP,100;<SYS><VOLUP=5></SYS>;

| Empfängt und wertet ein 4Bit Dimmtelegramm (EIS2) aus.
| Hierbei empfiehlt es sich, dass entsprechende KNX Telegramm zyklisch senden zu lassen
| (Einstellung am entspr. Sensor beachten), da der entsprechend auszuführende Befehl {mmh-Sequenz} nur je empfangenem  Telegramm angetriggert wird. 

|

 **Beispiele für den Scan Support:** ::

  [TABLE=Wohnzimmer];
  1/8/4
  1/8/5
  1/8/7
  1/4/3

  [TABLE=Schlafzimmer];
  1/4/3
  1/3/5
  1/2/7

|

  Definiert zwei Scan Tabellen, die unter Verwendung der SCAN Befehle abgerufen werden können. Der SCAN kann unmittelbar erfolgen, oder aber im Hintergrund ablaufen. Bitte beachten, dass ein SCAN nur funktionieren kann, wenn auch entsprechend das „l“ Flag des assoziierenden KNX Kommunikationsobjekt gesetzt ist. Je Adresse sollte dieses Flag nur einmalig an einem Kommunikationsobjekt gesetzt sein.

|

Die Unterscheidung in den beiden verschiedenen SCAN Methoden liegt im zeitlichen Abstand der Lese- anforderungen. Mit SCAN= können schnelle Abfragen generiert werden. Hier sollte jedoch beachtet werden, dass nicht zu viele Telegramme mit dieser Geschwindigkeit abgefragt werden. Für die störungsfreie Abfrage vieler Telegramme, wie zb für einen initial Scan, ist der BACKGROUNDSCAN= vorgesehen.

**Die Telegramme werden sequentiell nach Erhalt einer Antwort ausgeführt. Auf eine Antwort wird max. 1s gewartet. Wird innerhalb dieser Zeit keine Antwort empfangen, wir die Meldung ERR_NO_RESPONSE generiert. Die Antworten des Scan‘s erscheinen ebenfalls im Broadcast (BC):**

::

 bc: <KNX><15/2/181-Geli.DimBelLlp.ein/ausStatus=0></KNX>
 bc: <KNX><15/5/28-SOLL_TEMP_Serverschrank=27.00></KNX>
 bc: <KNX><15/2/21- mike.DimBelLlp.ein/ausStatus=0></KNX>

|

**Es existiert eine Befehlsklasse KNX mit folgenden Befehlen:**

=============================	=========================================================================================================================================================================================================================
SETVALUE={KNX-Adresse},{Wert}	Beschreibt eine KNX Gruppenadresse (muss in der .esf Datei definiert sein) mit einem Wert.
GETVALUE={KNX-Adresse}			Liest den aktuellen Wert einer KNX Gruppenadresse (muss in der .esf Datei definiert sein).
SCAN={Name}						Sendet an alle Adressen in der entsprechenden Tabelle einen KNX-Read-Befehl, sodass man mit einem Befehl ein komplettes Prozessabbild bekommen kann. Der Abstand der Abfragen kann mittels SENDRATE;x manipuliert werden.
BACKGROUNDSCAN={Name}			Wie vor, führt jedoch einen reduzierten Scan im Hintergrund aus. Abstand der Telegramme = 300ms
=============================	=========================================================================================================================================================================================================================

|

 **Beispiele:**

 ::

  <KNX><SCAN=Wohnzimmer></KNX>
  <KNX><SCAN=Wohnzimmer><SCAN=Schlafzimmer></KNX>

 Löst die Abfrage der Gruppenadressen, wie z.B. unter [TABLE=Schlafzimmer] definiert aus. Es können auch mehre Tabellen gleichzeitig abgefragt werden.

 ::

  <KNX><BACKGROUNDSCAN=Schlafzimmer></KNX>

 Löst den Hintergrundscan der Tabelle Schlafzimmer aus. Ein Hintergrundscan wird fix mit ca. 3 Telegramme/s ausgeführt.

 ::

  <KNX><SETVALUE=1/2/3,1></KNX>

 Setzt den Wert der Gruppenadresse 1/2/3 auf 1

 ::
 
  <KNX><SETVALUE=1/2/3,1></KNX>

 Setzt den Wert der Gruppenadresse 1/2/3 auf 1

 ::

  <KNX><SETVALUE=0/0/1,[TIME]></KNX>

 Setzt den Wert der Gruppenadresse 0/0/1 auf die aktuelle Systemzeit. Die fixe Systemvariable [TIME] ist im exakten Format für die Verwendung im KNX System formatiert. Gleiches gilt für die Verwendung der fixen Systemvariable [DATE].

 ::

  <KNX><GETVALUE=1/2/33></KNX>

 Wertabfrage der Gruppenadresse 1/2/33
