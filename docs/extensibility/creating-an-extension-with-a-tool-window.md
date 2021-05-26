---
title: ツール ウィンドウでの拡張機能の作成 | Microsoft Docs
description: VSIX プロジェクト テンプレートとカスタム ツール ウィンドウ項目テンプレートを使用して、ツール ウィンドウで拡張機能を作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 3/16/2019
ms.topic: how-to
ms.assetid: 585b0a3a-f85b-4f92-81bb-9ca499bb8a89
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: f956aa520bca79a84fe203093c225cfeb8389ba1
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105089200"
---
# <a name="create-an-extension-with-a-tool-window"></a>ツール ウィンドウでの拡張機能の作成

この手順では、VSIX プロジェクト テンプレートと **カスタム ツール ウィンドウ** 項目テンプレートを使用して、ツール ウィンドウで拡張機能を作成する方法について説明します。

## <a name="prerequisites"></a>必須コンポーネント

 Visual Studio 2015 以降では、ダウンロード センターからの Visual Studio SDK のインストールは行いません。 これは、Visual Studio セットアップにオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「[Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

### <a name="create-a-tool-window"></a>ツール ウィンドウを作成する

1. **FirstWindow** という名前の VSIX プロジェクトを作成します。 VSIX プロジェクト テンプレートは、 **[新しいプロジェクト]** ダイアログで「vsix」と検索すると見つかります。

2. プロジェクトが開いたら、**MyWindow** という名前のツール ウィンドウ項目テンプレートを追加します。 **ソリューション エクスプローラー** で、プロジェクト ノードを右クリックして、 **[追加]**  >  **[新しい項目]** の順に選択します。 **[新しい項目の追加]** ダイアログで、 **[Visual C#]**  >  **[機能拡張]** の順にアクセスし、 **[カスタム ツール ウィンドウ]** を選択します。 ウィンドウの下部にある **[名前]** フィールドで、ツール ウィンドウのファイル名を *MyWindow.cs* に変更します。

3. プロジェクトをビルドし、デバッグを開始します。

   Visual Studio の実験用インスタンスが表示されます。 実験用インスタンスの詳細については、「[実験用インスタンス](../extensibility/the-experimental-instance.md)」を参照してください。

4. 実験用インスタンスで、 **[ビュー]**  >  **[その他のウィンドウ]** の順にアクセスします。

   **MyWindow** のメニュー項目が表示されます。 このボタンをクリックします。

   **MyWindow** というタイトルのツール ウィンドウと、「**Click Me!** 」と書かれたボタンが表示されます。
