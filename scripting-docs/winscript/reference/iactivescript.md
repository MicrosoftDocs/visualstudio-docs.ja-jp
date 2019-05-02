---
title: IActiveScript |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IActiveScript interface
ms.assetid: d8acee11-7f0d-4999-b97a-66774af16f71
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 5b7e3a0172a798eab9a743f446dff3d339a785b2
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63436082"
---
# <a name="iactivescript"></a>IActiveScript
スクリプト エンジンを初期化するために必要なメソッドを提供します。 スクリプト エンジンを実装する必要があります、`IActiveScript`インターフェイス。  
  
## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[IActiveScript::SetScriptSite](../../winscript/reference/iactivescript-setscriptsite.md)|スクリプト エンジンに通知、 [IActiveScriptSite](../../winscript/reference/iactivescriptsite.md)ホストによって提供されるサイトです。|  
|[IActiveScript::GetScriptSite](../../winscript/reference/iactivescript-getscriptsite.md)|Windows スクリプト エンジンに関連付けられているサイト オブジェクトを取得します。|  
|[IActiveScript::SetScriptState](../../winscript/reference/iactivescript-setscriptstate.md)|指定した状態には、スクリプト エンジンを配置します。|  
|[IActiveScript::GetScriptState](../../winscript/reference/iactivescript-getscriptstate.md)|スクリプト エンジンの現在の状態を取得します。|  
|[IActiveScript::Close](../../winscript/reference/iactivescript-close.md)|により、スクリプト エンジンは、現在読み込まれているスクリプトの破棄の状態が失われるおよび closed の状態を入力するため、他のオブジェクトが任意のインターフェイス ポインターを解放します。|  
|[IActiveScript::AddNamedItem](../../winscript/reference/iactivescript-addnameditem.md)|スクリプト エンジンの名前空間には、ルート レベルの項目の名前を追加します。|  
|[IActiveScript::AddTypeLib](../../winscript/reference/iactivescript-addtypelib.md)|スクリプトの名前空間には、タイプ ライブラリを追加します。|  
|[IActiveScript::GetScriptDispatch](../../winscript/reference/iactivescript-getscriptdispatch.md)|取得、`IDispatch`実行中のスクリプトのインターフェイス。|  
|[IActiveScript::GetCurrentScriptThreadID](../../winscript/reference/iactivescript-getcurrentscriptthreadid.md)|現在実行中のスレッドのスクリプト エンジン定義の識別子を取得します。|  
|[IActiveScript::GetScriptThreadID](../../winscript/reference/iactivescript-getscriptthreadid.md)|特定の Microsoft Win32 スレッドに関連付けられているスレッドのスクリプト エンジン定義の識別子を取得します。|  
|[IActiveScript::GetScriptThreadState](../../winscript/reference/iactivescript-getscriptthreadstate.md)|スクリプトのスレッドの現在の状態を取得します。|  
|[IActiveScript::InterruptScriptThread](../../winscript/reference/iactivescript-interruptscriptthread.md)|実行中のスクリプト スレッドの実行を中断します。|  
|[IActiveScript::Clone](../../winscript/reference/iactivescript-clone.md)|現在のスクリプト エンジン (すべて現在の実行状態)、マイナス記号を現在のスレッドでサイトを持たない読み込まれたスクリプト エンジンを返すことを複製します。|  
  
## <a name="see-also"></a>関連項目  
 [Windows スクリプト インターフェイスのリファレンス](../../winscript/reference/windows-script-interfaces-reference.md)