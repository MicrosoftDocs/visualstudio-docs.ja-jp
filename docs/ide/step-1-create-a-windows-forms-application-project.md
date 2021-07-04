---
title: '手順 1: Windows フォーム アプリ プロジェクトを作成する'
description: 画像ビューアーの Windows フォーム アプリ プロジェクトの作成方法を説明します。
ms.custom: SEO-VS-2020
ms.date: 08/30/2019
ms.assetid: 16ac2422-e720-4e3a-b511-bc2a54201a86
ms.topic: tutorial
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
author: j-martens
ms.author: jmartens
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: fccce125b66101b05544cba22b3724a8a40dc0f3
ms.sourcegitcommit: 5fb4a67a8208707e79dc09601e8db70b16ba7192
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2021
ms.locfileid: "112307740"
---
# <a name="step-1-create-a-windows-forms-app-project"></a>手順 1: Windows フォーム アプリ プロジェクトを作成する

ピクチャ ビューアーを作成する場合、最初の手順は、Windows フォーム アプリ プロジェクトを作成することです。

::: moniker range="vs-2017"

## <a name="open-visual-studio-2017"></a>Visual Studio 2017 を開きます

1. メニュー バーで、 **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** を選択します。 ダイアログ ボックスは次のスクリーンショットのように表示されます。

     ![[新しいプロジェクト] ダイアログ ボックス](../ide/media/newprojectdialogcallouts.png)<br/>***[新しいプロジェクト]** _ _ダイアログ ボックス*

2. **[新しいプロジェクト]** ダイアログ ボックスの左側で、**[Visual C#]** または **[Visual Basic]** を選択し、**[Windows Desktop]** を選択します。

3. プロジェクト テンプレート リストで、**[Windows フォーム アプリ (.NET Framework)]** を選択します。 新しいフォームに「*PictureViewer*」という名前を付け、**[OK]** をクリックします。

    >[!NOTE]
    >**[Windows フォーム アプリケーション (.NET Framework)]** テンプレートが表示されない場合は、Visual Studio インストーラーを使用して **[.NET デスクトップ開発]** ワークロードをインストールします。<br/><br/>![Visual Studio インストーラーでの [.NET デスクトップ開発] ワークロード](../ide/media/dot-net-desktop-dev-workload.png)<br/><br/> 詳細については、「[Visual Studio のインストール](../install/install-visual-studio.md)」を参照してください。

::: moniker-end

::: moniker range=">=vs-2019"

## <a name="open-visual-studio"></a>Visual Studio を開きます

1. スタート ウィンドウで、 **[新しいプロジェクトの作成]** を選択します。

   ![[新しいプロジェクトの作成] ウィンドウを表示する](../get-started/media/vs-2019/create-new-project-dark-theme.png)

1. **[新しいプロジェクトの作成]** ウィンドウで、検索ボックスに「*Windows フォーム*」と入力またはタイプします。 次に、**[プロジェクトの種類]** 一覧から **[デスクトップ]** を選択します。

   **[プロジェクトの種類]** フィルターを適用したら、C# または Visual Basic の **[Windows フォーム アプリ (.NET Framework)]** テンプレートを選択し、**[次へ]** を選択します。

   ![Windows フォーム アプリ (.NET Framework) 用の C# または Visual Basic テンプレートを選択する](./media/create-new-project-search-winforms-filtered.png)

   > [!NOTE]
   > **[Windows フォーム アプリ (.NET Framework)]** テンプレートが表示されない場合は、**[新しいプロジェクトの作成]** ウィンドウからインストールできます。 **[お探しの情報が見つかりませんでしたか?]** メッセージで、 **[さらにツールと機能をインストールする]** リンクを選択します。
   >
   > ![[新しいプロジェクトの作成] ウィンドウに表示された [お探しの情報が見つかりませんでしたか?] での [さらにツールと機能をインストールする] リンク](../get-started/media/vs-2019/not-finding-what-looking-for.png)
   >
   > 次に、Visual Studio インストーラーで、 **[.NET デスクトップの開発]** ワークロードを選択します。
   >
   > ![Visual Studio インストーラーの .NET Core ワークロード](../ide/media/install-dot-net-desktop-env.png)
   >
   > その後、Visual Studio インストーラー内の **[変更]** ボタンをクリックします。 作業内容を保存するよう求められることがあります。その場合は、そのようにします。 次に、 **[続行]** を選択してワークロードをインストールします。

1. **[新しいプロジェクトの構成]** ウィンドウで、**[プロジェクト名]** ボックスに「*PictureViewer*」とタイプまたは入力します。 次に、 **[作成]** を選択します。

::: moniker-end

Visual Studio により、アプリのソリューションが作成されます。 ソリューションは、アプリに必要なすべてのプロジェクトとファイルのコンテナーとして機能します。 これらについては、このチュートリアルで後ほど詳しく説明します。

## <a name="about-the-windows-forms-app-project"></a>Windows フォーム アプリ プロジェクトについて

1. 開発環境には、3 つのウィンドウ (メイン ウィンドウ、**ソリューション エクスプローラー**、**[プロパティ]** ウィンドウ) があります。

     これらのウィンドウのいずれかが表示されていない場合は、既定のウィンドウ レイアウトを復元できます。 メニュー バーで、 **[ウィンドウ]**  >  **[ウィンドウ レイアウトのリセット]** の順に選びます。

     メニュー コマンドを使用してウィンドウを表示することもできます。 メニュー バーで、 **[表示]**  >  **[プロパティ ウィンドウ]** または **[ソリューション エクスプローラー]** の順に選択します。

     他のウィンドウが開いている場合は、右上隅の **[閉じる]** (x) ボタンを選択して閉じます。

    ::: moniker range="vs-2017"

    * **メイン ウィンドウ** このウィンドウでは、フォームの操作やコードの編集など、ほとんどの作業を行います。 このウィンドウに、**フォーム エディター** のフォームが表示されています。 ウィンドウの上部には、**[スタート ページ]** タブと **[Form1.cs [デザイン]]** タブが表示されています  (Visual Basic では、タブの名前は *.cs* ではなく *.vb* で終わります)。

    ::: moniker-end

    ::: moniker range=">=vs-2019"

    * **メイン ウィンドウ** このウィンドウでは、フォームの操作やコードの編集など、ほとんどの作業を行います。 このウィンドウに、**フォーム エディター** のフォームが表示されています。

    ::: moniker-end

    * **ソリューション エクスプローラーウィンドウ** このウィンドウでは、ソリューション内のすべての項目を確認し、各項目に移動できます。

    ファイルを選択すると、**[プロパティ]** ウィンドウの内容が変わります。 コード ファイル (C# の場合は *.cs*、Visual Basic の場合は *.vb* で終わるファイル) を開くと、コード ファイルまたはコード ファイルのデザイナーが表示されます。 デザイナーは、ボタンやリストなどのコントロールを追加できるビジュアル サーフェイスです。 Visual Studio のフォームでは、デザイナーは **Windows フォーム デザイナー** と呼ばれます。

    * **[プロパティ] ウィンドウ** このウィンドウでは、他のウィンドウで選択した項目のプロパティを変更できます。 たとえば、Form1 を選択した場合、**Text** プロパティを設定してタイトルを変更し、**Backcolor** プロパティを設定して背景色を変更することができます。

      > [!NOTE]
      > **ソリューション エクスプローラー** の先頭行には、"**ソリューション 'PictureViewer' (1 プロジェクト)**" と表示されています。これは、Visual Studio によってソリューションが作成されたことを意味します。 ソリューションには複数のプロジェクトを含めることができますが、ここでは、プロジェクトを 1 つだけ含むソリューションを使用します。

1. メニュー バーで、 **[ファイル]**  >  **[すべてを保存]** の順に選択します。

     または、次の画像に示すツール バーの **[すべてを保存]** ボタンを選択します。

     ![[すべてを保存] ツール バー ボタン](../ide/media/express_iconsaveall.png)<br/>
     ***[すべてを保存]** _ _ツール バー ボタン*

     Visual Studio によって自動的にフォルダー名およびプロジェクト名が指定され、projects フォルダーにプロジェクトが保存されます。

## <a name="next-steps"></a>次のステップ

* チュートリアルの次の手順に進むには、 **[手順 2: アプリの実行](../ide/step-2-run-your-program.md)** に関するページを参照してください。

* 概要のトピックに戻るには、「[チュートリアル 1: ピクチャ ビューアーの作成](../ide/tutorial-1-create-a-picture-viewer.md)」をご覧ください。

## <a name="see-also"></a>関連項目

* [チュートリアル 2: 制限時間ありの計算クイズの作成](tutorial-2-create-a-timed-math-quiz.md)
* [チュートリアル 3: 絵合わせゲームの作成](tutorial-3-create-a-matching-game.md)
