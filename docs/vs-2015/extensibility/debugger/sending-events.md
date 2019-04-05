---
title: イベントの送信 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], sending events
ms.assetid: 064231e7-59b5-4437-8240-a23c0a7ec2a9
caps.latest.revision: 8
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 98247b894d2db628d508713875ba0ea7d0642729
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "58975550"
---
# <a name="sending-events"></a>イベントの送信
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

デバッガーとデバッグ エンジン (DE) 間の通信メカニズムは、DCOM に基づいてイベント モデル。 イベントは、COM オブジェクトとして送信され、各イベントには、次を指定するパラメーター。  
  
- この DE イベントと呼ばれます。  
  
- 変更点の説明。  
  
- プロセス、プログラム、およびイベントの発生場所のコンテキストを識別するスレッドの情報。 プロセスは、ドイツから送信されたイベントは送信されません。  
  
- イベントが同期または非同期であるかどうかを示すイベントの種類。  
  
  メソッドを使用してすべてのデバッグ イベントが送信される[IDebugEventCallback2::Event](../../extensibility/debugger/reference/idebugeventcallback2-event.md)します。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [イベント ソース](../../extensibility/debugger/event-sources-visual-studio-sdk.md)  
 イベントの 2 つのソースについて説明します。 デバッグ エンジン (DE) とセッション デバッグ マネージャー (SDM)。  
  
 [サポートされているイベントの種類](../../extensibility/debugger/supported-event-types.md)  
 現在サポートされているイベントの種類について説明します。 非同期と同期します。  
  
 [イベントの説明](../../extensibility/debugger/event-descriptions.md)  
 イベントとその使用する理由を定義します。  
  
## <a name="related-sections"></a>関連項目  
 [カスタム デバッグ エンジンの作成](../../extensibility/debugger/creating-a-custom-debug-engine.md)  
 インタープリターまたはオペレーティング システムは、デバッグ サービスを提供すると、DE のしくみについて説明します。
