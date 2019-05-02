---
title: IActiveScriptSiteDebugEx::OnCanNotJITScriptErrorDebug |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptSiteDebugEx.OnCanNotJITScriptErrorDebug
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScriptSiteDebugEx::OnCanNotJITScriptErrorDebug
ms.assetid: 83f81476-bf12-47f2-897d-1d37d21137d4
caps.latest.revision: 6
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 4c643478da37b5a66c22b201ef8f8248df02e4ec
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62992338"
---
# <a name="iactivescriptsitedebugexoncannotjitscripterrordebug"></a>IActiveScriptSiteDebugEx::OnCanNotJITScriptErrorDebug
プロセス デバッグ マネージャーとは、スクリプト実行時のエラーについて、ホストには、Just In Time スクリプト デバッガーが見つからないことを通知します。  
  
 処理する必要があります、デバッガーに、ホストを実装する[IActiveScriptSiteDebug::OnScriptErrorDebug](../../winscript/reference/iactivescriptsitedebug-onscripterrordebug.md)します。 ユーザー操作に基づいて、ホストか、デバッガーをアタッチ、戻ってください。 または、OnScriptErrorDebug のデバッガーの起動を返す`pfEnterDebugger`パラメーター。 プロセス デバッグ マネージャーによって、解釈される外部のデバッガーがない場合でも、実行時エラーについての通知を取得するには、このインターフェイスを実装することも必要があります。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT OnCanNotJITScriptErrorDebug(  
   IActiveScriptErrorDebug*  pErrorDebug  
   BOOL *pfCallOnScriptErrorWhenContinuing  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pErrorDebug`  
 [in]発生した実行時エラー。  
  
 `pfCallOnScriptErrorWhenContinuingt`  
 [out]呼び出すかどうか[IActiveScriptSiteDebug::OnScriptErrorDebug](../../winscript/reference/iactivescriptsitedebug-onscripterrordebug.md)デバッグなしで続行をユーザーが決定した場合。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは `HRESULT` を返します。 有効な値を次の表に示しますが、これ以外にもあります。  
  
|[値]|説明|  
|-----------|-----------------|  
|`S_OK`|メソッドが成功しました。|  
  
## <a name="remarks"></a>Remarks  
 通知を取得するには、このインターフェイスを実装することも必要があります。  
  
## <a name="see-also"></a>関連項目  
 [IActiveScriptSiteDebugEx インターフェイス](../../winscript/reference/iactivescriptsitedebugex-interface.md)