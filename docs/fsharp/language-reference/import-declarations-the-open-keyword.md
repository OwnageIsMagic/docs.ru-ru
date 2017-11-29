---
title: "Объявления импорта: ключевое слово open (F#)"
description: "Дополнительные сведения о объявления импорта F # и как указать модуль или пространство имен, элементы которого можно ссылаться без использования полного имени."
keywords: "visual f#, f#, функциональное программирование"
author: cartermp
ms.author: phcart
ms.date: 05/16/2016
ms.topic: language-reference
ms.prod: .net
ms.technology: devlang-fsharp
ms.devlang: fsharp
ms.assetid: 1e98e48c-52e9-4314-8954-85d5583125f0
ms.openlocfilehash: a6d79bed3dd202657d06956edf9499a9b21a5f03
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/18/2017
---
# <a name="import-declarations-the-open-keyword"></a>Объявления импорта: `open` ключевое слово

> [!NOTE]
Ссылки на справочник по API в этой статье ведут на сайт MSDN.  Работа над справочником по API docs.microsoft.com не завершена.

*Объявление импорта* указывает модуль или пространство имен, элементы которого можно ссылаться без использования полного имени.


## <a name="syntax"></a>Синтаксис

```fsharp
open module-or-namespace-name
```

## <a name="remarks"></a>Примечания
Ссылки на код, используя полное имя пространства имен или модуля путь каждый раз можно создать код, который будет сложно запись, чтение и обслуживание. Вместо этого можно использовать `open` ключевое слово для часто используемых модулей и пространств имен, чтобы при ссылке на член этого модуля или пространства имен, можно использовать краткую форму имени вместо полное доменное имя. Это ключевое слово аналогично `using` ключевого слова C# `using namespace` в Visual C++ и `Imports` в Visual Basic.

Модуль или пространство имен должно быть в одном проекте или в связанном проекте или сборке. Если это не так, можно добавить ссылку на проект, или использовать `-reference` команда`-`строки (или ее сокращением `-r`). Дополнительные сведения см. в разделе [Параметры компилятора](compiler-options.md).

Объявление импорта доступные имена в коде ниже объявления до конца строки, включающего пространства имен, модуля или файла.

При использовании нескольких объявлений импорта, они должны выглядеть на разных строках.

В следующем коде показано использование `open` ключевое слово для упрощения кода.

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet6801.fs)]

Компилятор F # не выдает ошибку или предупреждение при возникновении неоднозначности, когда одно имя содержится в нескольких открытых модуль или пространство имен. В таких случаях F # отдает предпочтение более недавно открывавшихся модуль или пространство имен. Например, в следующем коде `empty` означает `Seq.empty`, даже если `empty` имеется как `List` и `Seq` модулей.

```fsharp
open List
open Seq
printfn "%A" empty
```

Поэтому будьте внимательны при открытии модули или пространства имен например `List` или `Seq` , содержащие члены, которые имеют одинаковые имена, вместо этого рекомендуется использовать полные имена. Следует избегать любой ситуации, в котором код зависит от порядка объявления импорта.


## <a name="namespaces-that-are-open-by-default"></a>Пространства имен, открываемые по умолчанию
Некоторые пространства имен, поэтому часто используются в коде F #, неявно их открытии без необходимости явно указывать объявление импорта. В следующей таблице показаны пространства имен, открываемые по умолчанию.

|Пространство имен|Описание|
|---------|-----------|
|`Microsoft.FSharp.Core`|Содержит определения базовых типов F # для встроенных типов, таких как `int` и `float`.|
|`Microsoft.FSharp.Core.Operators`|Содержит основные арифметические операции, такие как `+` и `*`.|
|`Microsoft.FSharp.Collections`|Содержит неизменяемые классы коллекций, такие как `List` и `Array`.|
|`Microsoft.FSharp.Control`|Содержит типы для управления конструкций, таких как отложенная оценка и асинхронные рабочие потоки.|
|`Microsoft.FSharp.Text`|Содержит функции для форматирования ввода/ВЫВОДА, такие как `printf` функции.|

## <a name="autoopen-attribute"></a>AutoOpen-атрибут
Можно применить `AutoOpen` атрибут к сборке, чтобы автоматически открыть пространство имен или модуль при ссылке на сборку. Можно также применить `AutoOpen` для модуля, чтобы автоматически открывать его при открытии родительского модуля или пространства имен атрибута. Дополнительные сведения см. в разделе [класс Core.AutoOpenAttribute](https://msdn.microsoft.com/visualfsharpdocs/conceptual/core.autoopenattribute-class-%5bfsharp%5d).


## <a name="requirequalifiedaccess-attribute"></a>RequireQualifiedAccess-атрибут
Некоторые модули, записи или объединения типов могут указать `RequireQualifiedAccess` атрибута. При ссылке элементы из этих модулей, записи или объединения, необходимо использовать полное имя независимо от того, следует ли включать объявление импорта. Если вы используете этот атрибут стратегически на типы, определяющие часто используемые имена, поможет избежать конфликтов имен и тем самым сделать код более устойчивым к изменениям в библиотеках. Дополнительные сведения см. в разделе [класс Core.RequireQualifiedAccessAttribute](https://msdn.microsoft.com/visualfsharpdocs/conceptual/core.requirequalifiedaccessattribute-class-%5Bfsharp%5D).


## <a name="see-also"></a>См. также
[# Справочник по языку](index.md)

[Пространства имен](namespaces.md)

[Модули](modules.md)
