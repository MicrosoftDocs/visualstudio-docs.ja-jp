---
title: IRemoteDebugApplicationThread::SetNextStatement |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IRemoteDebugApplicationThread.SetNextStatement
apilocation:
- pdm.dll
helpviewer_keywords:
- IRemoteDebugApplicationThread::SetNextStatement
ms.assetid: 356766da-f7b7-4e8d-b4f3-2ab8da0609b8
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 0c4b19322a15e92adcf2609c479af6b21e2078bd
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62788142"
---
# <a name="iremotedebugapplicationthreadsetnextstatement"></a>IRemoteDebugApplicationThread::SetNextStatement
特定のフレームのコンテキストで指定したコードのコンテキストにできるだけ近い、引き続き強制的に実行します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT SetNextStatement(  
   IDebugStackFrame*   pStackFrame,  
   IDebugCodeContext*  pCodeContext  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pStackFrame`  
 [in]スタック フレーム オブジェクト。 この引数には、null の場合、現在のスタック フレームを使用することを意味する可能性があります。  
  
 `pCodeContext`  
 [in]コード コンテキスト。 この引数には、null の場合、現在のコード コンテキストを使用することを意味する可能性があります。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは `HRESULT` を返します。 有効な値を次の表に示しますが、これ以外にもあります。  
  
|[値]|説明|  
|-----------|-----------------|  
|`S_OK`|メソッドが成功しました。|  
  
## <a name="remarks"></a>Remarks  
 このメソッドは、実行を継続によって指定されたコードのコンテキストにできるだけ近い`pCodeContext`で指定されたフレームのコンテキストで`pStackFrame`します。 これらの引数のいずれかの可能性があります`NULL`、現在のフレームまたはコンテキストを表します。  
  
## <a name="see-also"></a>関連項目  
 [IRemoteDebugApplicationThread インターフェイス](../../winscript/reference/iremotedebugapplicationthread-interface.md)