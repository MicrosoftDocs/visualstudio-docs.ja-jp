---
title: 'チュートリアル: プロジェクトとソリューション (Visual Basic)'
description: Visual Basic 開発者として Visual Studio でソリューションとプロジェクトを作成する方法について説明します。
ms.date: 12/12/2018
ms.technology: vs-ide-general
ms.custom:
- vs-acquisition
- get-started
- SEO-VS-2020
ms.topic: tutorial
author: TerryGLee
ms.author: tglee
manager: jmartens
dev_langs:
- VB
ms.workload:
- dotnet
ms.openlocfilehash: 813a6ce10b0c5bcc385ac72ba6fdf99495c457ee
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112384734"
---
# <a name="learn-about-projects-and-solutions-using-visual-basic"></a>Visual Basic を使用するプロジェクトとソリューションについて理解する

この入門記事では、Visual Studio で *ソリューション* と *プロジェクト* を作成することの意味について説明します。 ソリューションは、1 つまたは複数の関連するコード プロジェクトを整理するために使われるコンテナーです。たとえば、クラス ライブラリ プロジェクトとそれに対応するテスト プロジェクトなどです。 プロジェクトのプロパティと、プロジェクトに含めることができるファイルのいくつかを紹介します。 また、あるプロジェクトから別のプロジェクトへの参照も作成します。

::: moniker range="vs-2017"

> [!TIP]
> Visual Studio をまだインストールしていない場合は、[Visual Studio のダウンロード](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download) ページに移動し、無料試用版をインストールしてください。

::: moniker-end

::: moniker range="vs-2019"

> [!TIP]
> Visual Studio をまだインストールしていない場合は、[Visual Studio のダウンロード](https://visualstudio.microsoft.com/downloads) ページに移動し、無料試用版をインストールしてください。

::: moniker-end

::: moniker range="vs-2022"

> [!TIP]
> Visual Studio プレビューをまだインストールしていない場合は、[Visual Studio 2022 プレビューのダウンロード](https://visualstudio.microsoft.com/vs/preview/vs2022) ページに移動し、無料試用版をインストールしてください。

::: moniker-end

プロジェクトの概念を学習して理解するための演習として、ソリューションとプロジェクトをゼロから構築します。 Visual Studio の一般的な使い方として、新しいプロジェクトを作成するときに、Visual Studio で用意されているさまざまなプロジェクト "*テンプレート*" を使うことがよくあります。

> [!NOTE]
> Visual Studio でアプリを開発するにあたり、ソリューションとプロジェクトは必須ではありません。 また、コードが含まれているフォルダーを開いて、コードの作成、ビルド、およびデバッグを開始することもできます。 たとえば、[GitHub](https://github.com/) リポジトリを複製しても、それには Visual Studio のプロジェクトとソリューションが含まれていない場合があります。 詳細については、「[プロジェクトまたはソリューションを使用せずに Visual Studio でコードを開発する](../../ide/develop-code-in-visual-studio-without-projects-or-solutions.md)」を参照してください。

## <a name="solutions-and-projects"></a>ソリューションとプロジェクト

ソリューションは、その名前にもかかわらず、"答え" ではありません。 ソリューションは、Visual Studio で 1 つまたは複数の関連プロジェクトを整理するために使用される単なるコンテナーです。 Visual Studio でソリューションを開くと、ソリューションに含まれているすべてのプロジェクトが自動的に読み込まれます。

### <a name="create-a-solution"></a>ソリューションを作成する

空のソリューションを作成するところから説明を始めます。 Visual Studio に慣れてきても、自分が空のソリューションを頻繁に作成していることにはほとんど気づかないでしょう。 Visual Studio で新しいプロジェクトを作成するとき、ソリューションがまだ開いていなければ、プロジェクトを格納するためのソリューションが自動的に作成されます。

::: moniker range="vs-2017"

1. Visual Studio を開きます。

1. メニュー バーで、 **[ファイル]** > **[新規作成]** > **[プロジェクト]** を選択します。

   **[新しいプロジェクト]** ダイアログ ボックスが表示されます。

1. 左側のウィンドウで、 **[その他のプロジェクトの種類]** を展開し、 **[Visual Studio ソリューション]** を選択します。 中央のウィンドウで、 **[空のソリューション]** テンプレートを選択します。 ソリューションに **QuickSolution** という名前を付けて、**[OK]** を選択します。

   ![Visual Studio での空のソリューション テンプレート](../media/tutorial-projects-new-solution.png)

   **[スタート ページ]** が閉じて、Visual Studio ウィンドウの右側にある **ソリューション エクスプローラー** にソリューションが表示されます。 多くの場合、**ソリューション エクスプローラー** を使用して、プロジェクトの内容を参照することになります。

::: moniker-end

::: moniker range=">=vs-2019"

1. Visual Studio を開きます。

2. スタート ウィンドウで、 **[新しいプロジェクトの作成]** を選択します。

3. **[新しいプロジェクトの作成]** ページで、検索ボックスに「**空のソリューション**」と入力し、 **[空のソリューション]** テンプレートを選択して、 **[次へ]** を選択します。

   ![Visual Studio 2019 での空のソリューション テンプレート](../media/vs-2019/tutorial-projects-blank-solution-template.png)

4. ソリューションに **QuickSolution** という名前を設定して、 **[作成]** を選択します。

   Visual Studio ウィンドウの右側にある **ソリューション エクスプローラー** にソリューションが表示されます。 多くの場合、**ソリューション エクスプローラー** を使用して、プロジェクトの内容を参照することになります。

::: moniker-end

### <a name="add-a-project"></a>プロジェクトを追加する

次に、最初のプロジェクトをソリューションに追加してみましょう。 空のプロジェクトから始めて、そのプロジェクトに必要なアイテムを追加します。

::: moniker range="vs-2017"

1. **ソリューション エクスプローラー** で **ソリューション "QuickSolution"** の右クリックまたはコンテキスト メニューから、 **[追加]** > **[新しいプロジェクト]** を選択します。

   **[新しいプロジェクトの追加]** ダイアログ ボックスが表示されます。

1. 左側のウィンドウで、**[Visual Basic]** を展開し、**[Windows デスクトップ]** を選択します。 次に、中央のウィンドウで、 **[空のプロジェクト (.NET Framework)]** テンプレートを選択します。 プロジェクトに「**QuickDate**」という名前を付けて、**[OK]** ボタンを選択します。

   **ソリューション エクスプローラー** で、ソリューションの下に QuickDate という名前のプロジェクトが表示されます。 現在のところ、このプロジェクトには *App.config* と呼ばれるファイルが 1 つ含まれています。

   > [!NOTE]
   > ダイアログ ボックスの左側のウィンドウに **Visual Basic** が表示されない場合は、**.NET デスクトップ開発** Visual Studio *ワークロード* をインストールする必要があります。 Visual Studio は、ワークロード ベースのインストールを使って、行われる開発の種類に必要なコンポーネントだけをインストールします。 新しいワークロードをインストールする簡単な方法は、 **[新しいプロジェクトの追加]** ダイアログ ボックスの左下隅にある **[Visual Studio インストーラーを開く]** リンクをクリックすることです。 Visual Studio インストーラーが起動した後、 **[.NET デスクトップ開発]** ワークロードを選択して、 **[変更]** ボタンを選択します。
   >
   > ![Visual Studio インストーラー リンクを開く](media/tutorial-projects-open-installer-vb.png)

::: moniker-end

::: moniker range=">=vs-2019"

1. **ソリューション エクスプローラー** で **ソリューション "QuickSolution"** の右クリックまたはコンテキスト メニューから、 **[追加]** > **[新しいプロジェクト]** を選択します。

   **[新しいプロジェクトの追加]** ダイアログ ボックスが開きます。

1. 上部の検索ボックスに「**empty**」というテキストを入力し、**[言語]** で **[Visual Basic]** を選択します。

1. **[空のプロジェクト (.NET Framework)]** テンプレートを選択し、 **[次へ]** を選択します。

1. プロジェクトに「**QuickDate**」という名前を付けて、 **[作成]** を選択します。

   **ソリューション エクスプローラー** で、ソリューションの下に QuickDate という名前のプロジェクトが表示されます。 現在のところ、このプロジェクトには *App.config* と呼ばれるファイルが 1 つ含まれています。

   > [!NOTE]
   > **[空のプロジェクト (.NET Framework)]** テンプレートが表示されない場合は、**.NET デスクトップ開発** Visual Studio "*ワークロード*" をインストールする必要があります。 Visual Studio は、ワークロード ベースのインストールを使って、行われる開発の種類に必要なコンポーネントだけをインストールします。 新しいプロジェクトを作成するときに新しいワークロードをインストールする簡単な方法は、 **[探しているものが見つからない場合]** というテキストの下にある **[さらにツールと機能をインストールする]** リンクを選択することです。 Visual Studio インストーラーが起動した後、 **[.NET デスクトップ開発]** ワークロードを選択して、 **[変更]** ボタンを選択します。
   >
   > ![Visual Studio 2019 でのインストーラー リンク](../media/vs-2019/tutorial-projects-open-installer.png)

::: moniker-end

## <a name="add-an-item-to-the-project"></a>プロジェクトにアイテムを追加する

空のプロジェクトを用意しました。 コード ファイルを追加しましょう。

1. **ソリューション エクスプローラー** で **QuickDate** プロジェクトの右クリック メニューまたはコンテキスト メニューから、 **[追加]**  >  **[新しい項目]** を選択します。

   **[新しい項目の追加]** ダイアログ ボックスが開きます。

1. **[共通項目]** を展開し、**[コード]** を選択します。 中央のウィンドウで、**[クラス]** 項目テンプレートを選択します。 クラスに「**Calendar**」という名前を付け、 **[追加]** ボタンを選択します。

   *Calendar.vb* という名前のファイルがプロジェクトに追加されます。 末尾の *.vb* は、Visual Basic コード ファイルに付けられるファイル拡張子です。 **ソリューション エクスプローラー** のビジュアル プロジェクト階層にファイルが表示され、その内容がエディターで開かれます。

1. *Calendar.vb* ファイルの内容を次のコードに置き換えます。

   ```vb
   Class Calendar
       Public Shared Function GetCurrentDate() As Date
           Return DateTime.Now.Date
       End Function
   End Class
   ```

   `Calendar` クラスには、現在の日付を返す、`GetCurrentDate` という 1 つの関数が含まれます。

1. **ソリューション エクスプローラー** で **[My Project]** をダブルクリックして、プロジェクトのプロパティを開きます。 **[アプリケーション]** タブで、**[アプリケーションの種類]** を **[クラス ライブラリ]** に変更します。 この手順は、プロジェクトを正常にビルドするために必要です。

1. **ソリューション エクスプローラー** で **[QuickDate]** を右クリックし、**[ビルド]** を選択してプロジェクトをビルドします。 **[出力]** ウィンドウには、ビルドが成功したことを示すメッセージが表示されるはずです。

## <a name="add-a-second-project"></a>2 つ目のプロジェクトを追加する

ソリューションには複数のプロジェクトが含まれているのが一般的です。これらのプロジェクトは多くの場合、互いに参照しています。 ソリューション内に含めるプロジェクトはクラス ライブラリ、実行可能なアプリケーション、および単体テスト プロジェクトまたは Web サイトとすることができます。

単体テスト プロジェクトをソリューションに追加してみましょう。 今度はプロジェクト テンプレートから開始します。これにより、プロジェクトに追加のコード ファイルを追加する必要がなくなります。

1. **ソリューション エクスプローラー** で **ソリューション "QuickSolution"** の右クリックまたはコンテキスト メニューから、**[追加]** > **[新しいプロジェクト]** を選択します。

::: moniker range="Vs-2017"

2. 左側のウィンドウで、**[Visual Basic]** を展開し、**[テスト]** カテゴリを選択します。 中央のウィンドウで、**[単体テスト プロジェクト (.NET Framework)]** プロジェクト テンプレートを選択します。 プロジェクトに「**QuickTest**」という名前を付けて、**[OK]** を選択します。

   2 つ目のプロジェクトが **ソリューション エクスプローラー** に追加され、*UnitTest1.vb* という名前のファイルがエディターで開きます。

   ![2 つのプロジェクトを含む Visual Studio ソリューション エクスプローラー](media/tutorial-projects-solution-explorer-vb.png)

::: moniker-end

::: moniker range=">=vs-2019"

2. **[新しいプロジェクトの追加]** ダイアログ ボックスで、上部にある検索ボックスに「**unit test**」というテキストを入力し、**[言語]** で **[Visual Basic]** を選択します。

3. **[単体テスト プロジェクト (.NET Framework)]** プロジェクト テンプレートを選択してから、**[次へ]** を選択します。

4. プロジェクトに「**QuickTest**」という名前を付けて、**[作成]** を選択します。

   2 つ目のプロジェクトが **ソリューション エクスプローラー** に追加され、*UnitTest1.vb* という名前のファイルがエディターで開きます。

::: moniker-end

## <a name="add-a-project-reference"></a>プロジェクト参照を追加する

これから、新しい単体テスト プロジェクトを使用して **QuickDate** プロジェクト内のメソッドをテストします。それには、そのプロジェクトへの参照を追加する必要があります。 そうすることで、2 つのプロジェクトの間に "*ビルドの依存関係*" が作成されます。つまり、ソリューションをビルドすると、先に **QuickDate** がビルドされてから、**QuickTest** がビルドされます。

1. **QuickTest** プロジェクトで **[参照]** ノードを選択し、右クリックまたはコンテキスト メニューから、**[参照の追加]** を選択します。

   ![[参照の追加] メニュー](media/tutorial-projects-add-reference-vb.png)

   **[参照マネージャー]** ダイアログ ボックスが表示されます。

1. 左側のウィンドウで、**[プロジェクト]** を展開し、**[ソリューション]** を選択します。 中央のウィンドウで、**QuickDate** の横にあるチェック ボックスを選択し、**[OK]** ボタンを選択します。

   **QuickDate** プロジェクトへの参照が追加されます。

## <a name="add-test-code"></a>テスト コードを追加する

1. ここで、Visual Basic コード ファイルにテスト コードを追加します。 *UnitTest1.vb* の内容を次のコードに置き換えます。

   ```vb
   <TestClass()> Public Class UnitTest1

       <TestMethod()> Public Sub TestGetCurrentDate()
           Assert.AreEqual(Date.Now.Date, QuickDate.Calendar.GetCurrentDate())
       End Sub

   End Class
   ```

   コードの一部分の下に赤色の波線が表示されます。 テスト プロジェクトを、**QuickDate** プロジェクトに対する [フレンド アセンブリ](/dotnet/visual-basic/programming-guide/concepts/assemblies-gac/friend-assemblies)にすることで、このエラーを修正します。

1. **QuickDate** プロジェクトに戻り、*Calendar.vb* ファイルをまだ開いていない場合は開きます。さらに、次の [Imports ステートメント](/dotnet/visual-basic/language-reference/statements/imports-statement-net-namespace-and-type)と <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> 属性を追加して、テスト プロジェクトのエラーを解決します。

   ```vb
   Imports System.Runtime.CompilerServices

   <Assembly: InternalsVisibleTo("QuickTest")>
   ```

   コード ファイルは、次のようになります。

   ![Visual Basic コード](media/tutorial-projects-code-vb.png)

## <a name="project-properties"></a>プロジェクトのプロパティ

<xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> 属性を含む *Calendar.vb* ファイル内の行では、**QuickTest** プロジェクトのアセンブリ名 (ファイル名) を参照します。 アセンブリ名はプロジェクト名と常に同じであるとは限りません。 プロジェクトのアセンブリ名を検索するには、プロジェクトのプロパティを開きます。

1. **ソリューション エクスプローラー** で **QuickTest** プロジェクトを選択します。 右クリックまたはコンテキスト メニューから、**[プロパティ]** を選択するか、または **Alt**+**Enter** キーを押します。 (**ソリューション エクスプローラー** で **[My Project]** をダブルクリックすることもできます)。

   **[アプリケーション]** タブで、プロジェクトの "*プロパティ ページ*" が開きます。プロパティ ページには、プロジェクトのさまざまな設定が含まれます。 **QuickTest** プロジェクトのアセンブリ名が "QuickTest" であることに注目してください。 これを変更する場合は、ここでその変更を行います。 テスト プロジェクトをビルドすると、結果として得られるバイナリ ファイルの名前は *QuickTest.dll* から、選択した任意の名前に変わります。

   ![プロジェクトのプロパティ](../media/tutorial-projects-properties.png)

1. **[コンパイル]** や **[設定]** など、プロジェクトのプロパティ ページの他のいくつかのタブを紹介します。 これらのタブは、プロジェクトの種類によって異なります。

## <a name="optional-run-the-test"></a>(省略可能) テストを実行する

単体テストが動作していることを確認する場合は、メニュー バーから **[テスト]**  >  **[実行]**  >  **[すべてのテスト]** を選択します。 **テスト エクスプローラー** と呼ばれるウィンドウが開くので、**TestGetCurrentDate** テストが成功しているか確認する必要があります。

![テストに合格したことを示す Visual Studio のテキスト エクスプローラー](../media/tutorial-projects-test-explorer.png)

> [!TIP]
> **テスト エクスプローラー** が自動的に開かない場合は、メニュー バーから **[テスト]** > **[Windows]** > **[テスト エクスプローラー]** を選択して開きます。

## <a name="next-steps"></a>次のステップ

Visual Studio についてさらに詳しく調べる場合は、次のいずれかの [Visual Basic のチュートリアル](index.yml)に従って、アプリの作成を検討してください。

## <a name="see-also"></a>関連項目

- [プロジェクトとソリューションを作成する](../../ide/creating-solutions-and-projects.md)
- [プロジェクトおよびソリューションのプロパティの管理](../../ide/managing-project-and-solution-properties.md)
- [プロジェクト内の参照の管理](../../ide/managing-references-in-a-project.md)
- [プロジェクトまたはソリューションを使用せずに Visual Studio でコードを開発する](../../ide/develop-code-in-visual-studio-without-projects-or-solutions.md)
- [Visual Studio IDE の概要](../../get-started/visual-studio-ide.md)
