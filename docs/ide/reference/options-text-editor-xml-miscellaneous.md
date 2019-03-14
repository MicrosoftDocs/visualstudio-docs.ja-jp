---
title: '[オプション]、[テキスト エディター]、[XML]、[その他]'
ms.date: 10/29/2018
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.XML.Miscellaneous
ms.assetid: b6538cbe-badd-4313-a1fb-39e906736bbe
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: d3421580251a6a871adba311fd609e881e088ebd
ms.sourcegitcommit: 3ca33862c1cfc3ccb83de3e95f1e69e860ab143a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57525083"
---
# <a name="options-text-editor-xml-miscellaneous"></a>[オプション]、[テキスト エディター]、[XML]、[その他]

XML エディターのオート コンプリートとスキーマの設定を変更するには、**[その他]** オプション ページを使用します。 その他の XML オプションにアクセスするには、**[ツール]** > **[オプション]** > **[テキスト エディター]** > **[XML]** の順に選択して、**[その他]** を選択します。

## <a name="auto-insert"></a>自動挿入

**終了タグ**

テキスト エディターでは、XML 要素を作成すると、終了タグが追加されます。 要素の開始タグが選択されている場合、エディターは、一致する名前空間プレフィックスも含めて、一致する終了タグを挿入します。 既定では、このチェック ボックスはオンです。

**属性値の引用符**

XML 属性の作成時にエディターは文字 `="` および `"` を挿入し、引用符の内側にキャレット (**^**) を配置します。 既定では、このチェック ボックスはオンです。

**名前空間の宣言**

エディターは、必要に応じて名前空間の宣言を自動的に挿入します。 既定では、このチェック ボックスはオンです。

**その他のマークアップ (コメント、CDATA)**

コメント、CDATA、DOCTYPE、処理命令、およびその他のマークアップがオートコンプリートされます。 既定では、このチェック ボックスはオンです。

## <a name="network"></a>ネットワーク

**DTD とスキーマを自動的にダウンロードする**

HTTP の場所から、スキーマやドキュメント型定義 (DTD) を自動的にダウンロードします。 この機能は、プロキシ サーバーの自動検出を有効にした System.Net を使用します。 既定では、このチェック ボックスはオンです。

## <a name="outlining"></a>アウトライン

**[ファイルが開かれたときにアウトライン モードを実行する]**

ファイルが開かれたときにアウトライン機能をオンにします。 既定では、このチェック ボックスはオンです。

## <a name="caching"></a>キャッシュ

**スキーマ**

スキーマ キャッシュの場所を指定します。 **[参照ボタン]** ボタンをクリックすると、新しいウィンドウで現在のスキーマ キャッシュの場所が開きます。 既定の場所は *%VsInstallDir%\xml\Schemas* です。

## <a name="see-also"></a>関連項目

- [XML オプション - 書式設定](options-text-editor-xml-formatting.md)
- [Visual Studio の XML ツール](../../xml-tools/xml-tools-in-visual-studio.md)