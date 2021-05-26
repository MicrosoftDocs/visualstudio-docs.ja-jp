---
title: 拡張機能パックを作成する
description: 拡張機能パック項目テンプレートを使用して拡張機能パックを作成する方法について説明します
ms.custom: SEO-VS-2020
ms.date: 07/27/2018
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - extensions
ms.assetid: 5388EEBA-211D-4114-8CD9-70C899919F7E
author: leslierichardson95
ms.author: lerich
manager: Meng
ms.workload:
- vssdk
ms.openlocfilehash: 57b447be3ee411b737c1aea5b0a4be5ef966c8c6
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105062149"
---
# <a name="walkthrough-create-an-extension-pack"></a>チュートリアル: 拡張機能パックを作成する

拡張機能パックは、まとめてインストールできる一連の拡張機能です。 拡張機能パックを使用すると、お気に入りの拡張機能を他のユーザーと共有することや、特定のシナリオに合わせて一連の拡張機能をバンドルすることが簡単にできます。

## <a name="prerequisites"></a>必須コンポーネント

Visual Studio 2015 以降では、Visual Studio SDK が Visual Studio セットアップのオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「[Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

拡張機能パック機能は、Visual Studio 15.8 Preview 2 以降で使用できます。

## <a name="create-an-extension-with-an-extension-pack-item-template"></a>拡張機能パック項目テンプレートを使用して拡張機能を作成する

拡張機能パック項目テンプレートでは、まとめてインストールできる一連の拡張機能を使用して拡張機能パックを作成します。

1. **[新しいプロジェクト]** ダイアログで、"vsix" を検索し、 **[VSIX プロジェクト]** を選択します。 **[プロジェクト名]** に「Test Extension Pack」と入力します。 **［作成］** を選択します

2. **ソリューション エクスプローラー** で、プロジェクト ノードを右クリックして、 **[追加]**  >  **[新しい項目]** の順に選択します。 Visual C# の **[機能拡張]** ノードにアクセスし、 **[拡張機能パック]** を選択します。 既定のファイル名 (ExtensionPack1.cs) をそのまま使用します。

3. 次のコードを含む ExtensionPack1.vsext ファイルが追加されます

   ```json
   {
    "id": "ExtensionPack1",
    "name": "ExtensionPack1",
    "description": "Read about creating extension packs at https://aka.ms/vsextpack",
    "version": "1.0.0.0",
    "extensions": [  // List of extensions that are included in the Extension Pack.
      {
        "vsixId": "41858b2d-ff0b-4a43-80b0-f1b2d6084935", // The vsix id of the extension you want to   include.
        "name": "AlignAssignments"
      },
      {
          "vsixId": "42374550-426a-400e-96f9-237682e8dea6",
        "name": "CopyAsHtml"
      }
    ]
   }
   ```

4. 拡張機能パックに含める拡張機能の vsixId は、[Visual Studio Marketplace](https://marketplace.visualstudio.com/) で確認できます。 含める拡張機能を見つけて、 **[ID のコピー]** をクリックします。 上記のファイルの既存の **vsixId** を更新することも、別の拡張機能を一覧に追加することもできます。

    ![Marketplace から vsixId をコピーする](media/vsixid-marketplace.png)

5. プロジェクトをビルドし、拡張機能を Marketplace にアップロードします。 「[Visual Studio 拡張機能の発行](../extensibility/walkthrough-publishing-a-visual-studio-extension.md)」を参照してください。

> [!NOTE]
> 拡張機能パックでは、[Visual Studio Marketplace](https://marketplace.visualstudio.com/) または[プライベート ギャラリー](../extensibility/how-to-create-an-atom-feed-for-a-private-gallery.md)で利用できる拡張機能のみをインストールできます。

## <a name="install-the-extension-pack-from-the-visual-studio-marketplace"></a>Visual Studio Marketplace から拡張機能パックをインストールする

拡張機能が公開されたので、それを Visual Studio にインストールしてテストします。

::: moniker range="vs-2017"

1. Visual Studio の **[ツール]** メニューで、 **[拡張機能と更新プログラム]** をクリックします。

::: moniker-end

::: moniker range=">=vs-2019"

1. Visual Studio の **[拡張機能]** メニューで、 **[マネージ拡張]** をクリックします。

::: moniker-end

2. **[オンライン]** をクリックしてから、「Test Extension Pack」を検索します。

3. **[Download]** をクリックします。 その後、拡張機能と拡張機能パックに含まれている拡張機能の一覧が、インストール対象としてスケジュールされます。

4. **[拡張機能の管理]** ダイアログの拡張機能パックのダウンロードの表示例を次に示します。 拡張機能パックに含まれている拡張機能の一部のみをインストールする場合は、 **[インストールのスケジュール]** で拡張機能の一覧を変更できます。

    ![Marketplace から拡張機能パックをダウンロードする](media/vside-extensionpack.png)

5. インストールを完了するには、Visual Studio のすべてのインスタンスを閉じます。

## <a name="remove-the-extension"></a>拡張機能を削除する

コンピューターから拡張機能を削除するには:

::: moniker range="vs-2017"

1. Visual Studio の **[ツール]** メニューで、 **[拡張機能と更新プログラム]** をクリックします。

::: moniker-end

::: moniker range=">=vs-2019"

1. Visual Studio の **[拡張機能]** メニューで、 **[マネージ拡張]** をクリックします。

::: moniker-end

2. **[Test Extension Pack]** を選択してから、 **[アンインストール]** をクリックします。 その後、拡張機能と拡張機能パックに含まれている拡張機能の一覧が、アンインストール対象としてスケジュールされます。

3. アンインストールを完了するには、Visual Studio のすべてのインスタンスを閉じます。
