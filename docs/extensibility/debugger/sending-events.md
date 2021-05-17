---
title: イベントの送信 | Microsoft Docs
description: デバッガーとデバッグエンジンで、DCOM に基づくイベントモデルがどのように使用されるかを説明します。 イベントは COM オブジェクトとして送信されます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], sending events
ms.assetid: 064231e7-59b5-4437-8240-a23c0a7ec2a9
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 135dd0278ee765ef88ae6cef39675a2fa92236d7
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105070391"
---
# <a name="send-events"></a>送信イベント
デバッガーとデバッグ エンジン (DE) との間の通信の仕組みは、DCOM に基づくイベント モデルです。 イベントは COM オブジェクトとして送信され、各イベントには、以下を指定するパラメーターがあります。

- イベントを呼び出した DE。

- 発生した現象の説明。

- イベントが発生した場所のコンテキストを識別する、プロセス、プログラム、スレッドの情報。 プロセスは、DE から送信されたイベントについては送信されません。

- イベントが同期と非同期のどちらであるかを示すイベントの種類。

  すべてのデバッグ イベントは、メソッド [IDebugEventCallback2::Event](../../extensibility/debugger/reference/idebugeventcallback2-event.md)を使用して送信されます。

## <a name="in-this-section"></a>このセクションの内容
 「[イベント ソース](../../extensibility/debugger/event-sources-visual-studio-sdk.md)」では、デバッグ エンジン (DE) とセッション デバッグ マネージャー (SDM) の 2 つのイベント ソースについて説明します。

 「[サポートされるイベントの種類](../../extensibility/debugger/supported-event-types.md)」では、現在、サポートされているイベントの種類 (非同期および同期) について説明します。

 「[イベントの説明](../../extensibility/debugger/event-descriptions.md)」では、イベントとその使用理由を定義します。

## <a name="related-sections"></a>関連項目
 「[カスタム デバッグ エンジンの作成](../../extensibility/debugger/creating-a-custom-debug-engine.md)」では、DE がインタープリターやオペレーティング システムを使用して、どのようにデバッグ サービスを提供するかを説明します。
