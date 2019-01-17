---
title: IDebugApplicationThread::SynchronousCallIntoThread |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugApplicationThread.SynchronousCallIntoThread
apilocation:
- pdm.dll
helpviewer_keywords:
- IDebugApplicationThread::SynchronousCallIntoThread
ms.assetid: 8a91157f-dade-418a-ad02-5607ce12c95c
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: e5e25f42b2bce66cf3bb7ab3e69d3711e2526ae1
ms.sourcegitcommit: 116e9614867e0b3c627ce9001012a4c39435a42b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/08/2019
ms.locfileid: "54097059"
---
# <a name="idebugapplicationthreadsynchronouscallintothread"></a>IDebugApplicationThread::SynchronousCallIntoThread
呼び出し元アプリケーションのスレッドでコードを実行するためのメカニズムを提供します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT SynchronousCallIntoThread(  
   IDebugThreadCall*  pstcb,  
   DWORD_PTR          dwParam1,  
   DWORD_PTR          dwParam2,  
   DWORD_PTR          dwParam3  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pstcb`  
 [in]呼び出すオブジェクト。  
  
 `dwParam1`  
 [in]最初のパラメーターに渡す、`IDebugThreadCall::ThreadCallHandler`メソッド。  
  
 `dwParam2`  
 [in]2 番目のパラメーターに渡す、`IDebugThreadCall::ThreadCallHandler`メソッド。  
  
 `dwParam3`  
 [in]3 番目のパラメーターに渡す、`IDebugThreadCall::ThreadCallHandler`メソッド。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは `HRESULT` を返します。 有効な値を次の表に示しますが、これ以外にもあります。  
  
|[値]|説明|  
|-----------|-----------------|  
|`S_OK`|メソッドが成功しました。|  
  
## <a name="remarks"></a>Remarks  
 このメソッドは、呼び出し元が、デバッガー スレッドでコードを実行するためのメカニズムを提供します。 言語エンジンとホストは通常、1 つのスレッドの実装の上に、フリー スレッド オブジェクトを実装するためにこのメソッドを使用します。  
  
## <a name="see-also"></a>関連項目  
 [IDebugApplicationThread インターフェイス](../../winscript/reference/idebugapplicationthread-interface.md)   
 [IDebugThreadCall インターフェイス](../../winscript/reference/idebugthreadcall-interface.md)