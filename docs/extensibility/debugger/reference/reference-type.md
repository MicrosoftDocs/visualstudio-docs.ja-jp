---
title: REFERENCE_TYPE |Microsoft ドキュメント
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- REFERENCE_TYPE
helpviewer_keywords:
- REFERENCE_TYPE enumeration
ms.assetid: b1ffba10-eb9d-48ba-bf48-6d8b71d6f270
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 1c30bb562784d9de0d9b44a2c3169b595bb4bd39
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/16/2018
ms.locfileid: "31127143"
---
# <a name="referencetype"></a>REFERENCE_TYPE
参照型を指定します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
enum enum_REFERENCE_TYPE {   
   REF_TYPE_WEAK   = 0x0001,  
   REF_TYPE_STRONG = 0x0002  
};  
typedef DWORD REFERENCE_TYPE;  
```  
  
```csharp  
public enum enum_REFERENCE_TYPE {   
   REF_TYPE_WEAK   = 0x0001,  
   REF_TYPE_STRONG = 0x0002  
};  
```  
  
## <a name="members"></a>メンバー  
 REF_TYPE_WEAK  
 弱い参照を指定します。 組み合わせて使用できない`REF_TYPE_STRONG`です。  
  
 REF_TYPE_STRONG  
 強い参照を指定します。 組み合わせて使用できない`REF_TYPE_WEAK`です。  
  
## <a name="remarks"></a>コメント  
 として使用される、`dwRefType`のメンバー、 [DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md)構造体。  
  
 パラメーターとして渡される、 [SetReferenceType](../../../extensibility/debugger/reference/idebugreference2-setreferencetype.md)メソッドです。  
  
## <a name="requirements"></a>要件  
 ヘッダー: msdbg.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>関連項目  
 [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md)   
 [SetReferenceType](../../../extensibility/debugger/reference/idebugreference2-setreferencetype.md)