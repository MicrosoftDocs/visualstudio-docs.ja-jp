---
title: IDebugEngine2::GetEngineID | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- IDebugEngine2::GetEngineID
helpviewer_keywords:
- IDebugEngine2::GetEngineID
ms.assetid: 0d5674c8-a9b9-4b72-8211-d2d68695775a
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
ms.openlocfilehash: 0f680816fb7471334cb081e8d9bcac07faf92a87
ms.contentlocale: ja-jp
ms.lasthandoff: 08/23/2017

---
# <a name="idebugengine2getengineid"></a>IDebugEngine2::GetEngineID
Gets the GUID of the debug engine (DE).  
  
## <a name="syntax"></a>Syntax  
  
```cpp#  
HRESULT GetEngineID(   
   GUID* pguidEngine  
);  
```  
  
```cs  
int GetEngineID(   
   out Guid pguidEngine  
);  
```  
  
#### <a name="parameters"></a>Parameters  
 `pguidEngine`  
 [out] Returns the GUID of the DE.  
  
## <a name="return-value"></a>Return Value  
 If successful, returns `S_OK`; otherwise, returns an error code.  
  
## <a name="remarks"></a>Remarks  
 Some examples of typical GUIDs are `guidScriptEng`, `guidNativeEng`, or `guidSQLEng`. New debug engines will create their own GUID for identification.  
  
## <a name="example"></a>Example  
 The following example shows how to implement this method for a simple `CEngine` object that implements the [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md) interface.  
  
```cpp#  
HRESULT CEngine::GetEngineId(GUID *pguidEngine){    
   if (pguidEngine) {    
      // Set pguidEngine to guidBatEng, as defined in the Batdbg.idl file.    
      // Other languages would require their own guidDifferentEngine to be  
      //defined in the Batdbg.idl file.    
      *pguidEngine = guidBatEng;    
      return NOERROR; // This is typically S_OK.    
   } else {  
      return E_INVALIDARG;    
   }    
}    
```  
  
## <a name="see-also"></a>See Also  
 [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
