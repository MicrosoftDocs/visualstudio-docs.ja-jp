---
title: プログラム ノード | Microsoft Docs
description: この記事では、Visual Studio のデバッガー アーキテクチャにおけるプログラム ノードの定義と役割について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- program nodes, debugging context
- debugging [Debugging SDK], program nodes
- program nodes, adding
- program nodes, superceding
ms.assetid: 1c5a5c13-c14d-42c3-af11-4c63f1032c8d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 5658026b60006a58ba168ca713028b9876a3c57d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105094628"
---
# <a name="program-nodes"></a>プログラム ノード
デバッガー アーキテクチャでは、"*プログラム ノード*" は次のようなものです。

- プログラムの簡易な説明です。

- それ自体と、それが実行されているプロセスを識別できます。 プログラム ノードは、それを作成したデバッグ エンジン (DE) (存在する場合) にアタッチしたり、デタッチしたり、それについて説明したりできます。

- 通常は DE またはポートによって作成される [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md) インターフェイスによって表されます。 プログラム ノードは、[AddProgramNode](../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md) を呼び出すことによってポートに追加されます。 プログラム ノードがポートに追加されると、このプログラム ノードが表すプログラムが含まれているプロセスに追加されます。

  デバッグ セッションの開始後、デバッグ パッケージの実装によっては、プログラム ノードを使用して対応するプログラムが作成される場合があります。 プログラムのプロセスが照会されると、プログラムはプログラム ノードごとに 1 つずつ列挙されます。

  プログラムがアタッチされる前は、IDE にはプログラムの簡易な説明のみが必要です。 この情報はプログラム ノードから取得できます。 プログラムがアタッチされると、IDE には、プログラムで実行されているすべてのスレッドの一覧など、より詳細な情報が表示されます。 この情報は、プログラム自体から取得されます。

## <a name="see-also"></a>関連項目
- [Programs](../../extensibility/debugger/programs.md)
- [処理](../../extensibility/debugger/processes.md)
- [デバッグ エンジン](../../extensibility/debugger/debug-engine.md)
- [デバッガーの概念](../../extensibility/debugger/debugger-concepts.md)
- [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)
- [AddProgramNode](../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md)
