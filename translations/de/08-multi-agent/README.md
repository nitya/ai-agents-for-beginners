# Multi-Agent-Designmuster

Sobald Sie an einem Projekt arbeiten, das mehrere Agenten umfasst, müssen Sie das Multi-Agent-Designmuster in Betracht ziehen. Es ist jedoch nicht sofort ersichtlich, wann der Wechsel zu mehreren Agenten sinnvoll ist und welche Vorteile dies bietet.  

## Einführung

In dieser Lektion wollen wir die folgenden Fragen beantworten:

- Für welche Szenarien sind Multi-Agent-Systeme geeignet? 
- Welche Vorteile bieten Multi-Agent-Systeme gegenüber einem einzigen Agenten, der mehrere Aufgaben übernimmt? 
- Was sind die Bausteine zur Implementierung des Multi-Agent-Designmusters? 
- Wie können wir nachvollziehen, wie die verschiedenen Agenten miteinander interagieren?

## Lernziele

Nach dieser Lektion sollten Sie in der Lage sein:

- Szenarien zu identifizieren, in denen Multi-Agent-Systeme anwendbar sind.
- Die Vorteile von Multi-Agent-Systemen gegenüber einem einzelnen Agenten zu erkennen.
- Die Bausteine zur Implementierung des Multi-Agent-Designmusters zu verstehen.

Was ist der größere Zusammenhang?

*Multi-Agenten sind ein Designmuster, das es mehreren Agenten ermöglicht, zusammenzuarbeiten, um ein gemeinsames Ziel zu erreichen.* 

Dieses Muster wird in verschiedenen Bereichen häufig verwendet, darunter Robotik, autonome Systeme und verteiltes Rechnen. 

## Szenarien, in denen Multi-Agent-Systeme anwendbar sind

Welche Szenarien eignen sich also gut für den Einsatz von Multi-Agenten? Die Antwort lautet, dass es viele Szenarien gibt, in denen der Einsatz mehrerer Agenten von Vorteil ist, insbesondere in den folgenden Fällen:

- **Hohe Arbeitslasten**: Große Arbeitslasten können in kleinere Aufgaben aufgeteilt und verschiedenen Agenten zugewiesen werden, wodurch parallele Verarbeitung und schnellere Fertigstellung ermöglicht werden. Ein Beispiel hierfür ist die Verarbeitung großer Datenmengen.
- **Komplexe Aufgaben**: Komplexe Aufgaben können, ähnlich wie große Arbeitslasten, in kleinere Teilaufgaben zerlegt und verschiedenen Agenten zugewiesen werden, die jeweils auf einen spezifischen Aspekt der Aufgabe spezialisiert sind. Ein gutes Beispiel hierfür sind autonome Fahrzeuge, bei denen verschiedene Agenten für Navigation, Hinderniserkennung und Kommunikation mit anderen Fahrzeugen zuständig sind.
- **Vielfältige Expertise**: Unterschiedliche Agenten können über unterschiedliche Fachkenntnisse verfügen, wodurch sie verschiedene Aspekte einer Aufgabe effektiver bewältigen können als ein einzelner Agent. Ein Beispiel hierfür ist der Gesundheitsbereich, in dem Agenten Diagnosen, Behandlungspläne und Patientenüberwachung verwalten können.

## Vorteile von Multi-Agent-Systemen gegenüber einem einzelnen Agenten

Ein System mit einem einzelnen Agenten könnte für einfache Aufgaben gut funktionieren, aber für komplexere Aufgaben bieten mehrere Agenten einige Vorteile:

- **Spezialisierung**: Jeder Agent kann auf eine spezifische Aufgabe spezialisiert sein. Ein einzelner Agent ohne Spezialisierung könnte zwar alles erledigen, aber bei komplexen Aufgaben überfordert sein oder falsche Entscheidungen treffen.
- **Skalierbarkeit**: Es ist einfacher, Systeme durch Hinzufügen weiterer Agenten zu skalieren, als einen einzelnen Agenten zu überlasten.
- **Fehlertoleranz**: Wenn ein Agent ausfällt, können andere weiterhin funktionieren und die Zuverlässigkeit des Systems sicherstellen.

Betrachten wir ein Beispiel: Eine Reise für einen Benutzer zu buchen. Ein System mit einem einzelnen Agenten müsste alle Aspekte des Buchungsprozesses übernehmen, von der Flugsuche bis zur Hotel- und Mietwagenbuchung. Um dies zu bewältigen, müsste der Agent Werkzeuge für alle diese Aufgaben besitzen. Dies könnte zu einem komplexen und monolithischen System führen, das schwer zu warten und zu skalieren ist. Ein Multi-Agent-System hingegen könnte spezialisierte Agenten für die Flugsuche, die Hotelbuchung und die Mietwagenbuchung haben. Dies würde das System modularer, wartungsfreundlicher und skalierbarer machen.

Vergleichen Sie dies mit einem Reisebüro, das entweder von einem kleinen Familienbetrieb oder als Franchise geführt wird. Der Familienbetrieb hätte einen einzelnen Agenten, der alle Aspekte des Buchungsprozesses übernimmt, während das Franchise verschiedene Agenten für die unterschiedlichen Aufgaben hätte.

## Bausteine zur Implementierung des Multi-Agent-Designmusters

Bevor Sie das Multi-Agent-Designmuster implementieren können, müssen Sie die Bausteine verstehen, aus denen das Muster besteht.

Machen wir dies konkreter, indem wir erneut das Beispiel einer Reisebuchung betrachten. In diesem Fall wären die Bausteine:

- **Agentenkommunikation**: Agenten für die Flugsuche, die Hotelbuchung und die Mietwagenbuchung müssen kommunizieren und Informationen über die Präferenzen und Einschränkungen des Benutzers austauschen. Sie müssen Protokolle und Methoden für diese Kommunikation festlegen. Konkret bedeutet dies, dass der Agent für die Flugsuche mit dem Agenten für die Hotelbuchung kommunizieren muss, um sicherzustellen, dass das Hotel für dieselben Daten wie der Flug gebucht wird. Das bedeutet, dass Sie entscheiden müssen, *welche Agenten Informationen austauschen und wie sie dies tun*.
- **Koordinationsmechanismen**: Agenten müssen ihre Aktionen koordinieren, um sicherzustellen, dass die Präferenzen und Einschränkungen des Benutzers erfüllt werden. Eine Präferenz könnte sein, dass der Benutzer ein Hotel in der Nähe des Flughafens möchte, während eine Einschränkung sein könnte, dass Mietwagen nur am Flughafen verfügbar sind. Dies bedeutet, dass der Agent für die Hotelbuchung mit dem Agenten für die Mietwagenbuchung koordinieren muss, um die Präferenzen und Einschränkungen des Benutzers zu erfüllen. Sie müssen also entscheiden, *wie die Agenten ihre Aktionen koordinieren*.
- **Agentenarchitektur**: Agenten müssen eine interne Struktur haben, um Entscheidungen zu treffen und aus ihren Interaktionen mit dem Benutzer zu lernen. Beispielsweise muss der Agent für die Flugsuche eine interne Struktur haben, um Entscheidungen darüber zu treffen, welche Flüge dem Benutzer empfohlen werden. Sie müssen also entscheiden, *wie die Agenten Entscheidungen treffen und aus ihren Interaktionen mit dem Benutzer lernen*. Ein Beispiel, wie ein Agent lernen und sich verbessern könnte, ist, dass der Agent für die Flugsuche ein maschinelles Lernmodell verwendet, um Flüge basierend auf den bisherigen Präferenzen des Benutzers zu empfehlen.
- **Sichtbarkeit der Multi-Agent-Interaktionen**: Sie müssen nachvollziehen können, wie die verschiedenen Agenten miteinander interagieren. Dazu benötigen Sie Werkzeuge und Techniken, um die Aktivitäten und Interaktionen der Agenten zu verfolgen. Dies könnte in Form von Logging- und Überwachungstools, Visualisierungstools und Leistungsmetriken erfolgen.
- **Multi-Agent-Muster**: Es gibt verschiedene Muster zur Implementierung von Multi-Agent-Systemen, wie zentrale, dezentrale und hybride Architekturen. Sie müssen das Muster auswählen, das am besten zu Ihrem Anwendungsfall passt.
- **Mensch in der Schleife**: In den meisten Fällen wird ein Mensch in den Prozess eingebunden sein, und Sie müssen den Agenten Anweisungen geben, wann sie menschliche Eingriffe anfordern sollen. Dies könnte in Form eines Benutzers geschehen, der ein bestimmtes Hotel oder einen bestimmten Flug anfordert, den die Agenten nicht empfohlen haben, oder um Bestätigung bittet, bevor ein Flug oder Hotel gebucht wird.

## Sichtbarkeit der Multi-Agent-Interaktionen

Es ist wichtig, dass Sie nachvollziehen können, wie die verschiedenen Agenten miteinander interagieren. Diese Sichtbarkeit ist entscheidend für das Debuggen, die Optimierung und die Sicherstellung der Effektivität des Gesamtsystems. Um dies zu erreichen, benötigen Sie Werkzeuge und Techniken, um die Aktivitäten und Interaktionen der Agenten zu verfolgen. Dies könnte in Form von Logging- und Überwachungstools, Visualisierungstools und Leistungsmetriken erfolgen.

Betrachten wir beispielsweise die Buchung einer Reise für einen Benutzer. Sie könnten ein Dashboard haben, das den Status jedes Agenten, die Präferenzen und Einschränkungen des Benutzers sowie die Interaktionen zwischen den Agenten anzeigt. Dieses Dashboard könnte die Reisedaten des Benutzers, die vom Flugagenten empfohlenen Flüge, die vom Hotelagenten empfohlenen Hotels und die vom Mietwagenagenten empfohlenen Mietwagen anzeigen. Dies würde Ihnen einen klaren Überblick darüber geben, wie die Agenten miteinander interagieren und ob die Präferenzen und Einschränkungen des Benutzers erfüllt werden.

Schauen wir uns die einzelnen Aspekte genauer an:

- **Logging- und Überwachungstools**: Sie möchten, dass jede Aktion eines Agenten protokolliert wird. Ein Logeintrag könnte Informationen über den Agenten enthalten, der die Aktion ausgeführt hat, die ausgeführte Aktion, den Zeitpunkt der Aktion und das Ergebnis der Aktion. Diese Informationen können dann für Debugging, Optimierung und mehr verwendet werden.

- **Visualisierungstools**: Visualisierungstools können Ihnen helfen, die Interaktionen zwischen Agenten auf eine intuitivere Weise zu sehen. Zum Beispiel könnten Sie ein Diagramm haben, das den Informationsfluss zwischen Agenten zeigt. Dies könnte Ihnen helfen, Engpässe, Ineffizienzen und andere Probleme im System zu identifizieren.

- **Leistungsmetriken**: Leistungsmetriken können Ihnen helfen, die Effektivität des Multi-Agent-Systems zu verfolgen. Zum Beispiel könnten Sie die Zeit messen, die für die Erledigung einer Aufgabe benötigt wird, die Anzahl der pro Zeiteinheit erledigten Aufgaben und die Genauigkeit der Empfehlungen der Agenten. Diese Informationen können Ihnen helfen, Verbesserungsmöglichkeiten zu identifizieren und das System zu optimieren.

## Multi-Agent-Muster

Schauen wir uns einige konkrete Muster an, die wir zur Erstellung von Multi-Agent-Anwendungen verwenden können. Hier sind einige interessante Muster, die es zu berücksichtigen gilt:

### Gruppenchat

Dieses Muster ist nützlich, wenn Sie eine Gruppenchat-Anwendung erstellen möchten, in der mehrere Agenten miteinander kommunizieren können. Typische Anwendungsfälle für dieses Muster sind Teamzusammenarbeit, Kundensupport und soziale Netzwerke.

In diesem Muster repräsentiert jeder Agent einen Benutzer im Gruppenchat, und Nachrichten werden zwischen Agenten mithilfe eines Nachrichtenprotokolls ausgetauscht. Die Agenten können Nachrichten an den Gruppenchat senden, Nachrichten aus dem Gruppenchat empfangen und auf Nachrichten anderer Agenten antworten.

Dieses Muster kann mit einer zentralisierten Architektur implementiert werden, bei der alle Nachrichten über einen zentralen Server geleitet werden, oder mit einer dezentralisierten Architektur, bei der Nachrichten direkt ausgetauscht werden.

![Gruppenchat](../../../translated_images/multi-agent-group-chat.82d537c5c8dc833abbd252033e60874bc9d00df7193888b3377f8426449a0b20.de.png)

### Übergabe

Dieses Muster ist nützlich, wenn Sie eine Anwendung erstellen möchten, in der mehrere Agenten Aufgaben aneinander übergeben können.

Typische Anwendungsfälle für dieses Muster sind Kundensupport, Aufgabenmanagement und Workflow-Automatisierung.

In diesem Muster repräsentiert jeder Agent eine Aufgabe oder einen Schritt in einem Workflow, und Agenten können Aufgaben basierend auf vordefinierten Regeln an andere Agenten übergeben.

![Übergabe](../../../translated_images/multi-agent-hand-off.ed4f0a5a58614a8a3e962fc476187e630a3ba309d066e460f017b503d0b84cfc.de.png)

### Kollaboratives Filtern

Dieses Muster ist nützlich, wenn Sie eine Anwendung erstellen möchten, in der mehrere Agenten zusammenarbeiten, um Benutzern Empfehlungen zu geben.

Der Grund, warum mehrere Agenten zusammenarbeiten, ist, dass jeder Agent über unterschiedliche Fachkenntnisse verfügt und auf verschiedene Weise zum Empfehlungsprozess beitragen kann.

Nehmen wir ein Beispiel, bei dem ein Benutzer eine Empfehlung für die beste Aktie auf dem Markt wünscht:

- **Branchenexperte**: Ein Agent könnte ein Experte in einer bestimmten Branche sein. 
- **Technische Analyse**: Ein anderer Agent könnte Experte für technische Analysen sein. 
- **Fundamentalanalyse**: Ein weiterer Agent könnte Experte für Fundamentalanalysen sein. Durch die Zusammenarbeit können diese Agenten dem Benutzer eine umfassendere Empfehlung geben.  

![Empfehlung](../../../translated_images/multi-agent-filtering.719217d169391ddb118bbb726b19d4d89ee139f960f8749ccb2400efb4d0ce79.de.png)

## Szenario: Rückerstattungsprozess

Betrachten wir ein Szenario, in dem ein Kunde eine Rückerstattung für ein Produkt anfordert. Es können mehrere Agenten an diesem Prozess beteiligt sein. Lassen Sie uns diese in spezifische Agenten für diesen Prozess und allgemeine Agenten, die auch in anderen Prozessen verwendet werden können, unterteilen.

**Agenten spezifisch für den Rückerstattungsprozess**:

Nachfolgend einige Agenten, die am Rückerstattungsprozess beteiligt sein könnten:

- **Kundenagent**: Dieser Agent repräsentiert den Kunden und ist für die Einleitung des Rückerstattungsprozesses verantwortlich.
- **Verkäuferagent**: Dieser Agent repräsentiert den Verkäufer und ist für die Bearbeitung der Rückerstattung verantwortlich.
- **Zahlungsagent**: Dieser Agent repräsentiert den Zahlungsprozess und ist für die Rückerstattung der Zahlung des Kunden zuständig.
- **Klärungsagent**: Dieser Agent repräsentiert den Klärungsprozess und ist für die Lösung von Problemen zuständig, die während des Rückerstattungsprozesses auftreten.
- **Compliance-Agent**: Dieser Agent repräsentiert den Compliance-Prozess und stellt sicher, dass der Rückerstattungsprozess den Vorschriften und Richtlinien entspricht.

**Allgemeine Agenten**:

Diese Agenten können auch in anderen Geschäftsbereichen verwendet werden.

- **Versandagent**: Dieser Agent repräsentiert den Versandprozess und ist für den Rückversand des Produkts an den Verkäufer verantwortlich. Dieser Agent kann sowohl für den Rückerstattungsprozess als auch für den allgemeinen Versand eines Produkts, z. B. bei einem Kauf, verwendet werden.
- **Feedback-Agent**: Dieser Agent repräsentiert den Feedback-Prozess und ist für das Sammeln von Kundenfeedback zuständig. Feedback kann jederzeit eingeholt werden, nicht nur während des Rückerstattungsprozesses.
- **Eskalationsagent**: Dieser Agent repräsentiert den Eskalationsprozess und ist für die Eskalation von Problemen an eine höhere Supportebene zuständig. Dieser Agent kann für jeden Prozess verwendet werden, bei dem Probleme eskaliert werden müssen.
- **Benachrichtigungsagent**: Dieser Agent repräsentiert den Benachrichtigungsprozess und ist für das Senden von Benachrichtigungen an den Kunden in verschiedenen Phasen des Rückerstattungsprozesses zuständig.
- **Analyseagent**: Dieser Agent repräsentiert den Analyseprozess und analysiert Daten, die mit dem Rückerstattungsprozess zusammenhängen.
- **Audit-Agent**: Dieser Agent repräsentiert den Audit-Prozess und ist für die Prüfung des Rückerstattungsprozesses zuständig, um sicherzustellen, dass er korrekt durchgeführt wird.
- **Berichtsagent**: Dieser Agent repräsentiert den Berichtsprozess und erstellt Berichte über den Rückerstattungsprozess.
- **Wissensagent**: Dieser Agent repräsentiert den Wissensprozess und pflegt eine Wissensdatenbank mit Informationen, die mit dem Rückerstattungsprozess zusammenhängen. Dieser Agent könnte sowohl über Rückerstattungen als auch über andere Geschäftsbereiche informiert sein.
- **Sicherheitsagent**: Dieser Agent repräsentiert den Sicherheitsprozess und stellt die Sicherheit des Rückerstattungsprozesses sicher.
- **Qualitätsagent**: Dieser Agent repräsentiert den Qualitätsprozess und stellt die Qualität des Rückerstattungsprozesses sicher.

Es gibt eine ganze Reihe von Agenten, sowohl für den spezifischen Rückerstattungsprozess als auch für allgemeine Agenten, die in anderen Geschäftsbereichen verwendet werden können. Hoffentlich gibt Ihnen dies eine Vorstellung davon, wie Sie entscheiden können, welche Agenten Sie in Ihrem Multi-Agent-System verwenden möchten.

## Aufgabe

Was wäre eine gute Aufgabe für diese Lektion?

Entwerfen Sie ein Multi-Agent-System für einen Kundensupportprozess. Identifizieren Sie die Agenten, die an diesem Prozess beteiligt sind, ihre Rollen und Verantwortlichkeiten sowie ihre Interaktionen miteinander. Berücksichtigen Sie sowohl Agenten, die spezifisch für den Kundensupportprozess sind, als auch allgemeine Agenten, die in anderen Geschäftsbereichen verwendet werden können.

> Überlegen Sie, bevor Sie die Lösung unten lesen. Sie könnten mehr Agenten benötigen, als Sie denken.

> TIP: Denken Sie an die verschiedenen Phasen des Kundensupportprozesses und berücksichtigen Sie auch Agenten, die für jedes System benötigt werden.

## Lösung

[Solution](./solution/solution.md)

## Wissensfragen

Frage: Wann sollten Sie den Einsatz von Multi-Agenten in Betracht ziehen?

- [] A1: Wenn Sie eine geringe Arbeitslast und eine einfache Aufgabe haben.
- [] A2: Wenn Sie eine hohe Arbeitslast haben.
- [] A3: Wenn Sie eine einfache Aufgabe haben.

[Solution quiz](./solution/solution-quiz.md)

## Zusammenfassung

In dieser Lektion haben wir das Multi-Agent-Designmuster untersucht, einschließlich der Szenarien, in denen Multi-Agent-Systeme anwendbar sind, der Vorteile von Multi-Agent-Systemen gegenüber einem einzelnen Agenten, der Bausteine zur Implementierung des Multi-Agent-Designmusters und der Nachvollziehbarkeit der Interaktionen zwischen den verschiedenen Agenten.

## Zusätzliche Ressourcen

- [Autogen design patterns](https://microsoft.github.io/autogen/stable/user-guide/core-user-guide/design-patterns/intro.html)
- [Agentic design patterns](https://www.analyticsvidhya.com/blog/2024/10/agentic-design-patterns/)
```

**Haftungsausschluss**:  
Dieses Dokument wurde mithilfe von KI-gestützten maschinellen Übersetzungsdiensten übersetzt. Obwohl wir uns um Genauigkeit bemühen, weisen wir darauf hin, dass automatisierte Übersetzungen Fehler oder Ungenauigkeiten enthalten können. Das Originaldokument in seiner ursprünglichen Sprache sollte als maßgebliche Quelle betrachtet werden. Für kritische Informationen wird eine professionelle menschliche Übersetzung empfohlen. Wir übernehmen keine Haftung für Missverständnisse oder Fehlinterpretationen, die aus der Nutzung dieser Übersetzung resultieren.