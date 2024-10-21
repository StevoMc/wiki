# Qualitätssicherung und Testen von Software

---

## Inhaltsverzeichnis

1. [Überblick](#überblick)
2. [Testen: Einstiegsübung](#testen-einstiegsübung)
3. [Überblick über Qualitätssicherung](#überblick-über-qualitätssicherung)
4. [Definitionen](#definitionen)
   - [Qualität (ISO 8402)](#qualität-iso-8402)
   - [Softwarefehler und Ursachen](#softwarefehler-und-ursachen)
5. [Softwareprojekte: Beispiele](#softwareprojekte-beispiele)
6. [Fehlerquellen im Entwicklungsprozess](#fehlerquellen-im-entwicklungsprozess)
7. [Testmethoden](#testmethoden)
8. [Blackbox vs. Whitebox Testing](#blackbox-vs-whitebox-testing)
9. [Refactoring](#refactoring)
10. [Grundsätze des Testens](#grundsätze-des-testens)
11. [Testplanung und -durchführung](#testplanung-und-durchführung)
12. [Testautomatisierung](#testautomatisierung)
13. [Versionsverwaltung: Git](#versionsverwaltung-git)
14. [Werkzeuge für Qualitätssicherung](#werkzeuge-für-qualitätssicherung)
15. [Erfahrungsbasierte Tests und Metriken](#erfahrungsbasierte-tests-und-metriken)
16. [Testen objektorientierter Software](#testen-objektorientierter-software)
17. [Continuous Integration und Scrum](#continuous-integration-und-scrum)
18. [Testarten](#testarten)
    - [Modultest](#modultest)
    - [Integrationstest](#integrationstest)
    - [Systemtest](#systemtest)
    - [Abnahmetest](#abnahmetest)
19. [Spezialfälle des Testens](#spezialfälle-des-testens)
20. [Fehlerkostenschätzung und Fehlerklassifikation](#fehlerkostenschätzung-und-fehlerklassifikation)

---

## Begriffe

| Begriffe                  | Definition                                                                                                                                                                               | Anmerkungen                                                                                                           |
| ------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| **Qualität**              | Qualität ist die Gesamtheit von Merkmalen einer Einheit bezüglich ihrer Eignung, festgelegte und vorausgesetzte Erfordernisse zu erfüllen.                                               | Zu welchem Grad erfüllt die Software die an sie gestellten expliziten und impliziten Anforderungen?                   |
| **Qualitätssicherung**    | Anwendung von Methoden und Techniken, mit deren Hilfe Software-Fehler möglichst frühzeitig erkannt oder von vornherein vermieden werden können.                                          | Abweichungen von der geforderten Qualität verhindern und erkennen. Nicht: Fehler beheben (vgl. Debugging).            |
| **Anforderung**           | Merkmal oder Eigenschaft, welche die Software aufweisen soll. Idealerweise schriftlich genau spezifiziert. Kann auch implizit gefordert sein (berechtigte oder unberechtigte Erwartung). | Eigene Disziplin: Requirements Engineering                                                                            |
| **Test**                  | Eine Aktivität, bei der ein System oder eine Komponente unter festgelegten Bedingungen ausgeführt wird, die Ergebnisse beobachtet oder aufgezeichnet werden und eine Bewertung erfolgt.  | Spezifizieren, ausführen, beobachten, bewerten.                                                                       |
| **Fehler**                | Abweichung der vorhandenen Eigenschaften der Software von den geforderten und erwarteten Eigenschaften.                                                                                  | Die Abweichung ist messbar. Fehler können einander überlagern (Fehlermaskierung).                                     |
| **Debugging**             | Debugging ist der Prozess des Auffindens und Behebens von Defekten oder Problemen innerhalb eines Computerprogramms.                                                                     | Fehlerzustände aufspüren und beheben.                                                                                 |
| **Testobjekt**            | System oder Komponente, die geprüft bzw. getestet wird.                                                                                                                                  | Weitere Begriffe: Prüfling, SUT (System under test), TOE (Target of evaluation).                                      |
| **Testrahmen**            | Testumgebung (Summe aller Hard- und Softwareteile), in welcher der Prüfling zur Ausführung gebracht wird.                                                                                | Speziell modifizierte Komponenten zum Steuern (Point of Control) und Beobachten (Point of Observation) des Prüflings. |
| **Testfall und Testlauf** | Testfall: Beschreibung einer Testaktivität zur Prüfung einer bestimmten Eigenschaft eines Testobjekts. Testlauf: Durchführung eines Testfalls unter definierten Bedingungen.             | Ergebnis eines Testlaufs wird dokumentiert.                                                                           |
| **Tester**                | Allgemein: Person, die eine Testaktivität durchführt. Speziell: Person, die in der Organisation für Testaktivitäten zuständig ist.                                                       | Jeder kann ein Tester sein.                                                                                           |

---

## Definitionen

| Überschrift                                    | Inhalt                                                                                                                                                                                              |
| ---------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Definition von Qualität (ISO 8402)**         | Qualität ist die Gesamtheit von Merkmalen einer Einheit bezüglich ihrer Eignung, festgelegte und vorausgesetzte Erfordernisse zu erfüllen.                                                          |
| **Definition Softwarequalität**                | Fragen: Was ist eigentlich Software-„Qualität“, und was nicht? Wer bewertet, ob eine Software eine ausreichende Qualität hat? Ist Qualität messbar/beweisbar? Wodurch lässt sich Qualität ersetzen? |
| **Definition Softwarequalität nach ISO 25010** | Funktionale Eignung, Zuverlässigkeit, Performanz, Sicherheit, Kompatibilität, Wartbarkeit, Gebrauchstauglichkeit, Übertragbarkeit.                                                                  |

---

## Überblick

- **Qualitätssicherung** ist die Gesamtheit von Maßnahmen, die darauf abzielen, Softwarefehler frühzeitig zu erkennen und zu vermeiden.

- **Softwarefehler** entstehen durch verschiedene Ursachen wie Tippfehler, fehlende Sicherheitsabfragen oder ungeprüfte Wiederverwendung von Code.

- **Testen** ist ein wichtiger Bestandteil der Qualitätssicherung und umfasst sowohl **statische** als auch **dynamische** Testmethoden.

- **Refactoring** beschreibt die Umgestaltung des Quellcodes, ohne das Verhalten des Programms zu ändern, um die Lesbarkeit und Wartbarkeit zu verbessern.

- **Grundsätze des Testens** besagen, dass Testen die Anwesenheit von Fehlern zeigt, vollständiges Testen nicht möglich ist und frühes Testen Zeit und Geld spart.

- **Testplanung und -durchführung** sind wichtige Schritte im Testprozess, um die Qualität der Software zu gewährleisten.

- **Testautomatisierung** ist ein wesentlicher Bestandteil der modernen Qualitätssicherung und hilft dabei, Fehler kontinuierlich zu erkennen.

- **Versionsverwaltung** mit Git ermöglicht es Entwicklern, Änderungen nachzuverfolgen und zusammenzuführen.

- **Werkzeuge für Qualitätssicherung** wie Anforderungsverwaltung, Testfallverwaltung und Fehlerverfolgung unterstützen den Testprozess.

- **Erfahrungsbasierte Tests** und **Metriken** sind wichtige Instrumente, um Softwarequalität zu messen und zu verbessern.

- **Testen objektorientierter Software** stellt besondere Anforderungen an die Testbarkeit und erfordert spezielle Techniken wie Mocking.

- **Continuous Integration** und **Scrum** fördern kurze Entwicklungszyklen und erfordern automatisierte Builds und Tests.

---

## Testarten

### Modultest

Ein **Modultest** (Unit Test) ist die Überprüfung einzelner Module oder Funktionen. Hierbei wird der Quellcode auf Basis von **Unit-Tests** getestet, die typischerweise automatisiert durchgeführt werden.

### Integrationstest

Beim **Integrationstest** werden mehrere Module kombiniert und ihre Interaktionen getestet. Dies stellt sicher, dass die verschiedenen Komponenten eines Systems korrekt zusammenarbeiten.

### Systemtest

Der **Systemtest** überprüft das Gesamtsystem in seiner realen Betriebsumgebung. Es wird getestet, ob die Software als Ganzes die gestellten Anforderungen erfüllt.

### Abnahmetest

Der **Abnahmetest** wird vom Kunden durchgeführt, um zu prüfen, ob die Software alle Anforderungen erfüllt. Dieser Test entscheidet darüber, ob die Software in Produktion gehen kann.

---

## Spezialfälle des Testens

### Smoke Test

Ein **Smoke Test** ist eine einfache Überprüfung, ob das System grundlegend funktioniert, bevor tiefere Tests durchgeführt werden.

### Regressionstest

**Regressionstests** sind dafür gedacht, zu prüfen, ob neue Änderungen bestehende Funktionalitäten unbeabsichtigt beeinflusst haben.

---

## Fehlerkostenschätzung und Fehlerklassifikation

Die **Fehlerkostenschätzung** befasst sich mit der Einschätzung der Kosten, die durch das Beheben von Fehlern entstehen, insbesondere abhängig davon, in welchem Stadium des Entwicklungszyklus die Fehler gefunden werden.

### Fehlerklassifikation:

1. **Kritische Fehler**: Fehler, die das gesamte System unbrauchbar machen.
2. **Schwere Fehler**: Beeinträchtigen wesentliche Teile des Systems, aber eine eingeschränkte Nutzung ist möglich.
3. **Mittlere Fehler**: Betrifft weniger wesentliche Funktionen oder ist leicht zu umgehen.
4. **Geringe Fehler**: Kleinere Anomalien, die keine wesentlichen Auswirkungen haben.

---

## Testmethoden

- **Statische Tests**: Lesen und Analysieren des Quellcodes ohne Ausführung der Software.
- \*\*D

ynamische Tests\*\*: Ausführung der Software mit definierten Testdaten, um deren Verhalten zu überprüfen.

---

## Blackbox vs. Whitebox Testing

- **Blackbox-Test**: Es wird getestet, ob die Software für gegebene Eingaben die korrekten Ausgaben erzeugt, ohne den internen Code zu kennen.
- **Whitebox-Test**: Der Tester kennt den Quellcode und testet, ob die internen Abläufe korrekt funktionieren.

---

## Refactoring

**Refactoring** beschreibt die Umgestaltung des Quellcodes, ohne das Verhalten des Programms zu ändern. Es wird eingesetzt, um die **Lesbarkeit**, **Verständlichkeit** und **Wartbarkeit** zu verbessern.

### Refactoring Patterns

- **Rename**: Umbenennen eines Bezeichners.
- **Extract Method**: Einen wiederholten Codeabschnitt in eine Methode auslagern.
- **Move Field**: Ein Attribut von einer Klasse in eine andere verschieben.

---

## Testplanung und Durchführung

- **Testplanung**: Erstellen eines Testkonzepts mit Testzielen und Endkriterien.
- **Testdurchführung**: Durchführung von Testfällen und Dokumentation der Ergebnisse.

---

## Testautomatisierung

Automatisierung ist ein wesentlicher Bestandteil der modernen Qualitätssicherung:

- **Unit Tests** werden oft durch automatisierte Frameworks wie JUnit ausgeführt.
- **Automatisierte Testläufe** helfen dabei, Fehler während des Entwicklungsprozesses kontinuierlich zu erkennen.

---

## Versionsverwaltung: Git

Git ist ein **verteiltes Versionskontrollsystem**, das es Entwicklern ermöglicht, Änderungen nachzuverfolgen und zusammenzuführen:

- **Lokales Repository**: Änderungen werden lokal gespeichert.
- **Staging Area**: Änderungen werden für den Commit vorbereitet.
- **Branching und Merging**: Arbeiten in verschiedenen Branches und das Zusammenführen von Änderungen.

---

## Werkzeuge für Qualitätssicherung

- **Anforderungsverwaltung**: JIRA, Polarion
- **Testfallverwaltung**: TestRail, Quality Center
- **Fehlerverfolgung**: Redmine, Bugzilla
- **Versionsverwaltung**: Git, GitLab

---

## Continuous Integration und Scrum

- **Continuous Integration** (CI) integriert und testet Codeänderungen kontinuierlich.
- **Scrum** fördert kurze Entwicklungszyklen (Sprints) und erfordert, dass Tests in jedem Zyklus wiederholt und neue Tests hinzugefügt werden.
- **Automatisierte Builds** und Tests sind die Basis von CI und ermöglichen es, Software nach jeder Änderung zu validieren.
