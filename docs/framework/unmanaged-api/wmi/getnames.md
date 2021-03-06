---
title: "Функция GetNames (Справочник по неуправляемым API)"
description: "Функция GetNames извлекает имена свойств объекта."
ms.date: 11/06/2017
ms.prod: .net-framework
ms.technology: dotnet-clr
ms.topic: reference
api_name: GetNames
api_location: WMINet_Utils.dll
api_type: DLLExport
f1_keywords: GetNames
helpviewer_keywords: GetNames function [.NET WMI and performance counters]
topic_type: Reference
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 2ba2530dd43e6924187c80214d5efa13ebc548de
ms.sourcegitcommit: a53799f81351ad9afb3007cd68846ce6aeeb10cb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/15/2017
---
# <a name="getnames-function"></a>GetNames-функция
Возвращает подмножество или все имена свойств объекта. 

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]
    
## <a name="syntax"></a>Синтаксис  
  
```  
HRESULT GetNames (
   [in] int                 vFunc, 
   [in] IWbemClassObject*   ptr, 
   [in] LPCWSTR             wszQualifierName,
   [in] LONG                lFlags,
   [in] VARIANT*            pQualifierValue,
   [out] SAFEARRAY (BSTR)** pstrNames
); 
```  

## <a name="parameters"></a>Параметры

`vFunc`  
[in] Этот параметр не используется.

`ptr`  
[in] Указатель на [IWbemClassObject](https://msdn.microsoft.com/library/aa391433%28v=vs.85%29.aspx) экземпляра.

`wszQualifierName`  
[in] Указатель на допустимый `LPCWSTR` , задающий имя квалификатора, который работает как часть фильтра. Дополнительные сведения см. в разделе [примечания](#remarks) раздела. Этот параметр может иметь значение `null`. 

`lFlags`  
[in] Сочетание битовых полей. Дополнительные сведения см. в разделе [примечания](#remarks) раздела.

`pQualifierValue`   
[in] Указатель на допустимый `VARIANT` структуры инициализирован со значением фильтра. Этот параметр может иметь значение `null`. 

`pstrNames`  
[out] Объект `SAFEARRAY` структуру, содержащую имена свойств. На запись в этот параметр всегда должен быть указателем на `null`. В разделе [примечания](#remarks) Дополнительные сведения. 

## <a name="return-value"></a>Возвращаемое значение

Следующие значения, возвращаемые этой функцией, определяются в *WbemCli.h* файла заголовка, или их можно определить как константы в коде:

|Константа  |Значение  |Описание  |
|---------|---------|---------|
|`WBEM_E_FAILED` | 0x80041001 | Произошел общий сбой. |
|`WBEM_E_INVALID_PARAMETER` | 0x80041008 | Один или несколько параметров недопустимы или указано неверное сочетание флагов и параметры. |
|`WBEM_E_OUT_OF_MEMORY` | 0x80041006 | Недостаточно памяти для завершения операции. |
|`WBEM_S_NO_ERROR` | 0 | Успешный вызов функции.  |
  
## <a name="remarks"></a>Примечания

Эта функция создает оболочку для вызова [IWbemClassObject::GetNames](https://msdn.microsoft.com/library/aa391447(v=vs.85).aspx) метод.

Именованный вернул управляются сочетание флагов и параметры. Например функция может вернуть имена всех свойств или только имена ключевых свойств.  Основным фильтром указывается в `lFlags` параметр, а другие параметры различаются в зависимости от его.

Флаг значений в `lFlags` являются битовые поля


Флаги, которые могут быть переданы как `lEnumFlags` аргумент являются битовые поля, которые определены в *WbemCli.h* файла заголовка, или их можно определить как константы в коде.  Можно объединить один флаг из каждой группы с любого флага из другой группы. Однако флаги из той же группы являются взаимоисключающими. 

| Группа 1 флаги |Значение  |Описание  |
|---------|---------|---------|
| `WBEM_FLAG_ALWAYS` | 0 | Возвращает имена всех свойств. `strQualifierName`и `pQualifierVal` не используются. |
| `WBEM_FLAG_ONLY_IF_TRUE` | 1 | Возвращать только свойства, которые имеют квалификатор имени, указанного параметром `strQualifierName` параметр. Если этот флаг используется, необходимо указать `strQualifierName`. |
|`WBEM_FLAG_ONLY_IF_FALSE` | 2 |  Возвращать только свойства, которые не имеют квалификатор имени, указанного параметром `strQualifierName` параметр. Если этот флаг используется, необходимо указать `strQualifierName`. |
|`WBEM_FLAG_ONLY_IF_IDENTICAL` | 3 | Возвращать только те свойства, которые имеют квалификатор имени, указанного параметром `wszQualifierName` параметр и также имеют значения, идентичные значению, указанному `pQualifierVal` структуры. Если этот флаг используется, необходимо указать и `wszQualifierName` и `pQualifierValue`. |

| Группа 2 флаги |Значение  |Описание  |
|---------|---------|---------|
|`WBEM_FLAG_KEYS_ONLY` | 0x4 | Возвращать только имена свойств, определяющих ключи. |
|`WBEM_FLAG_REFS_ONLY` | 0x8 | Возврат только имена свойств, ссылки на объекты. |

| Флаги группа 3 |Значение  |Описание  |
|---------|---------|---------|
| `WBEM_FLAG_LOCAL_ONLY` | 0x10 | Возвращать только имена свойств, принадлежащих наиболее производного класса. Исключите свойства из родительских классов. |
| `WBEM_FLAG_PROPAGATED_ONLY` |  0x20 | Возвращать только имена свойств, принадлежащих родительских классов. |
|`WBEM_FLAG_SYSTEM_ONLY` | 0x30 | Возвращать только имена системных свойств. |
|`WBEM_FLAG_NONSYSTEM_ONLY` | 0x40 | Возвращать только имена свойств не является системной. |

Функция всегда выделяет новый `SAFEARRAY` при его использовании возвращается `WBEM_S_NO_ERROR`, и `pstrNames` всегда равно наведите на нее. Возвращаемый массив может иметь 0 элементов, если свойства не соответствуют указанным фильтрам. Если функция возвращает значение, отличное от `WBM_S_NO_ERROR`, новый `SAFEARRAY` структуры не возвращается.
 
## <a name="requirements"></a>Требования  
 **Платформы:** разделе [требования к системе для](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Заголовок:** WMINet_Utils.idl  
  
 **Версии платформы .NET framework:**[!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  
  
## <a name="see-also"></a>См. также  
[WMI и счетчиков производительности (Справочник по неуправляемым API)](index.md)
