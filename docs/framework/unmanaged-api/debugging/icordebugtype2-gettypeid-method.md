---
title: "Метод ICorDebugType2::GetTypeID"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
api_name: ICorDebugType2.GetTypeID
api_location: mscordbi.dll
api_type: COM
f1_keywords: ICorDebugType::GetTypeID
helpviewer_keywords:
- GetTypeID method, ICorDebugType2 interface [.NET Framework debugging]
- ICorDebugType2.GetTypeID method [.NET Framework debugging]
ms.assetid: 0b933686-226e-4373-92b7-fac579ee7b1a
topic_type: apiref
caps.latest.revision: "4"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 30b5259bfd39ac0c8c8b717d59a8d3165f6b6cbf
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/18/2017
---
# <a name="icordebugtype2gettypeid-method"></a>Метод ICorDebugType2::GetTypeID
Возвращает [COR_TYPEID](../../../../docs/framework/unmanaged-api/debugging/cor-typeid-structure.md) для этого типа.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
HRESULT GetTypeID(  
    ([out] COR_TYPEID *id  
);  
```  
  
#### <a name="parameters"></a>Параметры  
 `id`  
 [out] Указатель на [COR_TYPEID](../../../../docs/framework/unmanaged-api/debugging/cor-typeid-structure.md) для ICorDebugType.  
  
## <a name="return-value"></a>Возвращаемое значение  
 Возвращается значение `S_OK` при успешном выполнении или код ошибки `HRESULT` при сбое. `HRESULT` Коды включают следующее:  
  
|Код возврата|Описание|  
|-----------------|-----------------|  
|`S_OK`|Метод успешно выполнен. Метод извлеченные является допустимым [COR_TYPEID](../../../../docs/framework/unmanaged-api/debugging/cor-typeid-structure.md).|  
|`CORDBG_E_CLASS_NOT_LOADED`|Тип не был загружен.|  
|`CORDBG_E_UNSUPPORTED`|Тип не поддерживается.|  
  
## <a name="remarks"></a>Примечания  
 Этот метод обеспечивает сопоставление из ICorDebugType, который представляет тип, который может быть или могут не быть загружены в среду выполнения с [COR_TYPEID](../../../../docs/framework/unmanaged-api/debugging/cor-typeid-structure.md), который служит непрозрачный дескриптор, определяет тип, загружена в среду выполнения.  
  
 Если тип, представляющий ICorDebugType еще не были загружены, этот метод возвращает `CORDBG_E_CLASS_NOT_LOADED`.  Если тип не поддерживается, возвращается `CORDBG_E_UNSUPPORTED`.  
  
## <a name="requirements"></a>Требования  
 **Платформы:** разделе [требования к системе для](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Заголовок:** CorDebug.idl, CorDebug.h  
  
 **Библиотека:** CorGuids.lib  
  
 **Версии платформы .NET framework:**[!INCLUDE[net_current_v462plus](../../../../includes/net-current-v462plus-md.md)]  
  
## <a name="see-also"></a>См. также  
 [Интерфейс ICorDebugType2](../../../../docs/framework/unmanaged-api/debugging/icordebugtype2-interface.md)
