---
title: "Метод IAssemblyName::GetName"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: IAssemblyName.GetName
api_location: fusion.dll
api_type: COM
f1_keywords: IAssemblyName::GetName
helpviewer_keywords:
- GetName method, IAssemblyName interface [.NET Framework debugging]
- IAssemblyName::GetName method [.NET Framework fusion]
ms.assetid: 1dee9781-1cf3-48a9-a376-d18ea1f73280
topic_type: apiref
caps.latest.revision: "10"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 612efc9d5334fd34cc61f2243914de59370c45a0
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/18/2017
---
# <a name="iassemblynamegetname-method"></a>Метод IAssemblyName::GetName
Получает простое, нешифрованное имя сборки, упоминаемой в этом [IAssemblyName](../../../../docs/framework/unmanaged-api/fusion/iassemblyname-interface.md) объекта.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
HRESULT GetName (  
    [in, out] LPDWORD lpcwBuffer,  
    [out]     WCHAR *pwzName  
);  
```  
  
#### <a name="parameters"></a>Параметры  
 `lpcwBuffer`  
 [in, out] Размер `pwzName` из расширенных символов, включая завершающий символ null-символ.  
  
 `pwzName`  
 [out] Буфер для хранения имени сборки.  
  
## <a name="requirements"></a>Требования  
 **Платформы:** разделе [требования к системе для](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Заголовок:** Fusion.h  
  
 **Версии платформы .NET framework:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>См. также  
 [IAssemblyName-интерфейс](../../../../docs/framework/unmanaged-api/fusion/iassemblyname-interface.md)
