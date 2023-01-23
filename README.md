# Exercise one using Calculator Example 1.2 

Upgraded, tested and cleaned for Continuous Delivery Pipeline testing

## Installation

no special installation needed, currently upgraded Tools Version for 1.2
- Maven 3.8.6
- JDK 19.0.1

```bash
mvn clean
```

## Usage

```bash
mvn test
```

## Contributing

Pull requests are welcome. For major changes, please open an issue first
to discuss what you would like to change.

Please make sure to update tests as appropriate.

## License

[GNU GPLv3](https://choosealicense.com/licenses/gpl-3.0/)

# Dokumenation 
## Dokumenation Excercise 1
ALLE Schritte konnten ohne gröbere Vorkomnnisse(syntax fixes) erledigt werde.
(Bennenung bitte ignorieren) aber im seventh.yml befinden sich der eigene Workflow 

**Überlegen Sie sich, wie Sie die einzelnen Schritte (compile und test) separat als
steps abbilden können. Wäre das vorteilhaft? Begründen Sie Ihre Antwort.**

Trennen der Schritte von Kompilieren und Testen in separate Schritte in einem GitHub Actions Workflow kann vorteilhaft sein.

**Isolation**: Durch das Trennen der Schritte erhält man eine größere Kontrolle und Isolation jedes 
einzelnen Schrittes, was nützlich sein kann beim Debugging und Fehlersuche.

**Wiederverwendbarkeit**: Durch das Trennen der Schritte in separate Aktionen erhält man mehr Flexibilität 
und Wiederverwendbarkeit des Workflows.

**Parallelisierung**: Durch das Trennen der Schritte in separate Aktionen ist es möglich die Schritte zu parallelisieren, 
was die Gesamtleistung des Workflows verbessert.

**Einfachere Wartung:** Wenn die Schritte getrennt sind, ist es einfacher, sie zu aktualisieren oder zu modifizieren, ohne die anderen Schritte zu beeinflussen.

Es ist jedoch zu beachten, dass das Trennen der Schritte die Komplexität des Workflows erhöhen kann, was es schwieriger macht, es zu 
verstehen und zu warten. Es ist auch möglich, ähnliche Vorteile durch die Verwendung von verschiedenen Jobs im gleichen Workflow zu erzielen. 
Letztendlich hängt es von den spezifischen Anforderungen des Projekts und des Teams ab, ob das Trennen der Schritte in separate Schritte vorteilhaft ist.

Erstellen Sie nun für Ihr eigenes Projekt geeignete Workflows. Erweitern Sie bestehende
Workflows durch zusätzliche nützliche GitHub Actions. Beachten Sie dabei unter anderem
folgende Punkte und dokumentieren Sie Ihre Ergebnisse.
- Wann können Workflows ausgelöst werden?
- Wann macht es in einem Projekt Sinn einen Workflow auszulösen?
- Welche Schritte sind für Ihr Projekt automatisierbar?
- Wie sind Workflows grundlegend aufgebaut?
- Wozu dienen unterschiedliche Runner (Betriebssysteme) in GitHub Actions?
- Wie können auch unterschiedliche Versionen, zB Java mittels Workflows automatisiert
getestet werden? (Stichwort: Matrix Strategy):

1. Workflows können ausgelöst werden, wenn bestimmte Ereignisse im Projekt stattfinden, 
   wie zum Beispiel das Pushen von Code, das Erstellen oder Aktualisieren von Pull Requests, das Veröffentlichen von Releases usw.

2. Es macht Sinn, einen Workflow auszulösen, wenn automatisierte Schritte durchgeführt 
   werden müssen, die nach jeder Änderung am Projektcode ausgeführt werden sollen, wie zum Beispiel das Überprüfen des Codes auf Fehler, das Testen des Codes oder das Bereitstellen des Codes.

3. Schritte, die automatisierbar sind, können zum Beispiel das Überprüfen des Codes auf Fehler, 
   das Testen des Codes, das Generieren von Dokumentation, das Bereitstellen des Codes, das Testen auf unterschiedlichen Plattformen usw.

4. Workflows bestehen grundlegend aus einem oder mehreren Jobs, die aus mehreren Schritten bestehen. 
   Jeder Job wird von einem bestimmten Runner auf einem bestimmten Betriebssystem ausgeführt.

5. Unterschiedliche Runner ermöglichen es, Workflows auf verschiedenen Betriebssystemen auszuführen, um sicherzustellen, 
   dass der Code auf allen unterstützten Plattformen ordnungsgemäß funktioniert.
   
6. Um unterschiedliche Versionen von Java zu testen, kann man die Matrix-Strategie verwenden, bei der man mehrere Variablen definiert, 
   die die Versionen der zu testenden Software darstellen und die Schritte des Workflows mehrfach mit unterschiedlichen Werten dieser 
   Variablen ausführt. Auf diese Weise kann man sicherstellen, dass das Projekt auf allen unterstützten Plattformen ordnungsgemäß funktioniert.

## Dokumenation Excercise 2
Alle Schritte konnten erfolgreich durchgeführt werden
Im Grunde genommen habe ich einfach ihre steps nachgemacht und recherchiert, anfangs hatte ich viele Problem war teilweise typos verschuldet teilweise
fehlender configuration in der pom.xml alle fehler konnten aber behoben werden.

Hatte erst auch nicht die richtige Version der tar genommen aber mittels ls schnel rausgefunden dass ich da eine falsche version verwendet habe danch wurde
die calculation auch richtig durchgeführt. 

Folgende pom.xml anpassung hat mich viel Zeit gekostet:
<configuration>
<source>1.8</source>
<target>1.8</target>
</configuration>

Zudem musste ich im dockerfile eine andere Version nehmen da ich keine Rechte auf andere Versionen hatte:
FROM eclipse-temurin:11
WORKDIR /project
COPY target/*.jar .

Danch habe ich noch gemerkt dass mir ein File zerschossen wurde(sixth.yml the stylchecker) wurde angepasst und läuft wieder.

Für den build befehl selbst habe ich folgendes verwendet: docker build -t adamkhalil/calcapp .
für den container start :  docker run --name calcapp -it --entrypoint /bin/sh adamkhalil/calcapp

Ansonsten gab es keine besonderheiten 
login und push waren einwandfrei
Näher siehe code in third.yml udn dockerfile 