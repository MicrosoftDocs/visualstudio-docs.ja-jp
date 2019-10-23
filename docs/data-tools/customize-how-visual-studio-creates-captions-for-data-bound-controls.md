---
title: データバインドコントロールのキャプションをカスタマイズする
ms.date: 11/03/2017
ms.topic: conceptual
helpviewer_keywords:
- Label captions, Data Sources window
- smart captions
- captions, data-bound
- Data Sources Window, label captions
ms.assetid: 6d4d15f8-4d78-42fd-af64-779ae98d62c8
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 932d50d44fbfaa810225ef90c2f5361bc26d9b72
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72648565"
---
# <a name="customize-how-visual-studio-creates-captions-for-data-bound-controls"></a>Visual Studio がデータ バインド コントロールのキャプションを作成する方法をカスタマイズする

[[データソース] ウィンドウ](add-new-data-sources.md#data-sources-window)からデザイナーに項目をドラッグすると、特別な考慮事項が表示されます。2つ以上の単語が連結されていることがわかった場合、キャプションラベル内の列名は、より読みやすい文字列に再フォーマットされます。

::: moniker range="vs-2017"

HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\15.0 で**SmartCaptionExpression**、 **SmartCaptionReplacement**、 **SmartCaptionSuffix**の各値を設定することにより、これらのラベルの作成方法をカスタマイズできます。 **\Data Designer**レジストリキー。

::: moniker-end

::: moniker range=">=vs-2019"

HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\16.0 で**SmartCaptionExpression**、 **SmartCaptionReplacement**、 **SmartCaptionSuffix**の各値を設定することにより、これらのラベルの作成方法をカスタマイズできます。 **\Data Designer**レジストリキー。

::: moniker-end

> [!NOTE]
> このレジストリキーは、作成するまで存在しません。

スマートキャプションは、 **SmartCaptionExpression**値の値に入力された正規表現によって制御されます。 **データデザイナー**のレジストリキーを追加すると、キャプションラベルを制御する既定の正規表現がオーバーライドされます。 正規表現の詳細については、「 [Visual Studio での正規表現の使用](../ide/using-regular-expressions-in-visual-studio.md)」を参照してください。

次の表では、キャプションラベルを制御するレジストリ値について説明します。

|レジストリ項目|説明|
|-------------------|-----------------|
|**SmartCaptionExpression**|パターンに一致するために使用する正規表現。|
|**SmartCaptionReplacement**|**SmartCaptionExpression**に一致したすべてのグループを表示する形式。|
|**SmartCaptionSuffix**|キャプションの末尾に追加する省略可能な文字列。|

次の表は、これらのレジストリ値の内部既定の設定を示しています。

|レジストリ項目|既定値|説明|
|-------------------|-------------------|-----------------|
|**SmartCaptionExpression**|**(\\\p{Ll})(\\\p{Lu})&#124;_+**|小文字の後に大文字またはアンダースコアが続くパターンに一致します。|
|**SmartCaptionReplacement**|**$1 $2**|**$1**は、式の最初のかっこに一致したすべての文字を表し、 **$2**は2番目のかっこで囲まれた任意の文字を表します。 置換は、最初の一致、空白、および2番目の一致です。|
|**SmartCaptionSuffix**|**:**|返される文字列に付加された文字を表します。 たとえば、キャプションが `Company Name` 場合、サフィックスによって `Company Name:`|

> [!CAUTION]
> レジストリエディターで何かを実行する場合は注意が必要です。 編集する前にレジストリをバックアップしてください。 レジストリエディターを誤って使用すると、重大な問題が発生し、オペレーティングシステムの再インストールが必要になることがあります。 Microsoft では、レジストリエディターを誤って使用した場合に発生する問題を解決できないことを保証していません。 レジストリ エディターは、ご自身の責任において使用してください。
>
> レジストリのバックアップ、編集、および復元の詳細については、「 [advanced users の Windows レジストリ情報](https://support.microsoft.com/help/256986/windows-registry-information-for-advanced-users)」を参照してください。

## <a name="modify-the-smart-captioning-behavior-of-the-data-sources-window"></a>[データソース] ウィンドウのスマートキャプションの動作を変更する

1. **[開始]** をクリックしてコマンドウィンドウを開き、を**実行**します。

2. **[実行]** ダイアログボックスで「`regedit`」と入力し、 **[OK]** をクリックします。

3. **Microsoft**  > **VisualStudio**ノード  >  **HKEY_CURRENT_USER**  > **ソフトウェア**を展開します。

::: moniker range="vs-2017"

4. **[15.0]** ノードを右クリックし、`Data Designers` という名前の新しい**キー**を作成します。

::: moniker-end

::: moniker range=">=vs-2019"

4. **[16.0]** ノードを右クリックし、`Data Designers` という名前の新しい**キー**を作成します。

::: moniker-end

5. **[データデザイナー]** ノードを右クリックし、次の3つの新しい文字列値を作成します。

    - `SmartCaptionExpression`
    - `SmartCaptionReplacement`
    - `SmartCaptionSuffix`

6. **SmartCaptionExpression**値を右クリックし、 **[変更]** を選択します。

7. **[データソース]** ウィンドウで使用する正規表現を入力します。

8. **SmartCaptionReplacement**値を右クリックし、 **[変更]** を選択します。

9. 正規表現で一致したパターンを表示する方法で書式設定された置換文字列を入力します。

10. **SmartCaptionSuffix**値を右クリックし、 **[変更]** を選択します。

11. キャプションの末尾に表示する任意の文字を入力します。

    次に **[データソース]** ウィンドウから項目をドラッグすると、指定された新しいレジストリ値を使用してキャプションラベルが作成されます。

## <a name="turn-off-the-smart-captioning-feature"></a>スマートキャプション機能を無効にする

1. **[開始]** をクリックしてコマンドウィンドウを開き、を**実行**します。

2. **[実行]** ダイアログボックスで「`regedit`」と入力し、 **[OK]** をクリックします。

3. **Microsoft**  > **VisualStudio**ノード  >  **HKEY_CURRENT_USER**  > **ソフトウェア**を展開します。

::: moniker range="vs-2017"

4. **[15.0]** ノードを右クリックし、`Data Designers` という名前の新しい**キー**を作成します。

::: moniker-end

::: moniker range=">=vs-2019"

4. **[16.0]** ノードを右クリックし、`Data Designers` という名前の新しい**キー**を作成します。

::: moniker-end

5. **[データデザイナー]** ノードを右クリックし、次の3つの新しい文字列値を作成します。

    - `SmartCaptionExpression`
    - `SmartCaptionReplacement`
    - `SmartCaptionSuffix`

6. **SmartCaptionExpression**アイテムを右クリックし、 **[変更]** を選択します。

7. 値として `(.*)` を入力します。 これは、文字列全体に一致します。

8. **SmartCaptionReplacement**アイテムを右クリックし、 **[変更]** を選択します。

9. 値として `$1` を入力します。 これにより、文字列が一致した値に置き換えられます。文字列全体が変更されずに保持されます。

    次に **[データソース]** ウィンドウから項目をドラッグすると、キャプションラベルが、変更されていないキャプションで作成されます。

## <a name="see-also"></a>関連項目

- [Visual Studio でのデータへのコントロールのバインド](../data-tools/bind-controls-to-data-in-visual-studio.md)