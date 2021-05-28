---
title: カスタム配色可能項目 | Microsoft Docs
description: '[フォントおよび色] ダイアログ ボックスの項目 (キーワードやコメントなど) をオーバーライドして、言語サービスの一部としてカスタム配色可能項目を作成する方法について説明します。'
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- colorable items
- language services, custom colorable items
ms.assetid: b4d0ddee-c04b-48dc-ba82-f6068570cef0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: f08c5c9e533e3a21ec4b87e7d148c3022ee0fed1
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105056800"
---
# <a name="custom-colorable-items"></a>カスタム配色可能項目
言語サービスの一部としてカスタム配色可能項目を実装することで、彩色の種類 (キーワードやコメントなど) の一覧をオーバーライドできます。

## <a name="user-settings-of-colorable-items"></a>配色可能項目のユーザー設定
 **[フォントおよび色]** ダイアログ ボックスを表示するには、 **[ツール]** メニューの **[オプション]** を選択して、 **[環境]** の下の **[フォントおよび色]** を選択します。 **[テキスト エディター]** または **[コマンド ウィンドウ]** など表示を選択すると、 **[表示項目]** リスト ボックスにその表示の配色可能項目がすべて示されます。 各配色可能項目のフォント、サイズ、前景色、および背景色を表示および変更できます。 選択内容は、レジストリのキャッシュに格納され、配色可能項目名でアクセスできます。

## <a name="presentation-of-colorable-items"></a>配色可能項目のプレゼンテーション
 **[フォントおよび色]** ダイアログ ボックスでの配色可能項目のユーザーによるオーバーライドは IDE によって処理されるため、ユーザーはカスタム配色可能項目それぞれに名前を付けるだけです。 この名前が、 **[表示項目]** リストに表示されます。 配色可能項目はアルファベット順に表示されます。 言語サービスのカスタム配色可能項目をグループ化するには、それぞれの名前の最初に言語名を付けます (**NewLanguage - Comment** や **NewLanguage - Keyword** など)。

> [!CAUTION]
> 既存の配色可能項目名との競合を避けるために、配色可能項目の名前に言語名を含めてください。 開発中にいずれかの配色可能項目の名前を変更した場合は、その配色可能項目が最初にアクセスされたときに作成されたキャッシュをリセットする必要があります。 試験的キャッシュは **CreateExpInstance** ツールを使用してリセットできます。これは Visual Studio SDK と一緒に、通常は次のディレクトリにインストールされています。
>
> *C:\Program Files (x86)\Microsoft Visual Studio 14.0\VSSDK\VisualStudioIntegration\Tools\Bin*
>
> キャッシュをリセットするには、「**CreateExpInstance /Reset**」と入力します。 **CreateExpInstance** の詳細については、「[CreateExpInstance ユーティリティ](../../extensibility/internals/createexpinstance-utility.md)」を参照してください。

 配色可能項目の一覧の最初の項目は参照されません。 最初の項目は配色可能項目インデックス 0 に対応しており、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] によって、既定のテキスト色および属性が常にその項目に提供されます。 この未参照の項目を扱う最も簡単な方法は、一覧に最初の項目としてプレースホルダー配色可能項目を指定することです。

## <a name="implement-custom-colorable-items"></a>カスタム配色可能項目を実装する

1. キーワード、演算子、識別子など、ご使用の言語で彩色が必要なものを定義します。

2. これらの配色可能項目の列挙を作成します。

3. パーサーまたはスキャナーから返されるトークンの種類を列挙値に関連付けます。

    たとえば、トークンの種類を表す値を、カスタム配色可能項目列挙の同じ値にすることができます。

4. <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer> オブジェクトの <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A> メソッドの実装で、属性一覧に、パーサーまたはスキャナーから返されるトークンの種類に対応するカスタム配色可能項目列挙の値を入力します。

5. <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo> インターフェイスを実装する同じクラスに、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems> インターフェイスとその 2 つのメソッド (<xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetItemCount%2A> および <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetColorableItem%2A>) を実装します。

6. <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorableItem> インターフェイスを実装します。

7. 24 ビット以上の色値をサポートする場合は、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiColorItem> インターフェイスも実装します。

8. 言語サービス オブジェクトで、パーサーまたはスキャナーが識別できる配色可能項目に対して 1 つずつ、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorableItem> オブジェクトを含む一覧を作成します。

    一覧の各項目には、カスタム配色可能項目列挙の対応する値を使用してアクセスできます。 列挙値を一覧のインデックスとして使用します。 一覧内の最初の項目はアクセスされません。常に [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] によって処理される既定のテキスト スタイルに対応するためです。 これに対処するには、一覧の最初にプレースホルダー配色可能項目を挿入できます。

9. <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetItemCount%2A> メソッドの実装で、カスタム配色可能項目一覧の項目数を返します。

10. <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetColorableItem%2A> メソッドの実装で、要求された配色可能項目を一覧から返します。

    <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorableItem> インターフェイスおよび <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiColorItem> インターフェイスを実装する方法の例については、「<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiColorItem>」を参照してください。

## <a name="see-also"></a>こちらもご覧ください
- [従来の言語サービスのモデル](../../extensibility/internals/model-of-a-legacy-language-service.md)
- [カスタム エディターでの構文の色分け表示](../../extensibility/syntax-coloring-in-custom-editors.md)
- [従来の言語サービスでの構文の色分け表示](../../extensibility/internals/syntax-coloring-in-a-legacy-language-service.md)
- [構文の色分けを実装する](../../extensibility/internals/implementing-syntax-coloring.md)
- [方法: 組み込みの配色可能項目の使用](../../extensibility/internals/how-to-use-built-in-colorable-items.md)
