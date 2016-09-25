# AMW Overview

Mit AMW k�nnen s�mtliche Konfigurationen Ihrer Applikationsumgebung auf beliebig vielen Umgebungen in unterschiedlichen Versionen verwalten und automatisiert deployen.

## Key Features

AMW unterst�tzt die Middleware Konfiguration und Automatisierung auf den folgenden Ebenen:

* Serveraufbau
* Applikationsverteilung
* Konfigurationsverteilung

### Strukturierte Verwaltung der Konfiguration

Das generische Modell erm�glicht die strukturierte Verwaltung der Konfiguration und reduziert m�gliche Redundanzen in Ihrer Konfiguration. Dank dem hierarchischen Aufbau k�nnen Property Werte global, auf Umgebungsebene, pro Applikationsserver oder pro Applikation definiert respektive �berschrieben werden.

### Abbilden von  Abh�ngigkeiten

Beziehungen zwischen Ressourcen (Applikationen, Datenbanken, Webservices) werden mit AMW abgebildet und k�nnen zus�tzliche Konfigurationen und/oder Property-Werteanpassungen enthalten.

### Templatebasierte Generierung beliebiger Konfiguration

Die im generischen Modell abgebildeten Properties und deren Werte k�nnen mittels Runtime-spezifischen Templates in die von der Applikation und dem Applikationsserver ben�tigte Struktur generiert werden.

### Versionierung  und Historisierung

S�mtliche �nderungen an der Konfiguration werden protokolliert und abgespeichert. Zus�tzlich k�nnen explizite Konfigurationsst�nde �bergreifend getagged und somit einmal erreichte Zust�nde gesichert werden.


### Automatisiertes Deployment von Applikation und Konfiguration

Deployen von Applikationen und ganzen Umgebungen zeitgesteuert, per Knopfdruck oder via REST API integriert in Ihre Workflows und Deployment Pipelines.
 
Das ausgelagerte Deploymentmodul erm�glicht das Anbinden von diversen Applikationsrepositories, aus denen die Deployables skriptgesteuert geladen respektive gebuildet werden k�nnen:

* Maven Repository
* RPM Repository
* Generierung RPM on the fly
* Filebasiert
* etc.

### Environment  Health Check

Mit dem Environment Health Check kann nach einem Deployment einer Applikation oder einer gesamten Umgebung deren Status und Funktionalit�t �berpr�ft werden. So k�nnen auf Applikationsebene sogenannte Shakedowntests definiert werden, welche zum �berpr�fen der Applikation und deren n�heren Umgebung ausgef�hrt werden.

### Abbildung von  Entwicklungsprozessen

�ber das flexible Rollen- und Berechtigungskonzept k�nnen Sie die beteiligten Stellen im Entwicklungsprozess dynamisch abbilden.
So wird beispielsweise der Software Ingenieur berechtigt, Konfigurationen f�r seine Applikation auf den definierten Entwicklungsumgebungen eigenst�ndig zu verwalten und/oder Deployments auf anderen Umgebungen anzufordern, welche nach einer weiteren Best�tigung ausgef�hrt werden.
