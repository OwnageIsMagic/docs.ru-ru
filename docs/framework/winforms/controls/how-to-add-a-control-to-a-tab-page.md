---
title: "Практическое руководство. Добавление элемента управления на вкладку"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-winforms
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- TabPage control
- tab controls [Windows Forms], tab order
- tab pages [Windows Forms], adding controls
ms.assetid: b092532e-7346-469f-b9a1-897f9bea4fb7
caps.latest.revision: "19"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.openlocfilehash: 3ac6e436aeeafcaa66ff0e3bec213c2316302fd6
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/21/2017
---
# <a name="how-to-add-a-control-to-a-tab-page"></a>Практическое руководство. Добавление элемента управления на вкладку
Можно использовать в Windows Forms <xref:System.Windows.Forms.TabControl> для отображения других элементов управления в структуру предприятия. Ниже показано, как добавить кнопку на первую вкладку. Сведения о добавлении значка в часть метки страницу вкладки см [как: изменение внешнего вида элемента управления TabControl в Windows Forms](../../../../docs/framework/winforms/controls/how-to-change-the-appearance-of-the-windows-forms-tabcontrol.md).  
  
### <a name="to-add-a-control-programmatically"></a>Чтобы добавить элемент управления программными средствами  
  
1.  Используйте <xref:System.Windows.Forms.Control.ControlCollection.Add%2A> метод в коллекцию, возвращаемую <xref:System.Windows.Forms.Control.Controls%2A> свойства <xref:System.Windows.Forms.TabPage>:  
  
     [!code-cpp[TabPageControlCollectionHowToAdd#1](../../../../samples/snippets/cpp/VS_Snippets_Winforms/tabpagecontrolcollectionhowtoadd/cpp/add.cpp#1)]
     [!code-csharp[TabPageControlCollectionHowToAdd#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/tabpagecontrolcollectionhowtoadd/cs/add.cs#1)]
     [!code-vb[TabPageControlCollectionHowToAdd#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/tabpagecontrolcollectionhowtoadd/vb/add.vb#1)]  
  
## <a name="see-also"></a>См. также  
 [Элемент управления TabControl](../../../../docs/framework/winforms/controls/tabcontrol-control-windows-forms.md)  
 [Общие сведения об элементе управления TabControl](../../../../docs/framework/winforms/controls/tabcontrol-control-overview-windows-forms.md)  
 [Практическое руководство. Изменение внешнего вида элемента управления TabControl в Windows Forms](../../../../docs/framework/winforms/controls/how-to-change-the-appearance-of-the-windows-forms-tabcontrol.md)  
 [Практическое руководство. Блокировка доступа ко вкладкам](../../../../docs/framework/winforms/controls/how-to-disable-tab-pages.md)  
 [Практическое руководство. Добавление и удаление вкладок с помощью элемента управления TabControl в Windows Forms](../../../../docs/framework/winforms/controls/how-to-add-and-remove-tabs-with-the-windows-forms-tabcontrol.md)
