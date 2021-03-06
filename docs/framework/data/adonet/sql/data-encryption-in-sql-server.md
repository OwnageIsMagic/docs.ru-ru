---
title: "Шифрование данных в SQL Server"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-ado
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 83b992f7-b351-4678-b4b9-f4ffd58134cc
caps.latest.revision: "6"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 4428cf8fbfcaa853ca2c877a8cc4902f585b6754
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/21/2017
---
# <a name="data-encryption-in-sql-server"></a>Шифрование данных в SQL Server
SQL Server содержит функции шифрования и расшифровки данных с помощью сертификата и асимметричного или симметричного ключа. Все они содержатся во внутреннем хранилище сертификатов. Хранилище использует иерархию шифрования, обеспечивающую безопасность сертификатов и ключей на уровне, находящемся выше в иерархии. Эта область функций SQL Server называется секретным хранилищем.  
  
 Самым быстрым режимом шифрования, поддерживаемым функциями шифрования, является шифрование с помощью симметричного ключа. Этот режим подходит для управления большими томами данных. Симметричные ключи могут быть зашифрованы сертификатами, паролями или другими симметричными ключами.  
  
## <a name="keys-and-algorithms"></a>Ключи и алгоритмы  
 SQL Server поддерживает несколько алгоритмов шифрования симметричным ключом, включая DES, Triple DES, RC2, RC4, 128-разрядный RC4, DESX, 128-разрядный AES, 192-разрядный AES и 256-разрядный AES. Алгоритмы реализуются с помощью API-интерфейса Windows Crypto.  
  
 В пределах соединения с базой данных SQL Server может поддерживать несколько открытых симметричных ключей. Открытый ключ получается из хранилища и доступен для расшифровки данных. Не нужно указывать, какой симметричный ключ будет использоваться для расшифровки фрагмента данных. Каждое зашифрованное значение содержит идентификатор ключа (идентификатор GUID ключа), использованного для его шифрования. Если расшифрован и открыт верный ключ, то ядро сопоставляет зашифрованный поток байтов с открытым симметричным ключом. Этот ключ затем используется для выполнения расшифровки и возвращения данных. Если верный ключ не открыт, возвращается значение NULL.  
  
 Пример, демонстрирующий способы работы с зашифрованными данными в базе данных см. в разделе [как: шифрование столбца данных](http://go.microsoft.com/fwlink/?LinkID=128559) в электронной документации по SQL Server.  
  
## <a name="external-resources"></a>Внешние ресурсы  
 Дополнительные сведения о шифровании см. в одном из следующих источников.  
  
|||  
|-|-|  
|[Шифрование SQL Server](http://msdn.microsoft.com/library/bb510663.aspx) в электронной документации по SQL Server|Содержит общие сведения о шифровании в SQL Server. Этот раздел включает ссылки на дополнительные разделы и инструкции.|  
|[Иерархия средств шифрования](http://msdn.microsoft.com/library/ms189586.aspx) и [инструкции по шифрованию](http://msdn.microsoft.com/library/aa337557.aspx) в электронной документации по SQL Server|Содержит общие сведения о шифровании в SQL Server. В этом разделе даны ссылки на дополнительные разделы и инструкции.|  
  
## <a name="see-also"></a>См. также  
 [Защита приложений ADO.NET](../../../../../docs/framework/data/adonet/securing-ado-net-applications.md)  
 [Сценарии безопасности приложений в SQL Server](../../../../../docs/framework/data/adonet/sql/application-security-scenarios-in-sql-server.md)  
 [Проверка подлинности в SQL Server](../../../../../docs/framework/data/adonet/sql/authentication-in-sql-server.md)  
 [Сервер и роли базы данных в SQL Server](../../../../../docs/framework/data/adonet/sql/server-and-database-roles-in-sql-server.md)  
 [Владение и отделение пользователей от схем в SQL Server](../../../../../docs/framework/data/adonet/sql/ownership-and-user-schema-separation-in-sql-server.md)  
 [Авторизация и разрешения в SQL Server](../../../../../docs/framework/data/adonet/sql/authorization-and-permissions-in-sql-server.md)  
 [Центр разработчиков наборов данных и управляемых поставщиков ADO.NET](http://go.microsoft.com/fwlink/?LinkId=217917)
