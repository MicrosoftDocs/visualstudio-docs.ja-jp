---
title: スレッド | Microsoft Docs
description: この記事では、Visual Studio のデバッガー アーキテクチャにおけるスレッドの定義と役割について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- debugging [Debugging SDK], threads
- threading [Debugging SDK]
ms.assetid: 2243d24a-c3d2-41d1-abbb-6db21a2db9ee
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: dc745a4361c0935896048bbf72a4084f007ecf7b
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112905736"
---
# <a name="threads"></a>Threads
デバッガー アーキテクチャでは、 *スレッド* は次のようになります。

- 計算の基本単位です。 スレッドは、単一の呼び出し履歴のコンテキスト内で命令を順番に実行し、1 つのコード コンテキストから次のコンテキストに移動します。

- 自身とそれが実行されているプログラムを識別できます。 スレッドには名前を付け、中断し、再開することができます。 スレッドでは、関連付けられているスタック フレームを列挙することもできます。また、状況によっては、別のスタック フレームに移動できます。 スタック フレームのコンテキストが指定されている場合、スレッドから関連付けられている論理スレッド (存在する場合) を返すことができます。 スレッドには、IDE の **[スレッド]** ウィンドウに表示できる、中断カウントなどのプロパティがあります。

- [IDebugThread2](../../extensibility/debugger/reference/idebugthread2.md) インターフェイスによって表されます。通常は、プログラムを実行した結果として、デバッグ エンジン (DE) または仮想マシンによって作成されます。

## <a name="see-also"></a>関連項目
- [Programs](../../extensibility/debugger/programs.md)
- [スタック フレーム](../../extensibility/debugger/stack-frames.md)
- [デバッグ エンジン](../../extensibility/debugger/debug-engine.md)
- [デバッガーの概念](../../extensibility/debugger/debugger-concepts.md)
- [セッション デバッグ マネージャー](../../extensibility/debugger/session-debug-manager.md)
