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

## Modell


## Funktionen

### Globale Funktionen

AMW bietet die M�glichkeit unter Settings --> Global Functions globale Funktionen zur Verf�gung zu stellen. Diese Funktionen k�nnen wiederum in den Templates verwendet / included werden

```
<#include globalfunctions >

${myglobalFunction()}

```

### Resource Funktionen

Auf Resource Ebene k�nnen Funktionen ebenso definiert werden, innerhalb der Templateausf�hrung stehen die Funktionen dann auf der entsprechenden Resource zur Verf�gung.