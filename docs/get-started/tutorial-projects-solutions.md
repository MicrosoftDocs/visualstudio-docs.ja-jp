---
title: プロジェクトとソリューションの概要
description: プロジェクトとソリューションの違いと、Visual Studio でそれらを使用する方法について説明します。
ms.date: 11/17/2020
ms.technology: vs-ide-general
ms.custom:
- vs-acquisition
- get-started
- SEO-VS-2020
ms.topic: tutorial
f1_keywords:
- project.addnewitem
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 1d06b53afc811517ac86be9bdc3e86cf7593bbaf
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112390035"
---
# <a name="introduction-to-projects-and-solutions"></a>プロジェクトとソリューションの概要

この入門記事では、Visual Studio で *ソリューション* と *プロジェクト* を作成することの意味について説明します。 ソリューションは、1 つまたは複数の関連するコード プロジェクトを整理するために使われるコンテナーです。たとえば、クラス ライブラリ プロジェクトとそれに対応するテスト プロジェクトなどです。 プロジェクトのプロパティと、プロジェクトに含めることができるファイルのいくつかを紹介します。 また、あるプロジェクトから別のプロジェクトへの参照も作成します。

::: moniker range="vs-2017"

Visual Studio をまだインストールしていない場合は、[Visual Studio のダウンロード](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download) ページに移動し、無料試用版をインストールしてください。

::: moniker-end

::: moniker range="vs-2019"

Visual Studio をまだインストールしていない場合は、[Visual Studio のダウンロード](https://visualstudio.microsoft.com/downloads) ページに移動し、無料試用版をインストールしてください。

::: moniker-end

::: moniker range="vs-2022"

Visual Studio 2022 プレビューをまだインストールしていない場合は、[Visual Studio 2022 プレビューのダウンロード](https://visualstudio.microsoft.com/vs/preview/vs2022) ページに移動し、無料試用版をインストールしてください。

::: moniker-end

プロジェクトの概念を学習して理解するための演習として、ソリューションとプロジェクトをゼロから構築します。 Visual Studio の一般的な使い方として、新しいプロジェクトを作成するときに、Visual Studio で用意されているさまざまなプロジェクト "*テンプレート*" を使うことがよくあります。

> [!NOTE]
> Visual Studio でアプリを開発するにあたり、ソリューションとプロジェクトは必須ではありません。 また、コードが含まれているフォルダーを開いて、コードの作成、ビルド、およびデバッグを開始することもできます。 たとえば、[GitHub](https://github.com/) リポジトリをクローンしても、それには Visual Studio のプロジェクトとソリューションが含まれていない場合があります。 詳細については、「[プロジェクトまたはソリューションを使用せずに Visual Studio でコードを開発する](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md)」を参照してください。

## <a name="solutions-and-projects"></a>ソリューションとプロジェクト

ソリューションは、その名前にもかかわらず、"答え" ではありません。 ソリューションは、Visual Studio で 1 つまたは複数の関連プロジェクトを整理するために使用される単なるコンテナーです。 Visual Studio でソリューションを開くと、ソリューションに含まれているすべてのプロジェクトが自動的に読み込まれます。

### <a name="create-a-solution"></a>ソリューションを作成する

空のソリューションを作成するところから説明を始めます。 Visual Studio に慣れてきても、自分が空のソリューションを頻繁に作成していることにはほとんど気づかないでしょう。 Visual Studio で新しいプロジェクトを作成するとき、ソリューションがまだ開いていなければ、プロジェクトを格納するためのソリューションが自動的に作成されます。

::: moniker range="vs-2017"

1. Visual Studio を開きます。

1. 上部のメニュー バーで、 **[ファイル]** > **[新規作成]** > **[プロジェクト]** の順に選択します。

   **[新しいプロジェクト]** ダイアログ ボックスが表示されます。

1. 左側のウィンドウで、 **[その他のプロジェクトの種類]** を展開して、 **[Visual Studio ソリューション]** を選択します。 中央のウィンドウで、 **[空のソリューション]** テンプレートを選択します。 ソリューションに「**QuickSolution**」という名前を付けて、 **[OK]** ボタンを選択します。

   ![Visual Studio 2017 での空のソリューション テンプレート](media/tutorial-projects-new-solution.png "Visual Studio 2017 での空のソリューション テンプレート。")

   **[スタート ページ]** が閉じて、Visual Studio ウィンドウの右側にある **ソリューション エクスプローラー** にソリューションが表示されます。 多くの場合、**ソリューション エクスプローラー** を使用して、プロジェクトの内容を参照することになります。

::: moniker-end

::: moniker range=">=vs-2019"

1. Visual Studio を開きます。

2. [スタート ウィンドウ] で、 **[新しいプロジェクトの作成]** を選択します。

3. **[新しいプロジェクトの作成]** ページで、検索ボックスに「**空のソリューション**」と入力し、 **[空のソリューション]** テンプレートを選択して、 **[次へ]** を選択します。

   ![Visual Studio 2019 での空のソリューション テンプレート](media/vs-2019/tutorial-projects-blank-solution-template.png "Visual Studio 2019 での空のソリューション テンプレート。")

    > [!TIP]
    > 複数のワークロードがインストールされている場合、 **[空のソリューション]** テンプレートは、検索結果の一覧の先頭に表示されないことがあります。 一覧の **[検索に基づく他の結果]** セクションまでスクロールしてみてください。 そこに表示されているはずです。

4. ソリューションに 「**QuickSolution**」 という名前を付けて、 **[作成]** を選択します。

   Visual Studio ウィンドウの右側にある **ソリューション エクスプローラー** にソリューションが表示されます。 多くの場合、**ソリューション エクスプローラー** を使用して、プロジェクトの内容を参照することになります。

::: moniker-end

### <a name="add-a-project"></a>プロジェクトを追加する

次に、最初のプロジェクトをソリューションに追加してみましょう。 空のプロジェクトから始めて、そのプロジェクトに必要なアイテムを追加します。

::: moniker range="vs-2017"

1. **ソリューション エクスプローラー** で **ソリューション "QuickSolution"** の右クリックまたはコンテキスト メニューから、 **[追加]** > **[新しいプロジェクト]** の順に選択します。

   **[新しいプロジェクトの追加]** ダイアログ ボックスが表示されます。

1. 左側のウィンドウで、 **[Visual C#]** を展開し、 **[Windows デスクトップ]** を選択します。 次に、中央のウィンドウで、 **[空のプロジェクト (.NET Framework)]** テンプレートを選択します。 プロジェクトに「**QuickDate**」という名前を付けて、 **[OK]** を選択します。

   **ソリューション エクスプローラー** で、ソリューションの下に QuickDate という名前のプロジェクトが表示されます。 現在のところ、このプロジェクトには *App.config* と呼ばれるファイルが 1 つ含まれています。

   > [!NOTE]
   > ダイアログ ボックスの左側のウィンドウに **Visual C#** が表示されない場合は、 **.NET デスクトップ開発** Visual Studio ワークロードをインストールする必要があります。 Visual Studio は、ワークロード ベースのインストールを使って、行われる開発の種類に必要なコンポーネントだけをインストールします。 新しいワークロードをインストールする簡単な方法は、 **[新しいプロジェクトの追加]** ダイアログ ボックスの左下隅にある **[Visual Studio インストーラーを開く]** リンクをクリックすることです。 Visual Studio インストーラーが起動した後、 **[.NET デスクトップ開発]** ワークロードを選択して、 **[変更]** ボタンを選択します。
   >
   > ![Visual Studio インストーラー リンクを開く](media/tutorial-projects-open-installer.png "Visual Studio 2017 での [新しいプロジェクトの追加] ダイアログの [Visual Studio インストーラーを開く] リンク。")

::: moniker-end

::: moniker range=">=vs-2019"

1. **ソリューション エクスプローラー** で **ソリューション "QuickSolution"** の右クリックまたはコンテキスト メニューから、 **[追加]** > **[新しいプロジェクト]** の順に選択します。

   **[新しいプロジェクトの追加]** ダイアログ ボックスが開きます。

1. 上部の検索ボックスに「**空の**」というテキストを入力し、 **言語** で **C#** を選択します。

1. **[空のプロジェクト (.NET Framework)]** テンプレートを選択して、 **[次へ]** を選択します。

1. プロジェクトに「**QuickDate**」という名前を付けて、 **[作成]** を選択します。

   **ソリューション エクスプローラー** で、ソリューションの下に QuickDate という名前のプロジェクトが表示されます。 現在のところ、このプロジェクトには *App.config* と呼ばれるファイルが 1 つ含まれています。

   > [!NOTE]
   > **[空のプロジェクト (.NET Framework)]** テンプレートが表示されない場合は、 **.NET デスクトップ開発** Visual Studio ワークロードをインストールする必要があります。 Visual Studio は、ワークロード ベースのインストールを使って、行われる開発の種類に必要なコンポーネントだけをインストールします。
   >
   >新しいプロジェクトを作成するときに新しいワークロードをインストールする簡単な方法は、 **[探しているものが見つからない場合]** というテキストの下にある **[さらにツールと機能をインストールする]** リンクを選択することです。 Visual Studio インストーラーが起動した後、 **[.NET デスクトップ開発]** ワークロードを選択して、 **[変更]** ボタンを選択します。
   >
   > ![Visual Studio インストーラー リンクを開く](media/vs-2019/tutorial-projects-open-installer.png "Visual Studio での [新しいプロジェクトの作成] ダイアログの [Visual Studio インストーラーを開く] リンク。")

::: moniker-end

## <a name="add-an-item-to-the-project"></a>プロジェクトにアイテムを追加する

空のプロジェクトを用意しました。 コード ファイルを追加しましょう。

1. **ソリューション エクスプローラー** で **QuickDate** プロジェクトの右クリックまたはコンテキスト メニューから、 **[追加]**  >  **[新しい項目]** の順に選択します。

   **[新しい項目の追加]** ダイアログ ボックスが開きます。

1. **[Visual C# アイテム]** を展開して、 **[コード]** を選択します。 中央のウィンドウで、 **[クラス]** 項目テンプレートを選択します。 クラスに「**Calendar**」という名前を付けて、 **[追加]** ボタンを選択します。

   *Calendar.cs* という名前のファイルがプロジェクトに追加されます。 末尾の *.cs* は、C# コード ファイルに与えられるファイル拡張子です。 **ソリューション エクスプローラー** のビジュアル プロジェクト階層にファイルが表示され、その内容がエディターで開かれます。

1. *Calendar.cs* ファイルの内容を次のコードに置き換えます。

   ```csharp
   using System;

   namespace QuickDate
   {
       internal class Calendar
       {
           static void Main(string[] args)
           {
               DateTime now = GetCurrentDate();
               Console.WriteLine($"Today's date is {now}");
               Console.ReadLine();
           }

           internal static DateTime GetCurrentDate()
           {
               return DateTime.Now.Date;
           }
       }
   }
   ```

   このコードが何を行うかを理解する必要はありませんが、必要なら、**Ctrl**+**F5** キーを押してプログラムを実行し、コンソール (または標準出力) ウィンドウに今日の日付が出力されるのを確認することができます。

## <a name="add-a-second-project"></a>2 つ目のプロジェクトを追加する

ソリューションには複数のプロジェクトが含まれているのが一般的です。これらのプロジェクトは多くの場合、互いに参照しています。 ソリューション内に含めるプロジェクトはクラス ライブラリ、実行可能なアプリケーション、および単体テスト プロジェクトまたは Web サイトとすることができます。

単体テスト プロジェクトをソリューションに追加してみましょう。 今度はプロジェクト テンプレートから開始します。これにより、プロジェクトに追加のコード ファイルを追加する必要がなくなります。

1. **ソリューション エクスプローラー** で **ソリューション "QuickSolution"** の右クリックまたはコンテキスト メニューから、 **[追加]**  >  **[新しいプロジェクト]** の順に選択します。

::: moniker range="vs-2017"

2. 左側のウィンドウで、 **[Visual C#]** を展開し、 **[テスト]** カテゴリを選択します。 中央のウィンドウで、 **[MSTest テスト プロジェクト (.NET Core)]** プロジェクト テンプレートを選択します。 プロジェクトに「**QuickTest**」という名前を付けて、 **[OK]** を選択します。

   2 つ目のプロジェクトが **ソリューション エクスプローラー** に追加され、*UnitTest1.cs* という名前のファイルがエディターで開きます。

   ![2 つのプロジェクトを含む Visual Studio ソリューション エクスプローラー](media/tutorial-projects-solution-explorer.png "Visual Studio 2017 での 2 つのプロジェクトを含むソリューション エクスプローラー。")

::: moniker-end

::: moniker range=">=vs-2019"

2. **[新しいプロジェクトの追加]** ダイアログ ボックスで、上部にある検索ボックスに「**単体テスト**」というテキストを入力し、**[言語]** で **[C#]** を選択します。

3. .NET Core 用の **[単体テスト プロジェクト]** プロジェクト テンプレートを選択して、 **[次へ]** を選択します。

   > [!NOTE]
   > Visual Studio 2019 バージョン 16.9 以降では、MSTest プロジェクト テンプレートの名前が **MSTest 単体テスト プロジェクト (.NET Core)** から **[単体テスト プロジェクト]** に変更されました。 この更新では、プロジェクト作成のいくつかの手順が変更されました。

4. プロジェクトに「**QuickTest**」という名前を付けて、 **[次へ]** を選択します。

5. 推奨されるターゲット フレームワーク (.NET Core 3.1) または .NET 5 を選択し、 **[作成]** を選択します。

   2 つ目のプロジェクトが **ソリューション エクスプローラー** に追加され、*UnitTest1.cs* という名前のファイルがエディターで開きます。

   ![2 つのプロジェクトを含む Visual Studio ソリューション エクスプローラー](media/vs-2019/tutorial-projects-solution-explorer.png "Visual Studio での 2 つのプロジェクトを含むソリューション エクスプローラー。")

::: moniker-end

## <a name="add-a-project-reference"></a>プロジェクト参照を追加する

これから、新しい単体テスト プロジェクトを使用して **QuickDate** プロジェクト内のメソッドをテストします。それには、そのプロジェクトへの参照を追加する必要があります。 そうすることで、2 つのプロジェクトの間に "*ビルドの依存関係*" が作成されます。つまり、ソリューションをビルドすると、先に **QuickDate** がビルドされてから、**QuickTest** がビルドされます。

::: moniker range="vs-2017"

1. **QuickTest** プロジェクトで **[依存関係]** ノードを選択し、右クリックまたはコンテキスト メニューから、 **[参照の追加]** を選択します。

   **[参照マネージャー]** ダイアログ ボックスが表示されます。

1. 左側のウィンドウで、 **[プロジェクト]** を展開し、 **[ソリューション]** を選択します。 中央のウィンドウで、**QuickDate** の横にあるチェック ボックスをオンにして、 **[OK]** を選択します。

   **QuickDate** プロジェクトへの参照が追加されます。

   ![Visual Studio でのプロジェクト参照が示されているソリューション エクスプローラー](media/vs-2019/tutorial-projects-solution-explorer-reference.png "Visual Studio でのプロジェクト参照が示されているソリューション エクスプローラーのスクリーンショット。")

::: moniker-end

::: moniker range=">=vs-2019"

1. **QuickTest** プロジェクトで **[依存関係]** ノードを選択し、右クリックまたはコンテキスト メニューから、 **[プロジェクト参照の追加]** を選択します。

   **[参照マネージャー]** ダイアログ ボックスが表示されます。

1. 左側のウィンドウで、 **[プロジェクト]** を展開して、 **[ソリューション]** を選択します。 中央のウィンドウで、**QuickDate** の横にあるチェック ボックスをオンにして、 **[OK]** を選択します。

   **QuickDate** プロジェクトへの参照が追加されます。

   ![Visual Studio 2019 でのプロジェクト参照が示されているソリューション エクスプローラーのスクリーンショット](media/vs-2019/tutorial-projects-solution-explorer-reference.png)

::: moniker-end

## <a name="add-test-code"></a>テスト コードを追加する

1. ここで、C# テスト コード ファイルにテスト コードを追加します。 *UnitTest1.cs* の内容を次のコードに置き換えます。

   ```csharp
   using System;
   using Microsoft.VisualStudio.TestTools.UnitTesting;

   namespace QuickTest
   {
       [TestClass]
       public class UnitTest1
       {
           [TestMethod]
           public void TestGetCurrentDate()
           {
               Assert.AreEqual(DateTime.Now.Date, QuickDate.Calendar.GetCurrentDate());
           }
       }
   }
   ```

   コードの一部分の下に赤色の波線が表示されます。 テスト プロジェクトを、**QuickDate** プロジェクトに対する [フレンド アセンブリ](/dotnet/standard/assembly/friend-assemblies)にすることで、このエラーを修正します。

1. **QuickDate** プロジェクトに戻り、*Calendar.cs* ファイルをまだ開いていない場合は開きます。 テスト プロジェクトでのエラーを解決するには、次の [using ステートメント](/dotnet/csharp/language-reference/keywords/using-statement)と <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> 属性をファイルの先頭に追加します。

   ```csharp
   using System.Runtime.CompilerServices;

   [assembly: InternalsVisibleTo("QuickTest")]
   ```

   コード ファイルは、次のようになります。

   ![CSharp コード](media/tutorial-projects-cs-code.png "この記事の「テスト コードを追加する」セクションのコード スニペット。")

## <a name="project-properties"></a>プロジェクトのプロパティ

<xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> 属性を含む *Calendar.cs* ファイル内の行は、**QuickTest** プロジェクトのアセンブリ名 (ファイル名) を参照します。 アセンブリ名はプロジェクト名と常に同じであるとは限りません。 プロジェクトのアセンブリ名を検索するには、プロジェクトのプロパティを開きます。

1. **ソリューション エクスプローラー** で **QuickTest** プロジェクトを選択します。 右クリックまたはコンテキスト メニューから、**[プロパティ]** を選択するか、または **Alt**+**Enter** キーを押します。

   **[アプリケーション]** タブで、プロジェクトの "*プロパティ ページ*" が開きます。プロパティ ページには、プロジェクトのさまざまな設定が含まれます。 **QuickTest** プロジェクトのアセンブリ名が "QuickTest" であることに注目してください。 これを変更する場合は、ここでその変更を行います。 テスト プロジェクトをビルドすると、結果として得られるバイナリ ファイルの名前は *QuickTest.dll* から、選択した任意の名前に変わります。

   ![プロジェクトのプロパティ](media/tutorial-projects-netcore-properties.png "Visual Studio での [プロジェクトのプロパティ] ダイアログ。")

1. **[ビルド]** や **[デバッグ]** など、プロジェクトのプロパティ ページの他のいくつかのタブを見てみます。 これらのタブは、プロジェクトの種類によって異なります。

## <a name="next-steps"></a>次のステップ

::: moniker range="vs-2017"

単体テストが動作していることを確認する場合は、メニュー バーから **[テスト]**  >  **[実行]**  >  **[すべてのテスト]** を選択します。 **テスト エクスプローラー** と呼ばれるウィンドウが開くので、**TestGetCurrentDate** テストが成功しているか確認する必要があります。

::: moniker-end

::: moniker range=">=vs-2019"

単体テストが動作していることを確認する場合は、メニュー バーから **[テスト]**  >  **[すべてのテストを実行する]** の順に選択します。 **テスト エクスプローラー** と呼ばれるウィンドウが開くので、**TestGetCurrentDate** テストが成功しているか確認する必要があります。

::: moniker-end

![テストに合格したことを示す Visual Studio のテスト エクスプローラー](media/tutorial-projects-test-explorer.png "テストに合格したことを示す Visual Studio のテスト エクスプローラー。")

::: moniker range="vs-2017"

> [!TIP]
> **テスト エクスプローラー** が自動的に開かない場合は、メニュー バーから **[テスト]** > **[Windows]** > **[テスト エクスプローラー]** を選択して開きます。

::: moniker-end

::: moniker range=">=vs-2019"

> [!TIP]
> **テスト エクスプローラー** が自動的に開かない場合は、メニュー バーから **[テスト]**  >  **[テスト エクスプローラー]** を選択して開きます。

::: moniker-end

## <a name="see-also"></a>関連項目

- [プロジェクトとソリューションを使用する](../ide/creating-solutions-and-projects.md)
- [プロジェクトおよびソリューションのプロパティの管理](../ide/managing-project-and-solution-properties.md)
- [プロジェクト内の参照の管理](../ide/managing-references-in-a-project.md)
- [プロジェクトまたはソリューションを使用せずに Visual Studio でコードを開発する](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md)
- [Visual Studio IDE の概要](../get-started/visual-studio-ide.md)
