---
title: Python 用の C++ 拡張機能の記述
description: 混合モードのデバッグなど、Visual Studio、CPython、PyBind11 を使用して Python 用の C++ 拡張機能を作成するチュートリアルです。
ms.date: 05/11/2021
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: 866b588b8b46477b397cda92076780d1955cfa83
ms.sourcegitcommit: 9cb0097c33755a3e5cbadde3b0a6e9e76cee727d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/13/2021
ms.locfileid: "109848306"
---
# <a name="create-a-c-extension-for-python"></a>Python 用 C++ 拡張機能の作成

Python インタープリターの機能を拡張するため、およびオペレーティング システムの低レベル機能にアクセスするためには、C++ (または C) で記述されたモジュールがよく使われます。 モジュールの主要な種類は次の 3 つです。

- アクセラレータ モジュール: Python はインタープリター言語であるため、コードの特定の部分を C++ で書くことによってパフォーマンスを向上させることができます。
- ラッパー モジュール: 既存の C/C++ インターフェイスを Python コードに公開します。または、Python から使いやすい、より "Python らしい" API を公開します。
- 低レベル システム アクセス モジュール: `CPython` ランタイム、オペレーティング システム、または基盤ハードウェアの低レベル機能にアクセスするために作成します。

この記事では、双曲正接を計算する `CPython` 用の C++ 拡張モジュールを作成し、Python コードからそれを呼び出す手順について説明します。 Python では最初にルーチンを実装して、C++ で同じルーチンを実装した場合の相対的なパフォーマンス向上を示します。

この記事では、Python で C++ を使用できるようにする 2 つの方法も示します。

- [Python のドキュメント](https://docs.python.org/3/c-api/)で説明されている標準の `CPython` 拡張機能
- その簡潔さから C++ 11 に推奨される [PyBind11](https://github.com/pybind/pybind11)

このチュートリアルで使われているサンプルの完全版は [python-samples-vs-cpp-extension](https://github.com/Microsoft/python-sample-vs-cpp-extension) (GitHub) にあります。

## <a name="prerequisites"></a>前提条件

- **Python ネイティブ開発ツール** (これによりネイティブ拡張機能に必要な C++ ワークロードとツールセットが提供されます) を含む、**Python 開発** ワークロードがインストールされた Visual Studio 2017 以降。

    ![[Python ネイティブ開発ツール] オプションの選択](media/cpp-install-native.png)

    > [!Tip]
    > **データ サイエンスと分析アプリケーション** ワークロードをインストールすることでも、Python と **Python ネイティブ開発ツール** オプションが既定で含まれます。

インストール オプションの詳細については、[Visual Studio 用の Python サポートのインストール](installing-python-support-in-visual-studio.md)に関するページを参照してください。 Python を別個にインストールする場合は、そのインストーラーの **[詳細オプション]** で **[Download debugging symbols]\(デバッグ シンボルのダウンロード\)** を必ず選択してください。 このオプションは、Python コードとネイティブ コードの間で混合モードのデバッグを使用する場合に必要です。

## <a name="create-the-python-application"></a>Python アプリケーションを作成する

1. Visual Studio で **[ファイル]**  >  **[新規]**  >  **[プロジェクト]** の順に選択して、新しい Python プロジェクトを作成します。 "Python" と検索して **Python アプリケーション** テンプレートを選択し、任意の名前と場所を指定して、 **[OK]** を選択します。

1. プロジェクトの *.py* ファイルに、次のコードを貼り付けます (または、[Python の編集機能](editing-python-code-in-visual-studio.md)の一部を体験するために手動で入力します)。 このコードでは、数値演算ライブラリを使用せずに双曲線正接が計算されます。このコードは、ネイティブ拡張機能を使用して高速化する対象です。

    > [!Tip]
    > C++ で書き換える前に、純粋な Python でコードを記述します。 このようにすることで、ネイティブ コードが正しいかどうかをより簡単に確認できます。

    ```python
    from random import random
    from time import perf_counter

    COUNT = 500000  # Change this value depending on the speed of your computer
    DATA = [(random() - 0.5) * 3 for _ in range(COUNT)]

    e = 2.7182818284590452353602874713527

    def sinh(x):
        return (1 - (e ** (-2 * x))) / (2 * (e ** -x))

    def cosh(x):
        return (1 + (e ** (-2 * x))) / (2 * (e ** -x))

    def tanh(x):
        tanh_x = sinh(x) / cosh(x)
        return tanh_x

    def test(fn, name):
        start = perf_counter()
        result = fn(DATA)
        duration = perf_counter() - start
        print('{} took {:.3f} seconds\n\n'.format(name, duration))

        for d in result:
            assert -1 <= d <= 1, " incorrect values"

    if __name__ == "__main__":
        print('Running benchmarks with COUNT = {}'.format(COUNT))

        test(lambda d: [tanh(x) for x in d], '[tanh(x) for x in d] (Python implementation)')
    ```

1. **[デバッグ]**  >  **[デバッグなしで開始]** (**Ctrl**+**F5** キー) を使ってプログラムを実行し、結果を確認します。 `COUNT` 変数を調整して、ベンチマークの実行にかかる時間を変更することができます。 このチュートリアルの目的は、ベンチマークの所要時間を約 2 秒にするように、カウントを設定することです。

> [!TIP]
> ベンチマークを実行する場合は、常に **[デバッグ]**  >  **[デバッグなしで開始]** を使用して、Visual Studio デバッガー内でコードを実行するときに発生するオーバーヘッドを回避します。

## <a name="create-the-core-c-projects"></a>C++ のコア プロジェクトを作成する

"superfastcode"と"superfastcode2"という 2 つの同じ C++ プロジェクトを作成するには、このセクションの手順に従います。 後で、各プロジェクトで 2 種類の方法を使用して C++ コードを Python に公開します。

1. **ソリューション エクスプローラー** で、ソリューションを右クリックし、**[追加]** > **[新しいプロジェクト]** の順に選択します。 Visual Studio ソリューションには、Python プロジェクトと C++ プロジェクトの両方を含めることができます (これは Visual Studio for Python 使用の利点の 1 つです)。

1. "C++" を検索し、**[空のプロジェクト]** を選択し、"superfastcode" という名前 (2 番目のプロジェクトには "superfastcode2") を指定して **[OK]** を選択します。

    > [!Tip]
    > Visual Studio で **Python ネイティブ開発ツール** をインストールしたので、代わりに **Python 拡張モジュール** から始めることができます。このテンプレートには、以下で説明するものの多くが既に配置されています。 ただし、このチュートリアルでは、拡張モジュールの作成手順を実際に示すため、空のプロジェクトから始めます。 プロセスを理解したら、独自の拡張を記述するとき、テンプレートで時間が節約されます。

1. **[ソース ファイル]** ノードを右クリックして **[追加]** > **[新しい項目]** の順に選択し、**[C++ ファイル]** を選択して `module.cpp` という名前を付け、**[OK]** を選択し、新しいプロジェクトに C++ ファイルを作成します。

    > [!Important]
    > 後続の手順で C++ プロパティ ページを有効にするには、*.cpp* 拡張子を持つファイルが必要です。

1. 64 ビットの Python ランタイムを使用する場合は、メイン ツールバーのドロップダウンメ ニューを使用して **x64** 構成をアクティブにします。 32 ビットの Python ランタイムの場合は、**Win32** 構成をアクティブにします。

1. **ソリューション エクスプローラー** で C++ プロジェクトを右クリックして、**[プロパティ]** を選択します。 **[構成]** の値は **[アクティブ (デバッグ)]** にする必要があり、 **[プラットフォーム]** は、前の手順の選択に基づき **[アクティブ (x64)]** または **[アクティブ (Win32)]** にします。

    > [!Tip]
    > 独自のプロジェクトの場合、デバッグとリリースの構成を両方とも構成することが望ましいです。 ここでは、デバッグ構成のみ行い、`CPython` の "*リリース*" ビルドを使用するようにその構成を設定します。これにより、アサーションなど、C++ ランタイムの一部のデバッグ機能が無効になります。 `CPython` の "*デバッグ*" バイナリ (`python_d.exe`) を使用する場合は、異なる設定が必要になります。

1. 次の表に示すように、特定のプロパティを設定し、**[OK]** を選択します。
    ::: moniker range=">=vs-2019"
    | タブ | プロパティ | 値 |
    | --- | --- | --- |
    | **全般** | **[全般]** > **[ターゲット名]** | `from...import` ステートメントで Python からモジュールを参照するときのモジュール名を指定します。 この名前は、Python のモジュールを定義するときに C++ でも使用します。 プロジェクトの名前をモジュール名として使用する場合は、既定値の **$(ProjectName)** のままにしておきます。 |
    | | **詳細** > **ターゲット ファイル拡張子** | **.pyd** |
    | | **[プロジェクトの既定値]** > **[構成の種類]** | **ダイナミック ライブラリ (.dll)** |
    | **[C/C++]** > **[全般]** | **追加のインクルード ディレクトリ** | インストールに合わせて Python の *include* フォルダーを追加します (例: `c:\Python36\include`)。  |
    | **[C/C++]** > **[プリプロセッサ]** | **プリプロセッサの定義** | **CPython のみ**: 文字列の先頭に `Py_LIMITED_API;` (セミコロンを含む) を追加します。 この定義により、Python から呼び出すことができる一部の関数を制限し、Python の異なるバージョン間でのコードの移植性を高くします。 PyBind11 を使用している場合は、この定義を追加しないでください。追加すると、ビルド エラーが発生します。 |
    | **[C/C++]** > **[コード生成]** | **ランタイム ライブラリ** | **マルチスレッド DLL (/MD)** (下記の「警告」を参照) |
    | **[リンカー]** > **[全般]** | **追加のライブラリ ディレクトリ** | インストールに合わせて、*.lib* ファイルが含まれる Python の *libs* フォルダーを追加します (例: `c:\Python36\libs`)。 (*.py* ファイルが含まれる *Lib* フォルダー *ではなく*、*.lib* ファイルが含まれる *libs* フォルダーを必ず指定してください)。 |
    ::: moniker-end
    ::: moniker range="=vs-2017"
    | タブ | プロパティ | 値 |
    | --- | --- | --- |
    | **全般** | **[全般]** > **[ターゲット名]** | `from...import` ステートメントで Python からモジュールを参照するときのモジュール名を指定します。 この名前は、Python のモジュールを定義するときに C++ でも使用します。 プロジェクトの名前をモジュール名として使用する場合は、既定値の **$(ProjectName)** のままにしておきます。 `python_d.exe` では、名前の末尾に `_d` を追加します。 |
    | | **[全般]** > **[ターゲットの拡張子]** | **.pyd** |
    | | **[プロジェクトの既定値]** > **[構成の種類]** | **ダイナミック ライブラリ (.dll)** |
    | **[C/C++]** > **[全般]** | **追加のインクルード ディレクトリ** | インストールに合わせて Python の *include* フォルダーを追加します (例: `c:\Python36\include`)。  |
    | **[C/C++]** > **[プリプロセッサ]** | **プリプロセッサの定義** | **_DEBUG** 値を **NDEBUG** に変更して、`CPython` の非デバッグ バージョンに一致させます (存在する場合)。 (`python_d.exe` を使用する場合、これは変更せずそのままにします。) |
    | **[C/C++]** > **[コード生成]** | **ランタイム ライブラリ** | `CPython` の非デバッグ バージョンに一致する **[マルチスレッド DLL (/MD)]** 。 (`python_d.exe` を使用する場合、これは変更せずそのままにします。) |
    | **[リンカー]** > **[全般]** | **追加のライブラリ ディレクトリ** | インストールに合わせて、*.lib* ファイルが含まれる Python の *libs* フォルダーを追加します (例: `c:\Python36\libs`)。 (*.py* ファイルが含まれる *Lib* フォルダー *ではなく*、*.lib* ファイルが含まれる *libs* フォルダーを必ず指定してください)。 |
    ::: moniker-end
    
    > [!Tip]
    > プロジェクトのプロパティに [C/C++] タブが表示されない場合は、C/C++ ソース ファイルとして識別されるファイルがプロジェクトに含まれないためです。 このような条件は、*.c* または *.cpp* 拡張子を付けずにソース ファイルを作成すると発生する可能性があります。 たとえば、前の新しい項目のダイアログで「`module.cpp`」ではなく誤って「`module.coo`」と入力した場合、Visual Studio ではこのファイルを作成しますが、ファイルの種類が C/C++ のプロパティ タブをアクティブにする種類である [C/C+ コード] に設定されません。このような誤った識別は、このファイルの名前を `.cpp` に変更した場合でもそのままになります。 ファイルの種類を正しく設定するには、**ソリューション エクスプローラー** でファイルを右クリックして **[プロパティ]** を選び、 **[ファイルの種類]** を **[C/C++ コード]** に設定します。

1. C++ プロジェクトを右クリックし、 **[ビルド]** を選んで構成をテストします (**デバッグ** と **リリース** の両方)。 *.pyd* ファイルは、C++ のプロジェクト フォルダー自体ではなく、**Debug** および **Release** の下の **solution** フォルダーにあります。

1. C++ プロジェクトの *module.cpp* ファイルに、次のコードを追加します。

    ```cpp
    #include <Windows.h>
    #include <cmath>

    const double e = 2.7182818284590452353602874713527;

    double sinh_impl(double x) {
        return (1 - pow(e, (-2 * x))) / (2 * pow(e, -x));
    }

    double cosh_impl(double x) {
        return (1 + pow(e, (-2 * x))) / (2 * pow(e, -x));
    }

    double tanh_impl(double x) {
        return sinh_impl(x) / cosh_impl(x);
    }
    ```

1. C++ プロジェクトを再度ビルドし、コードが正しいことを確認します。

1. まだ行っていない場合は、上記の手順を繰り返して、同じコンテンツを持つ "superfastcode2" という名前の 2 番目のプロジェクトを作成します。

## <a name="convert-the-c-projects-to-extensions-for-python"></a>C++ プロジェクトを Python の拡張機能に変換する

C++ DLL を Python の拡張機能にするには、まず Python の型と対話するようにエクスポートしたメソッドを変更します。 その後、モジュールのメソッドの定義と共に、モジュールをエクスポートする関数を追加します。

次のセクションでは、`CPython` の拡張機能と PyBind11 の両方を使用してこれらの手順を実行する方法について説明します。

### <a name="cpython-extensions"></a>CPython の拡張機能

このセクションの内容の詳しい背景については、python.org の「[Python/C API リファレンスマニュアル](https://docs.python.org/3/c-api/index.html)」を参照してください。特に、「[モジュール オブジェクト](https://docs.python.org/3/c-api/module.html)」を参照してください (正しいドキュメントを表示するために、右上にあるドロップダウン コントロールからお使いのバージョンの Python を必ず選択してください)。

1. *module.cpp* の上部で、*Python.h* を含めます。

    ```cpp
    #include <Python.h>
    ```

1. Python の型 (つまり `PyObject*`) を受け付けて戻すように、`tanh_impl` メソッドを変更します。

    ```cpp
    PyObject* tanh_impl(PyObject* /* unused module reference */, PyObject* o) {
        double x = PyFloat_AsDouble(o);
        double tanh_x = sinh_impl(x) / cosh_impl(x);
        return PyFloat_FromDouble(tanh_x);
    }
    ```

1. Python に対して C++ の `tanh_impl` 関数を提示する方法を定義する構造体を追加します。

    ```cpp
    static PyMethodDef superfastcode_methods[] = {
        // The first property is the name exposed to Python, fast_tanh
        // The second is the C++ function with the implementation
        // METH_O means it takes a single PyObject argument
        { "fast_tanh", (PyCFunction)tanh_impl, METH_O, nullptr },

        // Terminate the array with an object containing nulls.
        { nullptr, nullptr, 0, nullptr }
    };
    ```

1. Python コードで参照するモジュールを定義する構造体を追加します。特に、`from...import` ステートメントを利用するタイミングを定義します。 (これを **[構成プロパティ]**  >  **[全般]**  >  **[ターゲット名]** にあるプロジェクト プロパティの値と一致するようにします)。次の例では、`fast_tanh` が `superfastcode_methods` 内で定義されているため、"superfastcode" のモジュール名は Python で `from superfastcode import fast_tanh` を使用できることを示します。 (*module.cpp* などの、C++ プロジェクト内部のファイル名は重要ではありません)。

    ```cpp
    static PyModuleDef superfastcode_module = {
        PyModuleDef_HEAD_INIT,
        "superfastcode",                        // Module name to use with Python import statements
        "Provides some functions, but faster",  // Module description
        0,
        superfastcode_methods                   // Structure that defines the methods of the module
    };
    ```

1. モジュールを読み込むときに Python が呼び出すメソッドを追加します。`PyInit_<module-name>` という名前にする必要があります。&lt;module_name&gt; は、C++ プロジェクトの **[全般]**  >  **[ターゲット名]** プロパティと正確に一致します (つまり、プロジェクトによってビルドされる *.pyd* のファイル名と一致します)。

    ```cpp
    PyMODINIT_FUNC PyInit_superfastcode() {
        return PyModule_Create(&superfastcode_module);
    }
    ```

1. もう一度 C++ プロジェクトをビルドして、コードを検証します。 エラーが発生した場合は、以下の「[トラブルシューティング](#troubleshooting)」セクションをご覧ください。

### <a name="pybind11"></a>PyBind11

前のセクションの手順を完了すると、C++ コードに必要なモジュール構造を作成するために多数の定型コードを使用したことに気付きます。 PyBind11 は、はるかに少ないコードで同じ結果を実現する C++ ヘッダー ファイルのマクロを使用してプロセスを簡略化します。 このセクションに表示される内容の背景については、[PyBind11 の基本](https://github.com/pybind/pybind11/blob/master/docs/basics.rst) (github.com) を参照してください。

1. pip (`pip install pybind11` または `py -m pip install pybind11`) を使用して PyBind11 をインストールします。 (または、[Python 環境] ウィンドウでインストールして、次の手順のために "Powershell で開く" コマンドを使用できます。)

1. 同じターミナルで `python -m pybind11 --includes` または `py -m pybind11 --includes` を実行します。 これにより、プロジェクトの **[C/C++]**  >  **[全般]**  >  **[追加のインクルード ディレクトリ]** プロパティに追加する必要があるパスの一覧が出力されます (`-I` プレフィックスが存在する場合、削除してください)。

1. 前のセクションの変更が含まれていない新しい *module.cpp* の上部に、*pybind11.h* を組み込みます。

    ```cpp
    #include <pybind11/pybind11.h>
    ```

1. *module.cpp* の下部で、`PYBIND11_MODULE` マクロを使用して C++ 関数にエントリ ポイントを定義します。

    ```cpp
    namespace py = pybind11;

    PYBIND11_MODULE(superfastcode2, m) {
        m.def("fast_tanh2", &tanh_impl, R"pbdoc(
            Compute a hyperbolic tangent of a single argument expressed in radians.
        )pbdoc");

    #ifdef VERSION_INFO
        m.attr("__version__") = VERSION_INFO;
    #else
        m.attr("__version__") = "dev";
    #endif
    }
    ```

1. C++ プロジェクトをビルドして、コードを検証します。 エラーが発生した場合は、次のトラブルシューティングをご覧ください。

### <a name="troubleshooting"></a>トラブルシューティング

C++ モジュールは、次の理由でコンパイルに失敗する場合があります。

- *Python.h* が見つからない (**E1696: ソース ファイル "Python.h" を開けません** や **C1083: インクルード ファイルを開けません: "Python.h": このようなファイルまたはディレクトリはありません**): プロジェクトのプロパティの **[C/C++]** > **[全般]** > **[追加のインクルード ディレクトリ]** のパスが Python インストールの *include* フォルダーに設定されていることを確認してください。 「[C++ のコア プロジェクトを作成する](#create-the-core-c-projects)」の手順 6 をご覧ください。

- Python ライブラリが見つかりません: プロジェクトのプロパティの **[リンカー]**  >  **[全般]**  >  **[追加のライブラリ ディレクトリ]** のパスが、Python インストールの *libs* フォルダーを指していることを確認します。 「[C++ のコア プロジェクトを作成する](#create-the-core-c-projects)」の手順 6 をご覧ください。

- ターゲット アーキテクチャに関連するリンカー エラー: C++ プロジェクトのターゲット アーキテクチャを、Python インストールのアーキテクチャと一致するように変更します。 たとえば、C++ プロジェクトで **Win32** をターゲットとする一方で、Python インストールが 64 ビットの場合は、C++ プロジェクトを **x64** に変更します。

## <a name="test-the-code-and-compare-the-results"></a>コードをテストして結果を比較する

これで、Python 拡張機能の構造の DLL ができたので、Python プロジェクトからそれらを参照し、モジュールをインポートして、それらのメソッドを使うことができます。

### <a name="make-the-dll-available-to-python"></a>Python で DLL を使用できるようする

Python で DLL を使えるようにするには 2 つの方法があります。

Python プロジェクトと C++ プロジェクトが同じソリューション内にある場合は、1 つ目の方法を使用します。 **ソリューション エクスプローラー** に移動し、Python プロジェクト内の **[参照設定]** ノードを右クリックし、 **[参照の追加]** をクリックします。 表示されるダイアログで **[プロジェクト]** タブを選択し、**superfastcode** プロジェクトと **superfastcode2** プロジェクトの両方を選択し、**[OK]** を選択します。

![superfastcode プロジェクトに参照を追加する](media/cpp-add-reference.png)

次の手順で説明する別の方法では、Python 環境にモジュールをインストールし、他の Python プロジェクトでも使えるようにします。 詳細なドキュメントについては、[**setuptools** プロジェクト](https://setuptools.readthedocs.io/)に関するページを参照してください。

1. プロジェクトを右クリックし、**[追加]** > **[新しい項目]** を選択して、C++ プロジェクトに *setup.py* という名前のファイルを作成します。 次に、**C++ File (.cpp)** を選択し、ファイルに `setup.py` という名前を付け、**[OK]** を選択します (*.py* 拡張子を使用してファイルに名前を付けることで、C++ ファイル テンプレートを使用していても、Visual Studio でそのファイルが Python として認識されるようにします)。 ファイルがエディターに表示されたら、拡張メソッドに応じて、そこに次のコードを貼り付けます。

    **`CPython` 拡張機能 (superfastcode プロジェクト):**

    ```python
    from setuptools import setup, Extension

    sfc_module = Extension('superfastcode', sources = ['module.cpp'])

    setup(
        name='superfastcode',
        version='1.0',
        description='Python Package with superfastcode C++ extension',
        ext_modules=[sfc_module]
    )
    ```

    **`PyBind11` (superfastcode2 プロジェクト):**

    ```python
    from setuptools import setup, Extension
    import pybind11

    cpp_args = ['-std=c++11', '-stdlib=libc++', '-mmacosx-version-min=10.7']

    sfc_module = Extension(
        'superfastcode2',
        sources=['module.cpp'],
        include_dirs=[pybind11.get_include()],
        language='c++',
        extra_compile_args=cpp_args,
        )

    setup(
        name='superfastcode2',
        version='1.0',
        description='Python package with superfastcode2 C++ extension (PyBind11)',
        ext_modules=[sfc_module],
    )
    ```

1. C++ プロジェクトで、*pyproject.toml* という名前の 2 番目のファイルを作成し、次のコードを貼り付けます。

    ```toml
    [build-system]
    requires = ["setuptools", "wheel", "pybind11"]
    build-backend = "setuptools.build_meta"
    ```

1. 拡張機能をビルドするために、開いている *pyproject.toml* タブを右クリックし、[完全なパスのコピー] を選択します (*pyproject.toml* 名は、使用前にパスから削除します)。

1. ソリューション エクスプローラーで、アクティブな Python 環境を右クリックし、 *[Python パッケージの管理]* を選択します。

    > [!Tip]
    > パッケージが既にインストールされている場合は、一覧内に表示されます。 続行する前に、[X] をクリックしてアンインストールします。

1. コピーしたパスを検索ボックスに貼り付け、末尾から `pyproject.toml` を削除します。 Enter キーを押して、そのディレクトリからインストールを行います。

    > [!Tip]
    > アクセス許可のエラーによってインストールが失敗した場合は、`--user` を追加し、コマンドを再試行します。


### <a name="call-the-dll-from-python"></a>Python から DLL を呼び出す

前のセクションで説明したように、Python で DLL を使用できるようにすると、Python コードから `superfastcode.fast_tanh` 関数と `superfastcode2.fast_tanh2` 関数を呼び出して、それらのパフォーマンスを Python の実装と比較できるようになります。

1. 次の行を *.py* ファイルに追加して、DLL からエクスポートされたメソッドを呼び出してその出力を表示します。

    ```python
    from superfastcode import fast_tanh
    test(lambda d: [fast_tanh(x) for x in d], '[fast_tanh(x) for x in d] (CPython C++ extension)')

    from superfastcode2 import fast_tanh2
    test(lambda d: [fast_tanh2(x) for x in d], '[fast_tanh2(x) for x in d] (PyBind11 C++ extension)')
    ```

1. Python プログラムを実行 ( **[デバッグ]**  >  **[デバッグなしで開始]** または **Ctrl**+**F5** キー) し、Python の実装よりも約 5 から 20 倍高速で C++ のルーチンが実行されることを確認します。 通常、次のような出力が表示されます。

    ```output
    Running benchmarks with COUNT = 500000
    [tanh(x) for x in d] (Python implementation) took 0.758 seconds

    [fast_tanh(x) for x in d] (CPython C++ extension) took 0.076 seconds

    [fast_tanh2(x) for x in d] (PyBind11 C++ extension) took 0.204 seconds
    ```

    **[デバッグなしで開始]** コマンドが無効な場合、**ソリューション エクスプローラー** で Python プロジェクトを右クリックして、 **[スタートアップ プロジェクトに設定]** を選択します。

1. 違いがより顕著になるように `COUNT` 変数を増やしてみてください。 また、C++ モジュールの **デバッグ** ビルドの実行は、**リリース** ビルドよりも低速になります。これは、**デバッグ** ビルドが十分に最適化されず、さまざまなエラー チェックが含まれるためです。 比較のために、これらの構成を自由に切り替えることができます (ただし、必ず前に戻って、**リリース** 構成の前のプロパティを更新してください)。

出力で、PyBind11 拡張機能が `CPython` 拡張機能ほど高速ではないものの、純粋な Python 実装よりも大幅に高速であることが確認できます。 この違いの主な原因は、複数のパラメーター、パラメーター名、またはキーワード引数をサポートしていない `METH_O` 呼び出しを使用したことです。 PyBind11 は、より Python に類似したインターフェイスを呼び出し元に提供するために、少し複雑なコードを生成しますが、テスト コードで関数が 50 万回呼び出されるため、結果的にオーバーヘッドが大幅に増加する可能性があります。

`for` ループをネイティブ コードに移動することで、オーバーヘッドをさらに軽減できます。 これには、各要素を処理するための[反復子プロトコル](https://docs.python.org/c-api/iter.html) (または[関数パラメーター](https://pybind11.readthedocs.io/en/stable/advanced/functions.html#python-objects-as-args)用の PyBind11 の `py::iterable` 型) の使用が含まれます。 Python と C++ の間で繰り返される切り替えを削除することは、シーケンスの処理にかかる時間を短縮する効果的な方法です。

### <a name="troubleshooting"></a>トラブルシューティング

モジュールをインポートしようとしたときに `ImportError` が発生した場合、次のいずれかの問題が原因として考えられます。

* プロジェクト参照を使用してビルドする場合は、C++ プロジェクトのプロパティが、Python プロジェクトでアクティブになっている Python 環境と一致していることを確認します (特に Include および Library ディレクトリ)。

* 出力ファイルが `superfastcode.pyd` という名前であることを確認します。 別の名前または拡張機能を使用すると、インポートできません。

* *setup.py* ファイルを使用してモジュールをインストールした場合、Python プロジェクト用にアクティブ化された Python 環境で *pip* コマンドを実行したことを確認します。 ソリューション エクスプローラーで Python 環境を展開すると、`superfastcode` のエントリが表示されます。

## <a name="debug-the-c-code"></a>C++ コードをデバッグする

Visual Studio では、Python と C++ コードを一緒にデバッグすることをサポートしています。 このセクションでは、**superfastcode** プロジェクトを使用するプロセスについて説明します。この手順は、**superfastcode2** プロジェクトでも同じです。

1. **ソリューション エクスプローラー** で Python プロジェクトを右クリックして、**[プロパティ]** の **[デバッグ]** タブを選び、**[デバッグ]** > **[ネイティブ コードのデバッグを有効にする]** オプションをオンにします。

    > [!Tip]
    > ネイティブ コードのデバッグを有効にすると、プログラムが通常の **[続行するには、任意のキーを押してください]** で一時停止せずに完了した場合に、Python の出力ウィンドウがすぐに消えることがあります。 強制的に一時停止するには、ネイティブ コードのデバッグを有効にするときに、 **[デバッグ]** タブの **[実行]**  >  **[インタープリターの引数]** フィールドに、`-i` オプションを追加します。 この引数を使用すると、Python インタープリターはコード終了後に対話モードになり、この時点でユーザーが **Ctrl**+**Z** > **Enter** キーを押して終了するのを待機します。 (または、Python コードを変更してもよい場合は、プログラムの最後に `import os` および `os.system("pause")` ステートメントを追加します。 このコードで、元の一時停止プロンプトが複製されます)。

1. **[ファイル]**  >  **[保存]** を選択して、プロパティの変更を保存します。

1. Visual Studio ツールバーで、ビルド構成を **[デバッグ]** に設定します。

    ![ビルド構成を [デバッグ] に設定する](media/cpp-set-debug.png)

1. 通常デバッガーでコードを実行するとより時間がかかるため、*.py* ファイルの `COUNT` 変数を約 5 倍小さい値 (たとえば、`500000` から `100000`) に変更できます。

1. C++ コードで `tanh_impl` メソッドの先頭行にブレークポイントを設定して、(**F5** キーを押すか、**[デバッグ]** > **[デバッグの開始]** の順に選択して) デバッガーを開始します。 そのコードが呼び出されるとデバッガーが停止します。 ブレークポイントがヒットしない場合は、構成が **[デバッグ]** に設定されていること、およびプロジェクトを保存していること (これはデバッガーの開始時に自動的に行われません) を確認します。

    ![C++ コードのブレークポイントでの停止](media/cpp-debugging.png)

1. この時点で、C++ コードをステップ実行したり、変数を調べたりできます。 これらの機能の詳細については、「[Python と C++ を同時にデバッグする](debugging-mixed-mode-c-cpp-python-in-visual-studio.md)」をご覧ください。

## <a name="alternative-approaches"></a>他の方法

次の表で説明するように、Python の拡張機能を作成するにはさまざまな方法があります。 `CPython` と `PyBind11` の最初の 2 つのエントリは、この記事で既に説明しています。

| アプローチ | Vintage | 代表的ユーザー | 
| --- | --- | --- |
| `CPython` 用の C/C++ 拡張モジュール | 1991 | 標準ライブラリ | 
| [PyBind11](https://github.com/pybind/pybind11) (C++ 向けに推奨) | 2015 |  |
| [Cython](https://cython.org) (C 向けに推奨) | 2007 | [gevent](https://www.gevent.org/)、[kivy](https://kivy.org/) |
| [HPy](https://hpyproject.org/) | 2019 | |
| [mypyc](https://mypyc.readthedocs.io/) | 2017 | |
| ctypes | 2003 | [oscrypto](https://github.com/wbond/oscrypto) | 
| cffi | 2013 | [cryptography](https://cryptography.io/)、[pypy](https://pypy.org/) |
| SWIG | 1996 | [crfsuite](http://www.chokkan.org/software/crfsuite/) | 
| [Boost.Python](https://www.boost.org/doc/libs/1_66_0/libs/python/doc/html/index.html) | 2002 | |
| [cppyy](https://cppyy.readthedocs.io/) | 2017 | |

## <a name="see-also"></a>こちらもご覧ください

このチュートリアルで使われているサンプルの完全版は [python-samples-vs-cpp-extension](https://github.com/Microsoft/python-sample-vs-cpp-extension) (GitHub) にあります。
