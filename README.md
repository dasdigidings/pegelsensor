## Inhalt:

 - Hardware / Komponenten
 - Zusammenbau 
 - Software 
 - Ausblick
 - ------------------------------

**Hardware**

 - Ultraschallsensor (MaxBotix) 0,5-10m
 - Hr-MaxTemp MB7957 Temperatur Sensor
 - Arduino Pro Mini 3.3 V (Prozessor: ATmega328P 3,3 V 8 MHz)
 - RFM 95 Lora Modul (EU868 Version für Deutschland)
 - ch2i Board Mini-Lora V1.2 ([Beschreibung und Bestückungsliste](https://github.com/hallard/Mini-LoRa))
 - DC/DC Converter 3,3VDC / 5VDC
 - 868 MHz Antenne
------------------
*optional - ja nach Aufbau / Anwendungsfall*
 - Netzteil 
 - Akku / Batterie 
 - Gehäuse

-------------------

**Zusammenbau:**

Zuerst wird das ch2i Mini-Lora Board vollständig bestück auf der Oberseite (*Reihenfolge folgt später*), Weiter gehts mit dem RFM95 Modul, welches als einziges Bauteil auf die Unterseite vom Board kommt. Dann wird eine 6-Pin Stiftleiste für die Programmierschnittstelle auf den Arduino gelötet, (von oben eingesteckt, von unten gelötet) und anschließend wird der Ardiuno auf die vorbereiteten 12-Pin Stiftleisten des Trägerboards gelötet.

Die Kabel für Spannungsversorgung, Datenleitung und Temperaturfühler werden an den Ultraschall-Sensor gelötet - Pin-1 sollte mit einer Markierung an der Lötleiste versehen sein (siehe beigefügte PDF-Dokumentation). Der Temperaturfühler wird an das mitgelieferte, geschirmte Kabel angelötet (siehe beigefügte PDF-Dokumentation). Der DC/DC Konverter wird vorbereitet - Eingangsspannung 3,3 Volt (vom Akku auch 3,6) - Die Ausgangsspannung beträgt dann 5 Volt (für Ultraschall, und Temperatursensor - der Arduino braucht 3,3 Volt !!

Die Verkabelung wird je nach Anwendungsfall konfiguriert (ob über kleine Klemmleisten verdrahtet oder direkt gelötet wird bleibt Euch überlassen). Wir haben das Glück und können für die meisten Sensoren große Gehäuse verwenden, daher werden Anschlußklemmen aus der Industrie-Automatisierung verwendet. Bei geringen Platz (zB. unser Aufbau in Version v.2) empfiehlt sich eine direkte Verdrahtung der Komponenten.

--------------

**Software:**

Wahlweise könnt Ihr je nach Eurer Erfahrung Microsoft Visual Studio Code oder Arduino IDE verwenden - Das .ino Projekt ist hier für Euch hinterlegt - Mit einer seriellen FTDI-Schnittstelle wird der Arduino beschrieben - Bei der Auswahl des Boards bitte auf die richtige Wahl achten - wir nehmen den "Ardiuno Pro oder Pro Mini" und als Prozessor den "ATmega328P 3,3 V 8 MHz" 

Außerdem müsst Ihr die Datei "ttn_secrets_h" herunterladen und bearbeiten. Die Datei enthält die Credentials für die Anmeldung vom Sensor im thethingsnetwork (Device_EUI, Application_EUI und Application_Key)  - Dies setzt einen Account im thethingsnetwork voraus, eine Application muß angelegt sein, außerdem ein Device muß bereits erstellt worden sein - Wenn nicht, ist Jetzt dafür der richtige Zeitpunkt. Für den Payload-Decoder in der TTN-Console könnt Ihr den Inhalt der Datei "decodeUplink.js" in das entsprechende Fenster einfügen, als Typ wählt Ihr natürilch dann Java-Script aus.

> *Hinweis: Device_EUI und Application_EUI müssen im LSB-Format (little-Endian, der Application-Key muß hingegen im MSB Format vorliegen (in der Datei ttn_secrets.h wird darauf auch hingewiesen)*


Nach den Vorbereitungen kann nun der Mikrokontroller mit der Software über die FTDI-Schnittstelle beschrieben werden. Nun kann mit dem Neustart vom Sensor (Reset-Button) das erste Mal gemessen werden - nach kurzer Boot-Zeit sollte sich das Gerät im thethingsnetwork anmelden und anschließend müssten Daten in der Konsole lesbar sein.

-------------------
 Herzlichen Glückwunsch - Euer neuer Pegel-Sensor funktioniert !

---------------------

**Ausblick**

 - MQTT - Daten aus der Cloud abholen 
 - node-Red, influxDB und Grafana eine Möglichkeit Daten zu visualisieren
 - opendatamap und opensensemapDaten "Opendata - offene Daten - für alle" sichtbar
   machen

--------------------------

**Quellen und Danksagung**

 - [Charles](https://github.com/hallard) für das [Mini-LoRa Board](https://github.com/hallard/Mini-LoRa))


--------------
*`Stand: 12.08.2021 dasdigidings e.V. Caspar Armster & Jens Nowak`*
