---
title: IDebugAddress2::GetProcessID | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- IDebugAddress2::GetProcessID
helpviewer_keywords:
- IDebugAddress2::GetProcessID method
ms.assetid: 2c18889d-074a-4b95-87b4-bf1a067f44ed
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 79cff8c6e0dea1ae4b954a4592debdb3ba8331c2
ms.sourcegitcommit: 2193323efc608118e0ce6f6b2ff532f158245d56
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/25/2019
ms.locfileid: "55001135"
---
# <a name="idebugaddress2getprocessid"></a>IDebugAddress2::GetProcessID
これによって表されるオブジェクトを所有するプロセスの ID を取得[IDebugAddress2](../../../extensibility/debugger/reference/idebugaddress2.md)インターフェイス。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetProcessID (  
   DWORD* pProcID  
);  
```  
  
```csharp  
int GetProcessID (  
   out uint pProcID  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pProcID`  
 [out]プロセス id です。  
  
## <a name="return-value"></a>戻り値  
 成功した場合、S_OK を返します。それ以外の場合、エラー コードを返します。  
  
## <a name="see-also"></a>関連項目  
 [IDebugAddress2](../../../extensibility/debugger/reference/idebugaddress2.md)