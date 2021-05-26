---
title: 従来の言語サービスでのステートメント入力補完 | Microsoft Docs
description: ステートメント入力補完の動作と、VSPackage で従来の言語サービスにそれを実装する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- statement completion
- language services, statement completion
ms.assetid: 617439dc-3f0e-4e5f-b346-3e4e7fcf3c1b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 63a784c850f4c88ecf17a978a2943577eb988a7b
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105080776"
---
# <a name="statement-completion-in-a-legacy-language-service"></a>従来の言語サービスでのステートメント入力補完
ステートメント入力補完は、ユーザーがコア エディターで言語キーワードまたは要素の入力を開始したときにその完成を支援する、言語サービスのプロセスです。 このトピックでは、ステートメント入力補完の動作と、言語サービスでのその実装方法について説明します。

 従来の言語サービスは VSPackage の一部として実装されていますが、言語サービス機能の新しい実装方法では MEF 拡張機能が使用されます。 ステートメント入力補完を実装する新しい方法の詳細については、「[チュートリアル: 入力候補の表示](../../extensibility/walkthrough-displaying-statement-completion.md)」を参照してください。

> [!NOTE]
> 新しいエディターの API をできるだけ早く使い始めることをお勧めします。 これにより、言語サービスのパフォーマンスが向上し、新しいエディター機能を利用できるようになります。

## <a name="implementing-statement-completion"></a>ステートメント入力補完の実装
 コア エディターでは、ステートメント入力補完によって特殊な UI がアクティブ化され、コードをすばやく簡単に記述できるようになります。 ステートメント入力補完では、関連するオブジェクトまたはクラスが必要に応じて表示されるため、特定の要素を記憶したり、ヘルプ リファレンス トピックで検索したりする必要がなくなります。

 ステートメント入力補完を実装するために、言語には解析可能なステートメント入力補完トリガーが必要です。 たとえば、[!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] ではドット (.) 演算子が使用され、[!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] では矢印 (->) 演算子が使用されます。 言語サービスでは、ステートメント入力補完を開始するためのトリガーを複数使用できます。 これらのトリガーは、コマンド フィルターでプログラミングされます。

## <a name="command-filters-and-triggers"></a>コマンド フィルターとトリガー
 コマンド フィルターは、トリガーの出現をインターセプトします。 コマンド フィルターをビューに追加するには、<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> インターフェイスを実装し、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A> メソッドを呼び出してビューにアタッチします。 ステートメント入力補完、エラー マーカー、メソッド ヒントなど、言語サービスのすべての側面に対して同じコマンド フィルター (<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>) を使用できます。 詳細については、「[従来の言語サービスのコマンドの受信](../../extensibility/internals/intercepting-legacy-language-service-commands.md)」を参照してください。

 エディター (具体的にはテキスト バッファー) にトリガーが入力されると、言語サービスで <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateCompletionStatus%2A> メソッドが呼び出されます。 これにより、エディターに UI が表示され、ユーザーはステートメント入力補完の候補から選択できます。 このメソッドでは、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompletionSet> および <xref:Microsoft.VisualStudio.TextManager.Interop.UpdateCompletionFlags> フラグをパラメーターとして実装する必要があります。 補完項目の一覧がスクロール リスト ボックスに表示されます。 ユーザーが入力を続けると、リスト ボックス内の選択内容が更新されて、最後に入力された文字に最も近い一致が反映されます。 コア エディターにはステートメント入力補完の UI が実装されていますが、言語サービスでは <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompletionSet> インターフェイスを実装して、ステートメントの候補となる補完項目のセットを定義する必要があります。

## <a name="see-also"></a>関連項目
- [従来の言語サービスのコマンドの受信](../../extensibility/internals/intercepting-legacy-language-service-commands.md)
