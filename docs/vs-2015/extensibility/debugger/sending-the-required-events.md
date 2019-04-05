---
title: 必要なイベントの送信 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], required events
ms.assetid: 08319157-43fb-44a9-9a63-50b919fe1377
caps.latest.revision: 8
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 1ec13cffddda09b51a6d674f9263e4eab24444fa
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "58962586"
---
# <a name="sending-the-required-events"></a>必要なイベントの送信
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

必要なイベントを送信するためには、この手順を使用します。  
  
## <a name="process-for-sending-required-events"></a>必要なイベントを送信するためのプロセス  
 次のイベントは、この順序は、エンジン (DE) の作成、デバッグおよびプログラムへのアタッチ、必要があります。  
  
1.  送信、 [IDebugEngineCreateEvent2](../../extensibility/debugger/reference/idebugenginecreateevent2.md)セッション デバッグ マネージャー (SDM) のプロセスで 1 つまたは複数のプログラムをデバッグするため、DE が初期化されるときにイベント オブジェクト。  
  
2.  デバッグするプログラムに関連付けられている場合は、送信、 [IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md) SDM にイベント オブジェクト。 このイベントによっては、エンジン設計の停止イベントがあります。  
  
3.  プロセスを起動するときに、プログラムが接続されている場合は、送信、 [IDebugThreadCreateEvent2](../../extensibility/debugger/reference/idebugthreadcreateevent2.md)に新しいスレッドの IDE に通知する SDM イベント オブジェクト。 このイベントによっては、エンジン設計の停止イベントがあります。  
  
4.  送信、 [IDebugLoadCompleteEvent2](../../extensibility/debugger/reference/idebugloadcompleteevent2.md) SDM デバッグ中のプログラムが完成した読み込みまたはプログラムへのアタッチが完了したときにイベント オブジェクト。 このイベントは stopping イベントである必要があります。  
  
5.  デバッグするアプリケーションを起動する場合は、送信、 [IDebugEntryPointEvent2](../../extensibility/debugger/reference/idebugentrypointevent2.md) SDM ランタイム アーキテクチャ内のコードの最初の命令が実行するときにイベント オブジェクト。 このイベントは、常に、停止イベントです。 デバッグ セッションをステップ実行、IDE は、このイベントで停止します。  
  
> [!NOTE]
>  多くの言語では、グローバル初期化子 (CRT ライブラリまたは _Main) からの外部のプリコンパイル済みの関数を使用して、そのコードの先頭にします。 デバッグ中のプログラムの言語には、これらの種類の最初のエントリ ポイントの前に要素のいずれかが含まれています、し、このコードが実行され、エントリ ポイント イベントが送信される場合、ユーザーのエントリ ポイントなど**メイン**または`WinMain`、達した。  
  
## <a name="see-also"></a>関連項目  
 [デバッグするプログラムの有効化](../../extensibility/debugger/enabling-a-program-to-be-debugged.md)
