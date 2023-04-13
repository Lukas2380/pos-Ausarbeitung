# Pos-Ausarbeitung

###  1) Datentypen und Datenkonvertierungen in C#

#### 1.1) Datentypen

Werttypen und Verweistypen sind die beiden Hauptkategorien von C#-Typen.

* Wertetypen
Wertetypen werden im Arbeitsspeicher direkt abgespeichert und enthalten einen Wert. Eine Variable eines Werttyps enthält eine Instanz des Typs. Jede Variable hat eine eigene Kopie der Daten, und auf eine Variable angewendete Vorgänge können die anderen Variablen nicht beeinflussen.

Wertetypen sind z.B:

| Typschlüsselwort | Wert                                                 |
| ---------------- | ---------------------------------------------------- |
| bool             | true / false                                         |
| char             | ein Unicode-Zeichen                                  |
| int              | Ganzzahlen                                           |
| float            | Ganzzahlen + Gleitkommazahlen bis 7 Nachkommastellen |

* Verweistypen
Verweistypen beinhalten eine Referenz auf den Speicherort. Also einen Verweis auf eine Instanz des Typs. Dadurch, dass bei Verweistypen zwei Variablen auf dasselbe Objekt verweisen, können auf eine Variable angewendete Operationen das Objekt beeinflussen, auf das von der anderen Variablen verwiesen wird. 

Verweistypen sind Typen die als ```class```, `delegate`, `Array` oder `interface` definiert sind. Wenn eine Variable eines Verweistypen deklariert wird, dann enthält sie den Wert null, bis eine Instanz dieses Typs zugewiesen oder über den new-Operator eine Instanz erstellt wird. 
Als Beispiel hier mit einer Klasse: 
```
MyClass myClass = new MyClass();
MyClass myClass2 = myClass;
```

* Datenkonvertierungen

Datenkonvertierung ist der Prozess der Umwandlung von Daten von einem Datentyp in einen anderen. Es gibt zwei Arten von Datenkonvertierung:

* Implizite Konvertierung
Keine besondere Syntax ist für das implizite Konvertieren erforderlich da die Konvertierung immer erfolgreich ist und keine Daten verloren gehen. 
Beispiele sind Konvertierungen von kleinere in größere Ganzzahltypen wie, wenn ein ```int``` zu einem ```long``` konvertiert wird.

	```c#
// Ein long kann alles halten was ein int halten kann.
int num = 2147483647;
long bigNum = num;
```

* Expliziete Konvertierung
Der Compiler fordert eine explizite Konvertierung wenn eine Konvertierung nicht ohne möglichen Informationsverlust durchgeführt werden kann. Will man einen String in einen Integer umwandeln dann gibt es verschiedene Wege:
* Cast:
```c#
string stringNum = "123";
int intNum = (int)stringNum;
```
Cast funktioniert nur dann, wenn der Wert des Strings tatsächlich in einen Integer umgewandelt werden kann.

* Verwendung der Methode `int.Parse()`
```c#
string stringNum = "123"; 
int intNum = int.Parse(stringNum);
```
`int.Parse()` funktioniert genau so wie `Convert.ToInt32()`. Bei beiden besteht das selbe Problem, dass genauso eine Ausnahme ausgelöst wird wenn die Umwandlung nicht gültig ist.
* Verwendung von `TryParse()`

```c#
string stringNum = "123";
int intNum;
bool success = int.TryParse(stringNum, out intNum);
if (success) {
// Der String konnte erfolgreich in einen Integer umgewandelt werden.
} else {
// Der String konnte nicht in einen Integer umgewandelt werden.
}
```
Im Gegensatz zu den anderen Methoden gibt `int.TryParse()` keinen Fehler aus, wenn der String nicht in einen gültigen Integer umgewandelt werden kann. Stattdessen gibt es einen boolschen Rückgabewert zurück, der angibt, ob die Konvertierung erfolgreich war oder nicht. Wenn die Konvertierung erfolgreich war, wird der konvertierte Integer in der Variable "intNum" gespeichert. Andernfalls bleibt die Variable "intNum" unverändert.
