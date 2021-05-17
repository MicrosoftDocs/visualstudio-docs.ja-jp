---
title: デバッガーを拡張するためのロードマップ |Microsoft Docs
description: デバッグに関する Visual Studio ドキュメントには、サンプル、リファレンス、およびデバッガーをカスタマイズする一般的な方法を示すいくつかのシナリオが含まれています。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], roadmap
- Debugging SDK, roadmap
ms.assetid: 1f4096a8-f7aa-4dfa-84e1-6d59263e70bb
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 69beed934764defe7e3926ba46e5e70f87a031ea
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105070623"
---
# <a name="roadmap-for-extending-the-debugger"></a>デバッガーを拡張するためのロードマップ
このドキュメントでは、[!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] で [!INCLUDE[vs_current_short](../../code-quality/includes/vs_current_short_md.md)] デバッガーを拡張するためのガイドとリファレンス情報を提供します。

 デバッグに関する [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ドキュメントには、サンプル、包括的なリファレンス、およびデバッガーをカスタマイズする一般的な方法を示すいくつかの代表的なシナリオが含まれています。

 コンパイラとその出力によって、製品のデバッグを設定するために必要なものが決まります。 コンパイラの機能に応じて、次のようになります。

- コンパイラが、Windows ネイティブ オペレーティング システムを対象とし、 *.PDB* ファイルを記述する場合は、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] に統合されているネイティブ コード デバッグ エンジン (DE) でプログラムをデバッグできます。 DE と式エバリュエーターのいずれも実装する必要はありません。 式エバリュエーターは、C++ プログラミング言語の構文用に作成されています。

- コンパイラが Microsoft 中間言語 (MSIL) 出力を生成する場合は、マネージド コード デバッグ エンジン DE でプログラムをデバッグできます。この DE も [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] に統合されています。 したがって、実装する必要があるのは、式エバリュエーターのみです。 サンプル式エバリュエーターが用意されています。 詳細については、次のトピックを参照してください。

   [式の評価](../../extensibility/debugger/expression-evaluation-visual-studio-debugging-sdk.md)

   [評価式](../../extensibility/debugger/evaluating-expressions.md)

   [式の評価のコンテキスト](../../extensibility/debugger/expression-evaluation-context.md)

   [中断モードでの式の評価](../../extensibility/debugger/expression-evaluation-in-break-mode.md)

   [共通言語ランタイム式エバリュエーターの作成](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)

- コンパイラが、独自のオペレーティング システムまたはその他の実行時環境を対象とする場合は、自分で DE を作成する必要があります。 ATL COM を使用して単純な DE を作成するチュートリアルが用意されています。 詳細については、次のトピックを参照してください。

   [カスタム デバッグ エンジンを作成する](../../extensibility/debugger/creating-a-custom-debug-engine.md)

   [チュートリアル: ATL COM を使用してデバッグ エンジンを構築する](/previous-versions/bb147024(v=vs.90))

   [ポート サプライヤーを実装する](../../extensibility/debugger/implementing-a-port-supplier.md)

   [サンプル](../../extensibility/debugger/visual-studio-debugging-samples.md)

## <a name="see-also"></a>関連項目
- [開始するには](../../extensibility/debugger/getting-started-with-debugger-extensibility.md)