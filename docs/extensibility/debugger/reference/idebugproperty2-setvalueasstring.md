---
title: IDebugProperty2::SetValueAsString | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- IDebugProperty2::SetValueAsString
helpviewer_keywords:
- IDebugProperty2::SetValueAsString
ms.assetid: 9e6a5054-41b7-4223-b509-b93689d366a5
caps.latest.revision: 10
ms.author: gregvanl
manager: ghogen
translation.priority.mt:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
ms.translationtype: MT
ms.sourcegitcommit: 4a36302d80f4bc397128e3838c9abf858a0b5fe8
ms.openlocfilehash: 4a8fe4e1a40aa9ab33cd0cfdb925bbb4f0607fbd
ms.contentlocale: ja-jp
ms.lasthandoff: 08/28/2017

---
# <a name="idebugproperty2setvalueasstring"></a>IDebugProperty2::SetValueAsString
Sets the value of a property from a given string.  
  
## <a name="syntax"></a>Syntax  
  
```cpp  
HRESULT SetValueAsString (   
   LPCOLESTR pszValue,  
   UINT      nRadix,  
   DWORD     dwTimeout  
);  
```  
  
```csharp  
int SetValueAsString (   
   string pszValue,  
   uint   nRadix,  
   uint   dwTimeout  
);  
```  
  
#### <a name="parameters"></a>Parameters  
 `pszValue`  
 [in] A string containing the value to be set.  
  
 `nRadix`  
 [in] A radix to be used in interpreting any numerical information. This can be 0 to attempt to determine the radix automatically.  
  
 `dwTimeout`  
 [in] Specifies the maximum time, in milliseconds, to wait before returning from this method. Use `INFINITE` to wait indefinitely.  
  
## <a name="return-value"></a>Return Value  
 If successful, returns `S_OK`; otherwise returns error code. The following table shows other possible values.  
  
|Value|Description|  
|-----------|-----------------|  
|`E_SETVALUE_VALUE_CANNOT_BE_SET`|The string could not be converted into a property value, or the property value could not be set.|  
|`E_SETVALUE_VALUE_IS_READONLY`|The property is read-only.|  
  
## <a name="see-also"></a>See Also  
 [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
