---
title: "Практическое руководство. Создание переключателей в элементах управления ToolStrip"
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
helpviewer_keywords:
- toggle buttons [Windows Forms], creating
- examples [Windows Forms], toolbars
- ToolStrip control [Windows Forms], creating toggle buttons
ms.assetid: d9c197df-4c65-43f2-beee-b68b52b2befc
caps.latest.revision: "9"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.openlocfilehash: a8529637db7bc4cca011d0992b257d5b8ce9aaff
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/21/2017
---
# <a name="how-to-create-toggle-buttons-in-toolstrip-controls"></a>Практическое руководство. Создание переключателей в элементах управления ToolStrip
Когда пользователь щелкает выключатель, он отображается утопленная и остается таковым, пока пользователь снова нажимает кнопку.  
  
### <a name="to-create-a-toggling-toolstripbutton"></a>Чтобы создать переключение видимости ToolStripButton  
  
-   Используйте код, как в следующем примере кода. Предполагается, что форма содержит <xref:System.Windows.Forms.ToolStrip> управления и что его <xref:System.Windows.Forms.ToolStrip.Items%2A> коллекция содержит <xref:System.Windows.Forms.ToolStripButton> вызывается `toolStripButton1`. Он также предполагается, что обработчик событий вызывается `toolStripButton1_CheckedChanged`.  
  
    ```vb  
    toolStripButton1.CheckOnClick = True  
    toolStripButton1.CheckedChanged AddressOf _  
    EventHandler(toolStripButton1_CheckedChanged);  
    ```  
  
    ```csharp  
    toolStripButton1.CheckOnClick = true;  
    toolStripButton1.CheckedChanged += new _  
    EventHandler(toolStripButton1_CheckedChanged);  
    ```  
  
## <a name="see-also"></a>См. также  
 <xref:System.Windows.Forms.ToolStripButton>  
 [Общие сведения об элементе управления ToolStrip](../../../../docs/framework/winforms/controls/toolstrip-control-overview-windows-forms.md)
