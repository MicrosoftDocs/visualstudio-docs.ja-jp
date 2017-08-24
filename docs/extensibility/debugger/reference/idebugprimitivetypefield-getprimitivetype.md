---
title: IDebugPrimitiveTypeField::GetPrimitiveType | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- GetPrimitiveType
- IDebugPrimitiveTypeField::GetPrimitiveType
ms.assetid: a186c922-bbfe-478c-a744-b21eb4672d8f
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
ms.sourcegitcommit: ff8ecec19f8cab04ac2190f9a4a995766f1750bf
ms.openlocfilehash: b3117424a4e72ca8cfbe75808ca1f92c3957d51f
ms.contentlocale: ja-jp
ms.lasthandoff: 08/23/2017

---
# <a name="idebugprimitivetypefieldgetprimitivetype"></a>IDebugPrimitiveTypeField::GetPrimitiveType
Retrieves the primitive type that is associated with this field.  
  
## <a name="syntax"></a>Syntax  
  
```cpp#  
HRESULT GetPrimitiveType (  
   DWORD* pdwType  
);  
```  
  
```cs  
int GetPrimitiveType (  
   out uint pdwType  
);  
```  
  
#### <a name="parameters"></a>Parameters  
 `pdwType`  
 [out] Value from the [CorElementType Enumeration](/dotnet/framework/unmanaged-api/metadata/corelementtype-enumeration) that represents the primitive type.  
  
## <a name="return-value"></a>Return Value  
 If successful, returns `S_OK`; otherwise, returns `S_FALSE`.  
  
## <a name="see-also"></a>See Also  
 [IDebugPrimitiveTypeField](../../../extensibility/debugger/reference/idebugprimitivetypefield.md)
