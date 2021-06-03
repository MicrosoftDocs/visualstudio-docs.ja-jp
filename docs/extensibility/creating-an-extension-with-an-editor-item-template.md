---
title: エディター項目テンプレートを使用した拡張機能の作成 | Microsoft Docs
description: Visual Studio SDK の項目テンプレートを使用して、分類子、表示要素、余白をエディターに追加する基本的なエディター拡張機能を作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], new - extensions
ms.assetid: fa3b993b-ab95-47fa-a38b-b788f3a5b2d8
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 06c3fbfabb4eccc08e528aef913e1c1ba502cbf1
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105089135"
---
# <a name="create-an-extension-with-an-editor-item-template"></a>エディター項目テンプレートを使用して拡張機能を作成する
Visual Studio SDK に含まれている項目テンプレートを使用すると、分類子、表示要素、余白をエディターに追加する基本的なエディター拡張機能を作成できます。 エディター項目テンプレートは、Visual C# または Visual Basic の VSIX プロジェクトで使用できます。

## <a name="prerequisites"></a>必須コンポーネント
 Visual Studio 2015 以降では、ダウンロード センターから Visual Studio SDK をインストールしません。 これは、Visual Studio のセットアップにオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「[Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-a-classifier-extension"></a>分類子の拡張機能を作成する
 エディター分類子項目テンプレートでは、任意のテキスト ファイル内の適切なテキスト (この場合はすべて) に色付けするエディター分類子が作成されます。

1. **[新しいプロジェクト]** ダイアログ ボックスで、 **[Visual C#]** または **[Visual Basic]** を展開し、 **[拡張性]** をクリックします。 **[テンプレート]** ペインで、 **[VSIX プロジェクト]** を選択します。 **[名前]** ボックスに「`TestClassifier`」と入力します。 **[OK]** をクリックします。

2. **ソリューション エクスプローラー** で、プロジェクト ノードを右クリックして、 **[追加]**  >  **[新しい項目]** の順に選択します。 Visual C# の **[拡張性]** ノードに移動して、 **[エディター分類子]** を選択します。 既定のファイル名 (*EditorClassifier1.cs*) をそのまま使用します。

3. 次の 4 つのコード ファイルがあります。

    - *EditorClassifier1.cs* には `EditorClassifier1` クラスが含まれています。

    - *EditorClassifier1ClassificationDefinition.cs* には `EditorClassifier1ClassificationDefinition` クラスが含まれています。

    - *EditorClassifier1Format.cs* には `EditorClassifier1Format` クラスが含まれています。

    - *EditorClassifier1Provider.cs* には `EditorClassifier1Provider` クラスが含まれています。

4. プロジェクトをビルドし、デバッグを開始します。 Visual Studio の実験用インスタンスが表示されます。

     テキスト ファイルを開くと、すべてのテキストが下線付きになり、背景が紫色で表示されます。

## <a name="create-a-text-relative-adornment-extension"></a>テキスト相対表示要素の拡張機能を作成する
 エディター テキスト表示要素テンプレートでは、赤色の枠線と青色の背景を持つボックスを使用して、テキスト文字 "a" のすべてのインスタンスを装飾するテキスト相対表示要素が作成されます。 テキスト相対と呼ぶのは、ボックスが移動または再度書式設定されても常に ' a ' という文字がオーバーレイされるためです。

1. **[新しいプロジェクト]** ダイアログ ボックスで、 **[Visual C#]** または **[Visual Basic]** を展開し、 **[拡張性]** をクリックします。 **[テンプレート]** ペインで、 **[VSIX プロジェクト]** を選択します。 **[名前]** ボックスに「`TestAdornment`」と入力します。 **[OK]** をクリックします。

2. **ソリューション エクスプローラー** で、プロジェクト ノードを右クリックして、 **[追加]**  >  **[新しい項目]** の順に選択します。 Visual C# の **[拡張性]** ノードに移動して、 **[エディター テキスト表示要素]** を選択します。 既定のファイル名 (*TextAdornment1.cs/vb*) をそのまま使用します。

3. 次の 2 つのコード ファイルがあります。

    - *TextAdornment1.cs* には `TextAdornment1` クラスが含まれています。

    - *TextAdornment1TextViewCreationListener.cs* には `TextAdornment1TextViewCreationListener` クラスが含まれています。

4. プロジェクトをビルドし、デバッグを開始します。 実験用インスタンスが表示されます。 テキスト ファイルを開くと、テキスト内のすべての ' a ' という文字が赤色の枠線で囲まれ、背景が青色で表示されます。

## <a name="create-a-viewport-relative-adornment-extension"></a>ビューポート相対表示要素の拡張機能を作成する
 エディター ビューポート表示要素テンプレートでは、ビューポート相対表示要素が作成されます。これにより、ビューポートの右上隅に赤色の枠線を持つ紫色のボックスが追加されます。

> [!NOTE]
> **ビューポート** は、現在表示されているテキスト ビューの領域です。

### <a name="to-create-a-viewport-adornment-extension-by-using-the-editor-viewport-adornment-template"></a>エディター ビューポート表示要素テンプレートを使用して、ビューポート表示要素の拡張機能を作成するには

1. **[新しいプロジェクト]** ダイアログ ボックスで、 **[Visual C#]** または **[Visual Basic]** を展開し、 **[拡張性]** をクリックします。 **[テンプレート]** ペインで、 **[VSIX プロジェクト]** を選択します。 **[名前]** ボックスに「`ViewportAdornment`」と入力します。 **[OK]** をクリックします。

2. **ソリューション エクスプローラー** で、プロジェクト ノードを右クリックして、 **[追加]**  >  **[新しい項目]** の順に選択します。 Visual C# の **[拡張性]** ノードに移動して、 **[エディター ビューポート表示要素]** を選択します。 既定のファイル名 (*ViewportAdornment1.cs/vb*) をそのまま使用します。

3. 次の 2 つのコード ファイルがあります。

    - *ViewportAdornment1.cs* には `ViewportAdornment1` クラスが含まれています。

    - *ViewportAdornment1TextViewCreationListener.cs* には `ViewportAdornment1TextViewCreationListener` クラスが含まれています

4. プロジェクトをビルドし、デバッグを開始します。 実験用インスタンスが表示されます。 新しいテキスト ファイルを作成すると、ビューポートの右上隅に、赤色の枠線を持つ紫色のボックスが表示されます。

## <a name="create-a-margin-extension"></a>余白の拡張機能を作成する
 エディター余白テンプレートでは、「**Hello world!* 」という単語と共に表示される緑の余白が 水平スクロール バーの下に作成されます。

### <a name="to-create-a-margin-extension-by-using-the-editor-margin-template"></a>エディター余白テンプレートを使用して、余白の拡張機能を作成するには

1. **[新しいプロジェクト]** ダイアログ ボックスで、 **[Visual C#]** または **[Visual Basic]** を展開し、 **[拡張性]** をクリックします。 **[テンプレート]** ペインで、 **[VSIX プロジェクト]** を選択します。 **[名前]** ボックスに「`MarginExtension`」と入力します。 **[OK]** をクリックします。

2. **ソリューション エクスプローラー** で、プロジェクト ノードを右クリックして、 **[追加]**  >  **[新しい項目]** の順に選択します。 Visual C# の **[拡張性]** ノードに移動して、 **[エディター余白]** を選択します。 既定のファイル名 (EditorMargin1.cs/vb) をそのまま使用します。

3. 次の 2 つのコード ファイルがあります。

    - *EditorMargin1.cs* には `EditorMargin1` クラスが含まれています。

    - *EditorMargin1Factory.cs* には `EditorMargin1Factory` クラスが含まれています。

4. このプロジェクトをビルドし、デバッグを開始します。 実験用インスタンスが表示されます。 テキスト ファイルを開くと、水平スクロール バーの下に「**Hello EditorMargin1**」という単語がある緑の余白が表示されます。

## <a name="see-also"></a>関連項目
- [言語サービスとエディターの拡張ポイント](../extensibility/language-service-and-editor-extension-points.md)
