# XSL-Basics
XSL steht für Extensible Stylesheet Language
<!-- warum benutzen wir XSL? -->
XSL ist auf XML ausgerichtet, insbesondere auf stark strukturierte, datenreiche Dokumente, 
die eine umfangreiche Formatierung erfordern. XSL ist für komplexe Formatierungen gedacht, 
bei denen der Inhalt des Dokuments an mehreren Stellen angezeigt werden kann; 
so kann beispielsweise der Text einer Überschrift auch in einem dynamisch generierten Inhaltsverzeichnis erscheinen.


## XPath

<!-- was ist XPath, kurze Erklärung, am besten mit Beispiel -->
XPath ist ein wichtiges Element des XSLT-Standards. XPath steht für XML Path Language
Es kann verwendet werden, um durch Elemente und Attribute in einem XML-Dokument zu __navigieren.__
XPath verwendet Ausdrücke, um "Nodes"(Knoten) oder "Nodesets"(Knotengruppen) in einem XML-Dokument auszuwählen. 
Diese Ausdrücke erinnern stark an die Ausdrücke, die Sie bei der Arbeit mit einem normalen Computerdateisystem sehen.
z.B. `/bookstore/book[1]` Wählt das erste Book-Element aus, das ein Kind des Bookstore-Elements ist.

### Funktionen
Eine Funktion ist einfach ein "Stück" Code, das Sie immer wieder verwenden können, anstatt es mehrfach auszuschreiben.
Funktionen ermöglichen es dem Programmierer, ein Problem in kleinere Teile zu zerlegen, von denen jeder eine bestimmte Aufgabe ausführt.

<!-- kurze Erläuterung der folgenden Funktionen -->

#### concat
Die Funktion Concat in XSLT hilft bei der Verkettung von zwei Zeichenketten(Strings) zu einer einzigen Zeichenkette(String). 
Die Funktion Concat() nimmt alle Argumente entgegen, die nicht die Zeichenkette sind, die in Zeichenketten umgewandelt wurde. 
Wir können so viele Zeichenketten wie möglich übergeben. Die Funktion Concat selbst verkettet die Ausgabe in der Textform.
Grundsätzlich, es nimmt alle Argumente und fügt sie zusammen.
z.B. `Concat(‘x’,’ y’)` – gibt 'xy'.

#### format-number
Die Funktion format-number() wird verwendet, um eine Zahl in eine Zeichenkette umzuwandeln.
z.B. `format-number($eingabezahl, $formatierungsmuster, $formatdefinition?)`

**$eingabezahl:** 
Obligatorisch. Das erste Argument bestimmt die zu formatie­rende Zahl. In XPath 2.0 muss diese vom Typ xs:double sein. 
(In XPath 1.0 wird das Eingabeargument gemäß den Regeln von number() in eine Zahl umgewandelt.)

**$formatierungsmuster:**
Obligatorisch. Das zweite Argument bestimmt das Muster (picture string), das zur Formatierung der übergebenen Zahl verwendet werden soll. 
Im Wesentlichen wird hier die Stellenzahl von Dezimalzahlen sowie die Anzahl von führenden und folgenden Nullen definiert.
Defaultmäßig wird die Ziffer 0 als Platzhalter für auszugebende führende oder folgende Nullen eingesetzt (zero-digit-sign) und das Hashzeichen # 
als Platzhalter für beliebige Ziffern an Stellen, wo deren Ausgabe entfallen kann (digit-sign). Bei Bedarf können aber in einer Formatdeklaration
durch xsl:decimal-format auch andere Zeichen für diese Rollen festgelegt werden.

**$formatdefinition:**
Optional. Das dritte Argument besteht aus dem QName einer durch xsl:decimal-format deklarierten Formatdefinition. In einer sol­chen Definition werden
die bei der Stringausgabe zu verwendenden Zeichen für Dezimaltrenner, Tausendertrennzeichen sowie NaN und weitere festgelegt.
Die Formatdefinition durch xsl:decimal-format hat keinen Einfluss auf die Form des als Formatierungsregel übergebenen zweiten Arguments,
bestimmt aber die dort verwendbaren Zeichensymbole.


#### normalize-space
Es tut drei Dinge: Es werden alle führenden Leerzeichen entfernt. Es entfernt alle nachgestellten Leerzeichen.
Es ersetzt jede Gruppe von aufeinanderfolgenden Leerzeichen durch ein einzelnes Leerzeichen. 
Beispiel: `str = "   cher      cher     tech     " normalize-space(string)`
Ergebnis: "cher cher tech"


#### substring
Die XPath-Funktion substring erlaubt, aus einer Zeichenkette einen Teilstring zu ermitteln.
Die substring-Funktion hat mindestens zwei, optional drei Parameter:
erster Parameter: der String selber
zweiter Parameter: Position der Stelle im String, an der der Teilstring beginnen soll, der vordere Teil wird verworfen.
*dritter Parameter:* Anzahl der Characters, die weiter folgen sollen
Beispiel: `substring('Beatles',1,4)`
Ergebnis: 'Beat'



## Variablen

<!-- was sind variablen, warum benutzen wir sie -->
Variablen werden verwendet, um Informationen zu speichern, die in einem Computerprogramm referenziert und manipuliert werden können. Sie bieten auch die Möglichkeit,
Daten mit einem beschreibenden Namen zu versehen, so dass unsere Programme für den Leser und uns selbst besser verständlich sind. 
Ihr einziger Zweck ist die Kennzeichnung und Speicherung von Daten im Speicher. Diese Daten können dann im gesamten Programm verwendet werden.

### Definition und Scope
Das Element `<xsl:variable>` wird verwendet, um eine lokale oder globale Variable zu deklarieren.
Hinweis: Die Variable ist global, wenn sie als Top-Level-Element deklariert wird, und lokal, wenn sie innerhalb einer Vorlage deklariert wird.

<!-- wie definiert man variablen, welchen scope haben variablen, was gibt es da zu beachten, beispiel -->
Die Synthax zur Definition einer Variablen sieht so aus:
`<xsl:variable name="color" select="'red'" />`

### Variablen benutzen
Es ist hilfreich, sich die Variablen als Behälter für Informationen vorzustellen. 
<!-- wie ruft man eine variable auf -->
Die Synthax zur Benutzung einer Variablen sieht so aus: 
`<xsl:value-of select="color" >`


## Konditionen / Bedingungen

<!-- was sind konditionen, warum brauchen wir die -->
Bedingungen sind Anweisungen, die vom Programmierer erstellt werden und Aktionen
im Programm auswerten, um festzustellen, ob sie wahr oder falsch sind.

### if

<!-- erklärung von if, beispiel, welche einschränkungen gibt es -->
Die Anweisung xsl:if wird eingesetzt, wenn ein Anweisungsabschnitt abhängig von einer Bedingung ausgeführt
oder übersprungen werden soll. Die Formulierung der Bedingung erfolgt mit Hilfe eines XPath-Ausdrucks, der zu einem booleschen Wert ausgewertet wird.
In XSLT <if> kann nur mit einer Bedingung verwendet werden. z.B.
`<xsl:if test="expression">
  ...some output if the expression is true...
</xsl:if>`

### choose -> when
Das `<xsl:choose>`-Element wird in Verbindung mit `<xsl:when>` und `<xsl:otherwise>` verwendet, um mehrere bedingte Tests auszudrücken.

<!-- erklärung von choose when, beispiel -->

Die Instruktion xsl:choose wählt aus einer Gruppe von Template-Anweisungen diejenige aus, für die eine mit xsl:when gestellte Bedingung erfüllt ist.
Ist keine der Bedingungen erfüllt, so tritt der Sequenzkonstruktor des optionalen xsl:otherwise-Containers in Kraft. Ist kein solcher enthalten, geschieht nichts.
Um einen mehrfach bedingten Test in die XML-Datei einzufügen, fügen Sie die Elemente `<xsl:choose>`, `<xsl:when>` und `<xsl:otherwise>` in die XSL-Datei ein z.B.
`<xsl:choose>
  <xsl:when test="kennzeichen='PM'">Potsdam Mittelmark</xsl:when>
  <xsl:when test="kennzeichen='MOL'">Märkisch Oberland</xsl:when>
  <xsl:when test="kennzeichen='B'">Berlin</xsl:when>
  ...
  <xsl:otherwise>
    <xsl:value-of select="kennzeichen"/>
  </xsl:otherwise>
</xsl:choose>`
**Fazit: Das <choose> Element in XSL wird im Vergleich zu anderen Sprachen in einer anderen Konstruktion dargestellt, da es der if-else-Bedingungsanweisung sehr ähnlich ist.**


## Schleifen / for-each
Eine Schleife ist eine Folge von Anweisungen, die ständig wiederholt wird, bis eine bestimmte Bedingung erreicht ist. In der Regel wird ein bestimmter Prozess durchgeführt,
z. B. das Abrufen und Ändern von Daten, und dann wird eine Bedingung überprüft, z. B. ob ein Zähler eine bestimmte Zahl erreicht hat.
<!-- warum schleifen?, wie benutzt man die, was gibt es zu beachten, beispiel -->
Das XSL-Element `<xsl:for-each>` kann verwendet werden, um jedes XML-Element eines bestimmten Knottgruppen(Node-Sets) auszuwählen.
Der Syntax sieht so aus `<xsl:for-each select="name">
   <xsl:value-of select="."/><xsl:element name="br"/>
 </xsl:for-each>` 


## Templates

<!-- was sind templates, warum templates -->
Ein XSL-Stylesheet besteht aus einem oder mehreren Regelsätzen, die als Vorlagen(Templates) genannt werden.
Eine Vorlage enthält Regeln, die angewendet werden, wenn ein bestimmter Knoten übereinstimmt.
Bei XSLT geht es darum, einen oder mehrere Knoten aus Ihrem XML-Dokument auszuwählen und dessen Inhalt zu transformieren oder durch etwas anderes zu ersetzen.
Das match-Attribut wird verwendet, um die Vorlage mit einem XML-Element zu verknüpfen. Das match-Attribut kann auch verwendet werden,
um eine Vorlage für einen ganzen Zweig des XML-Dokuments zu definieren (d. h. match="/" definiert das gesamte Dokument)
Man kann XSLT-Templates als Subroutinen sehen. Sie bieten alle grundlegenden Funktionen/Aktionen.


### Definition

<!-- wie definiert man templates, auch param einführen, beispiel -->
Das ist ein einfaches Beispiel für eine Vorlagendefinition:
`<xsl:template name="format_date">
        <xsl:param name="datetime"/>
        <xsl:value-of select="format-date(substring($datetime, 1, 10), '[D,2].[M,2].[Y]')"/>
 </xsl:template>`

### Aufruf / Templates benutzen
Und so ruft man die Vorlage auf 
<!-- wie ruft man templates auf, auch with-param einführen, beispiel -->
`<xsl:call-template name="format_date">
	<xsl:with-param name="datetime" select="Quote_Set/Quote/expirationdate"/>
</xsl:call-template>`