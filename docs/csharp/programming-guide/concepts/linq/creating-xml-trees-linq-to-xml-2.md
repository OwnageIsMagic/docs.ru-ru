---
title: "Создание деревьев XML в C# (LINQ to XML) | Документы Майкрософт"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: cc74234a-0bac-4327-9c8c-5a2ead15b595
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 92ba0d345183ec503d61254355f948f82a18f053
ms.lasthandoff: 03/13/2017

---
# <a name="creating-xml-trees-in-c-linq-to-xml"></a>Создание деревьев XML в C# (LINQ to XML)
В этом разделе размещены сведения о создании XML-деревьев при помощи языка C#.  
  
 Дополнительные сведения об использовании результатов запросов LINQ как содержимого для <xref:System.Xml.Linq.XElement> см. в разделе [Функциональное построение (LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/functional-construction-linq-to-xml.md).  
  
## <a name="constructing-elements"></a>Построение элементов  
 Сигнатуры конструкторов <xref:System.Xml.Linq.XElement> и <xref:System.Xml.Linq.XAttribute> позволяют передавать конструктору содержимое элемента или атрибута в качестве аргументов. Поскольку один из конструкторов принимает переменное количество аргументов, можно пропустить любое количество дочерних элементов. Естественно, каждый из этих дочерних элементов может содержать собственные дочерние элементы. Для любого элемента можно добавить любое количество атрибутов.  
  
 При добавлении объектов <xref:System.Xml.Linq.XNode> (включая <xref:System.Xml.Linq.XElement>) или <xref:System.Xml.Linq.XAttribute>, если новое содержимое не имеет родителя, объекты просто присоединяются к XML-дереву. Если у нового содержимого уже есть родитель и оно является частью другого XML-дерева, то новое содержимое клонируется и присоединяется к XML-дереву. Это демонстрирует последний пример из данного раздела.  
  
 Для создания <xref:System.Xml.Linq.XElement> `contacts` можно использовать следующий код:  
  
```csharp  
XElement contacts =  
    new XElement("Contacts",  
        new XElement("Contact",  
            new XElement("Name", "Patrick Hines"),   
            new XElement("Phone", "206-555-0144"),  
            new XElement("Address",  
                new XElement("Street1", "123 Main St"),  
                new XElement("City", "Mercer Island"),  
                new XElement("State", "WA"),  
                new XElement("Postal", "68042")  
            )  
        )  
    );  
```  
  
 Если отступы соблюдены верно, то код для создания объектов <xref:System.Xml.Linq.XElement> становится похож на структуру соответствующего XML.  
  
## <a name="xelement-constructors"></a>Конструкторы XElement  
 В классе <xref:System.Xml.Linq.XElement> используются следующие конструкторы для функционального построения. Обратите внимание, что существуют другие конструкторы для <xref:System.Xml.Linq.XElement>, однако, поскольку они не используются для функциональных построений, они здесь не приводятся.  
  
|Конструктор|Описание|  
|-----------------|-----------------|  
|`XElement(XName name, object content)`|Создает <xref:System.Xml.Linq.XElement>. Параметр `name` задает имя элемента; `content` задает содержание элемента.|  
|`XElement(XName name)`|Создает класс <xref:System.Xml.Linq.XElement> с <xref:System.Xml.Linq.XName>, инициализированным для заданного имени.|  
|`XElement(XName name, params object[] content)`|Создает класс <xref:System.Xml.Linq.XElement> с <xref:System.Xml.Linq.XName>, инициализированным для заданного имени. Атрибуты и/или дочерние элементы создаются из содержимого списка параметров.|  
  
 Параметр `content` чрезвычайно гибок. Он поддерживает любой тип объекта, который является действительным дочерним объектом <xref:System.Xml.Linq.XElement>. К различным типам объектов, передающимся в этом параметре, применимы следующие правила.  
  
-   Строка добавляется как текстовое содержимое.  
  
-   <xref:System.Xml.Linq.XElement> добавляется как дочерний элемент.  
  
-   <xref:System.Xml.Linq.XAttribute> добавляется как атрибут.  
  
-   <xref:System.Xml.Linq.XProcessingInstruction>, <xref:System.Xml.Linq.XComment> или <xref:System.Xml.Linq.XText> добавляется в качестве дочернего содержимого.  
  
-   <xref:System.Collections.IEnumerable> перечисляется, и эти правила рекурсивно применяются к результатам.  
  
-   Для любого другого типа вызывается метод `ToString`, при этом результат добавляется как текстовое содержимое.  
  
### <a name="creating-an-xelement-with-content"></a>Создание элемента XElement с содержимым (Content)  
 Можно создать <xref:System.Xml.Linq.XElement> с простым содержимым с помощью одного вызова метода. Чтобы это сделать, укажите содержимое в качестве второго параметра следующим образом:  
  
```csharp  
XElement n = new XElement("Customer", "Adventure Works");  
Console.WriteLine(n);  
```  
  
 В этом примере выводятся следующие данные:  
  
```xml  
<Customer>Adventure Works</Customer>  
```  
  
 Содержимому можно передать любой тип объекта. Например, в следующем коде выполняется создание элемента, в котором в качестве содержимого содержится число с плавающей запятой:  
  
```csharp  
XElement n = new XElement("Cost", 324.50);  
Console.WriteLine(n);  
```  
  
 В этом примере выводятся следующие данные:  
  
```xml  
<Cost>324.5</Cost>  
```  
  
 Число с плавающей запятой помещается в контейнер и передается конструктору. Это число в контейнере преобразуется в строку и используется в качестве содержимого элемента.  
  
### <a name="creating-an-xelement-with-a-child-element"></a>Создание элемента XElement с дочерним элементом  
 Если передать экземпляр класса <xref:System.Xml.Linq.XElement> как аргумент содержимого, конструктор создаст элемент с дочерним элементом:  
  
```csharp  
XElement shippingUnit = new XElement("ShippingUnit",  
    new XElement("Cost", 324.50)  
);  
Console.WriteLine(shippingUnit);  
```  
  
 В этом примере выводятся следующие данные:  
  
```xml  
<ShippingUnit>  
  <Cost>324.5</Cost>  
</ShippingUnit>  
```  
  
### <a name="creating-an-xelement-with-multiple-child-elements"></a>Создание элемента XElement с несколькими дочерними элементами  
 Вы можете передать ряд объектов <xref:System.Xml.Linq.XElement> для содержимого. Каждый объект <xref:System.Xml.Linq.XElement> включается в качестве дочернего элемента.  
  
```csharp  
XElement address = new XElement("Address",  
    new XElement("Street1", "123 Main St"),  
    new XElement("City", "Mercer Island"),  
    new XElement("State", "WA"),  
    new XElement("Postal", "68042")  
);  
Console.WriteLine(address);  
```  
  
 В этом примере выводятся следующие данные:  
  
```xml  
<Address>  
  <Street1>123 Main St</Street1>  
  <City>Mercer Island</City>  
  <State>WA</State>  
  <Postal>68042</Postal>  
</Address>  
```  
  
 Расширив предыдущим пример, можно создать все XML-дерево следующим образом:  
  
```csharp  
XElement contacts =  
    new XElement("Contacts",  
        new XElement("Contact",  
            new XElement("Name", "Patrick Hines"),                                                   
            new XElement("Phone", "206-555-0144"),  
            new XElement("Address",  
                new XElement("Street1", "123 Main St"),  
                new XElement("City", "Mercer Island"),  
                new XElement("State", "WA"),  
                new XElement("Postal", "68042")  
            )  
        )  
    );  
Console.WriteLine(contacts);  
```  
  
 В этом примере выводятся следующие данные:  
  
```xml  
<Contacts>  
  <Contact>  
    <Name>Patrick Hines</Name>  
    <Phone>206-555-0144</Phone>  
    <Address>  
      <Street1>123 Main St</Street1>  
      <City>Mercer Island</City>  
      <State>WA</State>  
      <Postal>68042</Postal>  
    </Address>  
  </Contact>  
</Contacts>  
```  
  
### <a name="creating-an-empty-element"></a>Создание пустого элемента  
 Чтобы создать пустой элемент <xref:System.Xml.Linq.XElement>, нужно просто не передавать никакое содержимое в конструктор. На следующем примере показано создание пустого элемента:  
  
```csharp  
XElement n = new XElement("Customer");  
Console.WriteLine(n);  
```  
  
 В этом примере выводятся следующие данные:  
  
```xml  
<Customer />  
```  
  
### <a name="attaching-vs-cloning"></a>Сравнение присоединения и клонирования  
 Как упоминалось ранее, при добавлении объектов <xref:System.Xml.Linq.XNode> (включая <xref:System.Xml.Linq.XElement>) или <xref:System.Xml.Linq.XAttribute>, если новое содержимое не имеет родителя, объекты просто присоединяются к XML-дереву. Если у нового содержимого уже есть родитель и оно является частью другого XML-дерева, то новое содержимое клонируется и присоединяется к XML-дереву.  
  
```csharp  
// Create a tree with a child element.  
XElement xmlTree1 = new XElement("Root",  
    new XElement("Child1", 1)  
);  
  
// Create an element that is not parented.  
XElement child2 = new XElement("Child2", 2);  
  
// Create a tree and add Child1 and Child2 to it.  
XElement xmlTree2 = new XElement("Root",  
    xmlTree1.Element("Child1"),  
    child2  
);  
  
// Compare Child1 identity.  
Console.WriteLine("Child1 was {0}",  
    xmlTree1.Element("Child1") == xmlTree2.Element("Child1") ?  
    "attached" : "cloned");  
  
// Compare Child2 identity.  
Console.WriteLine("Child2 was {0}",  
    child2 == xmlTree2.Element("Child2") ?  
    "attached" : "cloned");  
```  
  
 В этом примере выводятся следующие данные:  
  
```  
Child1 was cloned  
Child2 was attached  
```  
  
## <a name="see-also"></a>См. также  
 [Создание деревьев XML (C#)](../../../../csharp/programming-guide/concepts/linq/creating-xml-trees.md)