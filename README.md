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



###  2) Collections in C#

Collections sind Datentypen in C#, die eine Gruppe von Objekten speichern. Die Collection-Typen umfassen beispielsweise List, Dictionary und Stack. Diese Datentypen sind sehr nützlich, um Daten zu organisieren und zu verwalten. Im Gegensatz zu Arrays können Collections dynamisch erweitert werden.

In C# gibt es verschiedene Datentypen für Collections, die es ermöglichen, mehrere Werte in einer einzigen Variablen zu speichern und zu verwalten. Zu den Collection-Datentypen in C# gehören beispielsweise:

* `List<T>`:
Stellt eine stark typisierte Liste von Objekten dar, auf die über einen Index zugegriffen werden kann. Stellt Methoden zum Durchsuchen, Sortieren und Bearbeiten von Listen bereit.
Syntax: 
`List<int> nums = new List<int>(); // Eine Liste von Integers.`

Eigenschaften:


| Name  |  Eigenschaft |
| ------------ | ------------ |
| Capacity  | Ruft die Gesamtzahl der Elemente ab, die die interne Datenstruktur ohne Änderung der Größe aufnehmen kann, oder legt diese Anzahl fest.  |
| Count  | Ruft die Anzahl der Elemente ab, die in List<T> enthalten sind.  |
| Item[Int32] | Ruft das Element am angegebenen Index ab oder legt dieses fest. |
Diese Eigenschaften sind nicht spezifisch für die List, andere Arten der Collection haben diese, vielleicht in einer leicht abweichenden Art, auch. 

Besondere Methoden:

| Methodenname  | Beschreibung |
| ------------ | ------------ |
| Add(T)  |  Fügt am Ende der Liste ein Objekt hinzu. |
| AddRange(IEnumerable<T>) | Fügt die Elemente der angegebenen Auflistung am Ende von der Liste hinzu.  |
| Clear() | Entfernt alle Elemente aus der Liste.  |
| Contains(T)  | Bestimmt, ob sich ein Element in List<T> befindet.   |
| CopyTo(T[]) | Kopiert die gesamte List<T> in ein kompatibles eindimensionales Array, wobei am Anfang des Zielarrays begonnen wird. |
| Insert(Int32, T) | Fügt am angegebenen Index ein Element in die List<T> ein. |

* `Dictionary<TKey, TValue>`:
Das Dictionary speichert eine Sammlung von Schlüssel-Wert-Paaren, wobei jeder Schlüssel eindeutig ist und auf einen bestimmten Wert verweist. Diese Collection ist besonders nützlich, wenn man schnell auf bestimmte Elemente zugreifen möchte.
Syntax:
`Dictionary<int, string> dictionary = new Dictionary<int, string>(); // Ein Dictionary mit einem Integer als Key und einem String als Value`

* `Queue<T>`:
Eine Queue ist eine Collection, die nach dem Prinzip "First-In-First-Out" (FIFO) funktioniert. Das erste Element, das in die Queue eingefügt wird, ist das erste, das aus der Queue entfernt wird.
![](https://www.tutorialsteacher.com/Content/images/csharp/csharp-queue.png)
Syntax: 
`Queue<string> numbers = new Queue<string>(); // Eine Queue mit den Namen von Zahlen als strings`


* `Stack<T>`
Ein Stack ist eine Collection, die nach dem Prinzip "Last-In-First-Out" (LIFO) funktioniert. Das letzte Element, das in den Stack eingefügt wird, ist das erste, das aus dem Stack entfernt wird.
![](https://f4n3x6c5.stackpathcdn.com/UploadFile/78607b/stack-in-C-Sharp/Images/Stack.jpg)

Arrays hingegen sind auch eine Möglichkeit, eine Sammlung von Elementen in C# zu speichern. Ein Array ist jedoch eine feste Sammlung von Elementen, die bei der Deklaration eine bestimmte Größe haben muss und nicht dynamisch erweitert werden kann. Die interne Speicherung eines Arrays erfolgt in der Regel als zusammenhängender Block im Speicher, während Collections typischerweise auf dynamisch allokiertem Speicher arbeiten.

