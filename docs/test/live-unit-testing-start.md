---
title: ライブ単体テストを使用してコードをテストする方法
description: .NET Standard を対象とする簡単なクラス ライブラリを作成し、.NET Core を対象とする MSTest プロジェクトを作成してテストすることで、Live Unit Testing の使用を学習します。
ms.custom: SEO-VS-2020
ms.date: 04/03/2020
ms.topic: how-to
helpviewer_keywords:
- Live Unit Testing
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- dotnet
ms.openlocfilehash: 5c965fd73f63906f7a1e055ae5ff051eebab19d5
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107828814"
---
# <a name="get-started-with-live-unit-testing"></a>Live Unit Testing の概要

Visual Studio ソリューションで Live Unit Testing を有効にすると、テスト カバレッジとテストの状態が視覚的に示されます。 また、Live Unit Testing では、コードが変更されるたびにテストが動的に実行され、変更が原因でテストが不合格になった場合にはただちに通知されます。

Live Unit Testing を使用すると、.NET Framework または .NET Core のいずれかを対象とするソリューションをテストすることができます。 このチュートリアルでは、.NET Standard を対象とする簡単なクラス ライブラリを作成することによって Live Unit Testing の使用方法を学習し、それをテストするために .NET Core を対象とする MSTest プロジェクトを作成します。

完全な C# ソリューションは、GitHub 上の [MicrosoftDocs/visualstudio-docs](https://github.com/MicrosoftDocs/visualstudio-docs/tree/master/docs/test/samples/csharp/UtilityLibraries/) リポジトリからダウンロードできます。

## <a name="prerequisites"></a>必須コンポーネント

このチュートリアルでは、Visual Studio Enterprise エディションと **.NET Core クロスプラットフォームの開発** ワークロードがインストールされている必要があります。

## <a name="create-the-solution-and-the-class-library-project"></a>ソリューションとクラス ライブラリ プロジェクトを作成する

最初に、単一の .NET Standard クラス ライブラリ プロジェクト StringLibrary で構成される UtilityLibraries という名前の Visual Studio ソリューションを作成します。

このソリューションは、1 つまたは複数のプロジェクト用のコンテナーにすぎません。 空のソリューションを作成するには、Visual Studio を開き、次の手順を行います。

1. Visual Studio の最上位のメニューから、 **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** の順に選択します。

1. テンプレートの検索ボックスに「**ソリューション**」と入力して、 **[空のソリューション]** テンプレートを選択します。 プロジェクトに **UtilityLibraries** という名前を指定します。

   ::: moniker range="vs-2017"

   ![[新しいプロジェクト] ダイアログ](./media/lut-start/new-solution.png)

   ::: moniker-end

1. ソリューションの作成を終了します。

ソリューションを作成したので、次に、文字列を操作するための複数の拡張メソッドが含まれる StringLibrary という名前のクラス ライブラリを作成します。

1. **ソリューション エクスプローラー** で、UtilityLibraries ソリューションを右クリックし、 **[追加]**  >  **[新しいプロジェクト]** の順に選択します。

::: moniker range="vs-2017"

2. **[新しいプロジェクトの追加]** ダイアログで、C# ノードを選択し、 **[.NET Standard]** を選択します。

   > [!NOTE]
   > 使用するライブラリは特定の .NET 実装ではなく .NET Standard を対象としているので、そのバージョンの .NET Standard をサポートする任意の .NET 実装から呼び出すことができます。 詳細については、「[.NET Standard](/dotnet/standard/net-standard)」をご覧ください。

3. 次の図に示すように、右側のウィンドウで **[クラス ライブラリ (.NET Standard)]** テンプレートを選択し、 **[名前]** テキスト ボックスに「**StringLibrary**」と入力します。

   ![[新しいプロジェクトの追加] ダイアログ](./media/lut-start/add-project-cs.png)

4. **[OK]** をクリックして、プロジェクトを作成します。

::: moniker-end

::: moniker range=">=vs-2019"

2. テンプレートの検索ボックスに「**クラス ライブラリ**」と入力して、 **[クラス ライブラリ (.NET Standard)]** テンプレートを選択します。 **[次へ]** をクリックします。

   > [!NOTE]
   > 使用するライブラリは特定の .NET 実装ではなく .NET Standard を対象としているので、そのバージョンの .NET Standard をサポートする任意の .NET 実装から呼び出すことができます。 詳細については、「[.NET Standard](/dotnet/standard/net-standard)」をご覧ください。

3. プロジェクトに **StringLibrary** という名前を付けます。

4. **[作成]** をクリックして、プロジェクトを作成します。

::: moniker-end

5. コード エディター内の既存のコードをすべて、次のコードに置き換えます。

   ```csharp
   using System;

   namespace UtilityLibraries
   {
       public static class StringLibrary
       {
           public static bool StartsWithUpper(this string s)
           {
               if (String.IsNullOrWhiteSpace(s))
                   return false;

               return Char.IsUpper(s[0]);
           }

           public static bool StartsWithLower(this string s)
           {
               if (String.IsNullOrWhiteSpace(s))
                   return false;

               return Char.IsLower(s[0]);
           }

           public static bool HasEmbeddedSpaces(this string s)
           {
               foreach (var ch in s.Trim())
               {
                   if (ch == ' ')
                       return true;
               }
               return false;
           }
       }
   }
   ```

   StringLibrary には 3 つの静的メソッドがあります。

   - `StartsWithUpper` は、文字列が大文字で始まる場合は `true` を返し、それ以外の場合には `false` を返します。

   - `StartsWithLower` は、文字列が小文字で始まる場合は `true` を返し、それ以外の場合には `false` を返します。

   - `HasEmbeddedSpaces` は、埋め込み空白文字が文字列に含まれている場合は `true` を返し、それ以外の場合には `false` を返します。

6. Visual Studio の最上位メニューから、 **[ビルド]**  >  **[ソリューションのビルド]** の順に選択します。 ビルドは成功するはずです。

## <a name="create-the-test-project"></a>テスト プロジェクトの作成

次のステップとして、StringLibrary ライブラリをテストする単体テスト プロジェクトを作成します。 次の手順を実行して、単体テストを作成します。

1. **ソリューション エクスプローラー** で、UtilityLibraries ソリューションを右クリックし、 **[追加]**  >  **[新しいプロジェクト]** の順に選択します。

::: moniker range="vs-2017"

2. **[新しいプロジェクトの追加]** ダイアログで、C# ノードを選択し、次に **[.NET Core]** を選択します。

   > [!NOTE]
   > 単体テストを記述する言語は、クラス ライブラリと同じ言語でなくてもかまいません。

3. 次の図に示すように、右側のウィンドウで **[単体テスト プロジェクト (.NET Core)]** テンプレートを選択し、 **[名前]** テキスト ボックスに「**StringLibraryTests**」と入力します。

   ![単体テスト プロジェクトの場合の [新しいプロジェクトの追加] ダイアログ](./media/lut-start/add-unit-test-cs.png)

4. **[OK]** をクリックして、プロジェクトを作成します。

   > [!NOTE]
   > このはじめに (チュートリアル) では、Live Unit Testing を MSTest テスト フレームワークと一緒に使用します。 また、xUnit および NUnit のテスト フレームワークを使用することもできます。

::: moniker-end

::: moniker range=">=vs-2019"

2. テンプレート検索ボックスに「**単体テスト**」と入力し、言語として **C#** を選択してから、.Net Core テンプレートの **[単体テスト プロジェクト]** を選択します。 **[次へ]** をクリックします。

   > [!NOTE]
   > Visual Studio 2019 バージョン 16.9 以降では、MSTest プロジェクト テンプレートの名前が **MSTest 単体テスト プロジェクト (.NET Core)** から **[単体テスト プロジェクト]** に変更されました。

3. プロジェクトに「**StringLibraryTests**」という名前を指定し、 **[次へ]** をクリックします。

4. 推奨されるターゲット フレームワーク (.NET Core 3.1) または .NET 5 を選択し、 **[作成]** を選択します。

   > [!NOTE]
   > このはじめに (チュートリアル) では、Live Unit Testing を MSTest テスト フレームワークと一緒に使用します。 また、xUnit および NUnit のテスト フレームワークを使用することもできます。

::: moniker-end

5. 単体テスト プロジェクトは、テスト対象のクラス ライブラリに自動的にアクセスすることはできません。 テスト ライブラリへのアクセス権を付与するには、クラス ライブラリ プロジェクトへの参照を追加します。 これを行うには、`StringLibraryTests` プロジェクトを右クリックし、 **[追加]**  >  **[参照]** の順にクリックします。 次の図に示すように、 **[参照マネージャー]** ダイアログで、 **[ソリューション]** タブが選択されていることを確認し、StringLibrary プロジェクトを選択します。

   ![[参照マネージャー] ダイアログ](./media/lut-start/add-reference.png)

6. テンプレートで入力されている定型的な単体テスト コードを次のコードに置き換えます。

   ```csharp
   using System;
   using Microsoft.VisualStudio.TestTools.UnitTesting;
   using UtilityLibraries;

   namespace StringLibraryTest
   {
       [TestClass]
       public class UnitTest1
       {
           [TestMethod]
           public void TestStartsWithUpper()
           {
               // Tests that we expect to return true.
               string[] words = { "Alphabet", "Zebra", "ABC", "Αθήνα", "Москва" };
               foreach (var word in words)
               {
                   bool result = word.StartsWithUpper();
                   Assert.IsTrue(result,
                                 $"Expected for '{word}': true; Actual: {result}");
               }
           }

           [TestMethod]
           public void TestDoesNotStartWithUpper()
           {
               // Tests that we expect to return false.
               string[] words = { "alphabet", "zebra", "abc", "αυτοκινητοβιομηχανία", "государство",
                                  "1234", ".", ";", " " };
               foreach (var word in words)
               {
                   bool result = word.StartsWithUpper();
                   Assert.IsFalse(result,
                                  $"Expected for '{word}': false; Actual: {result}");
               }
           }

           [TestMethod]
           public void DirectCallWithNullOrEmpty()
           {
               // Tests that we expect to return false.
               string[] words = { String.Empty, null };
               foreach (var word in words)
               {
                   bool result = StringLibrary.StartsWithUpper(word);
                   Assert.IsFalse(result,
                                  $"Expected for '{(word == null ? "<null>" : word)}': " +
                                  $"false; Actual: {result}");
               }
           }
       }
   }
   ```

7. ツール バーの **[保存]** アイコンを選択してプロジェクトを保存します。

   単体テスト コードには ASCII 以外の文字がいくつか含まれているため、既定の ASCII 形式でファイルを保存すると失われる文字が存在することを警告する次のようなダイアログが表示されます。

8. **[その他のエンコードで保存]** ボタンを選択します。

   ![ファイルのエンコードを選択](media/lut-start/ascii-encoding.png)

9. 次の図に示すように、 **[保存オプションの詳細設定]** ダイアログの **[エンコード]** ドロップダウン リストから **[Unicode (UTF-8 シグネチャ付き) - コードページ 65001]** を選択します。

   ![UTF-8 エンコードを選択](media/lut-start/utf8-encoding.png)

10. Visual Studio の最上位メニューから、 **[ビルド]**  >  **[ソリューションのリビルド]** の順に選択して、単体テスト プロジェクトをコンパイルします。

クラス ライブラリと、これに対する複数の単体テストが作成されました。 これで、Live Unit Testing を使用するために必要な準備作業が完了しました。

## <a name="enable-live-unit-testing"></a>Live Unit Testing の有効化

StringLibrary クラス ライブラリ用のテストを作成しましたが、まだ実行していません。 Live Unit Testing を有効にすると、テストが自動的に実行されます。 Live Unit Testing を有効にするには、次の手順を実行します。

1. 必要に応じて、StringLibrary のコードが含まれているコード エディター ウィンドウを選択します。 C# プロジェクトの *Class1.cs* か、Visual Basic プロジェクトの *Class1.vb* のどちらかです。 (このステップでは、Live Unit Testing を有効にした後で、テストの結果とコード カバレッジの範囲を視覚的に検査します。)

1. Visual Studio の最上位メニューから **[テスト]**  >  **[Live Unit Testing]**  >  **[開始]** の順に選びます。

1. Visual Studio が Live Unit Test を開始します。これによりすべてのテストが自動的に実行されます。

::: moniker range="vs-2017"
テストの実行が終了すると、**テスト エクスプローラー** に全体の結果と個々のテストの結果とが両方とも表示されます。 さらに、コード エディター ウィンドウには、テスト コードのカバレッジとテストの結果とが両方ともグラフィカルに表示されます。 次の図に示すように、3 つのテストはいずれも正常に実行されています。 また、テストは `StartsWithUpper` メソッド内のすべてのコード パスをカバーしており、それらのテストはすべて正常に実行されていることがわかります (緑色のチェック マーク "✓" によって示されている)。 最後に、StringLibrary 内の他のメソッドにはコード カバレッジが設定されていないことがわかります (青い線 "➖" によって示されている)。

![Live Unit Testing の開始後のテスト エクスプローラーとコード エディター ウィンドウ](media/lut-start/lut-results-cs.png)
::: moniker-end
::: moniker range=">=vs-2019"
テストの実行が終了すると、 **[Live Unit Testing]** に全体の結果と個々のテストの結果の両方が表示されます。 さらに、コード エディター ウィンドウには、テスト コードのカバレッジとテストの結果とが両方ともグラフィカルに表示されます。 次の図に示すように、3 つのテストはいずれも正常に実行されています。 また、テストは `StartsWithUpper` メソッド内のすべてのコード パスをカバーしており、それらのテストはすべて正常に実行されていることがわかります (緑色のチェック マーク "✓" によって示されている)。 最後に、StringLibrary 内の他のメソッドにはコード カバレッジが設定されていないことがわかります (青い線 "➖" によって示されている)。

![Live Unit Testing の開始後の Live Test Explorer とコード エディター ウィンドウ](media/lut-start/vs-2019/lut-results-cs.png)
::: moniker-end

また、コード エディター ウィンドウ内の特定のコード カバレッジ アイコンを選択することにより、テスト カバレッジとテスト結果に関する詳細情報を取得することもできます。 この詳細を調べるには、次の手順を実行します。

1. `StartsWithUpper` メソッド内の `if (String.IsNullOrWhiteSpace(s))` という行に表示された緑のチェック マークをクリックします。 次の図に示すように、Live Unit Testing では、そのコード行が 3 つのテストでカバーされており、いずれのテストも正常に実行されたことが示されています。

   !["If" 条件付きステートメントのコード カバレッジ](media/lut-start/code-coverage-cs1.png)

1. `StartsWithUpper` メソッド内の `return Char.IsUpper(s[0])` という行に表示された緑のチェック マークをクリックします。 次の図に示すように、Live Unit Testing では、そのコード行が 2 つのテストのみでカバーされており、いずれのテストも正常に実行されたことが示されています。

   ![Return ステートメントのコード カバレッジ](media/lut-start/code-coverage-cs2.png)

Live Unit Testing は、重大な問題として不完全なコード カバレッジを明らかにしています。 この問題は、次のセクションで取り上げます。

## <a name="expand-test-coverage"></a>テスト カバレッジの展開

このセクションでは、単体テストを `StartsWithLower` メソッドに展開します。 展開を行っている間も、Live Unit Testing によって引き続きコードのテストが実行されます。

コード カバレッジを `StartsWithLower` メソッドに展開するには、次の手順を実行します。

1. 次の `TestStartsWithLower` メソッドと `TestDoesNotStartWithLower` メソッドをプロジェクトのテスト ソース コード ファイルに追加します。

   :::code language="csharp" source="../test/samples/snippets/csharp/lut-start/unittest2.cs" id="Snippet1":::

1. [`Microsoft.VisualStudio.TestTools.UnitTesting.Assert.IsFalse`](/dotnet/api/microsoft.visualstudio.testtools.unittesting.assert.isfalse) メソッドへの呼び出しのすぐ後に、次のコードを追加して、`DirectCallWithNullOrEmpty` メソッドを変更します。

   :::code language="csharp" source="../test/samples/snippets/csharp/lut-start/unittest2.cs" id="Snippet2":::

1. ソース コードを変更すると、Live Unit Testing によって新しいテストと変更したテストが自動的に実行されます。 次の図に示すように、追加した 2 つのテストと変更した 1 つのテストを含むすべてのテストが成功しています。

   ::: moniker range="vs-2017"
   ![テスト カバレッジを展開した後のテスト エクスプローラー](media/lut-start/test-dynamic.png)
   ::: moniker-end
   ::: moniker range=">=vs-2019"
   ![テスト カバレッジを展開した後の Live Test Explorer](media/lut-start/vs-2019/test-dynamic.png)
   ::: moniker-end

1. StringLibrary クラスのソース コードが含まれるウィンドウに切り替えます。 Live Unit Testing は、コード カバレッジが `StartsWithLower` メソッドに展開されていることを示します。

    ![StartsWithLower メソッドのコード カバレッジ](media/lut-start/lut-extended-cs.png)

場合によっては、成功したテストが **テスト エクスプローラー** で、灰色表示されることがあります。これは、テストが現在実行中であることを示すか、または最後に実行されてから、テストに影響する変更がコードに加えられていないために、テストが再度実行されなかったことを示します。

これまで、すべてのテストが成功しています。 次のセクションでは、テスト エラーを処理する方法について説明します。

## <a name="handle-a-test-failure"></a>テスト エラーの処理

このセクションでは、Live Unit Testing を使用してテスト エラーを識別し、トラブルシューティングを行い、対処する方法を説明します。 そのために、テスト カバレッジを `HasEmbeddedSpaces` メソッドに展開します。

1. テスト ファイルに次のメソッドを追加します。

   :::code language="csharp" source="../test/samples/snippets/csharp/lut-start/unittest2.cs" id="Snippet3":::

1. 次の図に示すように、テストが実行されると、Live Unit Testing では `TestHasEmbeddedSpaces` メソッドが失敗したことが示されます。

   ::: moniker range="vs-2017"
   ![失敗したテストを示すテスト エクスプローラー](media/lut-start/test-failure.png)
   ::: moniker-end
   ::: moniker range=">=vs-2019"
   ![失敗したテストを示す Live Test Explorer](media/lut-start/vs-2019/test-failure.png)
   ::: moniker-end

1. ライブラリ コードが表示されたウィンドウを選択します。 Live Unit Testing によって `HasEmbeddedSpaces` メソッドまでコード カバレッジが広げられています。 また、Live Unit Testing は、失敗したテストでカバーされている行に赤い "🞩" を追加することで、テスト エラーを報告しています。

1. `HasEmbeddedSpaces`メソッド シグネチャが含まれている行にマウス ポインターを合わせます。 次の図に示すように、Live Unit Testing では、メソッドが 1 つのテストでカバーされていることを知らせるヒントが表示されます。

   ![失敗したテストに関する Live Unit Testing の情報](media/lut-start/test-failure-info-cs.png)

1. 失敗した **TestHasEmbeddedSpaces** テストを選択します。 次の図に示すように、Live Unit Testing には、すべてのテストの実行やすべてのテストのデバッグなど、いくつかのオプションが用意されています。

   ::: moniker range="vs-2017"
   ![テストが失敗した場合のための Live Unit Testing のオプション](media/lut-start/test-failure-options.png)
   ::: moniker-end
   ::: moniker range=">=vs-2019"
   ![テストが失敗した場合のための Live Unit Testing のオプション](media/lut-start/vs-2019/test-failure-options.png)
   ::: moniker-end

1. **[すべてデバッグ]** を選択して、失敗したテストをデバッグします。

1. Visual Studio はデバッグ モードでテストを実行します。

   テストでは、配列内の各文字列が `phrase` という名前の変数に割り当てられ、その変数が `HasEmbeddedSpaces` メソッドに渡されます。 アサーション式が初めて `false` になると、プログラムの実行は一時停止し、デバッガーが呼び出されます。 [`Microsoft.VisualStudio.TestTools.UnitTesting.Assert.IsTrue`](/dotnet/api/microsoft.visualstudio.testtools.unittesting.assert.istrue) のメソッド呼び出しに予期しない値が含まれていると、以下の図に示すような例外ダイアログが表示されます。

   ![Live Unit Testing の例外ダイアログ](media/lut-start/exception-dialog-cs.png)

   さらに、次の図に示すように、Visual Studio で用意されているすべてのデバッグ ツールを使用することで、失敗したテストのトラブルシューティングを効果的に行うことができます。

   ![Visual Studio のデバッグ ツール](media/lut-start/debugging-tools-cs.png)

   **[自動変数]** ウィンドウで、`phrase` 変数の値が "Name\tDescription" (配列の 2 番目の要素) になっていることに注目してください。 テスト メソッドは、この文字列が `HasEmbeddedSpaces` に渡された場合に `true` が返されるのを期待していますが、実際に返されるのは `false` です。 タブ文字である "\t" が埋め込みスペースとして認識されていないのは明らかです。

1. テスト プログラムの実行を続行するには、 **[デバッグ]**  >  **[続行]** の順に選択するか、**F5** キーを押すか、あるいはツールバーの **[続行]** ボタンをクリックします。 ハンドルされない例外が発生したため、テストは終了します。
これは、バグの予備調査を行う上で十分な情報です。 `TestHasEmbeddedSpaces` (テスト ルーチン) で不適切な想定が行われたか、または `HasEmbeddedSpaces` がすべての埋め込みスペースを正しく認識していません。

1. 問題を診断し解決するには、`StringLibrary.HasEmbeddedSpaces` メソッドから始めます。 `HasEmbeddedSpaces` メソッドでの比較を確認します。 このメソッドでは、埋め込みスペースを U+0020 と見なしています。 ただし、Unicode Standard には、その他にも多くの空白文字が含まれています。 このことは、空白文字かどうかのテストが、ライブラリ コードで正しく行われていないことを示しています。

1. 等価比較を、<xref:System.Char.IsWhiteSpace%2A?displayProperty=fullName> メソッドへの呼び出しに置き換えます。

   :::code language="csharp" source="../test/samples/snippets/csharp/lut-start/program2.cs" id="Snippet1":::

1. 失敗したテスト メソッドは、Live Unit Testing によって自動的に再実行されます。

   更新された結果は、Live Unit Testing とコード エディター ウィンドウに表示されます。

## <a name="see-also"></a>関連項目

- [Visual Studio の Live Unit Testing](live-unit-testing.md)
- [Live Unit Testing についてよく寄せられる質問](live-unit-testing-faq.md)
