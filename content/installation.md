# Installation

AMW ist eine Java EE 6 Applikation und wird entsprechend in einen Java Applikationsserver deployed.

Die Applikation AMW unterst�tzt aktuell die folgenden Applikationsserverversionen

* JBoss EAP 6.4
* Wildfly 10 (Techpreview)

## Prerequisites

* Java 8 
* Java Cryptography Extension Unlimited Strength f�r Oracle und IBM Java Versionen
* Datenbank Oracle 11g / 12g

## Deployment

Das entsprechende Applikations Archiv (EAR) kann im Applikationsserver wie folgt deployed werden:

* Kopieren des EAR- Files in den standalone/deployments
* zus�tzlich muss der [Oracle JDBC Driver](http://www.oracle.com/technetwork/database/features/jdbc/index-091264.html) mit installiert werden
 * Als JBoss Modul (https://access.redhat.com/documentation/en-US/JBoss_Enterprise_Application_Platform/6/html/Administration_and_Configuration_Guide/Example_Oracle_Datasource.html) Daf�r muss das oracle jdbc driver jar entsprechend vom Oracle herunter geladen und wie beschrieben paketiert und koniguriert werden.
 * Jar direkt deployen, den Oracle JDBC Driver herunterladen und unter standalone/deployments mitdeployen, in der Konfiguration entsprechend direkt referenzieren, siehe [Konfiguration](configuration.md)
 

## Zugriff 

Die Applikation ist anschliessend �ber http://server:8080/AMW_web zugreifbar.