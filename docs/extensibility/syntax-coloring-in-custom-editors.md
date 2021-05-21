---
title: カスタム エディターでの構文の色分け表示 | Microsoft Docs
description: 特定のドキュメント ビューに指定された色を表示する Visual Studio Environment SDK カスタム エディターの構文の色分けについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], custom - syntax coloring
ms.assetid: 74900b9a-baef-432a-8231-4568fb5e19ad
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 06cd4ae1db1187cc650a4fd9486f4b1686c6b015
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105063696"
---
# <a name="syntax-coloring-in-custom-editors"></a>カスタム エディターでの構文の色分け表示
特定の構文項目を識別し、特定のドキュメント ビューに対して指定した色で表示するために、コア エディターを含む Visual Studio Environment SDK エディターには言語サービスが使用されています。

## <a name="colorization-requirements"></a>色分けの要件
 言語サービスの色分けツールを実装するすべてのエディターにより、以下のことを行う必要があります。

1. <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer> を実装するオブジェクトを使用して色分けするテキストを管理し、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> を実装するオブジェクトを使用してテキストのドキュメント ビューを提供します。

2. 言語サービスの識別 GUID を使用して VSPackage のサービス プロバイダーのクエリを実行することにより、特定の言語サービスへのインターフェイスを取得します。

3. <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer> を実装するオブジェクトの <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer.SetLanguageServiceID%2A> メソッドを呼び出します。 このメソッドにより、言語サービスは、色分けされるテキストを管理するために VSPackage に使用される <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer> の実装に関連付けられます。

## <a name="core-editor-usage-of-a-language-services-colorizer"></a>コア エディターによる言語サービスの色分けツールの使用法
 色分けツールを備えた言語サービスがコア エディターのインスタンスによって取得されると、言語サービスの色分けツールによるテキストの解析とレンダリングは、ユーザー側の追加の操作を必要とせずに自動的に行われます。

 IDE により、透過的に以下が実行されます。

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer> の実装での追加時または変更時に、テキストを解析および分析するために、必要に応じて色分けツールを呼び出します。

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> の実装によって提供されたドキュメント ビューによる表示を更新し、色分けツールから返された情報を使用して再描画する処理を確実に行います。

## <a name="non-core-editor-usage-of-a-language-services-colorizer"></a>非コア エディターによる言語サービスの色分けツールの使用法
 非コア エディター インスタンスからも言語サービスの構文の色分けサービスを使用できますが、サービスの色分けツールを明示的に取得して適用し、ドキュメント ビュー自体を再描画する必要があります。

 これを行うには、非コア エディターで以下を実行する必要があります。

1. 言語サービスの色分けツール オブジェクト (<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer> と <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer2> を実装します) を取得します。 VSPackage でこれを行うには、言語サービスのインターフェイスに対して <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetColorizer%2A> メソッドを呼び出します。

2. 特定のテキスト範囲を色分けするように要求するには、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A> メソッドを呼び出します。

     <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A> メソッドから、色分けされたテキスト範囲内の各文字に対応する値の配列が返されます。 また、コメント、キーワード、データ型など、特定の種類の色分け可能な項目としてテキスト範囲が識別されます。

3. <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A> から返された色分け情報を使用して、テキストを再描画して表示します。

> [!NOTE]
> VSPackage の場合、言語サービスの色分けツールを使用するだけでなく、汎用の Visual Studio Environment SDK テキストの色分けメカニズムを使用することもできます。 このメカニズムの詳細については、「[フォントと色の使用](/previous-versions/visualstudio/visual-studio-2015/extensibility/using-fonts-and-colors?preserve-view=true&view=vs-2015)」を参照してください。

## <a name="see-also"></a>こちらもご覧ください

- [従来の言語サービスでの構文の色分け表示](../extensibility/internals/syntax-coloring-in-a-legacy-language-service.md)
- [構文の色分け表示の実装](../extensibility/internals/implementing-syntax-coloring.md)
- [方法: ビルトインの配色可能な項目の使用](../extensibility/internals/how-to-use-built-in-colorable-items.md)
- [カスタムの配色可能な項目](../extensibility/internals/custom-colorable-items.md)