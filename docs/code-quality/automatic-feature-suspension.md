---
title: 自動機能の中断
ms.date: 11/04/2016
description: システム メモリが制限されている場合に、Visual Studio で実行される分析スコープの縮小、ガベージ コレクションの低遅延モードの無効化、キャッシュのフラッシュについて説明します。
ms.custom: SEO-VS-2020
ms.topic: conceptual
helpviewer_keywords:
- live code analysis
- background analysis
- analysis scope
- full solution analysis
- performance
- low-memory
ms.assetid: 572c15aa-1fd0-468c-b6be-9fa50e170914
author: Mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: efd053a846a7bf70f475db44788b14152498dc0b
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99843723"
---
# <a name="automatic-feature-suspension"></a>自動機能の中断

使用可能なシステム メモリが 200 MB 以下になると、Visual Studio のコード エディターに次のメッセージが表示されます。

![ソリューションの完全な分析の中断を通知するアラートのテキスト](../code-quality/media/fsa_alert.png)

Visual Studio では、メモリ不足の状態が検出されると、安定性を維持できるように、特定の高度な機能が自動的に中断されます。 Visual Studio は以前と同様に機能しますが、パフォーマンスが低下します。

メモリ不足の状態では、次のアクションが実行されます。

- Visual C# および Visual Basic のライブ コード分析を最小限のスコープに縮小する。

- Visual C# および Visual Basic の[ガベージ コレクション](/dotnet/standard/garbage-collection/index) (GC) の低遅延モードを無効にする。

- Visual Studio のキャッシュをフラッシュする。

## <a name="improve-visual-studio-performance"></a>Visual Studio のパフォーマンスを向上させる

大規模なソリューションやメモリ不足の状態に対処するときに Visual Studio のパフォーマンスを向上させる方法に関するヒントとテクニックについては、[大規模なソリューションのパフォーマンスに関する考慮事項](https://github.com/dotnet/roslyn/blob/master/docs/wiki/Performance-considerations-for-large-solutions.md)に関するページを参照してください。

## <a name="live-code-analysis-is-reduced-to-minimal-scope"></a>ライブ コード分析を最小限のスコープに縮小する

既定では、ライブ コード分析は、開いているドキュメントとプロジェクトに対して実行されます。 この分析スコープをカスタマイズして、現在のドキュメントに縮小したり、ソリューション全体に拡大したりできます。 詳細については、「[方法:方法: マネージド コードのライブ コード分析スコープを構成する](./configure-live-code-analysis-scope-managed-code.md)」を参照してください。 メモリ不足の状態では、Visual Studio によって、ライブ分析スコープが現在のドキュメントに強制的に縮小されます。 ただし、情報バーが表示されているときに **[再有効化]** ボタンを選択するか、Visual Studio を再起動することで、優先する分析スコープを再度有効にできます。 [オプション] ダイアログ ボックスには、常に現在のライブ コード分析スコープ設定が表示されます。

## <a name="gc-low-latency-disabled"></a>GC の低遅延を無効にする

GC の低遅延モードを再度有効にするには、Visual Studio を再起動します。 既定では、Visual Studio は入力時に GC の低遅延モードを有効にして、入力によって GC 操作がブロックされないようにします。 ただし、メモリ不足の状態が原因で Visual Studio に自動中断の警告が表示された場合、そのセッションでは GC の低遅延モードが無効になります。 Visual Studio を再起動すると、GC の既定の動作が再度有効になります。 詳細については、「<xref:System.Runtime.GCLatencyMode>」を参照してください。

## <a name="visual-studio-caches-flushed"></a>Visual Studio のキャッシュをフラッシュする

現在の開発セッションを続行するか、Visual Studio を再起動すると、Visual Studio のすべてのキャッシュが即座に空になりますが、再作成が開始されます。 フラッシュされるキャッシュには、次の機能のキャッシュが含まれます。

- [すべての参照の検索]

- [移動]

- [using の追加]

さらに、Visual Studio の内部操作に使用されるキャッシュもクリアされます。

> [!NOTE]
> 機能の自動中断の警告は、セッションごとではなく、ソリューションごとに 1 回だけ発生します。 つまり、Visual Basic から Visual C# (またはその逆) に切り替え、別のメモリ不足の状態になった場合、機能の自動中断の別の警告が表示される可能性があります。

## <a name="see-also"></a>関連項目

- [方法: マネージド コードのライブ コード分析スコープを構成する](./configure-live-code-analysis-scope-managed-code.md)
- [ガベージ コレクションの基礎](/dotnet/standard/garbage-collection/fundamentals)
- [大規模なソリューションのパフォーマンスに関する考慮事項](https://github.com/dotnet/roslyn/blob/master/docs/wiki/Performance-considerations-for-large-solutions.md)
