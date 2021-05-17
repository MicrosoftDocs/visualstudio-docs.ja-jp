---
title: セッション デバッグ マネージャー | Microsoft Docs
description: セッション デバッグ マネージャーについて説明します。セッション デバッグ マネージャーは、任意の数のコンピューター上の複数のプロセスで、プログラムをデバッグしている複数のデバッグ エンジンを管理します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- session debug manager, unifying session views
- session debug manager, broadcasting
- debugging [Debugging SDK], session debug manager
- session debug manager
- session debug manager, debug engine multiplexing
- session debug manager, delegating
ms.assetid: fbb1928d-dddc-43d1-98a4-e23b0ecbae09
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 2e5a206b8ece21b14758dfeb02563d4d323dcf60
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105079463"
---
# <a name="session-debug-manager"></a>セッション デバッグ マネージャー
セッション デバッグ マネージャー (SDM) は、任意の数のコンピューター上の複数のプロセスで、任意の数のプログラムをデバッグしている任意の数のデバッグ エンジン (DE) を管理します。 デバッグ エンジンのマルチプレクサーに加えて、SDM ではデバッグ セッションの統合ビューを IDE に提供します。

## <a name="session-debug-manager-operation"></a>セッション デバッグ マネージャーの操作
 セッション デバッグ マネージャー (SDM) では、DE を管理します。 1 台のコンピューターで複数のデバッグ エンジンを同時に実行することもできます。 DE を多重化するために、SDM は DE からの複数のインターフェイスをラップし、1 つのインターフェイスとして IDE に公開します。

 パフォーマンスを向上させるために、一部のインターフェイスは多重化されません。 代わりに、これらは DE から直接使用され、これらのインターフェイスへの呼び出しは SDM を経由しません。 たとえば、メモリ、コード、ドキュメント コンテキストで使用されるインターフェイスは多重化されません。これは、特定の DE によってデバッグされる特定のプログラムにある特定の命令、メモリ、またはドキュメントを参照しているためです。 そのような通信レベルでは他の DE が関与する必要はありません。

 これは、すべてのコンテキストに当てはまるわけではありません。 式の評価のコンテキスト インターフェイスへの呼び出しは、SDM を経由します。 式の評価中に、SDM では IDE に渡す [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) インターフェイスをラップします。これは、その式が評価されるときに複数の DE が関与する可能性があり、それぞれの DE でデバッグするプログラムは同じプロセス内にあり、同じスレッドで実行されている可能性があるためです。

 SDM は通常、委任機構として機能しますが、ブロードキャスト機構として機能する場合があります。 たとえば、式の評価中、SDM はブロードキャスト機構として機能し、指定されたスレッドでコードを実行できることをすべての DE に通知します。 同様に、SDM で停止イベントを受け取ると、実行を停止することをプログラムにブロードキャストします。 ステップが呼び出されると、SDM では、実行を継続できることをプログラムにブロードキャストします。 ブレークポイントも、すべての DE にブロードキャストされます。

 SDM では、現在のプログラム、スレッド、またはスタック フレームを追跡しません。 プロセス、プログラム、およびスレッドの情報は、特定のデバッグ イベントと共に SDM に送信されます。

## <a name="see-also"></a>関連項目
- [デバッグ エンジン](../../extensibility/debugger/debug-engine.md)
- [デバッガー コンポーネント](../../extensibility/debugger/debugger-components.md)
- [デバッガー コンテキスト](../../extensibility/debugger/debugger-contexts.md)
