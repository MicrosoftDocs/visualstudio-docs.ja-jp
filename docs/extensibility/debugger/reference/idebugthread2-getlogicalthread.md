---
title: IDebugThread2::GetLogicalThread |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugThread2::GetLogicalThread
helpviewer_keywords:
- IDebugThread2::GetLogicalThread
ms.assetid: bce6230e-41d4-49b7-a050-2dde5efb6805
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 99e8dbd78ef262479fbc8405b77fa0cf53f8087a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62915572"
---
# <a name="idebugthread2getlogicalthread"></a>IDebugThread2::GetLogicalThread
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

デバッグ エンジンは、このメソッドを実装していません。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT GetLogicalThread(   
   IDebugStackFrame2*     pStackFrame,  
   IDebugLogicalThread2** ppLogicalThread  
);  
```  
  
```csharp  
int GetLogicalThread(   
   IDebugStackFrame2        pStackFrame,  
   out IDebugLogicalThread2 ppLogicalThread  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pStackFrame`  
 [in][IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)スタック フレームを表すオブジェクト。  
  
 `ppLogicalThread`  
 [out]返します、`IDebugLogicalThread2`関連付けられた論理スレッドを表すインターフェイスです。 デバッグ エンジンの実装は、null 値にこれを設定する必要があります。  
  
## <a name="return-value"></a>戻り値  
 デバッグ エンジン実装を常に戻り`E_NOTIMPL`します。  
  
## <a name="see-also"></a>関連項目  
 [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
