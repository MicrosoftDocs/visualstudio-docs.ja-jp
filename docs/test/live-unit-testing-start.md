---
title: Visual Studio 2017 で Live Unit Testing を使用してコードをテストする方法 | Microsoft Docs
ms.date: 08/31/2017
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio ALM
- Live Unit Testing
author: rpetrusha
ms.author: ronpet
ms.workload:
- dotnet
ms.openlocfilehash: 83cc24d72bfb679a1b683a67b995356fc887064c
ms.sourcegitcommit: d9e4ea95d0ea70827de281754067309a517205a1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/29/2018
ms.locfileid: "37117798"
---
# <a name="get-started-with-live-unit-testing-in-visual-studio"></a>Visual Studio 2017 で Live Unit Testing の使用を開始する

Visual Studio ソリューションで Live Unit Testing を有効にすると、テスト カバレッジとテストの状態が視覚的に示されます。 またコードを変更するたびに、テストが動的に実行されます。 変更によってコードが破損すると即時にその旨が通知され、追加のテストを必要とする領域が示されます。

Live Unit Testing を使用すると、.NET Framework または .NET Core のいずれかを対象とするソリューションをテストすることができます。 このチュートリアルでは、Live Unit Testing の使用方法を学習するために .NET Standard を対象とする単純なクラス ライブラリを作成します。さらに、それをテストするために、.NET Core を対象とする MSTest プロジェクトを作成します。

# <a name="ctabcsharp"></a>[C#](#tab/csharp)
完全な C# ソリューションは、GitHub 上の [MicrosoftDocs/visualstudio-docs](https://github.com/MicrosoftDocs/visualstudio-docs/tree/master/docs/test/samples/csharp/UtilityLibraries/) リポジトリからダウンロードできます。
# <a name="visual-basictabvisual-basic"></a>[Visual Basic](#tab/visual-basic)
完全な Visual Basic ソリューションは、GitHub 上の [MicrosoftDocs/visualstudio-docs](https://github.com/MicrosoftDocs/visualstudio-docs/tree/master/docs/test/samples/visual-basic/UtilityLibraries/) リポジトリからダウンロードできます。

---

## <a name="prerequisites"></a>必須コンポーネント

このチュートリアルでは、.NET Core 2.0 ワークロードを使用する Visual Studio 2017 Enterprise Edition バージョン 15.3 がインストールされている必要があります。

## <a name="create-the-solution-and-the-class-library-project"></a>ソリューションとクラス ライブラリ プロジェクトを作成する

単一の .NET Standard クラス ライブラリ プロジェクト `StringLibrary` から成る `UtilityLibraries` という名前の Visual Studio ソリューションを作成することから始めます。 `StringLibrary` は、C# または Visual Basic のどちらでも記述することができます。

このソリューションは、1 つまたは複数のプロジェクト用のコンテナーにすぎません。 ソリューションを作成するには、Visual Studio 2017 を開き、次の手順を実行します。

1. Visual Studio の最上位のメニューから、**[ファイル]** > **[新規作成]** > **[プロジェクト]** の順に選択します。

1. **[新しいプロジェクト]** ダイアログの **[その他のプロジェクトの種類]** ノードを展開し、**[Visual Studio ソリューション]** を選択します。 次の図に示すように、右側のウィンドウで **[空のソリューション]** テンプレートを選択し、**[名前]** テキスト ボックスに「`UtilityLibraries`」と入力します。

   ![[新しいプロジェクト] ダイアログ](./media/lut-start/new-solution.png)

1. **[OK]** を選択して、ソリューションを作成します。

ソリューションが作成されたので、次に、文字列を操作するための拡張メソッドを複数格納する `StringLibrary` という名前のクラス ライブラリを作成します。

# <a name="ctabcsharp"></a>[C#](#tab/csharp)
1. **ソリューション エクスプローラー**で、`UtilityLibraries` ソリューションを右クリックし、**[追加]** > **[新しいプロジェクト]** の順に選択します。

1. **[新しいプロジェクトの追加]** ダイアログで、C# ノードを選択し、**[.NET Standard]** を選択します。

   > [!NOTE]
   > 使用するライブラリは特定の .NET 実装ではなく .NET Standard を対象としているので、.NET Standard の所定のバージョンをサポートする任意の .NET 実装から呼び出すことができます。 詳細については、「[.NET Standard](/dotnet/standard/net-standard)」をご覧ください。

1. 次の図に示すように、右側のウィンドウで **[クラス ライブラリ (.NET Standard)]** テンプレートを選択し、**[名前]** テキスト ボックスに「`StringLibrary`」と入力します。

   ![[新しいプロジェクトの追加] ダイアログ](./media/lut-start/add-project-cs.png)

1. **[OK]** をクリックして、プロジェクトを作成します。

1. コード ウィンドウ内の既存のコードをすべて、次のコードに置き換えます。

   [!code-csharp[StringLibrary source code](samples/csharp/utilitylibraries/stringlibrary/class1.cs)]

   `StringLibrary` には 3 つの静的メソッドが格納されています。

      - `StartsWithUpper` は、文字列が大文字で始まる場合は `true` を返し、それ以外の場合には `false` を返します。

      - `StartsWithLower` は、文字列が小文字で始まる場合は `true` を返し、それ以外の場合には `false` を返します。

      - `HasEmbeddedSpaces` は、埋め込み空白文字が文字列に含まれている場合は `true` を返し、それ以外の場合には `false` を返します。

1.  Visual Studio の最上位メニューから、**[ビルド]**、**[ソリューションのビルド]** の順に選択します。 Visual Studio によって目的のライブラリが正常にビルドされるはずです。

# <a name="visual-basictabvisual-basic"></a>[Visual Basic](#tab/visual-basic)
1. **ソリューション エクスプローラー**で、`UtilityLibraries` ソリューションを右クリックし、**[追加]** > **[新しいプロジェクト]** の順に選択します。

1. **[新しいプロジェクトの追加]** ダイアログで、Visual Basic ノードを選択し、次に **[.NET Standard]** を選択します。

   > [!NOTE]
   > 使用するライブラリは特定の .NET 実装ではなく .NET Standard を対象としているので、.NET Standard の所定のバージョンをサポートする任意の .NET 実装から呼び出すことができます。 詳細については、「[.NET Standard](/dotnet/standard/net-standard)」をご覧ください。

1. 次の図に示すように、右側のウィンドウで **[クラス ライブラリ (.NET Standard)]** テンプレートを選択し、**[名前]** テキスト ボックスに「`StringLibrary`」と入力します。

   ![[新しいプロジェクトの追加] ダイアログ](./media/lut-start/add-project-vb.png)

1. **[OK]** をクリックして、プロジェクトを作成します。

1. コード ウィンドウ内の既存のコードをすべて、次のコードに置き換えます。

   [!code-vb[StringLibrary source code](samples/visual-basic/utilitylibraries/stringlibrary/class1.vb)]

   `StringLibrary` には 3 つの静的メソッドが格納されています。

      - `StartsWithUpper` は、文字列が大文字で始まる場合は `true` を返し、それ以外の場合には `false` を返します。

      - `StartsWithLower` は、文字列が小文字で始まる場合は `true` を返し、それ以外の場合には `false` を返します。

      - `HasEmbeddedSpaces` は、埋め込み空白文字が文字列に含まれている場合は `true` を返し、それ以外の場合には `false` を返します。

1. **ソリューション エクスプローラー**で、StringLibrary プロジェクトを右クリックし、**[プロパティ]** を選択します。 次の図に示すように、**[アプリケーション]** タブで、**[ルート名前空間]** テキスト ボックス内のテキストを削除します。 ルート名前空間は、ソース コード内の [Namespace ステートメント](/dotnet/visual-basic/language-reference/statements/namespace-statement)によって定義されます。

   ![Visual Basic プロジェクトの [プロジェクト プロパティ] ダイアログ](./media/lut-start/vb-properties.png)

1.  Visual Studio の最上位メニューから、**[ビルド]**、**[ソリューションのビルド]** の順に選択します。 Visual Studio によって目的のライブラリが正常にビルドされるはずです。

---

## <a name="create-the-test-project"></a>テスト プロジェクトの作成

次のステップとして、`StringLibrary` ライブラリをテストする単体テスト プロジェクトを作成します。 次の手順を実行して、単体テストを作成します。

# <a name="ctabcsharp"></a>[C#](#tab/csharp)
1. **ソリューション エクスプローラー**で、`UtilityLibraries` ソリューションを右クリックし、**[追加]** > **[新しいプロジェクト]** の順に選択します。

1. **[新しいプロジェクトの追加]** ダイアログで、C# ノードを選択し、次に **[.NET Core]** を選択します。

   > [!NOTE]
   > 単体テストを記述する言語は、クラス ライブラリと同じ言語でなくてもかまいません。

1. 次の図に示すように、右側のウィンドウで **[単体テスト プロジェクト (.NET Core)]** テンプレートを選択し、**[名前]** テキスト ボックスに「`StringLibraryTests`」と入力します。

   ![単体テスト プロジェクトの場合の [新しいプロジェクトの追加] ダイアログ](./media/lut-start/add-unit-test-cs.png)

1. **[OK]** をクリックして、プロジェクトを作成します。

   > [!NOTE]
   > このはじめに (チュートリアル) では、Live Unit Testing を MSTest テスト フレームワークと一緒に使用します。 また、xUnit および NUnit のテスト フレームワークを使用することもできます。

1. 単体テスト プロジェクトは、テスト対象のクラス ライブラリに自動的にアクセスすることはできません。 テスト ライブラリへのアクセス権を付与するには、クラス ライブラリ プロジェクトへの参照を追加します。 これを行うには、`StringLibraryTests` プロジェクトを右クリックし、**[追加]**、**[参照]** の順にクリックします。 次の図に示すように、**[参照マネージャー]** ダイアログで、**[ソリューション]** タブが選択されていることを確認し、`StringLibrary` プロジェクトを選択します。

   ![[参照マネージャー] ダイアログ](./media/lut-start/add-reference.png)

1. テンプレートで入力されている定型的な単体テスト コードを次のコードに置き換えます。

   [!code-csharp[StringLibraryTest source code](samples/snippets/csharp/lut-start/unittest1.cs)]

1. ツール バーの **[保存]** アイコンを選択してプロジェクトを保存します。

1. 単体テスト コードには ASCII 以外の文字がいくつか含まれているため、既定の ASCII 形式でファイルを保存すると失われる文字が存在することを警告する次のようなダイアログが表示されます。 **[その他のエンコードで保存]** ボタンを選択します。

   ![ファイルのエンコードを選択](media/lut-start/ascii-encoding.png)

1. 次の図に示すように、**[保存オプションの詳細設定]** ダイアログの **[エンコード]** ドロップダウン リストから **[Unicode (UTF-8 シグネチャ付き) - コードページ 65001]** を選択します。

   ![UTF-8 エンコードを選択](media/lut-start/utf8-encoding.png)

1. Visual Studio の最上位メニューから、**[ビルド]**、**[ソリューションのリビルド]** の順に選択して、単体テスト プロジェクトをコンパイルします。

# <a name="visual-basictabvisual-basic"></a>[Visual Basic](#tab/visual-basic)

1. **ソリューション エクスプローラー**で、`UtilityLibraries` ソリューションを右クリックし、**[追加]** > **[新しいプロジェクト]** の順に選択します。

1. **[新しいプロジェクトの追加]** ダイアログで、Visual Basic ノードを選択し、**[.NET Core]** を選択します。

   > [!NOTE]
   > 単体テストを記述する言語は、クラス ライブラリと同じ言語でなくてもかまいません。

1. 次の図に示すように、右側のウィンドウで **[単体テスト プロジェクト (.NET Core)]** テンプレートを選択し、**[名前]** テキスト ボックスに「`StringLibraryTests`」と入力します。

   ![単体テストの場合の [新しいプロジェクトの追加] ダイアログ](./media/lut-start/add-unit-test-vb.png)

1. **[OK]** をクリックして、プロジェクトを作成します。

   > [!NOTE]
   > このはじめに (チュートリアル) では、Live Unit Testing を MSTest テスト フレームワークと一緒に使用します。 また、xUnit および NUnit のテスト フレームワークを使用することもできます。

1. 単体テスト プロジェクトは、テスト対象のクラス ライブラリに自動的にアクセスすることはできません。 テスト ライブラリへのアクセス権を付与するには、クラス ライブラリ プロジェクトへの参照を追加します。 これを行うには、`StringLibraryTests` プロジェクトを右クリックし、**[追加]**、**[参照]** の順にクリックします。 次の図に示すように、**[参照マネージャー]** ダイアログで、**[ソリューション]** タブが選択されていることを確認し、`StringLibrary` プロジェクトを選択します。

   ![[参照マネージャー] ダイアログ](./media/lut-start/add-reference.png)

1. テンプレートで入力されている定型的な単体テスト コードを次のコードに置き換えます。

   [!code-vb[StringLibraryTest source code](samples/snippets/visual-basic/lut-start/unittest1.vb)]

1. ツール バーの **[保存]** アイコンを選択してプロジェクトを保存します。

1. 単体テスト コードには ASCII 以外の文字がいくつか含まれているため、既定の ASCII 形式でファイルを保存すると失われる文字が存在することを警告する次のようなダイアログが表示されます。 **[その他のエンコードで保存]** ボタンを選択します。

   ![ファイルのエンコードを選択](media/lut-start/ascii-encoding.png)

1. 次の図に示すように、**[保存オプションの詳細設定]** ダイアログの **[エンコード]** ドロップダウン リストから **[Unicode (UTF-8 シグネチャ付き) - コードページ 65001]** を選択します。

   ![UTF-8 エンコードを選択](media/lut-start/utf8-encoding.png)

1. Visual Studio の最上位メニューから、**[ビルド]**、**[ソリューションのリビルド]** の順に選択して、単体テスト プロジェクトをコンパイルします。

---

クラス ライブラリと、これに対する複数の単体テストが作成されました。 これで、Live Unit Testing を使用するために必要な準備作業が完了しました。

## <a name="enable-live-unit-testing"></a>Live Unit Testing の有効化

`StringLibrary` クラス ライブラリ用のテストを作成しましたが、まだこのテストを実行していません。 Live Unit Testing を有効にすると、テストが自動的に実行されます。 Live Unit Testing を有効にするには、次の手順を実行します。

1. 必要に応じて、`StringLibrary` のコードが含まれているコード ウィンドウを選択します。 C# プロジェクトの class1.cs か、Visual Basic プロジェクトの Class1.vb のいずれかです  (このステップでは、Live Unit Testing を有効にした後で、テストの結果とコード カバレッジの範囲を視覚的に検査します)。

1. Visual Studio の最上位メニューから **[テスト]**、**[Live Unit Testing]**、**[開始]** の順に選びます。

1. Visual Studio が Live Unit Test を開始します。これによりすべてのテストが自動的に実行されます。

テストの実行が終了すると、**テスト エクスプローラー**に全体の結果と個々のテストの結果とが両方とも表示されます。 さらに、コード ウィンドウには、テスト コードのカバレッジとテストの結果とが両方ともグラフィカルに表示されます。 次の図に示すように、3 つのテストはいずれも正常に実行されています。 また、テストは `StartsWithUpper` メソッド内のすべてのコード パスをカバーしており、それらのテストはすべて正常に実行されていることがわかります (緑色のチェック マーク "✓" によって示されている)。 最後に、`StringLibrary` 内の他のメソッドにはコード カバレッジが設定されていないことがわかります (青い線 "➖" によって示されている)。

# <a name="ctabcsharp"></a>[C#](#tab/csharp)
![Live Unit Testing の開始後のテスト エクスプローラーとコード ウィンドウ](media/lut-start/lut-results-cs.png)

# <a name="visual-basictabvisual-basic"></a>[Visual Basic](#tab/visual-basic)
![Live Unit Testing の開始後のテスト エクスプローラーとコード ウィンドウ](media/lut-start/lut-results-vb.png)

---

また、コード ウィンドウ内の特定のコード カバレッジ アイコンを選択することにより、テスト カバレッジとテスト結果に関する詳細情報を取得することもできます。 この詳細を調べるには、次の手順を実行します。

# <a name="ctabcsharp"></a>[C#](#tab/csharp)
1. `StartsWithUpper` メソッド内の `if (String.IsNullOrWhiteSpace(s))` という行に表示された緑のチェック マークをクリックします。 次の図に示すように、Live Unit Testing は、そのコード行が 3 つのテストでカバーされており、いずれのテストも正常に実行されていることを示します。

   !["If" 条件付きステートメントのコード カバレッジ](media/lut-start/code-coverage-cs1.png)

1. `StartsWithUpper` メソッド内の `return Char.IsUpper(s[0])` という行に表示された緑のチェック マークをクリックします。 次の図に示すように、Live Unit Testing は、そのコード行が 2 つのテストのみでカバーされており、いずれのテストも正常に実行されていることを示します。

   ![Return ステートメントのコード カバレッジ](media/lut-start/code-coverage-cs2.png)

# <a name="visual-basictabvisual-basic"></a>[Visual Basic](#tab/visual-basic)
1. `StartsWithUpper` メソッド内の `If (String.IsNullOrWhiteSpace(s)) Then` という行に表示された緑のチェック マークをクリックします。 次の図に示すように、Live Unit Testing は、そのコード行が 3 つのテストでカバーされており、いずれのテストも正常に実行されていることを示します。

   !["If" 条件付きステートメントのコード カバレッジ](media/lut-start/code-coverage-vb1.png)

1. `StartsWithUpper` メソッド内の `Return Char.IsUpper(s(0))` という行に表示された緑のチェック マークをクリックします。 次の図に示すように、Live Unit Testing は、そのコード行が 2 つのテストのみでカバーされており、いずれのテストも正常に実行されていることを示します。

   ![Return ステートメントのコード カバレッジ](media/lut-start/code-coverage-vb2.png)

---

Live Unit Testing は、重大な問題として不完全なコード カバレッジを明らかにしています。 この問題は、次のセクションで取り上げます。

## <a name="expand-test-coverage"></a>テスト カバレッジの展開

このセクションでは、単体テストを `StartsWithLower` メソッドに展開します。 展開を行っている間も、Live Unit Testing によって引き続きコードのテストが実行されます。

コード カバレッジを `StartsWithLower` メソッドに展開するには、次の手順を実行します。

# <a name="ctabcsharp"></a>[C#](#tab/csharp)
1. 次の `TestStartsWithLower` メソッドと `TestDoesNotStartWithLower` メソッドをプロジェクトのテスト ソース コード ファイルに追加します。

    [!code-csharp[StringLibraryTest source code](samples/snippets/csharp/lut-start/unittest2.cs#1)]

1. [`Microsoft.VisualStudio.TestTools.UnitTesting.Assert.IsFalse`](/dotnet/api/microsoft.visualstudio.testtools.unittesting.assert.isfalse) メソッドへの呼び出しのすぐ後に、次のコードを追加して、`DirectCallWithNullOrEmpty` メソッドを変更します。

    [!code-csharp[StringLibraryTest source code](samples/snippets/csharp/lut-start/unittest2.cs#2)]

1. ソース コードを変更すると、Live Unit Testing によって新しいテストと変更したテストが自動的に実行されます。 次の図に示すように、**テスト エクスプローラー**に、追加した 2 つのテストと変更した 1 つのテストを含むすべてのテストが成功したことが表示されます。

   ![テスト カバレッジを展開した後のテスト エクスプローラー](media/lut-start/test-dynamic.png)

1. `StringLibrary` クラスのソース コードを含むウィンドウに切り替えます。 Live Unit Testing は、コード カバレッジが `StartsWithLower` メソッドに展開されていることを示します。

    ![StartsWithLower メソッドのコード カバレッジ](media/lut-start/lut-extended-cs.png)

# <a name="visual-basictabvisual-basic"></a>[Visual Basic](#tab/visual-basic)
1. 次の `TestStartsWithLower` メソッドと `TestDoesNotStartWithLower` メソッドをプロジェクトのテスト ソース コード ファイルに追加します。

    [!code-vb[StringLibraryTest source code](samples/snippets/visual-basic/lut-start/unittest2.vb#1)]

1. [`Microsoft.VisualStudio.TestTools.UnitTesting.Assert.IsFalse`](/dotnet/api/microsoft.visualstudio.testtools.unittesting.assert.isfalse) メソッドへの呼び出しのすぐ後に、次のコードを追加して、`DirectCallWithNullOrEmpty` メソッドを変更します。

    [!code-vb[StringLibraryTest source code](samples/snippets/visual-basic/lut-start/unittest2.vb#2)]

1. ソース コードを変更すると、Live Unit Testing によって新しいテストと変更したテストが自動的に実行されます。 次の図に示すように、**テスト エクスプローラー**に、追加した 2 つのテストと変更した 1 つのテストを含むすべてのテストが成功したことが表示されます。

   ![テスト カバレッジを展開した後のテスト エクスプローラー](media/lut-start/test-dynamic.png)

1. `StringLibrary` クラスのソース コードを含むウィンドウに切り替えます。 Live Unit Testing は、コード カバレッジが `StartsWithLower` メソッドに展開されていることを示します。

    ![StartsWithLower のコード カバレッジ](media/lut-start/lut-extended-vb.png)

---

場合によっては、成功したテストが**テスト エクスプローラー**で、灰色表示されることがあります。これは、テストが現在実行中であることを示すか、または最後に実行されてから、テストに影響する変更がコードに加えられていないために、テストが再度実行されなかったことを示します。

これまで、すべてのテストが成功しています。 次のセクションでは、テスト エラーを処理する方法について説明します。

## <a name="handling-a-test-failure"></a>テスト エラーの処理

このセクションでは、Live Unit Testing を使用してテスト エラーを識別し、トラブルシューティングを行い、対処する方法を説明します。 そのために、テスト カバレッジを `HasEmbeddedSpaces` メソッドに展開します。

# <a name="ctabcsharp"></a>[C#](#tab/csharp)
1. テスト ファイルに次のメソッドを追加します。

    [!code-csharp[The TestHasEmbeddedSpaces test method](samples/snippets/csharp/lut-start/unittest2.cs#3)]

1. 次の図に示すように、テストが実行されると、Live Unit Testing は `TestHasEmbeddedSpaces` メソッドが失敗したことを示します。![失敗したテストを示すテスト エクスプローラー](media/lut-start/test-failure.png)

1. ライブラリ コードが表示されたウィンドウを選択します。 Live Unit Testing によって `HasEmbeddedSpaces` メソッドにコード カバレッジが展開されていることに注目してください。 また、Live Unit Testing は、失敗したテストでカバーされている行に赤い "🞩" を追加することで、テスト エラーを報告しています。

1. `HasEmbeddedSpaces`メソッド シグネチャが含まれている行にマウス ポインターを合わせます。 次の図に示すように、Live Unit Testing は、メソッドが 1 つのテストでカバーされていることを知らせるツールヒントを表示します。

   ![失敗したテストに関する Live Unit Testing の情報](media/lut-start/test-failure-info-cs.png)

1. 失敗した **TestHasEmbeddedSpaces** テストを選択します。 次の図に示すように、すべてのテストの実行、選択したテストの実行、すべてのテストのデバッグ、選択したテストのデバッグなど、Live Unit Testing には多くのオプションが用意されています。

   ![テストが失敗した場合のための Live Unit Testing のオプション](media/lut-start/test-failure-options.png)

1. **[選択されたテストのデバッグ]** を選択して、失敗したテストをデバッグします。

1. Visual Studio はデバッグ モードでテストを実行します。 テストでは、配列内の各文字列が `phrase` という名前の変数に割り当てられ、その変数が `HasEmbeddedSpaces` メソッドに渡されます。 アサーション式が初めて `false` になると、プログラムの実行は一時停止し、デバッガーが呼び出されます。 [`Microsoft.VisualStudio.TestTools.UnitTesting.Assert.IsTrue`](/dotnet/api/microsoft.visualstudio.testtools.unittesting.assert.istrue) メソッドの呼び出しに予期しない値が含まれていると、以下の図に示すような例外ダイアログが表示されます。

   ![Live Unit Testing の例外ダイアログ](media/lut-start/exception-dialog-cs.png)

   さらに、次の図に示すように、Visual Studio で用意されているすべてのデバッグ ツールを使用することで、失敗したテストのトラブルシューティングを効果的に行うことができます。

   ![Visual Studio のデバッグ ツール](media/lut-start/debugging-tools-cs.png)

   **[自動変数]** ウィンドウで、`phrase` 変数の値が "Name\tDescription" (配列の 2 番目の要素) になっていることに注目してください。 テスト メソッドは、この文字列が `HasEmbeddedSpaces` に渡された場合に `true` が返されるのを期待していますが、実際に返されるのは `false` です。 タブ文字である "\t" が埋め込みスペースとして認識されていないのは明らかです。

1. テスト プログラムの実行を続行するには、**[デバッグ]**、**[続行]** の順に選択するか、F5 キーを押すか、あるいはツールバーの **[続行]** ボタンをクリックします。 ハンドルされない例外が発生したため、テストは終了します。

# <a name="visual-basictabvisual-basic"></a>[Visual Basic](#tab/visual-basic)
1. テスト ファイルに次のメソッドを追加します。

    [!code-vb[The TestHasEmbeddedSpaces test method](samples/snippets/visual-basic/lut-start/unittest2.vb#3)]

1. 次の図に示すように、テストが実行されると、Live Unit Testing は `TestHasEmbeddedSpaces` メソッドが失敗したことを示します。

   ![失敗したテストを示すテスト エクスプローラー](media/lut-start/test-failure.png)

1. ライブラリ コードが表示されたウィンドウを選択します。 Live Unit Testing によって `HasEmbeddedSpaces` メソッドにコード カバレッジが展開されていることに注目してください。 また、Live Unit Testing は、失敗したテストでカバーされている行に赤い "🞩" を追加することで、テスト エラーを報告しています。

1. `HasEmbeddedSpaces`メソッド シグネチャが含まれている行にマウス ポインターを合わせます。 次の図に示すように、Live Unit Testing は、メソッドが 1 つのテストでカバーされていることを知らせるツールヒントを表示します。

   ![失敗したテストに関する Live Unit Testing の情報](media/lut-start/test-failure-info-vb.png)

1. 失敗した **TestHasEmbeddedSpaces** テストを選択します。 次の図に示すように、すべてのテストの実行、選択したテストの実行、すべてのテストのデバッグ、選択したテストのデバッグなど、Live Unit Testing には多くのオプションが用意されています。

   ![テストが失敗した場合のための Live Unit Testing のオプション](media/lut-start/test-failure-options.png)

1. **[選択されたテストのデバッグ]** を選択して、失敗したテストをデバッグします。

1. Visual Studio はデバッグ モードでテストを実行します。 テストでは、配列内の各文字列が `phrase` という名前の変数に割り当てられ、その変数が `HasEmbeddedSpaces` メソッドに渡されます。 アサーション式が初めて `false` になると、プログラムの実行は一時停止し、デバッガーが呼び出されます。 [`Microsoft.VisualStudio.TestTools.UnitTesting.Assert.IsTrue`](/dotnet/api/microsoft.visualstudio.testtools.unittesting.assert.istrue) メソッドの呼び出しに予期しない値が含まれていると、以下の図に示すような例外ダイアログが表示されます。

   ![Live Unit Testing の例外ダイアログ](media/lut-start/exception-dialog-vb.png)

   さらに、次の図に示すように、Visual Studio で用意されているすべてのデバッグ ツールを使用することで、失敗したテストのトラブルシューティングを効果的に行うことができます。

   ![Visual Studio のデバッグ ツール](media/lut-start/debugging-tools-vb.png)

   **[自動変数]** ウィンドウで、`phrase` 変数の値が "Name" + vbTab + "Description" (配列の 2 番目の要素) になっていることに注目してください。 テスト メソッドは、この文字列が `HasEmbeddedSpaces` に渡された場合に `true` が返されるのを期待していますが、実際に返されるのは `false` です。 タブ文字が埋め込みスペースとして認識されていないのは明らかです。

1. テスト プログラムの実行を続行するには、**[デバッグ]**、**[続行]** の順に選択するか、F5 キーを押すか、あるいはツールバーの **[続行]** ボタンをクリックします。 ハンドルされない例外が発生したため、テストは終了します。

---

これは、バグの予備調査を行う上で十分な情報です。 テスト ルーチンである `TestHasEmbeddedSpaces` で不適切な想定が行われたか、または`HasEmbeddedSpaces` がすべての埋め込みスペースを正しく認識していません。 問題を診断し解決するには、`StringLibrary.HasEmbeddedSpaces` メソッドから始めます。

# <a name="ctabcsharp"></a>[C#](#tab/csharp)
1. `HasEmbeddedSpaces` メソッドでの比較を確認します。 このメソッドでは、埋め込みスペースを U+0020 と見なしています。 ただし、Unicode Standard には、その他にも多くの空白文字が含まれています。 このことは、空白文字かどうかのテストが、ライブラリ コードで正しく行われていないことを示しています。

1. 等価比較を、<xref:System.Char.IsWhiteSpace%2A?displayProperty=fullName> メソッドへの呼び出しに置き換えます。

    [!code-csharp[The TestHasEmbeddedSpaces test method](samples/snippets/csharp/lut-start/program2.cs#1)]

1. 次の図に示すように、Live Unit Testing は、失敗したテスト メソッドを再実行し、コード ウィンドウ内の結果と**テスト エクスプローラー**内の結果を更新する処理を自動的に行います。

    ![成功した HasEmbeddedSpaces テスト](media/lut-start/test-success-cs.png)

# <a name="visual-basictabvisual-basic"></a>[Visual Basic](#tab/visual-basic)
1. `HasEmbeddedSpaces` メソッドでの比較を確認します。 このメソッドでは、埋め込みスペースを U+0020 と見なしています。 ただし、Unicode Standard には、その他にも多くの空白文字が含まれています。 このことは、空白文字かどうかのテストが、ライブラリ コードで正しく行われていないことを示しています。

1. 等価比較を、<xref:System.Char.IsWhiteSpace%2A?displayProperty=fullName> メソッドへの呼び出しに置き換えます。

    [!code-vb[The TestHasEmbeddedSpaces test method](samples/snippets/visual-basic/lut-start/class2.vb#1)]

1. 次の図に示すように、Live Unit Testing は、失敗したテスト メソッドを再実行し、コード ウィンドウ内の結果と**テスト エクスプローラー**内の結果を更新する処理を自動的に行います。

    ![成功した HasEmbeddedSpaces テスト](media/lut-start/test-success-vb.png)

---

## <a name="see-also"></a>関連項目
[Visual Studio の Live Unit Testing](live-unit-testing.md)
[Live Unit Testing についてよく寄せられる質問](live-unit-testing-faq.md)
