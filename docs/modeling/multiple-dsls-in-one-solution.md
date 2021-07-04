---
title: 1 つのソリューション内の複数の DSL
description: 複数のドメイン固有言語 (DSL) を 1 つのソリューションの一部としてパッケージ化して、それらが一緒にインストールされるようにする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 11baf6439062e28c7361e2fabb4dea4a3430f237
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112390920"
---
# <a name="multiple-dsls-in-one-solution"></a>1 つのソリューション内の複数の DSL

いくつかの DSL を単一ソリューションの一部としてパッケージ化し、同時にインストールすることができます。

複数の DSL を統合するためにいくつかの手法を使用できます。 詳細については、[Visual Studio Modelbus を使用したモデルの統合](../modeling/integrating-models-by-using-visual-studio-modelbus.md)に関するページ、[ドラッグ アンド ドロップ ハンドラーを追加する方法](../modeling/how-to-add-a-drag-and-drop-handler.md)に関するページ、および[コピー動作のカスタマイズ](../modeling/customizing-copy-behavior.md)に関するページを参照してください。

## <a name="build-more-than-one-dsl-in-the-same-solution"></a>複数の DSL を同じソリューションの中にビルドする

1. 新しい **VSIX プロジェクト** プロジェクトを作成します。

2. VSIX ソリューション ディレクトリ内に 2 つ以上の DSL プロジェクトを作成します。

   - 各 DSL について、Visual Studio の新しいインスタンスを開きます。 新しい DSL を作成し、同じソリューション フォルダとして VSIX ソリューションを指定します。

   - 各 DSL は異なるファイル拡張子名を付けて作成します。

   - **Dsl** および **DslPackage** プロジェクトの名前はすべて異なるように変更します。 たとえば、`Dsl1`、`DslPackage1`、`Dsl2`、`DslPackage2` のようになります。

   - 各 **DslPackage\*\source.extension.tt** で、次の行を正しい Dsl プロジェクト名に更新します。

      `string dslProjectName = "Dsl2";`

   - VSIX ソリューションで、Dsl* および DslPackage\* プロジェクトを追加します。 各ペアを独自のソリューション フォルダーに配置することを推奨します。

2. 以下のように DSL の VSIX マニフェストを結合します。

   1. _YourVsixProject_ **\source.extension.manifest** を開きます。

   2. 各 DSL に対して、 **[コンテンツの追加]** を選択し、以下のように追加します。

       - **[MEF コンポーネント]** として `Dsl*` プロジェクト

       - **[MEF コンポーネント]** として `DslPackage*` プロジェクト

       - **VS パッケージ** として `DslPackage*` プロジェクト

3. ソリューションをビルドします。

   この結果の VSIX では両方の DSL がインストールされます。 F5 キーを使用してテストするか、_YourVsixProject_ **\bin\Debug\\\*.vsix** を配置できます。

## <a name="see-also"></a>関連項目

- [Visual Studio Modelbus によるモデルの統合](../modeling/integrating-models-by-using-visual-studio-modelbus.md)
- [方法: ドラッグ アンド ドロップ ハンドラーを追加する](../modeling/how-to-add-a-drag-and-drop-handler.md)
- [コピー動作のカスタマイズ](../modeling/customizing-copy-behavior.md)