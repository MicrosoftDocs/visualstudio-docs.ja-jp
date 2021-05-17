---
title: '方法: 従来の言語サービスでのアウトラインのサポート | Microsoft Docs'
description: 従来の言語サービスで、さまざまなテキスト領域のアウトライン、展開、または折りたたみのサポートを提供する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], collapse to definitions command
- language services, supporting Collapse to Definitions command
- hidden text, Collapse to Definitions command
ms.assetid: bb6e74c3-93e4-4ef7-afc7-1c9b342f083b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 0c275a6a466cc58187293f6ebd84a39fdf8064e6
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105078686"
---
# <a name="how-to-support-outlining-in-a-legacy-language-service"></a>方法: 従来の言語サービスでのアウトラインのサポート
アウトラインは、さまざまなテキスト領域を展開したり折りたたんだりするために使用されます。 アウトラインの使用方法は、言語別に異なる方法で定義できます。 詳細については、「[アウトライン](../../ide/outlining.md)」を参照してください。

 従来の言語サービスは VSPackage の一部として実装されていますが、言語サービス機能の新しい実装方法では MEF 拡張機能が使用されます。 アウトラインを実装する新しい方法の詳細については、「[チュートリアル: アウトライン](../../extensibility/walkthrough-outlining.md)」を参照してください。

> [!NOTE]
> 新しいエディターの API をできるだけ早く使い始めることをお勧めします。 これにより、言語サービスのパフォーマンスが向上し、新しいエディター機能を利用できるようになります。

 次に、このコマンドを言語サービスでサポートする方法を示します。

## <a name="to-support-outlining"></a>アウトラインをサポートするには

1. 言語サービス オブジェクトに <xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningCapableLanguage> を実装します。

2. 新しいアウトライン領域を追加するには、現在のアウトライン セッション オブジェクトで <xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningSession.AddOutlineRegions%2A> を呼び出します。

## <a name="robust-programming"></a>信頼性の高いプログラミング
 ユーザーが **[アウトライン]** メニューの **[定義に折りたたむ]** を選択すると、IDE では言語サービスで <xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningCapableLanguage.CollapseToDefinitions%2A> が呼び出されます。

 このメソッドが呼び出されると、IDE では <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines> ポインター (テキスト バッファーへのポインター) と <xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningSession> (現在のアウトライン セッションへのポインター) が渡されます。

 `rgOutlnReg` パラメーターでこれらの領域を指定することで、複数のアウトライン領域に対して <xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningSession.AddOutlineRegions%2A> メソッドを呼び出すことができます。 `rgOutlnReg` パラメーターは <xref:Microsoft.VisualStudio.TextManager.Interop.NewOutlineRegion> 構造体です。 このプロセスでは、特定の領域が展開されているか折りたたまれているかなど、非表示領域のさまざまな特性を指定できます。

> [!NOTE]
> 改行文字の非表示に注意してください。 非表示テキストは、セクションの最初の行の先頭から最後の行の最後の文字まで延長する必要があり、最後の改行文字は表示されたままになります。

## <a name="see-also"></a>関連項目
- [方法: 従来の言語サービスでの隠し文字サポートの提供](../../extensibility/internals/how-to-provide-hidden-text-support-in-a-legacy-language-service.md)
- [方法: 従来の言語サービスでのアウトラインの拡張サポートの提供](../../extensibility/internals/how-to-provide-expanded-outlining-support-in-a-legacy-language-service.md)
