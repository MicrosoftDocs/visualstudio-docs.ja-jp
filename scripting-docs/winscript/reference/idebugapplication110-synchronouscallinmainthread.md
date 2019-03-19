---
title: IDebugApplication110::SynchronousCallInMainThread |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IDebugApplication110::SynchronousCallInMainThread
ms.assetid: 57475ae5-1520-45ef-800d-ccfc6235a5d1
caps.latest.revision: 5
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 25742c5284c7f0f0a8ba91065489f1c6a24e072a
ms.sourcegitcommit: d3a485d47c6ba01b0fc9878cbbb7fe88755b29af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2019
ms.locfileid: "58149433"
---
# <a name="idebugapplication110synchronouscallinmainthread"></a>IDebugApplication110::SynchronousCallInMainThread
メイン スレッドで同期呼び出しを実行します。  
  
> [!IMPORTANT]
>  [IDebugApplication110 インターフェイス](../../winscript/reference/idebugapplication110-interface.md)PDM v11.0 以降によって実装された以降には。 activdbg100.h にあります。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT SynchronousCallInMainThread([in] IDebugThreadCall* pptc, [in] DWORD_PTR dwParam1, [in] DWORD_PTR dwParam2, [in] DWORD_PTR dwParam3);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pptc`  
 [IDebugThreadCall インターフェイス](../../winscript/reference/idebugthreadcall-interface.md)を呼び出すオブジェクト。  
  
 `dwParam1`  
 呼び出しの最初のパラメーター。  
  
 `dwParam1`  
 呼び出しの最初のパラメーター。  
  
 `dwParam2`  
 呼び出しの 2 番目のパラメーター。  
  
 `dwParam3`  
 呼び出しの 3 番目のパラメーター。  
  
## <a name="see-also"></a>関連項目  
 [IDebugApplication110 インターフェイス](../../winscript/reference/idebugapplication110-interface.md)