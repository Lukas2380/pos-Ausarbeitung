# Pos-Ausarbeitung

##  1) Datentypen und Datenkonvertierungen in C#

### 1.1) Datentypen

Werttypen und Verweistypen sind die beiden Hauptkategorien von C#-Typen.

* Wertetypen

    Wertetypen werden im Arbeitsspeicher direkt abgespeichert und enthalten einen Wert. Eine Variable eines Werttyps enthält eine Instanz des Typs. Jede Variable hat       eine eigene Kopie der Daten, und auf eine Variable angewendete Vorgänge können die anderen Variablen nicht beeinflussen.

    Wertetypen sind z.B:

    | Typschlüsselwort | Wert                                                 |
    | ---------------- | ---------------------------------------------------- |
    | bool             | true / false                                         |
    | char             | ein Unicode-Zeichen                                  |
    | int              | Ganzzahlen                                           |
    | float            | Ganzzahlen + Gleitkommazahlen bis 7 Nachkommastellen |

* Verweistypen

    Verweistypen beinhalten eine Referenz auf den Speicherort. Also einen Verweis auf eine Instanz des Typs. Dadurch, dass bei Verweistypen zwei Variablen auf dasselbe     Objekt verweisen, können auf eine Variable angewendete Operationen das Objekt beeinflussen, auf das von der anderen Variablen verwiesen wird. 

    Verweistypen sind Typen die als ```class```, `delegate`, `Array` oder `interface` definiert sind. Wenn eine Variable eines Verweistypen deklariert wird, dann           enthält sie den Wert null, bis eine Instanz dieses Typs zugewiesen oder über den new-Operator eine Instanz erstellt wird. 
    Als Beispiel hier mit einer Klasse: 
    ```cs
    MyClass myClass = new MyClass();
    MyClass myClass2 = myClass;
    ```

### 1.2) Datenkonvertierungen

Datenkonvertierung ist der Prozess der Umwandlung von Daten von einem Datentyp in einen anderen. Es gibt zwei Arten von Datenkonvertierung:

* Implizite Konvertierung

    Keine besondere Syntax ist für das implizite Konvertieren erforderlich da die Konvertierung immer erfolgreich ist und keine Daten verloren gehen. 
    Beispiele sind Konvertierungen von kleinere in größere Ganzzahltypen wie, wenn ein ```int``` zu einem ```long``` konvertiert wird.

    ```cs
    // Ein long kann alles halten was ein int halten kann.
    int num = 2147483647;
    long bigNum = num;
    ```

* Expliziete Konvertierung
     Der Compiler fordert eine explizite Konvertierung wenn eine Konvertierung nicht ohne möglichen Informationsverlust durchgeführt werden kann. Will man einen String      in einen Integer umwandeln dann gibt es verschiedene Wege:
     
    * **Cast**:
    
        ```cs
        string stringNum = "123";
        int intNum = (int)stringNum;
        ```
        Cast funktioniert nur dann, wenn der Wert des Strings tatsächlich in einen Integer umgewandelt werden kann.

    * **Verwendung der Methode `int.Parse()`**
    
        ```cs
        string stringNum = "123"; 
        int intNum = int.Parse(stringNum);
        ```
        `int.Parse()` funktioniert genau so wie `Convert.ToInt32()`. Bei beiden besteht das selbe Problem, dass genauso eine Ausnahme ausgelöst wird wenn die                   Umwandlung nicht gültig ist.
    * **Verwendung von `TryParse()`**

        ```cs
        string stringNum = "123";
        int intNum;
        bool success = int.TryParse(stringNum, out intNum);
        if (success) {
        // Der String konnte erfolgreich in einen Integer umgewandelt werden.
        } else {
        // Der String konnte nicht in einen Integer umgewandelt werden.
        }
        ```
        Im Gegensatz zu den anderen Methoden gibt `int.TryParse()` keinen Fehler aus, wenn der String nicht in einen gültigen Integer umgewandelt werden kann.                  Stattdessen gibt es einen boolschen Rückgabewert zurück, der angibt, ob die Konvertierung erfolgreich war oder nicht. Wenn die Konvertierung erfolgreich                war, wird der konvertierte Integer in der Variable "intNum" gespeichert. Andernfalls bleibt die Variable "intNum" unverändert.



##  2) Collections in C#

Collections sind Datentypen in C#, die eine Gruppe von Objekten speichern. Die Collection-Typen umfassen beispielsweise List, Dictionary und Stack. Diese Datentypen sind sehr nützlich, um Daten zu organisieren und zu verwalten. Im Gegensatz zu Arrays können Collections dynamisch erweitert werden.

In C# gibt es verschiedene Datentypen für Collections, die es ermöglichen, mehrere Werte in einer einzigen Variablen zu speichern und zu verwalten. Zu den Collection-Datentypen in C# gehören beispielsweise:

*  `List <T>`
*  `Dictionary <T>`  
*  `Queue <T>`
*  `LinkedList <T>`
*  `SortedDictionary<K,V> SortedList\<K,V>` 
*  `Stack<T>`
*  `HashSet <T>`

### List \<T>
Stellt eine stark typisierte Liste von Objekten dar, auf die über einen Index zugegriffen werden kann. Stellt Methoden zum Durchsuchen, Sortieren und Bearbeiten von Listen bereit.
####  Beispiel:

```cs
	public static void Main(string[] args)
	{
		List<int> myintegers = new List<int>();
		myintegers.Add(1);
		myintegers.Add(2);
		myintegers.Add(3);

		foreach (int i in myintegers)
		{
			Console.Write(i.ToString()); // 1 2 3
		}
	}
```
#### Eigenschaften:

| Name  |  Eigenschaft |
| ------------ | ------------ |
| Capacity  | Ruft die Gesamtzahl der Elemente ab, die die interne Datenstruktur ohne Änderung der Größe aufnehmen kann, oder legt diese Anzahl fest.  |
| Count  | Ruft die Anzahl der Elemente ab, die in List<T> enthalten sind.  |
| Item[Int32] | Ruft das Element am angegebenen Index ab oder legt dieses fest. |

Diese Eigenschaften sind nicht spezifisch für die List, andere Arten der Collection haben diese, vielleicht in einer leicht abweichenden Art, auch. 

### Dictionary \<K,V>
Das Dictionary speichert eine Sammlung von eindeutigen Schlüssel-Wert(key-value) Paaren, wobei jeder Schlüssel eindeutig ist und auf einen bestimmten Wert verweist. Diese Collection ist besonders nützlich, wenn man schnell auf bestimmte Elemente zugreifen möchte. Bei einem Dictionary müssen alle Schlüssel und Werte (jeweils) den selben Typen haben.

#### Eigenschaften: 
|  Name | Eigenschaft |
| ------------ | ------------ |
| Count  |  Ruft die Anzahl der Schlüssel-Wert-Paare im `Dictionary<TKey,TValue>` ab. |
| Item[TKey]  | Ruft den Wert ab, der dem angegebenen Schlüssel zugeordnet ist, oder legt diesen fest.  |
| Keys  |  Ruft eine Auflistung ab, die die Schlüssel im `Dictionary<TKey,TValue>` enthält. |
| Values  | Ruft eine Auflistung ab, die die Werte im `Dictionary<TKey,TValue>` enthält.  |


#### Beispiel:
~~~cs
IDictionary<int, string> numberNames = new Dictionary<int, string>();
~~~

 * Die Schlüsselklasse muss Vergleichsoperationen durchführen können. Das heißt gegebenenfalls muss diese eine `CompareTo` Methode implementiert haben.
 * Die Schlüssel müssen einzigartig sein. (unique)  
Also wenn man versucht ein Element mit einem Schlüssel hinzuzufügen wenn bereits ein Schlüssel im Dictionary verwendet wird, wird das Programm eine Exception werfen.
 * Ein Schlüssel darf nicht `null` sein.

 #### Methoden:
 *  `Remove(TKey)`
    * löscht das Elemente und liefert true zurück wenn das Element erfolgreich gefunden wurde.
 *  `Item [TKey]`
    *   Der Wert wird anhand eines Schlüssels zurückgegeben bzw. gesetzt.
 *  `Add(TKey, TValue)`
    *  Der Schlüssel und der Wert werden hinzugefügt.

### Queues \<T>
Eine Queue ist eine Collection, die nach dem Prinzip "First-In-First-Out" (FIFO) funktioniert. Das erste Element, das in die Queue eingefügt wird, ist das erste, das aus der Queue entfernt wird. 

![](https://www.tutorialsteacher.com/Content/images/csharp/csharp-queue.png)

#### Die wichtigsten Methoden:
* `Enqueue(T Element)`
  *  Ein Element vom generischen Typ T wird der Warteschlange hinzugefügt.
* `T Deque()`
  *  Es wird ein Elenemt am Kopf der Queue entfernt und das Objekt wird zurückgegeben.
* `Clear(), Contains(T Element), Peek(), ....`

### SortedDictionary\<K,V> SortedList\<K,V>
Das SortedDictionary und die Sorted List sind ähnlich strukturiert wie ein gewöhnlichtes Dictionary/List wobei diese anhand der Schlüssel sortiert werden können.
*   Ist ein Array von 'Key-Value-Pairs'
*   Ein Schlüssel muss 'unique' sein und darf nicht `null` sein
*   Eine SortedList benötigt weniger Speicher als ein SortedDictionary.
*   Die SortedList ist schneller beim Datenabruf als ein SortedDictionary.
*   Das SortedDictionary ist jedoch schneller beim Einfügen und Löschen von 'Key-Value-Pairs'.

### Stack \<T>
Ein Stack ist eine Collection, die nach dem Prinzip "Last-In-First-Out" (LIFO) funktioniert. Das letzte Element, das in den Stack eingefügt wird, ist das erste, das aus dem Stack entfernt wird.
	
![](https://f4n3x6c5.stackpathcdn.com/UploadFile/78607b/stack-in-C-Sharp/Images/Stack.jpg)
#### Die wichtigesten Methoden:
*   `Push(T item) `
    * Fügt ein Element oben auf den Stack hinzu.
*   `T Peek()`
    *  Retourned das oberste Stack-Element.
*   `T Pop()`
    * Entfernt das oberste Element vom Stack und es wird zurückgegeben.
*  `Contains(T item)`
    * Überprüft ob ein existierendes Element sich auf dem Stack befindet oder nicht.
*  `Clear()`
    *   Entfernt alle Element vom Stack.


### HashSet\<T>
Die `HashSet<T>` Klasse stellt hochperformante Vorgänge zu Verfügung. Das Set ist eine Auflistung, die keine doppelten Elemente enthält und wo diese sich in keiner Reihenfolge befinden. Neben den üblichen generischen Methoden wie Add, Count, Contains, Clear und vielen anderne verfügt die `HashSet<T>` Klasse auch viele Methoden die bekannt sind aus der Mengenlehre:

+   `UnionWith`
+   `IntersectWith`
+   `ExceptWith`
+   `SymetricExeptWith`
+   `IsSubSetOf`
+   `IsSuperSetOf`


#### Vergleich zu Arrays
Ein Array ist jedoch eine feste Sammlung von Elementen, die bei der Deklaration eine bestimmte Größe haben muss und nicht dynamisch erweitert werden kann. Die interne Speicherung eines Arrays erfolgt in der Regel als zusammenhängender Block im Speicher, während Collections typischerweise auf dynamisch allokiertem Speicher arbeiten.


## 3) Permanentes Speichern von Daten
In C# gibt es verschiedene Möglichkeiten, Daten permanent zu speichern. Hier sind einige Beispiele:

### 3.1) Textdateien
Textdateien sind einfache, zeichenorientierte Dateien, die Text in einem bestimmten Format enthalten und von Mensch und Maschiene lesbar sind. Sie sind einfach zu erstellen und zu lesen, aber sie bieten keine Möglichkeit, komplexe Datenstrukturen oder Objekte zu speichern. 

##### C# stellt die folgenden Klassen zur Verfügung um Files und Verzeichnisse zu verwalten:

* File
* FileInfo
* Directory
* DirectoryInfo
* Path
* StreamReader/StreamWriter
* BinaryReader/BinaryWriter

###Dateien lesen und schreiben
Es gibt mehrere Wege, um mithilfe von System.IO, von einem File zu lesen oder in ein File zu schreiben. Bei allen Methoden muss man wissen wo genau das File liegt sonst wirft der Compiler einen Fehler.

#### Auslesen mithilfe von der `System.IO.File` Klasse:
###### Beispiel:
```cs
string text = System.IO.File.ReadAllText(@"C:\MyFolder\MyTextFile.txt");
// oder
string[] lines = System.IO.File.ReadAllLines(@"C:\MyFolder\MyTextFile.txt");
```
#### Schreiben mithilfe von der `System.IO.File` Klasse:
###### Beispiel:
```cs
string text = "String that will be stored in the file";
System.IO.File.WriteAllText(@"C:\MyFolder\OutputFile.txt", text);
// oder
string[] lines = { "My first string", "My second string", "and even a third string" };
System.IO.File.WriteAllLines(@"C:\MyFolder\OutputFile.txt", lines);
```

#### Mithilfe der System.IO.StreamWriter Klasse:
Mit dieser Methodik kann man Zeile für Zeile in ein File schreiben.
###### Beispiel:
```cs
string[] lines = { "My first string", "My second string", "and even a third string" };
using (System.IO.StreamWriter sw = new System.IO.StreamWriter(@"C:\MyFolder\OutputText.txt"))
	{
 		foreach (string line in lines)
 	{
 		sw.WriteLine(line);
	 }
}

```
\* Man bemerke das `using` Keywort. Dieses versichert, dass das Object des StreamWriters zerstört wird sobald es nicht mehr gebraucht wird.

###Datei erstellen
Mit der Statischen Create funktion von der File Klasse kann man leicht Dateien erstellen. Die Methode creiert ein File am angegebenen Pfad und gleichzeitig öffnet es das File und gibt die Möglichkeit mit `FileStream` etwas zu machen. Der Stream muss im Nachhinein wieder geschlossen werden.
###### Beispiel:
```cs
// Erste Möglichkeit:
string[] lines = { "My first string", "My second string", "and even a third string" };
System.IO.File.WriteAllLines(@"C:\MyFolder\OutputFile.txt", lines);

// Zweite Möglichkeit:
using(var fileStream1 = File.Create("samplePath"))
{
 /// you can write to the fileStream1
}

// Dritte Möglichkeit:
File.Create("samplePath").Close();
```



### 3.2) CSV-Dateien
CSV steht für "Comma Separated Values" und ist ein Dateiformat, das häufig zum Speichern von Tabellen verwendet wird. CSV-Dateien können einfach mit C# gelesen und geschrieben werden, und es gibt viele Bibliotheken, die das Lesen und Schreiben von CSV-Dateien erleichtern.
###### Beispiel:
```cs
using System.IO;

string[] rows = {"Name, Alter", "Max Mustermann, 30", "Anna Müller, 25"};
string path = @"C:\temp\example.csv";

File.WriteAllLines(path, rows);
```

### 3.3) Binärdateien
Binärdateien sind Dateien, die Daten in binärer Form enthalten. Sie können komplexe Datenstrukturen und Objekte speichern, aber sie sind schwieriger zu lesen und zu bearbeiten als Textdateien. Binärdateien können in C# mit der Klasse System.IO.BinaryWriter und System.IO.BinaryReader erstellt und bearbeitet werden. 

###### Beispiel:

```cs
using System.IO;

string text = "Dies ist ein Text, der in die Binärdatei geschrieben wird.";
int number = 42;
string path = @"C:\temp\example.bin";

using (BinaryWriter writer = new BinaryWriter(File.Open(path, FileMode.Create)))
{
    writer.Write(text);
    writer.Write(number);
}
```

### 3.4) Datenbanken
Datenbanken sind eine leistungsstarke Möglichkeit, Daten permanent zu speichern und abzurufen. Sie können komplexe Datenstrukturen und Objekte speichern und sind in der Lage, große Datenmengen effizient zu verwalten. C# unterstützt verschiedene Arten von Datenbanken, wie z.B. Microsoft SQL Server, MySQL oder MongoDB. Die zwei besten Möglichkeiten sich mit einer Datenbank zu verbinden sind: 

* Einen SQL Server im Hintergrund laufen zu haben und sich mittels Code wie diesen zu verbinden:

	```cs
	private void Connect(){
	   string connectionString = @"Data Source=MyServerName;Initial Catalog=MyDbName; User ID=Admin; Password=Root";
	   SqlConnection connection = new SqlConnection(connectionString);
	   connection.Open();
	   // Hier Inhalte lesen/schreiben
	   connection.Close();
	}
	```

* Oder mittels Entity Framework:
	Entity Framework wurde von Microsoft entwickelt und dient dazu die Datenbankverbindung für Entwickler zu erleichtern. Es erleichtert den Zugriff auf 		Datenbanken, indem es Objekte als Schnittstelle zwischen der Anwendung und der Datenbank verwendet.

	###### Eine Tabelle die mittels Entity Framework mit Code geschrieben wurde könnte so Ähnlich aussehen: 
	```cs
	using System;
	using System.Data.Entity;

	public class Customer
	{
	    public int Id { get; set; }
	    public string Name { get; set; }
	    public string Email { get; set; }
	}

	```

### 4) Delegates

In C# ist ein Delegate ein spezieller Typ, der eine Referenz auf eine Methode mit einem bestimmten Signatur enthält. Mit Delegates können Methoden als Parameter an andere Methoden übergeben oder als Rückgabewert zurückgegeben werden.

Delegates werden oft in der ereignisgesteuerten Programmierung verwendet, um Event-Handler-Funktionen zu definieren, die aufgerufen werden, wenn ein bestimmtes Ereignis eintritt. Delegates können auch in der asynchronen Programmierung und in der parallelen Programmierung nützlich sein.

#### Deklaration eines Delegates:
```cs
public delegate int PerformCalculation(int x, int y);
```

#### Eigenschaften eines Delegates:
* sind Zeiger auf eine Methode und sind vollständig objektorientiert.
* kapseln sowohl eine Objektinstanz als auch eine Methode.
* ermöglichen es Methoden als Parameter zu übergeben.
* können zum Definieren von Rückrufmethoden verwendet werden.
* können miteinander verkettet werden (Es können mehrere Methoden für ein einziges Event aufgerufen werden).
* Methoden müssen nicht exakt mit dem Typ des Delegaten übereinstimmen (Varianz in Delgates).
* Lambdaausdrücke sind eine präzisere Methode zum Schreiben von Inlinecodeblöcken. Lambdaausdrücke werden (in bestimmten Kontexten) in Delegattypen kompiliert.

Hier ist ein Beispiel für die Verwendung von Delegates in C#:

``` cs
public delegate int MathOperation(int x, int y);

public class Calculator {
    public int Add(int x, int y) {
        return x + y;
    }

    public int Subtract(int x, int y) {
        return x - y;
    }

    public int Calculate(int x, int y, MathOperation operation) {
        return operation(x, y);
    }
}

public class Program {
    static void Main(string[] args) {
        Calculator calculator = new Calculator();

        MathOperation operation = calculator.Add;
        int result = operation(2, 3); // result is 5

        operation = calculator.Subtract;
        result = operation(5, 3); // result is 2

        result = calculator.Calculate(2, 3, operation); // result is also 2
    }
}

```
