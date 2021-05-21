---
title: データバインド コントロールのキャプションをカスタマイズする
description: Visual Studio がデータバインド コントロールのキャプションを作成する方法をカスタマイズします。 [データ ソース] ウィンドウのスマート キャプションの動作を変更します。 スマート キャプションをオフにします。
ms.custom: SEO-VS-2020
ms.date: 11/03/2017
ms.topic: how-to
helpviewer_keywords:
- Label captions, Data Sources window
- smart captions
- captions, data-bound
- Data Sources Window, label captions
ms.assetid: 6d4d15f8-4d78-42fd-af64-779ae98d62c8
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: be9a6840c3b41b442e5019e08c4d2f4d2fa5c3dd
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99858996"
---
# <a name="customize-how-visual-studio-creates-captions-for-data-bound-controls"></a>Visual Studio がデータ バインド コントロールのキャプションを作成する方法をカスタマイズする

[[データ ソース] ウィンドウ](add-new-data-sources.md#data-sources-window)からデザイナーに項目をドラッグするときには、特別な配慮が必要です。複数の単語が連結されているキャプション ラベルの列名は、より読みやすい文字列に再設定されます。

::: moniker range="vs-2017"

**HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\15.0\Data Designers** レジストリ キーの **SmartCaptionExpression**、**SmartCaptionReplacement**、**SmartCaptionSuffix** の各値を設定することによって、これらのラベルの作成方法をカスタマイズできます。

::: moniker-end

::: moniker range=">=vs-2019"

**HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\16.0\Data Designers** レジストリ キーの **SmartCaptionExpression**、**SmartCaptionReplacement**、**SmartCaptionSuffix** の各値を設定することによって、これらのラベルの作成方法をカスタマイズできます。

::: moniker-end

> [!NOTE]
> このレジストリ キーは作成するまで存在しません。

スマート キャプションは、**SmartCaptionExpression** 値の値に入力された正規表現によって制御されます。 **Data Designers** レジストリ キーを追加すると、キャプション ラベルを制御する既定の正規表現が上書きされます。 正規表現の詳細については、「[Visual Studio での正規表現の使用](../ide/using-regular-expressions-in-visual-studio.md)」を参照してください。

次の表に、キャプション ラベルを制御するレジストリ値を示します。

|レジストリ項目|説明|
|-------------------|-----------------|
|**SmartCaptionExpression**|パターンに一致させるために使用する正規表現。|
|**SmartCaptionReplacement**|**SmartCaptionExpression** で一致したグループを表示する形式。|
|**SmartCaptionSuffix**|キャプションの末尾に追加する省略可能な文字列。|

次の表に、これらのレジストリ値の既定の内部設定を示します。

|レジストリ項目|既定値|説明|
|-------------------|-------------------|-----------------|
|**SmartCaptionExpression**|**(\\\p{Ll})(\\\p{Lu})&#124;_+**|小文字の後に大文字またはアンダースコアが続くパターンに一致します。|
|**SmartCaptionReplacement**|**$1 $2**|**$1** は、式の最初のかっこ内の一致する文字を表し、 **$2** は 2 番目のかっこ内の一致する文字を表します。 置換後は、最初の一致、スペース、2 番目の一致の順になります。|
|**SmartCaptionSuffix**|**:**|返された文字列に追加される文字を表します。 たとえば、キャプションが `Company Name` の場合、このサフィックスによって `Company Name:` になります。|

> [!CAUTION]
> レジストリ エディターで何かを実行するときは十分に注意してください。 レジストリを編集する前にバックアップしておいてください。 レジストリ エディターの使い方を誤ると、重大な問題が発生する可能性があり、オペレーティング システムの再インストールが必要になる場合があります。 Microsoft では、レジストリ エディターの誤った使い方が原因で発生した問題については、解決できることを保証していません。 レジストリ エディターは、各自の責任で使用してください。
>
> レジストリのバックアップ、編集、復元については、「[上級ユーザー向け Windows レジストリ情報](https://support.microsoft.com/help/256986/windows-registry-information-for-advanced-users)」を参照してください。

## <a name="modify-the-smart-captioning-behavior-of-the-data-sources-window"></a>[データ ソース] ウィンドウのスマート キャプションの動作を変更する

1. **[スタート]** 、 **[実行]** の順にクリックして、コマンド ウィンドウを開きます。

2. **[実行]** ダイアログ ボックスに「`regedit`」と入力し、 **[OK]** をクリックします。

3. **[HKEY_CURRENT_USER]**  >  **[Software]**  >  **[Microsoft]**  >  **[VisualStudio]** ノードを展開します。

::: moniker range="vs-2017"

4. **[15.0]** ノードを右クリックし、`Data Designers` という名前の新しい **キー** を作成します。

::: moniker-end

::: moniker range=">=vs-2019"

4. **[16.0]** ノードを右クリックし、`Data Designers` という名前の新しい **キー** を作成します。

::: moniker-end

5. **[Data Designers]** ノードを右クリックし、次の 3 つの新しい文字列値を作成します。

    - `SmartCaptionExpression`
    - `SmartCaptionReplacement`
    - `SmartCaptionSuffix`

6. **SmartCaptionExpression** 値を右クリックし、 **[変更]** を選択します。

7. **[データ ソース]** ウィンドウで使用する正規表現を入力します。

8. **SmartCaptionReplacement** 値を右クリックし、 **[変更]** を選択します。

9. 正規表現で一致するパターンを表示する方法で書式設定された置換文字列を入力します。

10. **SmartCaptionSuffix** 値を右クリックし、 **[変更]** を選択します。

11. キャプションの末尾に表示する文字を入力します。

    次回、 **[データ ソース]** ウィンドウから項目をドラッグしたときには、指定された新しいレジストリ値を使用してキャプション ラベルが作成されます。

## <a name="turn-off-the-smart-captioning-feature"></a>スマート キャプション機能をオフにする

1. **[スタート]** 、 **[実行]** の順にクリックして、コマンド ウィンドウを開きます。

2. **[実行]** ダイアログ ボックスに「`regedit`」と入力し、 **[OK]** をクリックします。

3. **[HKEY_CURRENT_USER]**  >  **[Software]**  >  **[Microsoft]**  >  **[VisualStudio]** ノードを展開します。

::: moniker range="vs-2017"

4. **[15.0]** ノードを右クリックし、`Data Designers` という名前の新しい **キー** を作成します。

::: moniker-end

::: moniker range=">=vs-2019"

4. **[16.0]** ノードを右クリックし、`Data Designers` という名前の新しい **キー** を作成します。

::: moniker-end

5. **[Data Designers]** ノードを右クリックし、次の 3 つの新しい文字列値を作成します。

    - `SmartCaptionExpression`
    - `SmartCaptionReplacement`
    - `SmartCaptionSuffix`

6. **SmartCaptionExpression** 項目を右クリックし、 **[変更]** を選択します。

7. 値に「`(.*)`」と入力します。 これは文字列全体に一致します。

8. **SmartCaptionReplacement** 項目を右クリックし、 **[変更]** を選択します。

9. 値に「`$1`」と入力します。 これは、文字列を一致する値に置き換えます。一致する値は文字列全体であるため、文字列は変更されないことになります。

    次回、 **[データ ソース]** ウィンドウから項目をドラッグしたときには、変更されていないキャプションでキャプション ラベルが作成されます。

## <a name="see-also"></a>関連項目

- [Visual Studio でのデータへのコントロールのバインド](../data-tools/bind-controls-to-data-in-visual-studio.md)
