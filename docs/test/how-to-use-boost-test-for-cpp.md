---
title: C++ 用の Boost.Test を使用する方法
description: Boost.Test を使用し、Visual Studio で単体テストを作成します。
ms.date: 05/06/2019
ms.topic: conceptual
author: mikeblome
ms.author: mblome
manager: jillfra
ms.workload:
- cplusplus
ms.openlocfilehash: 966983fa15b60db33f11645b25561a74ad5fadbe
ms.sourcegitcommit: dcbb876a5dd598f2538e62e1eabd4dc98595b53a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/28/2019
ms.locfileid: "72983447"
---
# <a name="how-to-use-boosttest-for-c-in-visual-studio"></a>Visual Studio で C++ 用の Boost.Test を使用する方法

Visual Studio 2017 以降では、Boost.Test テスト アダプターが **[C++ によるデスクトップ開発]** ワークロードのコンポーネントとして Visual Studio IDE に統合されています。

![Test Adapter for Boost.Test](media/cpp-boost-component.png)

**[C++ によるデスクトップ開発]** ワークロードがインストールされていない場合は、**Visual Studio インストーラー**を開きます。 **[C++ によるデスクトップ開発]** ワークロードを選んで、 **[変更]** ボタンを選択します。

## <a name="install-boost"></a>Boost をインストールする

Boost.Test には [Boost](https://www.boost.org/) が必要です。 Boost がインストールされていない場合は、Vcpkg パッケージ マネージャーを使うことをお勧めします。

1. 「[vcpkg: Windows 用の C++ パッケージ マネージャー](/cpp/vcpkg)」の説明に従って、vcpkg をインストールします (まだない場合)。

1. Boost.Test のダイナミック ライブラリまたはスタティック ライブラリをインストールします。

    - Boost.Test のダイナミック ライブラリをインストールするには、**vcpkg install boost-test** を実行します。

       または

    - Boost.Test のスタティック ライブラリをインストールするには、**vcpkg install boost-test:x86-windows-static** を実行します。

1. **vcpkg integrate install** を実行して、ライブラリで Visual Studio を構成し、Boost のヘッダーとバイナリへのパスを組み込みます。

## <a name="add-the-item-template-visual-studio-2017-version-156-and-later"></a>項目テンプレートを追加する (Visual Studio 2017 バージョン 15.6)

1. テスト用の *.cpp* ファイルを追加するには、**ソリューション エクスプローラー**でプロジェクト ノードを右クリックし、 **[新しい項目の追加]** を選択します。

   ![Boost.Test 項目テンプレート](media/boost_test_item_template.png)

1. 新しいファイルには、サンプル テスト メソッドが含まれます。 プロジェクトをビルドして、**テスト エクスプ ローラー**がメソッドを検出できるようにします。

項目テンプレートは、Boost.Test の単一ヘッダー バリアントを使用しますが、スタンドアロン ライブラリ バリアントを使用するように #include パスを変更できます。 詳細については、「[インクルード ディレクティブを追加する](#add-include-directives)」を参照してください。

## <a name="create-a-test-project"></a>テスト プロジェクトを作成する

Visual Studio 2017 バージョン 15.5 には、Boost.Test に利用できる構成済みのテスト プロジェクトまたは項目テンプレートはありません。 したがって、テストを保持するコンソール アプリケーション プロジェクトを作成して構成する必要があります。

1. **ソリューション エクスプローラー**で、ソリューション ノードを右クリックして、 **[追加]**  >  **[新しいプロジェクト]** の順に選択します。

1. 左側のウィンドウで **[Visual C++]**  >  **[Windows デスクトップ]** を選んだ後、 **[Windows コンソール アプリケーション]** テンプレートを選択します。

1. プロジェクト名を設定し、 **[OK]** を選択します。

1. *.cpp* ファイル内の `main` 関数を削除します。

1. Boost.Test の単一ヘッダーまたは動的ライブラリ バージョンを使用している場合は、「[インクルード ディレクティブを追加する](#add-include-directives)」に進みます。 スタティック ライブラリ バージョンを使用している場合は、追加の構成を実行する必要があります。

   a. プロジェクト ファイルを編集するには、最初にプロジェクト ファイルをアンロードします。 **ソリューション エクスプローラー**で、プロジェクト ノードを右クリックして **[プロジェクトのアンロード]** を選択します。 次に、プロジェクト ノードを右クリックして、 **[<名前\>.vcxproj の編集]** を選択します。

   b. 次に示すように、**Globals** プロパティ グループに 2 つの行を追加します。

    ```xml
    <PropertyGroup Label="Globals">
    ....
        <VcpkgTriplet>x86-windows-static</VcpkgTriplet>
        <VcpkgEnabled>true</VcpkgEnabled>
    </PropertyGroup>
    ```

   c. *\*.vcxproj* ファイルを保存して閉じた後、プロジェクトをリロードします。

   d. **プロパティ ページ**を開くには、プロジェクト ノードを右クリックして、 **[プロパティ]** を選択します。

   d. **[C/C++]**  >  **[コード生成]** の順に展開し、 **[ランタイム ライブラリ]** を選択します。 スタティック ランタイム ライブラリをデバッグする場合は **/MTd** を、スタティック ランタイム ライブラリをリリースする場合は **/MT** を選択します。

   f. **[リンカー]**  >  **[システム]** の順に展開します。 **[サブシステム]** が **[コンソール]** に設定されていることを確認します。

   g. **[OK]** を選んで、プロパティ ページを閉じます。

## <a name="add-include-directives"></a>インクルード ディレクティブを追加する

1. テストの *.cpp* ファイルで、必要な `#include` ディレクティブを追加して、プログラムの型と関数がテスト コードに認識されるようにします。 通常、プログラムはフォルダー階層で 1 つ上のレベルです。 「`#include "../"`」と入力すると IntelliSense ウィンドウが表示され、ヘッダー ファイルへの完全パスを選択できます。

   ![#include ディレクティブを追加する](media/cpp-gtest-includes.png)

   次のようにすると、スタンドアロン ライブラリを使うことができます。

   ```cpp
   #include <boost/test/unit_test.hpp>
   ```

   または、次のようにすると、単一ヘッダー バージョンを使うことができます。

   ```cpp
   #include <boost/test/included/unit_test.hpp>
   ```

   次に、`BOOST_TEST_MODULE` を定義します。

テストが**テスト エクスプローラー**で検出されるのに十分な例を次に示します。

```cpp
#define BOOST_TEST_MODULE MyTest
#include <boost/test/included/unit_test.hpp\> //single-header
#include "../MyProgram/MyClass.h" // project being tested
#include <string>

BOOST_AUTO_TEST_CASE(my_boost_test)
{
    std::string expected_value = "Bill";

    // assume MyClass is defined in MyClass.h
    // and get_value() has public accessibility
    MyClass mc;
    BOOST_CHECK(expected_value == mc.get_value());
}
```

## <a name="write-and-run-tests"></a>テストを作成して実行する

Boost テストを作成して実行する準備が整いました。 テスト マクロについては、[Boost Test ライブラリのドキュメント](https://www.boost.org/doc/libs/1_71_0/libs/test/doc/html/index.html)をご覧ください。 **テスト エクスプローラー**を使ってテストを検出、実行、グループ化する方法については、「[テスト エクスプローラーを使用して単体テストを実行する](run-unit-tests-with-test-explorer.md)」をご覧ください。

## <a name="see-also"></a>関連項目

- [C/C++ 用の単体テストの記述](writing-unit-tests-for-c-cpp.md)
