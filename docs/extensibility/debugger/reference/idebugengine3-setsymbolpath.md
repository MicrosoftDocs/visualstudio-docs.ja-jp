---
title: IDebugEngine3::SetSymbolPath | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- IDebugEngine3::SetSymbolPath
helpviewer_keywords:
- IDebugEngine3::SetSymbolPath
ms.assetid: 47b48f84-8a96-401f-84df-0baa8a96d26e
caps.latest.revision: 12
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
ms.openlocfilehash: 63c68eab87ec26d3cf20c66e7a53061e8be79186
ms.contentlocale: ja-jp
ms.lasthandoff: 08/28/2017

---
# <a name="idebugengine3setsymbolpath"></a>IDebugEngine3::SetSymbolPath
Sets the path or paths that are searched for debugging symbols.  
  
## <a name="syntax"></a>Syntax  
  
```cpp  
HRESULT SetSymbolPath (  
   LPOLESTR            szSymbolSearchPath,  
   LPOLESTR            szSymbolCachePath,  
   LOAD_SYMBOLS_FLAGS  Flags  
);  
```  
  
```csharp  
int SetSymbolPath(  
   string                    szSymbolSearchPath,   
   string                    szSymbolCachePath,   
   enum_LOAD_SYMBOLS_FLAGS   Flags  
);  
```  
  
#### <a name="parameters"></a>Parameters  
  
|Parameter|Description|  
|---------------|-----------------|  
|`szSymbolSearchPath`|[in] String containing the symbol search path or paths. See "Remarks" for details. Cannot be null.|  
|`szSymbolCachePath`|[in] String containing the local path where symbols can be cached. Cannot be null.|  
|`Flags`|[in] Not used; always set to 0.|  
  
## <a name="return-value"></a>Return Value  
 If successful, returns S_OK; otherwise returns an error code.  
  
## <a name="remarks"></a>Remarks  
 The string `szSymbolSearchPath` is a list of one or more paths, separated by semicolons, to search for symbols. These paths can be a local path, a UNC-style path, or a URL. These paths can also be a mix of different types. If the path is UNC (for example, \\\Symserver\Symbols), then the debug engine should determine if the path is to a symbol server and should be able to load symbols from that server, caching them in the path specified by `szSymbolCachePath`.  
  
 The symbol path can also contain one or more cache locations. Caches are listed in priority order, with the highest priority cache first, and separated by * symbols. For example:  
  
```  
\\symbols\symbols;\\someotherserver\symbols;c:\symbols\httpsymbols*http://msdl.microsoft.com  
```  
  
 The [LoadSymbols](../../../extensibility/debugger/reference/idebugengine3-loadsymbols.md) method performs the actual load of the symbols.  
  
## <a name="see-also"></a>See Also  
 [LoadSymbols](../../../extensibility/debugger/reference/idebugengine3-loadsymbols.md)   
 [IDebugEngine3](../../../extensibility/debugger/reference/idebugengine3.md)
