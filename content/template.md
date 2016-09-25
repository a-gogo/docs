# Template

In diesem Kapitel wird beschrieben wie innerhalb der Templates auf das Datenmodell im AMW zugegriffen werden kann, welche Funktionen zur Verf�gung stehen und wie die entsprechenden Werte ausgegeben werden k�nnen.

## Template Sprache

AMW verwendet [Freemarker](http://freemarker.org/) als Templating Sprache. Freemarker ist sehr m�chtig, so haben Sie die M�glichkeit innerhalb der Templates in AMW, die die Konfigurationsfiles aufbereiten 
Logik einzubauen.

Grunds�tzlich stehen folgende Funktionen zur Verf�gung:

* Werte aus dem Modell ausgeben ``${key}``
* If Else Conditions / Vergleiche
* Formatieren
* Funktionen / Macros definieren und ausf�hren
* Listen, Hashes
* Operationen auf Werten String, Numbers, ...
* ...

Eine komplette Liste der Funktionalit�t steht unter http://freemarker.org/ zur Verf�gung.

## Zugriff auf Modell

### Globale Elemente

Globale Elemente die in jedem Template zur Verf�gung stehen:

* appServer (current Applicationserver Resource)
* node (current Node Resource) 
* env (Environment)
* deployment
* deploymentId
* runtime
* deploy (true wenn in deploymodus)

### Property

Der Zugriff auf ein Property erfolgt �ber die Angabe seines namens (propertyName), die Properties der aktuellen Resource befinden sich direkt unter root:

```
${propertyName}
oder
${propertyName.currentValue}
```

Will man beispielsweise auf ein ApplicationServer Property zugreifen, wird dies wie folgt gemacht:

```
${appServer.propertyName}
oder
${appServer.propertyName.currentValue}
```

#### Zugriff auf PropertyDescriptoren
Auf die Metainformationen einer Property kann mittels seines TechnicalKeys, gefolgt von ``_descriptor`` zugegriffen werden. F�r ein Property mit dem TechnicalKey "propertyName" s�he dies im Template so aus:

```
${propertyName._descriptor.propertyName}
${propertyName._descriptor.displayName}
${propertyName._descriptor.encrypt}
${propertyName._descriptor.valueOptional}
${propertyName._descriptor.keyOptional}
${propertyName._descriptor.validationLogic}
${propertyName._descriptor.propertyComment}
${propertyName._descriptor.cardinalityProperty}
${propertyName._descriptor.technicalKey}
${propertyName._descriptor.defaultValue}
${propertyName._descriptor.exampleValue}
${propertyName._descriptor.machineInterpretationKey}
```

Sollte ein TechnicalKey einen Punkt "." enthalten, so ist dieser via Backslash ``\`` zu escapen:
```
${property\.Name._descriptor.propertyName}
```

Mittels der hasContent Methode auf einem Property kann abgefragt werden, ob ein Wert vorhanden ist oder nicht.
gibt true zur�ck wenn currentValue null oder [empty String] ist.
```
${propertyName.hasContent}
```

#### PropertyTags
Eine Liste der dem Property zugeordneten Tags, ist via 
```
${propertyName._descriptor.tags}
```
verf�gbar. Mittels
```
${propertyName._descriptor.hasTag("tag")}
```
kann �berpr�ft werden, ob dem Property ein bestimmter Tag zugeordnet ist.

#### Aufl�sen der PropertyWerte im Generator
Ein PropertyDescriptor kann mehrere PropertyValues besitzen - f�r einen bestimmten Kontext gibt es aber immer nur einen einzigen g�ltigen Wert. Die Auswertung der PropertyValues f�r einen bestimmten Kontext folgt einer spezifischen Priorisierungsreihenfolge: F�r einen Kontext/eine Umgebung wird versucht, dieser aufgrund der Kontexthierarchie aufzul�sen - also z.B. zuerst "B", wenn dort nichts definiert wurde auf "DEV" ? "GLOBAL". Dabei sollen Werte auf der Instanz wie auch auf deren Typen (inkl. Typhierarchie) gepr�ft. Dabei kommen die folgenden beiden M�glichkeiten erst dann zum Tragen wenn bei der Aufl�sung kein PropertyValue definiert wurde (sprich vom Benutzer kein Wert gesetzt wurde):

* Ber�cksichtigung synthetisierter Werte: Besitzt der Propertydescriptor ein MachineInterpretation-Key, so wird der Wert zum Aufl�sungszeitpunkt aufgel�st - der aufgel�ste Wert wird nur f�r die aktuelle Generierung verwendet und wird nicht persistiert. (vgl. \ref{subsec:functonalProperties})
* Ber�cksichtigung eines Default-Values: Der allenfalls auf dem Propertydescriptor definierte Default-Wert �bernommen.

#### Dynamische Properties

Der Wert von dynamischen Properties wird nicht von einem Benutzer definiert - stattdessen steht hinter einem dynamischen Property eine Aufl�sungslogik, welche den Wert herleitet. Ein g�ngiges Beispiel ist hier die Aufl�sung einer Webservice-Endpoint-URL zu erw�hnen. AMW definiert dynamische Properties in Form eines MachineInterpretationKey (MIK).  Anhand dieses Keys wird in AMW definiert, welche Funktionalit�t verwendet wird um dieses dynamisch Property abzuf�llen.
Ist ein dynamisches Property optional und erh�lt nach dessen Aufl�sung einen leeren Wert, so wird dieses nicht in das Template geschrieben. Der Wert des dynamischen Properties kann vom Benutzer �berschrieben werden. Ist ein Wert vom Benutzer gesetzt, wird die Aufl�selogik nicht ausgef�hrt.
Terminologisch k�nnen wir nun zwischen den dynamischen properties und den einfachen Properties unterscheiden. Die einfachen Properties entsprechen den bisher in AMW etablierten Properties.
Nun haben wir gesehen, was dynamische Properties sind, wie sie eingesetzt werden und wie sie sich von einfachen Properties unterscheiden. F�r die Umsetzung ist von dynamischen Properties m�ssen deren Bestandteile analysiert werden. Konzeptionell besteht ein dynamisches Property aus zwei Teilen: 

* Enth�lt vom Benutzer definierte Logik, wie ein Propertywert basierend auf einfachen Properties und Funktionen aufgel�st wird.
* Das dynamische Property unterscheidet sich vom einfachen Property durch die Angabe des MIK im Propertydeskriptor. Selbst enth�lt das dynamische Property keine Funktionalit�t.


## Funktionen

### Globale Funktionen

AMW bietet die M�glichkeit unter Settings --> Global Functions globale Funktionen zur Verf�gung zu stellen. Diese Funktionen k�nnen wiederum in den Templates verwendet / included werden

```
<#include globalfunctions >

${myglobalFunction()}

```

### Resource Funktionen

Auf Resource Ebene k�nnen Funktionen ebenso definiert werden, innerhalb der Templateausf�hrung stehen die Funktionen dann auf der entsprechenden Resource zur Verf�gung.
Diese Funktionen werden verwendet um in dynamischen Properties als MIKs entsprechend Werte aufzul�sen.

Diese Funktionen k�nnen auch in einem Template aufgerufen werden, wenn man sich auf der selben Resource befindet, sieht das wie folgt aus:

```

${amwfunction.myFunction()}

```