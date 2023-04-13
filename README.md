### 4) Delegates

In C# ist ein Delegate ein spezieller Typ, der eine Referenz auf eine Methode mit einem bestimmten Signatur enthält. Mit Delegates können Methoden als Parameter an andere Methoden übergeben oder als Rückgabewert zurückgegeben werden.

Delegates werden oft in der ereignisgesteuerten Programmierung verwendet, um Event-Handler-Funktionen zu definieren, die aufgerufen werden, wenn ein bestimmtes Ereignis eintritt. Delegates können auch in der asynchronen Programmierung und in der parallelen Programmierung nützlich sein.

#### Deklaration eines Delegates:
```
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

``` 
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
