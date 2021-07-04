---
title: プログラム | Microsoft Docs
description: この記事では、Visual Studio のデバッガー アーキテクチャにおけるプログラムの定義と役割について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- debugging [Debugging SDK], programs
- programs, debugging
ms.assetid: e1f955d8-95da-493b-837e-e97741a26d7e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 07b23fbafd9342b555e2578c4bc0401371e30785
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112901280"
---
# <a name="programs"></a>プログラム
デバッガー アーキテクチャでは、"*プログラム*" は次のようなものです。

- 一連のスレッドと一連のモジュールの両方のためのコンテナーです。 Windows オペレーティング システムではプログラムに 1 つの類似性はありません。

     プログラムは一種のサブプロセスです。 たとえば、Web サイトをデバッグする場合は、スクリプトをプログラムと見なすことができます。 スクリプトは他のスクリプトに依存せずにスクリプト エンジン プロセスで実行されますが、独自のスレッド セットもあります。 デバッグ エンジン (DE) は、プロセスやスレッドではなく、プログラムにアタッチします。

- それ自体と、それが実行されているプロセスを識別できます。 プログラムは、それを作成した DE (存在する場合) にアタッチしたり、デタッチしたり、それについて説明したりできます。 プログラムは、実行、停止、続行、および終了することもできます。

- そのすべてのスレッドを列挙できます。 プログラムは、独自の逆アセンブリ ストリームを提供し、特定のドキュメントの位置のすべてのコード コンテキストを列挙することもできます。

- 実装に応じて、プログラムがアタッチされる前に、またはアタッチ プロセスの一環として作成される [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md) インターフェイスによって表されます。 ポートがプロセスのプログラムを列挙すると、各プログラムは、[AddProgramNode](../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md) に引数として渡される、対応する [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md) インターフェイスに従って作成されます。 デバッグ エンジンもプログラムを表す `IDebugProgram2` インターフェイスを作成しますが、これらのプログラムはプログラム ノードに従って作成されません。 DE によって作成される `IDebugProgramNode2` インターフェイスは実際のデバッグに使用されますが、ポートによって作成されたものは、プロセスで実行されているプログラムを検出するためにのみ使用されます。

## <a name="see-also"></a>関連項目
- [処理](../../extensibility/debugger/processes.md)
- [プログラム ノード](../../extensibility/debugger/program-nodes.md)
- [モジュール](../../extensibility/debugger/modules.md)
- [デバッガーの概念](../../extensibility/debugger/debugger-concepts.md)
- [デバッグ エンジン](../../extensibility/debugger/debug-engine.md)
- [ドキュメントの位置](../../extensibility/debugger/document-position.md)
- [コード コンテキスト](../../extensibility/debugger/code-context.md)
- [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)
- [AddProgramNode](../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md)
