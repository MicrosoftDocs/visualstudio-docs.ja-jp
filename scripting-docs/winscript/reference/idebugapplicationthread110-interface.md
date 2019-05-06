---
title: IDebugApplicationThread110 インターフェイス |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IDebugApplicationThread110 Interface
ms.assetid: 25bc351f-3451-4387-9302-078f6292ddff
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 44df7168c241c9a750354e1a603d6c5ba96dabd2
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63440545"
---
# <a name="idebugapplicationthread110-interface"></a>IDebugApplicationThread110 インターフェイス
多くの機能、 [IDebugApplicationThread インターフェイス](../../winscript/reference/idebugapplicationthread-interface.md)インターフェイス。  
  
> [!IMPORTANT]
> このインターフェイスは、PDM v11.0 以降によって実装されます。 activdbg100.h にあります。  
  
## <a name="methods"></a>メソッド  
 `IDebugApplicationThread110` インターフェイスは、以下のメソッドを公開します。  
  
|メソッド|説明|  
|------------|-----------------|  
|[IDebugApplicationThread110::AsynchronousCallIntoThread](../../winscript/reference/idebugapplicationthread110-asynchronouscallintothread.md)|メイン スレッドで非同期呼び出しを使用します。|  
|[IDebugApplicationThread110::GetActiveThreadRequestCount](../../winscript/reference/idebugapplicationthread110-getactivethreadrequestcount.md)|PDM のスレッドの切り替えのメカニズムからスレッド要求の数が現在処理中の数。 0 または 1 のより高い場合は 1 つのスレッドの呼び出しの処理を開始が、スレッドからの同期呼び出しをトリガー、またはそれ以外の場合 (たとえば、デバッガーで発行される IDebugApplicationEvents イベントをトリガーすることによって、スレッドを中断することは、通常のスレッド)|  
|[IDebugApplicationThread110::IsSuspendedForBreakPoint](../../winscript/reference/idebugapplicationthread110-issuspendedforbreakpoint.md)|[IDebugApplicationThreadEvents110::OnSuspendForBreakPoint](../../winscript/reference/idebugapplicationthreadevents110-onsuspendforbreakpoint.md)がこのスレッドで呼び出され、まだ完了していません。|  
|[IDebugApplicationThread110::IsThreadCallable](../../winscript/reference/idebugapplicationthread110-isthreadcallable.md)|このスレッドは PDM のスレッドの切り替え (SynchronousCallInThread) などのメカニズムを使用して行われた呼び出しを処理できる状態です。|