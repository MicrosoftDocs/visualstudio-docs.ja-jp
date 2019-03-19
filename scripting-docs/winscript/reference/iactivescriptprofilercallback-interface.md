---
title: IActiveScriptProfilerCallback インターフェイス |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 76f9164b-b086-4b29-ac79-76f9c76f1d11
caps.latest.revision: 13
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: a0eb8ef209e1fc55fabf37c0c4469fd390f5a478
ms.sourcegitcommit: d3a485d47c6ba01b0fc9878cbbb7fe88755b29af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2019
ms.locfileid: "58146332"
---
# <a name="iactivescriptprofilercallback-interface"></a>IActiveScriptProfilerCallback インターフェイス
イベントが発生したときにプロファイラー オブジェクトを通知するスクリプト エンジンで使用されるメソッドを提供します。 このインターフェイスは、プロファイラー オブジェクトによって実装されます。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[IActiveScriptProfilerCallback::Initialize](../../winscript/reference/iactivescriptprofilercallback-initialize.md)|スクリプト エンジンでプロファイリングが開始されるたびに、プロファイラー オブジェクトを初期化するために呼び出されます。|  
|[IActiveScriptProfilerCallback::Shutdown](../../winscript/reference/iactivescriptprofilercallback-shutdown.md)|解放し、プロファイラー オブジェクトをリリース スクリプト エンジンのプロファイリングを停止するたびに呼び出されます。|  
|[IActiveScriptProfilerCallback::ScriptCompiled](../../winscript/reference/iactivescriptprofilercallback-scriptcompiled.md)|スクリプトのコンパイル、スクリプト エンジン オブジェクトをプロファイラーに通知します。|  
|[IActiveScriptProfilerCallback::FunctionCompiled](../../winscript/reference/iactivescriptprofilercallback-functioncompiled.md)|スクリプトをコンパイルするときに、スクリプト エンジン オブジェクトは、関数が発生しました、プロファイラーに通知します。|  
|[IActiveScriptProfilerCallback::OnFunctionEnter](../../winscript/reference/iactivescriptprofilercallback-onfunctionenter.md)|ドキュメント オブジェクト モデル (DOM) への呼び出しではない関数呼び出しの実行を開始するスクリプト エンジンは、プロファイラーのオブジェクトに通知します。|  
|[IActiveScriptProfilerCallback::OnFunctionExit](../../winscript/reference/iactivescriptprofilercallback-onfunctionexit.md)|オブジェクト、スクリプト エンジン関数の実行が完了するを呼び出すことがない DOM への呼び出しをプロファイラーに通知します。|  
  
## <a name="remarks"></a>Remarks  
 関数呼び出しにドキュメント オブジェクト モデル (DOM) の通知がによって提供される、 [IActiveScriptProfilerCallback2 インターフェイス](../../winscript/reference/iactivescriptprofilercallback2-interface.md)します。  
  
> [!NOTE]
>  プロファイリング、スクリプトが実行されているときに開始および停止する機能を追加するには、次のメソッドを呼び出します。 これらのメソッドを使用する場合、完全な呼び出し履歴を取得できます[!INCLUDE[javascript](../../javascript/includes/javascript-md.md)]開始またはプロファイリングを停止するときに実行します。  
> 
> - 呼び出す[IActiveScriptProfilerControl2::CompleteProfilerStart](../../winscript/reference/iactivescriptprofilercontrol2-completeprofilerstart.md)をプロファイリングが開始したことをプロファイラーに通知します。  
>   -   呼び出す[IActiveScriptProfilerControl2::PrepareProfilerStop](../../winscript/reference/iactivescriptprofilercontrol2-prepareprofilerstop.md)をプロファイリングするをすぐに停止することをプロファイラーに通知します。  
  
## <a name="see-also"></a>関連項目  
 [アクティブ スクリプト プロファイラーのインターフェイス](../../winscript/reference/active-script-profiler-interfaces.md)