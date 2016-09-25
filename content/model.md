# AMW Datenmodell

Grunds�tzlich besteht das Modell in dem Sie die Konfiguration in AMW abbilden aus den folgenden Grundelementen:

* ApplicationServer (AS) - Der Applikationsserver auf dem die Applikationen deployed werden
* Application (App) - Die zu deployende Applikation
* Node - Der Node in Kombination mit einem AS entspricht einem Deployment des AS auf einem Server
* Runtime - Die Runtime definiert am AS um welchen Applikationsserver es sich handelt, typischerweise JBoss EAP 6, JBoss EAP 7, Websphere, ...
* Resources - Als Resourcen werden alle anderen Elemente die an einem AS, einer App, einer Node oder Runtime als Abh�ngigkeiten angeh�ngt werden k�nnen
 * Datenbank an Applikation
 * Webservice SOAP / REST
 * Queue
 * Zertifikate
 * ...
 
 
Allegmein sprechen wir bei den obigen Elementen von **Ressourcen** die zu einander mittels Relations in Beziehung stehen. 

Jede Ressource besitzt einen **Namen** und einen **ResourceType**

## ResourceTypes

ResourceTypes entsprechen der generalisierten Auspr�gung von Ressourcen. So werden beispielsweise auf dem RessourceType ApplikationServer generelle Informationen, Templates, Properties usw. eingepflegt, die sonst auf Instanzebene redundat pro Applicationserver verwaltet werden m�ssten.

Man hat also damit die M�glichkeit, generell geltende Sachen f�r alle Applikationsserver einmal zu definieren.

Ein ResourceInstanz ist immer einerseits �ber den ResourceType und �ber die effektive Instanz definiert.

Auf ResourceTypes k�nnen die folgenden Elemente definiert werden:

* PropertyDescriptoren (PropertyKeys)
* PropertyWerte
* Templates
* Functions

Auf ResourceInstance Ebene k�nnen folgende Elemente definiert werden:

* Zus�tzliche PropertyDescriptoren (Zus�tzlich zu den Descriptoren der ResourceTypes)
* PropertyWerte
* PropertyWerte von ResourceTypes k�nnen �berschrieben werden.
* Templates
* Functions
* Relations

## PropertyTypes

Ein PropertyType (PropertyTypeEntity) ist als Template f�r PropertyDescriptors zu verstehen.
Folgende Werte k�nnen auf dem PropertyType definiert werden:

* id: eindeutiger Identifier
* propertyTypeName: Name des PropertyType
* validationRegex: Validierungslogik f�r den Property-Wert
* encrypt: gibt an ob der Property-Wert verschl�sselt wird
* propertyTags: Einsatzzwecke, eine Sammlung von Gruppierungselementen, welche in den Templates als Selektionskriterium zur Verf�gung steht

## Properties

In AMW wird ein Property (PropertyEntity) durch eine Kombination aus sogenannten PropertyDescriptors und Property-
Values repr�sentiert: W�hrend ein PropertyDescriptor die eigentlichen Eigenschaften eines Properties enth�lt, stellen die PropertyValues kontextabh�ngige Werte eines Properties dar.
Folgende Werte k�nnen auf dem PropertyDescriptor definiert werden:

* id: eindeutiger Identifier
* technicalKey: TechnicalKey - vollst�ndiger, technischer Schl�ssel inkl. komplexem Namespace zur Sicherstellung der Uniqueness
* displayName: Optionaler Name f�r die Darstellung im GUI, da der propertyName in gewissen F�llen sehr lang und unleserlich sein kann
* encrypt: gibt an ob der Property-Wert verschl�sselt wird
* valueOptional: gibt an ob der Property-Wert null sein darf
* keyOptional: gibt an, ob ein Property mit diesem Key im Generator zur Verf�gung gestellt werden muss
* testing: gibt an ob das Property f�r Shakedowntests verwendet wird, diese Properties werden im GUI nur im Testingmode angezeigt.
* validationLogic: Validierungslogik f�r den Property-Wert
* propertyComment: Kommentar zu diesem Property
* cardinalityProperty: wenn dieser Wert nicht null ist, handelt es sich um ein SystemProperty und hat eine spezielle Bedeutung. Ein solche Property kann z.Bsp. nicht von einem Benutzer gel�scht werden. Ausserdem wirkt sich die Kardinalit�t auf die Darstellungsreihenfolge im GUI aus.
* propertyTypeEntity: das Template f�r das Property, gewisse Werte werden vom Typ �bernommen falls sie nicht im descriptor �berschrieben werden. Falls null handelt es sich um ein Custom-Property.
* defaultValue: Defaultwert falls auf dem Property kein value gesetzt ist.
* exampleValue: Beispielwert als Hilfe f�r den Benutzer
* machineInterpretationKey:
* propertyTags: Einsatzzwecke, eine Sammlung von Gruppierungselementen, welche in den Templates als Selektionskriterium zur Verf�gung steht


## Beziehungen / Relations

Ressourcen k�nnen �ber sogenannte Relations in Beziehung zu einander gesetzt werden:

* App --> Datenbank, eine Applikation konsumiert eine Datenbank �ber eine ConsumedRelation
* App --> Webservice, eine Applikation stellt einen Webservice �ber eine ProvidedRelation zur Verf�gung.


## Beispiel Applikation AMW

Als Beispiel hier beschreiben wir die Applikation AMW selber, AMW wird auf einem JBoss EAP 6.4 deployed und besitzt eine Datenbank und versendet via Mail Session Emails

In unserem Beispiel wird nur eine Applikation auf den Applicationserver deployed.

* Applicationserver: amw
* Application: amwApp
* Runtime: EAP64
* Database: oracle
* Node: Node1