---
title: 拡張機能の発行 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- publishing web controls
- web controls, publishing
ms.assetid: a7816161-0490-4043-86f5-0f7331ed83b3
caps.latest.revision: 21
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: f8cec34f5eb814dfd236aa5fab46bcc811c8c88f
ms.sourcegitcommit: 53aa5a413717a1b62ca56a5983b6a50f7f0663b3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59669706"
---
# <a name="walkthrough-publishing-a-visual-studio-extension"></a>チュートリアル: Visual Studio の拡張機能を発行する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

**注**:Visual Studio ギャラリーは、Visual Studio Marketplace に置き換えられます。 詳細については、このトピックの最新バージョンを参照してください。

このチュートリアルでは、Visual Studio 拡張機能を Visual Studio ギャラリーに発行する方法を示します。 ギャラリーに、拡張機能を追加すると、開発者が使用できる**拡張機能と更新**新規および更新された拡張機能の参照があります。

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルに従うには、Visual Studio SDK をインストールする必要があります。 詳細については、次を参照してください。 [Visual Studio SDK](../extensibility/visual-studio-sdk.md)します。

## <a name="create-a-visual-studio-extension"></a>Visual Studio 拡張機能を作成します。
 ここで、既定の VSPackage 拡張機能を使用していますが、同じ手順は拡張機能のすべての種類に対して無効です。

1.  C# という名前の VSPackage を作成`TestPublishing`を持つメニュー コマンド。 詳細については、次を参照してください。[メニュー コマンドを使用して拡張機能の作成](../extensibility/creating-an-extension-with-a-menu-command.md)です。

## <a name="test-the-extension"></a>拡張機能をテストします。
 拡張機能を配布する前にビルドしてテストを Visual Studio の実験用インスタンスで正しくインストールされていることを確認します。

1.  Visual Studio でデバッグを開始します。 Visual Studio の実験用インスタンスを開きます。

2.  実験用のインスタンスに移動、**ツール**メニューをクリックします**拡張機能マネージャー**します。 TestPublishing 拡張機能では、中央のウィンドウに表示する必要があり、有効にします。

3.  **ツール** メニューの テスト コマンドを表示するかどうかを確認します。

## <a name="publish-the-extension-to-the-visual-studio-gallery"></a>拡張機能を Visual Studio ギャラリーに公開します。
 今すぐ、拡張機能を Visual Studio ギャラリーに発行できます。

1.  拡張機能のリリース バージョンが組み込まれているし、最新の状態であるようにします。

2.  Web ブラウザーで開く、 [Visual Studio Marketplace](https://marketplace.visualstudio.com/) web サイト。

3.  右上隅にある次のようにクリックします。 **SIGN IN**します。

4.  Microsoft アカウントを使用してサインインします。 Microsoft アカウントがない、この時点で作成できます。

5.  **[アップロード]** をクリックします。

6.  **手順 1。拡張機能の種類**、**ツール**順にクリックします**次**。

7.  **手順 2。アップロード**、Visual Studio ギャラリーに直接アップロードまたは独自の web サイトにリンクを追加することもできます。 ここで **ツールをアップロードしたい**します。 **、コントロールを選択**ボックスが表示されます。 クリックして**参照**し、プロジェクトの \bin\Release フォルダーで TestPublish.vsix を選択します。 **[次へ]** をクリックします。

8.  **手順 3。基本的な情報**、source.extension.vsixmanifest ファイルのフィールドが表示されます。 適切な選択**カテゴリ**追加**タグ**拡張機能を見つけられるようにします。 詳細な概要と説明 (説明は、少なくとも 280 文字である必要があります) を追加することがあります。 ままに**拡張機能の種類**として **、Microsoft 拡張機能ではない**と**原価カテゴリ**として**試用版**します。

9. ページの下部に投稿物に関する契約を読んで確認**同意**します。

10. クリックして**投稿を作成する**します。 これには、拡張機能では Visual Studio ギャラリーのページがまだ発行されているメッセージにページが表示されます。

11. **[発行]** をクリックします。

12. 拡張機能の Visual Studio ギャラリーを検索します。 TestPublish 拡張機能の一覧が表示されます。

## <a name="install-the-extension-from-the-visual-studio-gallery"></a>Visual Studio ギャラリーから拡張機能をインストールします。
 これで、拡張機能を公開すると、Visual Studio にインストールし、テストします。

1.  Visual Studio での**ツール** メニューのをクリックして**拡張機能と更新**します。

2.  クリックして**オンライン**TestPublish し検索します。 TestPublish 拡張機能の一覧が表示されます。

3.  **[ダウンロード]** をクリックします。 拡張機能をダウンロードした後、 **[インストール]** をクリックします。

4.  インストールが完了するには、Visual Studio を再起動します。

## <a name="removing-the-extension"></a>拡張機能を削除
 お使いのコンピューターと、Visual Studio ギャラリーから拡張機能を削除できます。

#### <a name="to-remove-the-extension-from-the-visual-studio-gallery"></a>Visual Studio ギャラリーから拡張機能を削除するには

1.  開く、 [Visual Studio Marketplace](https://marketplace.visualstudio.com/) web サイト。

2.  右上隅にある次のようにクリックします。**マイ Extenions**します。 TestPublish の一覧が表示されます。

3.  **[Delete]** をクリックします。

#### <a name="to-remove-the-extension-from-your-computer"></a>お使いのコンピューターから、拡張機能を削除するには

1.  Visual Studio の **[ツール]** メニューで、 **[拡張機能マネージャー]** をクリックします。

2.  TestPublish を選択し、クリックして**アンインストール**します。

3.  アンインストールを完了するには、Visual Studio を再起動します。
