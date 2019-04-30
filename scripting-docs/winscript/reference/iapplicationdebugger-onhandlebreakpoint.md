---
title: IApplicationDebugger::onHandleBreakPoint |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IApplicationDebugger.onHandleBreakPoint
apilocation:
- scrobj.dll
helpviewer_keywords:
- IApplicationDebugger::onHandleBreakPoint
ms.assetid: 31adcecd-d6c1-4222-ab2c-32ec2fefb322
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: edf8816cd646596ce1f897dfd9d949790d52b7b1
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62991347"
---
# <a name="iapplicationdebuggeronhandlebreakpoint"></a>IApplicationDebugger::onHandleBreakPoint
ブレークポイント イベントを処理します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT onHandleBreakPoint(  
   IRemoteDebugApplicationThread*  prpt,  
   BREAKREASON                     br,  
   IActiveScriptErrorDebug*        pError  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `prpt`  
 [in]スレッドは、ブレークポイントが発生しました。  
  
 `br`  
 [in]ブレークポイントの理由です。  
  
 `pError`  
 [in]時にランタイム エラーについては、指定の値`br`BREAKREASON_ERROR です。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは `HRESULT` を返します。 有効な値を次の表に示しますが、これ以外にもあります。  
  
|[値]|説明|  
|-----------|-----------------|  
|`S_OK`|メソッドが成功しました。|  
  
## <a name="remarks"></a>Remarks  
 ブレークポイントがヒットしたときに、このメソッドを呼び出すと`IDebugApplication::HandleBreakPoint`が呼び出されます。  
  
 デバッガー IDE を呼び出すまで、アプリケーションは中断されたまま`IRemoteDebugApplication::ResumeFromBreakPoint`します。  
  
## <a name="see-also"></a>関連項目  
 [IApplicationDebugger インターフェイス](../../winscript/reference/iapplicationdebugger-interface.md)   
 [IDebugApplication::HandleBreakPoint](../../winscript/reference/idebugapplication-handlebreakpoint.md)   
 [IRemoteDebugApplication::ResumeFromBreakPoint](../../winscript/reference/iremotedebugapplication-resumefrombreakpoint.md)   
 [BREAKREASON 列挙型](../../winscript/reference/breakreason-enumeration.md)