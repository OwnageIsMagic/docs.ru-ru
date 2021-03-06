---
title: "Оператор new (Справочник по C#)"
ms.date: 07/20/2015
ms.prod: .net
ms.technology: devlang-csharp
ms.topic: article
helpviewer_keywords: new operator keyword [C#]
ms.assetid: a212b697-a79b-4105-9923-1f7b108036e8
caps.latest.revision: "22"
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: 3c2b484b9872a54ce42520de77a723b9edb441a9
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/21/2017
---
# <a name="new-operator-c-reference"></a>Оператор new (Справочник по C#)
Применяется для создания объектов и вызова конструкторов. Например:  
  
```  
Class1 obj  = new Class1();  
```  
  
 Он также используется для создания экземпляров анонимных типов.  
  
```  
var query = from cust in customers  
            select new {Name = cust.Name, Address = cust.PrimaryAddress};  
```  
  
 С помощью оператора `new` можно вызвать заданный по умолчанию конструктор для типов значений. Например:  
  
```  
int i = new int();  
```  
  
 В предыдущем операторе `i` инициализируется значением `0`, которое является значением по умолчанию для типа `int`. Этот оператор приводит к результату, представленному далее.  
  
```  
int i = 0;  
```  
  
 Полный список значений по умолчанию см. в разделе [Таблица значений по умолчанию](../../../csharp/language-reference/keywords/default-values-table.md).  
  
 Следует помнить, что объявление конструктора по умолчанию для [структуры](../../../csharp/language-reference/keywords/struct.md) является ошибкой, поскольку каждый тип значения неявно имеет открытый заданный по умолчанию конструктор. Можно объявить параметризованные конструкторы в типе структуры, чтобы задать начальные значения, однако это необходимо, только если требуются значения, отличные от установленных по умолчанию.  
  
 Объекты типа значения, например структуры, создаются в стеке, тогда как объекты ссылочного типа, например классы, создаются в куче. Уничтожение обоих типов объектов выполняется автоматически, но объекты на основе типов значений удаляются при выходе за рамки области действия, а объекты на основе ссылочных типов — в неуказанное время после удаления последней ссылки, указывающей на них. Для ссылочных типов, использующих фиксированные ресурсы, например большой объем памяти, файловые дескрипторы, сетевые подключения, иногда рекомендуется использовать детерминированную финализацию для обеспечения скорейшего уничтожения объекта. Дополнительные сведения см. в разделе [Оператор using](../../../csharp/language-reference/keywords/using-statement.md).  
  
 Оператор `new` перегрузить нельзя.  
  
 Если оператору `new` не удается выделить память, он создает исключение <xref:System.OutOfMemoryException>.  
  
## <a name="example"></a>Пример  
 В следующем примере создаются объект `struct` и объект класса, которые инициализируются с помощью оператора `new`, после чего им присваиваются значения. Отображаются заданные по умолчанию и присвоенные значения.  
  
 [!code-csharp[csrefKeywordsOperator#7](../../../csharp/language-reference/keywords/codesnippet/CSharp/new-operator_1.cs)]  
  
 Обратите внимание, что в примере строка имеет значение по умолчанию `null`. Поэтому она не отображается.  
  
## <a name="c-language-specification"></a>Спецификация языка C#  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>См. также  
 [Справочник по C#](../../../csharp/language-reference/index.md)  
 [Руководство по программированию на C#](../../../csharp/programming-guide/index.md)  
 [Ключевые слова в C#](../../../csharp/language-reference/keywords/index.md)  
 [Ключевые слова операторов](../../../csharp/language-reference/keywords/operator-keywords.md)  
 [new](../../../csharp/language-reference/keywords/new.md)  
 [Анонимные типы](../../../csharp/programming-guide/classes-and-structs/anonymous-types.md)
