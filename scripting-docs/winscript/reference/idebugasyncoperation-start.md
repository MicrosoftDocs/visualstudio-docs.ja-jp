---
title: IDebugAsyncOperation::Start |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugAsyncOperation.Start
apilocation:
- pdm.dll
helpviewer_keywords:
- IDebugAsyncOperation::Start
ms.assetid: a7272364-28e0-48ae-8405-b8bce8a6b9fd
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: b3e02869abab65878412f96b77d5782b9717a1b6
ms.sourcegitcommit: d3a485d47c6ba01b0fc9878cbbb7fe88755b29af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2019
ms.locfileid: "58155707"
---
# <a name="idebugasyncoperationstart"></a>IDebugAsyncOperation::Start
非同期の操作が開始されます。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT Start(  
   IDebugAsyncOperationCallBack*  padocb  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `padocb`  
 この操作からステータス イベントを受信するコールバック インターフェイス。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは `HRESULT` を返します。 有効な値を次の表に示しますが、これ以外にもあります。  
  
|[値]|説明|  
|-----------|-----------------|  
|`S_OK`|メソッドが成功しました。|  
|`E_UNEXPECTED`|操作が、既に保留中です。|  
  
## <a name="remarks"></a>Remarks  
 このメソッドにより`IDebugSyncOperation::Execute`から取得したスレッドで非同期的に呼び出される`IDebugSyncOperation::GetTargetThread`します。 このメソッドは、デバッガーのスレッド内からのみ呼び出す必要があります。それ以外の場合、操作が完了するまでを返すことはできません。  
  
## <a name="see-also"></a>関連項目  
 [IDebugAsyncOperation::Abort](../../winscript/reference/idebugasyncoperation-abort.md)   
 [IDebugAsyncOperation インターフェイス](../../winscript/reference/idebugasyncoperation-interface.md)   
 [IDebugSyncOperation::Execute](../../winscript/reference/idebugsyncoperation-execute.md)   
 [IDebugSyncOperation::GetTargetThread](../../winscript/reference/idebugsyncoperation-gettargetthread.md)