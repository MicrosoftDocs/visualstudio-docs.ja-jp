---
title: '方法: C++ DLL 用の単体テストの記述'
description: テスト ファースト メソドロジを使用してネイティブ C++ DLL を開発する方法について説明します。 まず、ネイティブ テスト プロジェクトを作成します。
ms.custom: SEO-VS-2020
ms.date: 06/13/2019
ms.topic: how-to
ms.author: corob
manager: markl
ms.workload:
- cplusplus
author: corob-msft
ms.openlocfilehash: cfdc580b94760cb0c5160918210ba6c3dd8fa2f6
ms.sourcegitcommit: 4b2b6068846425f6964c1fd867370863fc4993ce
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/12/2021
ms.locfileid: "112042926"
---
# <a name="how-to-write-unit-tests-for-c-dlls"></a>方法: C++ DLL 用の単体テストを作成する

このチュートリアルでは、テスト ファースト メソドロジを使ってネイティブ C++ DLL を開発する方法について説明します。 基本的な手順は次のとおりです。

1. [ネイティブのテスト プロジェクトを作成する](#create_test_project)。 テスト プロジェクトは、DLL プロジェクトと同じソリューションに格納されます。

2. [DLL プロジェクトを作成する](#create_dll_project)。 このチュートリアルでは新しい DLL を作成しますが、既存の DLL をテストする手順は類似しています。

3. [DLL 関数をテストに表示させる](#make_functions_visible)。

4. [テストを反復拡張する](#iterate)。 コードの開発がテストによって主導される「red-green-refactor」サイクルの使用をお勧めします。

5. [失敗したテストをデバッグする](#debug)。 テストをデバッグ モードで実行することができます。

6. [テストを変更しないままリファクタリングする](#refactor)。 リファクタリングとは、外部の動作を変更せずに、コードの構造を改善するという意味です。 リファクタリングを行うと、コードのパフォーマンス、拡張性、または読みやすさが向上します。 目的は動作を変更しないことであるため、コードへの変更をリファクタリングするときはテストを変更しないでください。 テストは、リファクタリング中にバグを持ち込んでいないことを確認するのに役立ちます。

7. [カバレッジを確認する](using-code-coverage-to-determine-how-much-code-is-being-tested.md)。 単体テストは、コードをより多く実行する場合はさらに有用です。 コードのどの部分がテストで使用されたかを見つけ出すことができます。

8. [外部リソースから単位を分離する](using-stubs-to-isolate-parts-of-your-application-from-each-other-for-unit-testing.md)。 一般に、DLL は、他の DLL、データベース、またはリモートのサブシステムなど、開発中のシステムの他のコンポーネントに依存しています。 各単位をその依存関係から分離してテストすると役立ちます。 外部コンポーネントは、テストの実行を遅くする可能性があります。 開発中、他のコンポーネントが不完全であることもあり得ます。

## <a name="create-a-native-unit-test-project"></a><a name="create_test_project"></a> ネイティブ単体テスト プロジェクトを作成する

1. **[ファイル]** メニューで、 **[新規]**  >  **[プロジェクト]** の順にクリックします。

     **Visual Studio 2017 以前**: **[インストール済み]** 、 **[テンプレート]** 、 **[Visual C++]** 、 **[テスト]** の順に展開します。
     **Visual Studio 2019**: **[言語]** を C++ に設定し、検索ボックスに "test" と入力します。

     **ネイティブ単体テスト プロジェクト** テンプレートまたはインストールされている他の好みのフレームワークを選びます。 Google Test や Boost.Test などの別のテンプレートを選んだ場合、基本的な原則は同じですが、いくつかの詳細は異なります。

     このチュートリアルでは、テスト プロジェクトの名前は `NativeRooterTest`です。

2. 新しいプロジェクトで、 **unittest1.cpp** を検査します。

     ![TEST&#95;CLASS と TEST&#95;METHOD が表示されたテスト プロジェクト](../test/media/utecpp2.png)

     次のことに注意してください。

    - 各テストは `TEST_METHOD(YourTestName){...}` を使用して定義されます。

         従来の関数の署名を記述する必要はありません。 署名は、マクロ TEST_METHOD によって作成されます。 マクロは、void を返すインスタンス関数を生成します。 また、テスト メソッドに関する情報を返す静的関数も生成します。 この情報により、テスト エクスプ ローラーはメソッドを見つけます。

    - テスト メソッドは、 `TEST_CLASS(YourClassName){...}`を使用してクラスにグループ化されます。

         テストが実行されると、各テスト クラスのインスタンスが作成されます。 テスト メソッドが呼び出される順序は決まっていません。 各モジュール、クラス、またはメソッドの前後に呼び出される特殊なメソッドを定義することができます。

3. テストがテスト エクスプ ローラーで実行することを確認します。

    1. 幾らかのテスト コードを挿入します。

        ```cpp
        TEST_METHOD(TestMethod1)
        {
            Assert::AreEqual(1,1);
        }
        ```

         `Assert` クラスは、テスト メソッドで結果を確認するために使用するいくつかの静的メソッドを提供することに注意してください。

    2. **[テスト]** メニューで **[実行]**  >  **[すべてのテスト]** を選択します。

         テストがビルドし、実行します。

         **テスト エクスプローラー** が表示されます。

         **[合格したテスト]** の下にテストが表示されます。

         ![1 つのテストが成功したことを示す単体テスト エクスプローラー](../test/media/utecpp04.png)

## <a name="create-a-dll-project"></a><a name="create_dll_project"></a> DLL プロジェクトを作成する

::: moniker range=">=vs-2019"

次の手順は、Visual Studio 2019 で DLL プロジェクトを作成する方法を示しています。

1. **Windows デスクトップ ウィザード** を使用し、C++ プロジェクトを作成します。**ソリューション エクスプローラー** でソリューションを右クリックし、 **[追加]** 、 **[新しいプロジェクト]** の順に選択します。 **[言語]** を C++ に設定し、検索ボックスに "windows" と入力します。 結果の一覧から **[Windows デスクトップ ウィザード]** を選択します。

     このチュートリアルでは、プロジェクトの名前を `RootFinder`とします。

2. **[作成]** をクリックします。 次のダイアログの **[アプリケーションの種類]** で **[ダイナミックリンク ライブラリ (dll)]** を選択し、**[シンボルのエクスポート]** にもチェックを入れます。

     **[シンボルのエクスポート]** オプションは、エクスポートされたメソッドの宣言に使用できる便利なマクロを生成します。

     ![[DLL] と [シンボルのエクスポート] が設定された C++ プロジェクト ウィザード](../test/media/vs-2019/windows-desktop-project-dll.png)

3. プリンシパル *.h* ファイルでエクスポートされた関数を宣言します。

     ![API マクロを使用した新しい DLL コード プロジェクトと .h ファイル](../test/media/utecpp07.png)

     宣言子 `__declspec(dllexport)` は、クラスのパブリック メンバーと保護されるメンバーが DLL の外部で表示できるようにします。 詳細については、「 [Using dllimport and dllexport in C++ Classes](/cpp/cpp/using-dllimport-and-dllexport-in-cpp-classes)」を参照してください。

4. プリンシパル *.cpp* ファイルでは、最小限の本体を関数に追加します。

    ```cpp
        // Find the square root of a number.
        double CRootFinder::SquareRoot(double v)
        {
            return 0.0;
        }
    ```

::: moniker-end

::: moniker range="vs-2017"

次の手順では、Visual Studio 2017 で DLL プロジェクトを作成する方法を示します。

1. **Win32 プロジェクト** テンプレートを使用して C++ プロジェクトを作成します。

     このチュートリアルでは、プロジェクトの名前を `RootFinder`とします。

2. [Win32 アプリケーション ウィザード] で **[DLL]** と **[シンボルのエクスポート]** を選択します。

     **[シンボルのエクスポート]** オプションは、エクスポートされたメソッドの宣言に使用できる便利なマクロを生成します。

     ![[DLL] と [シンボルのエクスポート] が設定された C++ プロジェクト ウィザード](../test/media/utecpp06.png)

3. プリンシパル *.h* ファイルでエクスポートされた関数を宣言します。

     ![API マクロを使用した新しい DLL コード プロジェクトと .h ファイル](../test/media/utecpp07.png)

     宣言子 `__declspec(dllexport)` は、クラスのパブリック メンバーと保護されるメンバーが DLL の外部で表示できるようにします。 詳細については、「 [Using dllimport and dllexport in C++ Classes](/cpp/cpp/using-dllimport-and-dllexport-in-cpp-classes)」を参照してください。

4. プリンシパル *.cpp* ファイルでは、最小限の本体を関数に追加します。

    ```cpp
        // Find the square root of a number.
        double CRootFinder::SquareRoot(double v)
        {
            return 0.0;
        }
    ```

::: moniker-end

## <a name="couple-the-test-project-to-the-dll-project"></a><a name="make_functions_visible"></a> DLL プロジェクトにテスト プロジェクトを結合する

1. DLL プロジェクトをテスト プロジェクトのプロジェクト参照に追加します。

   1. **ソリューション エクスプローラー** でプロジェクト ノードを右クリックして、**[追加]** > **[参照]** を選びます。

   2. **[参照の追加]** ダイアログ ボックスで、DLL プロジェクトを選択し、 **[追加]** をクリックします。

        ![C++ プロジェクト プロパティ | 新しい参照の追加](../test/media/utecpp09.png)

2. プリンシパルの単体テストの *.cpp* ファイルに、DLL コードの *.h* ファイルを含めます。

   ```cpp
   #include "..\RootFinder\RootFinder.h"
   ```

3. エクスポートされた関数を使用する基本テストを追加します。

   ```cpp
   TEST_METHOD(BasicTest)
   {
      CRootFinder rooter;
      Assert::AreEqual(
         // Expected value:
         0.0,
         // Actual value:
         rooter.SquareRoot(0.0),
         // Tolerance:
         0.01,
        // Message:
        L"Basic test failed",
        // Line number - used if there is no PDB file:
        LINE_INFO());
   }
   ```

4. ソリューションをビルドします。

    **テスト エクスプローラー** に新しいテストが表示されます。

5. **テスト エクスプローラー** で **[すべて実行]** をクリックします。

    ![単体テスト エクスプローラー &#45 基本テスト成功](../test/media/utecpp10.png)

   テストとコード プロジェクトをセット アップして、コード プロジェクトで関数を実行するテストを実行できることを確認しました。 ここで、実際のテストおよびコードの記述を開始できます。

## <a name="iteratively-augment-the-tests-and-make-them-pass"></a><a name="iterate"></a> テストを繰り返し増やして成功させる

1. 新しいテストを追加します。

    ```cpp
    TEST_METHOD(RangeTest)
    {
      CRootFinder rooter;
      for (double v = 1e-6; v < 1e6; v = v * 3.2)
      {
        double actual = rooter.SquareRoot(v*v);
        Assert::AreEqual(v, actual, v/1000);
      }
    }
    ```

    > [!TIP]
    > 合格したテスト内容を変更しないことをお勧めします。 代わりに、新しいテストを追加し、テストが合格するようにコードを更新してから別のテストを追加する、という過程を繰り返します。
    >
    > ユーザーが要件を変更したら、正しくなくなったテストを無効にします。 新しいテストを作成し、一度に 1 つずつ、同じ増分方式で処理するようにします。

2. ソリューションをビルドし、**テスト エクスプローラー** で **[すべて実行]** を選択します。

     新しいテストは失敗します。

     ![RangeTest 失敗](../test/media/ute_cpp_testexplorer_rangetest_fail.png)

    > [!TIP]
    > 各テストが記述した後すぐに失敗することを確認します。 これは、絶対に失敗しないテストを記述するという簡単なミスを避けることに役立ちます。

3. 新しいテストが成功するように、DLL のコードを修正します。

    ```cpp
    #include <math.h>
    ...
    double CRootFinder::SquareRoot(double v)
    {
      double result = v;
      double diff = v;
      while (diff > result/1000)
      {
        double oldResult = result;
        result = result - (result*result - v)/(2*result);
        diff = abs (oldResult - result);
      }
      return result;
    }
    ```

4. ソリューションをビルドし、**テスト エクスプローラー** で **[すべて実行]** を選択します。

     両方のテストが合格します。

     ![単体テスト エクスプローラー &#45 範囲テスト成功](../test/media/utecpp12.png)

    > [!TIP]
    > 一度に 1 つのテストを追加してコードを開発します。 各反復処理の後にすべてのテストが合格することを確認します。

## <a name="debug-a-failing-test"></a><a name="debug"></a> 失敗したテストをデバッグする

1. 別のテストを追加します。

    ```cpp
    #include <stdexcept>
    ...
    // Verify that negative inputs throw an exception.
    TEST_METHOD(NegativeRangeTest)
    {
      wchar_t message[200];
      CRootFinder rooter;
      for (double v = -0.1; v > -3.0; v = v - 0.5)
      {
        try
        {
          // Should raise an exception:
          double result = rooter.SquareRoot(v);

          _swprintf(message, L"No exception for input %g", v);
          Assert::Fail(message, LINE_INFO());
        }
        catch (std::out_of_range ex)
        {
          continue; // Correct exception.
        }
        catch (...)
        {
          _swprintf(message, L"Incorrect exception for %g", v);
          Assert::Fail(message, LINE_INFO());
        }
      }
    }
    ```

2. ソリューションをビルドし、 **[すべて実行]** をクリックします。

3. 失敗したテストを開きます (またはダブルクリックします)。

     失敗したアサーションが強調表示されます。 エラー メッセージは、**テスト エクスプローラー** の [詳細] ウィンドウに表示されます。

     ![NegativeRangeTest 失敗](../test/media/ute_cpp_testexplorer_negativerangetest_fail.png)

4. テストが失敗した理由を表示するには、関数をステップ実行します。

    1. SquareRoot 関数の始めに、ブレークポイントを設定します。

    2. 失敗したテストのショートカット メニューで **[選択したテストのデバッグ]** をクリックします。

         実行がブレークポイントで停止したら、コードをステップ実行します。

5. 開発中の関数にコードを挿入します。

    ```cpp

    #include <stdexcept>
    ...
    double CRootFinder::SquareRoot(double v)
    {
        // Validate parameter:
        if (v < 0.0)
        {
          throw std::out_of_range("Can't do square roots of negatives");
        }

    ```

6. 今回は、すべてのテストに合格します。

   ![すべてのテストの成功](../test/media/ute_ult_alltestspass.png)

::: moniker range="vs-2017"

> [!TIP]
> 何らかの順序で実行することを禁止する依存関係が個々のテストにない場合、![ で並列テスト実行をオンにします。テスト エクスプローラー ツール バーのテスト実行トグル ボタンのスクリーンショット。 このボタンが選択されると、テストが並列実行されます。](../test/media/ute_parallelicon-small.png) トグル ボタンで並列テストの実行を有効にします。 これにより、すべてのテスト実行にかかる時間を著しく短縮できます。

::: moniker-end

::: moniker range=">=vs-2019"

> [!TIP]
> 個々のテストに実行順序を定める依存関係がない場合、ツール バーの設定メニューで並列テストの実行を有効にします。 これにより、すべてのテスト実行にかかる時間を著しく短縮できます。

::: moniker-end

## <a name="refactor-the-code-without-changing-tests"></a><a name="refactor"></a> テストを変更せずにコードをリファクタリングする

1. SquareRoot 関数の中心的な計算を簡素化します。

    ```cpp
    // old code:
    //   result = result - (result*result - v)/(2*result);
    // new code:
         result = (result + v/result)/2.0;

    ```

2. ソリューションをビルドし、 **[すべて実行]** をクリックして、エラーが持ち込まれていないことを確認します。

    > [!TIP]
    > 一連の単体テストがうまくいくことは、コードを変更する際にバグが持ち込まれていないという信用を与えます。
    >
    > 常に他の変更とは別にリファクタリングしてください。

## <a name="next-steps"></a>次のステップ

- **分離。** ほとんどの DLL は、データベースや他の DLL など、他のサブシステムに依存しています。 これらの他のコンポーネントは、多くの場合、並列で開発されます。 他のコンポーネントがまだ使用可能でないときに単体テストを行えるようにするには、モックまたは

- **ビルド確認テスト。** 設定された間隔で、チームのビルド サーバーでテストを実行することができます。 これにより、複数のチーム メンバーの作業が統合されてもバグが持ち込まれることはありません。

- **チェックイン テスト。** 各チーム メンバーがコードをソース管理にチェックインする前にテストを実行することを要求できます。 通常、これはビルド確認テストの完全なセットのサブセットです。

   また、最低限のコード カバレッジも要求できます。

## <a name="see-also"></a>関連項目

- [既存の C++ アプリケーションへの単体テストの追加](../test/how-to-use-microsoft-test-framework-for-cpp.md)
- [Microsoft.VisualStudio.TestTools.CppUnitTestFramework の使用](how-to-use-microsoft-test-framework-for-cpp.md)
- [ネイティブ コードをデバッグする](../debugger/debugging-native-code.md)
- [チュートリアル: ダイナミック リンク ライブラリの作成と使用 (C++)](/cpp/build/walkthrough-creating-and-using-a-dynamic-link-library-cpp)
- [インポートとエクスポート](/cpp/build/importing-and-exporting)
