---
title: "Служба: количество сбоев при проверке безопасности и проверке подлинности"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 55c98268-b1ad-459d-851b-25ef52248187
caps.latest.revision: "7"
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.openlocfilehash: 808c0d648043df6c5a3dda4646e45ba1492345a0
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/18/2017
---
# <a name="service-security-validation-and-authentication-failures"></a>Служба: количество сбоев при проверке безопасности и проверке подлинности
Имя счетчика: Security Validation and Authentication Failures  
  
## <a name="description"></a>Описание  
 Значение этого счетчика увеличивается всякий раз, когда сообщение отклоняется из-за проблемы безопасности, не относящейся к счетчику "Security Calls Not Authorized". К таким проблемам относятся следующие.  
  
-   Невозможно прочесть в этом сообщении маркер клиента.  
  
-   Маркер клиента не прошел проверку подлинности (например, неправильный пароль).  
  
-   Сбой при проверке подписи (например, сообщение было искажено).  
  
-   Сообщение является копией предыдущего, что может свидетельствовать об атаке воспроизведения.  
  
-   Произошел сбой при расшифровке.  
  
-   В сообщении отсутствуют некоторые обязательные элементы (например, отсутствует отметка времени или зашифрованный блок данных).  
  
-   Во время подтверждения TLSNEGO/SPNEGO произошли ошибки.
