---
title: 従来の言語サービスでの構文の色分け表示 | Microsoft Docs
description: 言語の要素を識別してエディターに色付きで表示するために、従来の言語サービスでの構文の色分け表示サービスが Visual Studio にどのように実装されているかについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- syntax coloring
- language services, syntax coloring
ms.assetid: f65ff67e-8c20-497a-bebf-5e2a5b5b012f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8b8886daa5bbdd7adb03f9bf90fba7a875ab483a
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105080529"
---
# <a name="syntax-coloring-in-a-legacy-language-service"></a>従来の言語サービスでの構文の色分け表示

Visual Studio では、色分け表示サービスを使用して言語の要素を識別し、指定された色でエディターに表示します。

## <a name="colorizer-model"></a>カラーライザー モデル
 言語サービスには <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer> インターフェイスが実装されています。このインターフェイスは、エディターによって使用されます。 この実装は、次の図に示すように、言語サービスとは別のオブジェクトです。

 ![SVC Colorizer グラフィック](../../extensibility/internals/media/figlgsvccolorizer.gif)

> [!NOTE]
> 構文の色分け表示サービスは、テキストを色分けするための一般的な Visual Studio メカニズムとは別のものです。 色分けをサポートする一般的な [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] メカニズムの詳細については、「[フォントと色の使用](/previous-versions/visualstudio/visual-studio-2015/extensibility/using-fonts-and-colors?preserve-view=true&view=vs-2015)」を参照してください。

 言語サービスでは、カラーライザーの他に、エディターで使用されるカスタムの配色可能な項目を提供できます。そのためには、カスタムの配色可能な項目を提供することをアドバタイズします。 これを行うには、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo> インターフェイスを実装するのと同じオブジェクトに <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems> インターフェイスを実装します。 これにより、エディターで <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetItemCount%2A> メソッドが呼び出されるとカスタムの配色可能な項目の数が返され、エディターで <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetColorableItem%2A> メソッドが呼び出されるとカスタムの配色可能な項目が 1 つ返されます。

 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetColorableItem%2A> メソッドは、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorableItem> インターフェイスを実装するオブジェクトを返します。 言語サービスで 24 ビットまたはハイカラーの値がサポートされている場合は、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorableItem> インターフェイスと同じオブジェクトに <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiColorItem> インターフェイスを実装する必要があります。

## <a name="how-a-vspackage-uses-a-language-service-colorizer"></a>VSPackage で言語サービスのカラーライザーを使用する方法

1. VSPackage には適切な言語サービスを取得する必要があります。そのためには、言語サービスの VSPackage で次の操作を行う必要があります。

    1. <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer> インターフェイスを実装しているオブジェクトを使用して、テキストを色分けします。

         通常、テキストは、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> インターフェイスを実装するオブジェクトを使用して表示されます。

    2. VSPackage のサービス プロバイダーに言語サービスの GUID を照会して、言語サービスを取得します。 言語サービスは、レジストリでファイル拡張子によって識別されます。

    3. 言語サービスと <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer> を、その <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer.SetLanguageServiceID%2A> メソッドを呼び出すことによって関連付けます。

2. これで、VSPackage でカラーライザー オブジェクトを次のように取得して使用できます。

    > [!NOTE]
    > コア エディターを使用する VSPackage では、言語サービスのカラーライザー オブジェクトを明示的に取得する必要はありません。 コア エディターのインスタンスは、適切な言語サービスを取得するとすぐに、ここに示されているすべての色分けタスクを実行します。

    1. 言語サービスの <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo> オブジェクトの <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetColorizer%2A> メソッドを呼び出すことによって、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer> および <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer2> インターフェイスを実装する言語サービスのカラーライザー オブジェクトを取得します。

    2. <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A> メソッドを呼び出して、テキストの特定の範囲に関するカラーライザー情報を取得します。

         <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A> は、色分けされたテキスト範囲内の各文字に対応する値の配列を返します。 値は、配色可能な項目のリストのインデックスです。このリストは、コア エディターによって管理される既定の配色可能な項目のリストか、言語サービス自体によって管理されるカスタムの配色可能な項目のリストです。

    3. <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A> メソッドから返された色分け情報を使用して、選択されたテキストを表示します。

> [!NOTE]
> 言語サービスのカラーライザーを使用するだけでなく、汎用的な Visual Studio テキスト色分け表示メカニズムを使用することもできます。 このメカニズムの詳細については、「[フォントと色の使用](/previous-versions/visualstudio/visual-studio-2015/extensibility/using-fonts-and-colors?preserve-view=true&view=vs-2015)」を参照してください。

## <a name="in-this-section"></a>このセクションの内容
- [構文の色分け表示の実装](../../extensibility/internals/implementing-syntax-coloring.md)

 エディターで言語サービスの構文の色分け表示にアクセスする方法と、構文の色分け表示をサポートするために言語サービスで実装する必要がある内容について説明します。

- [方法: ビルトインの配色可能な項目の使用](../../extensibility/internals/how-to-use-built-in-colorable-items.md)

 言語サービスのビルトインの配色可能な項目を使用する方法を示します。

- [カスタムの配色可能な項目](../../extensibility/internals/custom-colorable-items.md)

 カスタムの配色可能な項目を実装する方法について説明します。
