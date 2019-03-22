---
title: IDebugApplicationThreadEvents110 インターフェイス |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IDebugApplicationThreadEvents110 Interface
ms.assetid: 91a98b0e-7c81-4118-af75-82f75fd4f25a
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 0051f18c67fffc9801ad326745a0dc9dd63f4391
ms.sourcegitcommit: d3a485d47c6ba01b0fc9878cbbb7fe88755b29af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2019
ms.locfileid: "58148855"
---
# <a name="idebugapplicationthreadevents110-interface"></a>IDebugApplicationThreadEvents110 インターフェイス
複数のスレッドのイベントを追加します。 これらのイベントはローカルのみです。 ことがサブスクライブしている対象のプロセスでのみを使用して、デバッグ、 [IConnectionPoint](http://go.microsoft.com/fwlink/?LinkId=232738)ことをお勧めして、PDM アプリケーション スレッド オブジェクトでメソッドをアドバイズ (実装するオブジェクト[IDebugApplicationThreadインターフェイス](../../winscript/reference/idebugapplicationthread-interface.md))。 発信元のスレッドで発生します。  
  
> [!IMPORTANT]
>  このインターフェイスは、PDM v11.0 以降によって実装されます。 activdbg100.h にあります。  
  
## <a name="methods"></a>メソッド  
 `IDebugActivationThreadEvents110` インターフェイスは、以下のメソッドを公開します。  
  
|メソッド|説明|  
|------------|-----------------|  
|[IDebugApplicationThreadEvents110 ::OnBeginThreadRequest](../../winscript/reference/idebugapplicationthreadevents110-onbeginthreadrequest.md)|呼び出しに PDM のスレッドを使用して、スレッドの切り替えが開始されました。|  
|[IDebugApplicationThreadEvents110::OnResumeFromBreakPoint](../../winscript/reference/idebugapplicationthreadevents110-onresumefrombreakpoint.md)|スレッドがブレークポイントから再開され、もう一度アクティブになります。|  
|[IDebugApplicationThreadEvents110::OnSuspendForBreakPoint](../../winscript/reference/idebugapplicationthreadevents110-onsuspendforbreakpoint.md)|スレッドは中断しています。 ブレークポイントを設定してを完全に中断するスレッドを必要とする呼び出しを処理できます。|  
|[IDebugApplicationThreadEvents110::OnThreadRequestComplete](../../winscript/reference/idebugapplicationthreadevents110-onthreadrequestcomplete.md)|呼び出しに PDM のスレッドを使用して、スレッドの切り替えが完了します。|