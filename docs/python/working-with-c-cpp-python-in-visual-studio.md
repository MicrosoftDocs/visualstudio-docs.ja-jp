---
title: Python 用の C++ 拡張機能の記述
description: 混合モードのデバッグなど、Visual Studio、CPython、PyBind11 を使用して Python 用の C++ 拡張機能を作成するチュートリアルです。
ms.date: 11/19/2018
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: df3d32bfedfc730b8fae0837ce0e48f50e6496f4
ms.sourcegitcommit: 925db7adb9cb554b081c7e727d09680d4863feed
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2021
ms.locfileid: "107941150"
---
# <a name="create-a-c-extension-for-python"></a>Python 用 C++ 拡張機能の作成

Python インタープリターの機能を拡張するため、およびオペレーティング システムの低レベル機能にアクセスするためには、C++ (または C) で記述されたモジュールがよく使われます。 モジュールの主要な種類は次の 3 つです。

- アクセラレータ モジュール: Python はインタープリター言語であるため、コードの特定の部分を C++ で書くことによってパフォーマンスを向上させることができます。
- ラッパー モジュール: 既存の C/C++ インターフェイスを Python コードに公開します。または、Python から使いやすい、より "Python らしい" API を公開します。
- 低レベル システム アクセス モジュール: CPython ランタイム、オペレーティング システム、または基盤ハードウェアの低レベル機能にアクセスするために作成します。

この記事では、双曲正接を計算する CPython 用の C++ 拡張モジュールを作成し、Python コードからそれを呼び出す手順について説明します。 Python では最初にルーチンを実装して、C++ で同じルーチンを実装した場合の相対的なパフォーマンス向上を示します。

この記事では、Python で C++ を使用できるようにする 2 つの方法も示します。

- [Python のドキュメント](https://docs.python.org/3/c-api/)で説明されている標準の CPython 拡張機能
- その簡潔さから C++ 11 に推奨される [PyBind11](https://github.com/pybind/pybind11)

これらの方法と他の方法の比較については、この記事の最後にある「[別の方法](#alternative-approaches)」をご覧ください。

このチュートリアルで使われているサンプルの完全版は [python-samples-vs-cpp-extension](https://github.com/Microsoft/python-sample-vs-cpp-extension) (GitHub) にあります。

## <a name="prerequisites"></a>前提条件

- **C++ によるデスクトップ開発** と **Python 開発** ワークロードの両方を備えた Visual Studio 2017 以降が既定のオプションでインストールされます。
- **Python 開発** ワークロードでは、**[Python ネイティブ開発ツール]** の横のボックスもオンにします。 このオプションによって、この記事で説明するほとんどの構成が設定されます。 (このオプションには、C++ のワークロードも自動的に含まれます)。

    ![[Python ネイティブ開発ツール] オプションの選択](media/cpp-install-native.png)

    > [!Tip]
    > **データ サイエンスと分析アプリケーション** ワークロードをインストールすることでも、Python と **Python ネイティブ開発ツール** オプションが既定で含まれます。

他のバージョンの Visual Studio の使用など、詳細については [Visual Studio 用の Python サポートのインストール](installing-python-support-in-visual-studio.md)に関する記事をご覧ください。 Python を別にインストールする場合は、インストーラーで **[詳細オプション]** の **[Download debugging symbols (デバッグ シンボルのダウンロード)]** と **[Download debug binaries (デバッグ バイナリのダウンロード)]** を必ず選んでください。 このオプションを選択すると、デバッグ ビルドを行う場合に、必要なデバッグ ライブラリを確実に使用できます。

## <a name="create-the-python-application"></a>Python アプリケーションを作成する

1. Visual Studio で **[ファイル]**  >  **[新規]**  >  **[プロジェクト]** の順に選択して、新しい Python プロジェクトを作成します。 "Python" を検索し、**Python アプリケーション** テンプレートを選択し、適切な名前と場所を指定し、**[OK]** を選択します。

1. C++ を使用するには、32 ビットの Python インタープリターを使用する必要があります (Python 3.6 以降を推奨)。 Visual Studio の **[ソリューション エクスプローラー]** ウィンドウに、プロジェクト ノードを展開し、**[Python 環境]** ノードを展開します。 (太字または **グローバル デフォルト** ラベルで) 既定として 32 ビット環境が表示されない場合、[プロジェクト用の Python 環境の選択](selecting-a-python-environment-for-a-project.md)に関する記事の指示に従ってください。 32 ビット インタープリターをインストールしていない場合、「[Python インタープリターのインストール](installing-python-interpreters.md)」をご覧ください。

1. プロジェクトの *.py* ファイルに、双曲正接の計算をベンチマークする次のコードを貼り付けます (簡単に比較できるよう、数値演算ライブラリを使わずに実装されています)。 自由に手動でコードを入力し、[Python の編集機能](editing-python-code-in-visual-studio.md)を体験してください。

    ```python
    from itertools import islice
    from random import random
    from time import perf_counter

    COUNT = 500000  # Change this value depending on the speed of your computer
    DATA = list(islice(iter(lambda: (random() - 0.5) * 3.0, None), COUNT))

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

"superfastcode"と"superfastcode2"という 2 つの同じ C++ プロジェクトを作成するには、このセクションの手順に従います。 後で、各プロジェクトで別の手段を使用して C++ コードを Python に公開します。

1. `PYTHONHOME` 環境変数が使用する Python インタープリターに設定されていることを確認してください。 Visual Studio の C++ プロジェクトは、この変数に戻づいて、Python 拡張機能の作成時に使用される *python.h* などのファイルを見つけます。

1. **ソリューション エクスプローラー** で、ソリューションを右クリックし、**[追加]** > **[新しいプロジェクト]** の順に選択します。 Visual Studio ソリューションには、Python プロジェクトと C++ プロジェクトの両方を含めることができます (これは Visual Studio for Python 使用の利点の 1 つです)。

1. "C++" を検索し、**[空のプロジェクト]** を選択し、"superfastcode" という名前 (2 番目のプロジェクトには "superfastcode2") を指定して **[OK]** を選択します。

    > [!Tip]
    > Visual Studio で **Python ネイティブ開発ツール** をインストールしたので、代わりに **Python 拡張モジュール** から始めることができます。このテンプレートには、以下で説明するものの多くが既に配置されています。 ただし、このチュートリアルでは、拡張モジュールの作成手順を実際に示すため、空のプロジェクトから始めます。 プロセスを理解したら、独自の拡張を記述するとき、テンプレートで時間が節約されます。

1. **[ソース ファイル]** ノードを右クリックして **[追加]** > **[新しい項目]** の順に選択し、**[C++ ファイル]** を選択して `module.cpp` という名前を付け、**[OK]** を選択し、新しいプロジェクトに C++ ファイルを作成します。

    > [!Important]
    > 後続の手順で C++ プロパティ ページを有効にするには、*.cpp* 拡張子を持つファイルが必要です。

1. **ソリューション エクスプローラー** で C++ プロジェクトを右クリックして、**[プロパティ]** を選択します。

1. 表示される **[プロパティ ページ]** ダイアログ ボックスの上部で、**[構成]** を **[すべての構成]** に、**[プラットフォーム]** を **[Win32]** に設定します。

1. 次の表に示すように、特定のプロパティを設定し、**[OK]** を選択します。

    | タブ | プロパティ | 値 |
    | --- | --- | --- |
    | **全般** | **[全般]**  >  **[ターゲット名]** | `from...import` ステートメントで Python からモジュールを参照するときのモジュール名を指定します。 この名前は、Python のモジュールを定義するときに C++ でも使用します。 プロジェクトの名前をモジュール名として使用する場合は、既定値の **$(ProjectName)** のままにしておきます。 |
    | | **[全般]**  >  **[ターゲットの拡張子]** | **.pyd** |
    | | **[プロジェクトの既定値]**  >  **[構成の種類]** | **ダイナミック ライブラリ (.dll)** |
    | **[C/C++]**  >  **[全般]** | **追加のインクルード ディレクトリ** | インストールに合わせて Python の *include* フォルダーを追加します (例: `c:\Python36\include`)。  |
    | **[C/C++]**  >  **[プリプロセッサ]** | **プリプロセッサの定義** | **CPython のみ**: 文字列の先頭に `Py_LIMITED_API;` (セミコロンを含む) を追加します。 この定義により、Python から呼び出すことができる一部の関数を制限し、Python の異なるバージョン間でのコードの移植性を高くします。 PyBind11 を使用している場合は、この定義を追加しないでください。追加すると、ビルド エラーが発生します。 |
    | **[C/C++]**  >  **[コード生成]** | **ランタイム ライブラリ** | **マルチスレッド DLL (/MD)** (下記の「警告」を参照) |
    | **[リンカー]**  >  **[全般]** | **追加のライブラリ ディレクトリ** | インストールに合わせて、*.lib* ファイルが含まれる Python の *libs* フォルダーを追加します (例: `c:\Python36\libs`)。 (*.py* ファイルが含まれる *Lib* フォルダー *ではなく*、*.lib* ファイルが含まれる *libs* フォルダーを必ず指定してください)。 |

    > [!Tip]
    > プロジェクトのプロパティに [C/C++] タブが表示されない場合は、C/C++ ソース ファイルとして識別されるファイルがプロジェクトに含まれないためです。 このような条件は、*.c* または *.cpp* 拡張子を付けずにソース ファイルを作成すると発生する可能性があります。 たとえば、前の新しい項目のダイアログで「`module.cpp`」ではなく誤って「`module.coo`」と入力した場合、Visual Studio ではこのファイルを作成しますが、ファイルの種類が C/C++ のプロパティ タブをアクティブにする種類である [C/C+ コード] に設定されません。このような誤った識別は、このファイルの名前を `.cpp` に変更した場合でもそのままになります。 ファイルの種類を正しく設定するには、**ソリューション エクスプローラー** でファイルを右クリックして **[プロパティ]** を選び、 **[ファイルの種類]** を **[C/C++ コード]** に設定します。

    > [!Warning]
    > デバッグ構成の場合でも **[C/C++]**  >  **[コード生成]**  >  **[ランタイム ライブラリ]** のオプションを常に **マルチスレッド DLL (/MD)** に設定します。これは、この設定がデバッグ以外の Python バイナリのビルドに使用されるためです。 CPython では、 **[マルチスレッド デバッグ DLL (/MDd)]** オプションを設定した場合、 **[デバッグ]** 構成のビルドによって "**C1189: Py_LIMITED_API は Py_DEBUG、Py_TRACE_REFS、Py_REF_DEBUG と互換性がありません**" というエラーが発生します。 さらに、ビルド エラーを避けるために `Py_LIMITED_API` を削除すると (CPython では必要ですが、PyBind11 では不要)、モジュールをインポートしようとしたときに Python がクラッシュします (後で説明しますが、クラッシュは DLL の`PyModule_Create` の呼び出し内で発生し、出力メッセージは "**Fatal Python error: PyThreadState_Get: no current thread (Python 致命的エラー: PyThreadState_Get: 現在のスレッドがありません)**" です)。
    >
    > /MDd オプションは Python デバッグ バイナリ (*python_d.exe* など) のビルドに使われますが、拡張 DLL に対して選ぶと、やはり `Py_LIMITED_API` のビルド エラーになります。

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

次のセクションでは、CPython の拡張機能と PyBind11 の両方を使用してこれらの手順を実行する方法について説明します。

### <a name="cpython-extensions"></a>CPython の拡張機能

このセクションに登場する Python 3.x の機能の背景については、python.org の「[Python/C API リファレンスマニュアル](https://docs.python.org/3/c-api/index.html)」を参照してください。特に、「[モジュールオブジェクト](https://docs.python.org/3/c-api/module.html)」を参照してください。右上にあるドロップダウン コントロールから必ずお使いのバージョンの Python を選択すると該当文書が表示されます。

Python 2.7 を使用している場合は、代わりに python.org で [C や C++ による Python 2.7 の拡張](https://docs.python.org/2.7/extending/extending.html)に関するページや「[Python 3 への拡張モジュール移植](https://docs.python.org/2.7/howto/cporting.html)」を参照してください。

1. *module.cpp* の上部で、*Python.h* を含めます。

    ```cpp
    #include <Python.h>
    ```

1. Python の型 (つまり `PyObject*`) を受け付けて戻すように、`tanh_impl` メソッドを変更します。

    ```cpp
    PyObject* tanh_impl(PyObject *, PyObject* o) {
        double x = PyFloat_AsDouble(o);
        double tanh_x = sinh_impl(x) / cosh_impl(x);
        return PyFloat_FromDouble(tanh_x);
    }
    ```

1. Python に対して C++ の `tanh_impl` 関数を提示する方法を定義する構造体を追加します。

    ```cpp
    static PyMethodDef superfastcode_methods[] = {
        // The first property is the name exposed to Python, fast_tanh, the second is the C++
        // function name that contains the implementation.
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

1. ターゲットの構成を **リリース** に設定し、もう一度 C++ プロジェクトをビルドして、コードを検証します。 エラーが発生した場合は、以下の「[トラブルシューティング](#troubleshooting)」セクションをご覧ください。

### <a name="pybind11"></a>PyBind11

前のセクションの手順を完了すると、C++ コードに必要なモジュール構造を作成するために多数の定型コードを使用したことに気付きます。 PyBind11 は、はるかに少ないコードで同じ結果を実現する C++ ヘッダー ファイルのマクロを使用してプロセスを簡略化します。 このセクションに表示される内容の背景については、[PyBind11 の基本](https://github.com/pybind/pybind11/blob/master/docs/basics.rst) (github.com) を参照してください。

1. pip (`pip install pybind11` または `py -m pip install pybind11`) を使用して PyBind11 をインストールします。

1. *module.cpp* の上部で、*pybind11.h* を含めます。

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

1. ターゲットの構成を **リリース** に設定し、C++ プロジェクトをビルドして、コードを検証します。 エラーが発生した場合は、次のトラブルシューティングをご覧ください。

### <a name="troubleshooting"></a>トラブルシューティング

C++ モジュールは、次の理由でコンパイルに失敗する場合があります。

- *Python.h* が見つからない (**E1696: ソース ファイル "Python.h" を開けません** や **C1083: インクルード ファイルを開けません: "Python.h": このようなファイルまたはディレクトリはありません**): プロジェクトのプロパティの **[C/C++]** > **[全般]** > **[追加のインクルード ディレクトリ]** のパスが Python インストールの *include* フォルダーに設定されていることを確認してください。 「[C++ のコア プロジェクトを作成する](#create-the-core-c-projects)」の手順 6 をご覧ください。

- Python ライブラリが見つかりません: プロジェクトのプロパティの **[リンカー]**  >  **[全般]**  >  **[追加のライブラリ ディレクトリ]** のパスが、Python インストールの *libs* フォルダーを指していることを確認します。 「[C++ のコア プロジェクトを作成する](#create-the-core-c-projects)」の手順 6 をご覧ください。

- ターゲット アーキテクチャに関連するリンカー エラー: C++ プロジェクトのターゲット アーキテクチャを、Python インストールのアーキテクチャと一致するように変更します。 たとえば、C++ プロジェクトで x64 をターゲットとするが、Python インストールが x86 の場合は、C++ プロジェクトを x86 をターゲットとするように変更します。

## <a name="test-the-code-and-compare-the-results"></a>コードをテストして結果を比較する

これで、Python 拡張機能の構造の DLL ができたので、Python プロジェクトからそれらを参照し、モジュールをインポートして、それらのメソッドを使うことができます。

### <a name="make-the-dll-available-to-python"></a>Python で DLL を使用できるようする

Python で DLL を使えるようにするには 2 つの方法があります。

Python プロジェクトと C++ プロジェクトが同じソリューション内にある場合は、1 つ目の方法を使用します。 **ソリューション エクスプローラー** に移動し、Python プロジェクト内の **[参照設定]** ノードを右クリックし、 **[参照の追加]** をクリックします。 表示されるダイアログで **[プロジェクト]** タブを選択し、**superfastcode** プロジェクトと **superfastcode2** プロジェクトの両方を選択し、**[OK]** を選択します。

![superfastcode プロジェクトに参照を追加する](media/cpp-add-reference.png)

次の手順で説明する別の方法では、グローバル Python 環境にモジュールをインストールし、他の Python プロジェクトでも使えるようにします  (そのためには、通常、その環境に合わせて Visual Studio 2017 バージョン 15.5 以前で IntelliSense 入力候補データベースを更新する必要があります。 環境からモジュールを削除するときも、更新する必要があります)。

1. Visual Studio 2017 以降を使っている場合は、Visual Studio インストーラーを実行して **[変更]** を選び、**[個別のコンポーネント]** > **[コンパイラ、ビルド ツール、およびランタイム]** > **[Visual C++ 2015.3 v140 ツールセット]** を選びます。 この手順が必要な理由は、Python (for Windows) 自体が Visual Studio 2015 (バージョン 14.0) でビルドされ、ここで説明する方法で拡張機能をビルドするときはこれらのツールが使えることが想定されるためです。 (32 ビット バージョンの Python をインストールし、DLL を x64 ではなく Win32 にターゲットする必要がある場合があることに注意してください)。

1. プロジェクトを右クリックし、**[追加]** > **[新しい項目]** を選択して、C++ プロジェクトに *setup.py* という名前のファイルを作成します。 次に、**C++ File (.cpp)** を選択し、ファイルに `setup.py` という名前を付け、**[OK]** を選択します (*.py* 拡張子を使用してファイルに名前を付けることで、C++ ファイル テンプレートを使用していても、Visual Studio でそのファイルが Python として認識されるようにします)。 ファイルがエディターに表示されたら、拡張メソッドに応じて、そこに次のコードを貼り付けます。

    **CPython の拡張機能 (superfastcode プロジェクト):**

    ```python
    from distutils.core import setup, Extension, DEBUG

    sfc_module = Extension('superfastcode', sources = ['module.cpp'])

    setup(name = 'superfastcode', version = '1.0',
        description = 'Python Package with superfastcode C++ extension',
        ext_modules = [sfc_module]
        )
    ```

    このスクリプトについては、「[Building C and C++ Extensions](https://docs.python.org/3/extending/building.html)」 (C と C++ の拡張機能のビルド) (python.org) をご覧ください。

    **PyBind11 (superfastcode2 プロジェクト):**

    ```python
    import os, sys

    from distutils.core import setup, Extension
    from distutils import sysconfig

    cpp_args = ['-std=c++11', '-stdlib=libc++', '-mmacosx-version-min=10.7']

    sfc_module = Extension(
        'superfastcode2', sources = ['module.cpp'],
        include_dirs=['pybind11/include'],
        language='c++',
        extra_compile_args = cpp_args,
        )

    setup(
        name = 'superfastcode2',
        version = '1.0',
        description = 'Python package with superfastcode2 C++ extension (PyBind11)',
        ext_modules = [sfc_module],
    )
    ```

1. *setup.py* コードをコマンド ラインから使用すると、Visual Studio 2015 C++ ツールセット使って拡張機能をビルドするように Python に指示します。 管理者特権でコマンド プロンプトを開き、C++ プロジェクトを含むフォルダー (つまり *setup.py* を含むフォルダー) に移動して、次のコマンドを入力します。

    ```command
    pip install .
    ```

    または

    ```command
    py -m pip install .
    ```

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

1. 違いがより顕著になるように `COUNT` 変数を増やしてみてください。 また、C++ モジュールの **デバッグ** ビルドの実行は、**リリース** ビルドよりも低速になります。これは、**デバッグ** ビルドが十分に最適化されず、さまざまなエラー チェックが含まれるためです。 これらの構成間を自由に切り替えて比較することができます。

> [!NOTE]
> 出力で、PyBind11 拡張機能が CPython 拡張機能ほど高速ではないものの、Python をそのまま実装した場合よりも大幅に高速であることが確認できます。 この差は、C++ インターフェイスを劇的に簡素化するために、PyBind11 によってもたらされる呼び出しごとの少量のオーバーヘッドによるものです。 この呼び出しごとの差は、実際には完全に無視できるほど小さいものです。テスト コードは、extension 関数を 500,000 回呼び出すため、ここに表されている結果には、そのオーバーヘッドが大幅に増幅されています。 通常、C++ 関数は、ここで使用されている単純な `fast_tanh[2]` メソッドよりもずっと多くの作業を行っており、この場合にはオーバーヘッドは重要ではありません。 ただし、1 秒あたり何千回も呼び出される可能性があるメソッドを実装する場合は、CPython のアプローチを使用することで、PyBind11 よりも高いパフォーマンスを実現できます。

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

次の表で説明するように、Python の拡張機能を作成するにはさまざまな方法があります。 CPython と PyBind11 の最初の 2 つのエントリは、この記事で既に説明しています。

| アプローチ | Vintage | 代表的ユーザー | 
| --- | --- | --- |
| CPython 用の C/C++ 拡張モジュール | 1991 | 標準ライブラリ | 
| [PyBind11](https://github.com/pybind/pybind11) (C++ 向けに推奨) | 2015 |  |
| Cython (C に推奨) | 2007 | [gevent](https://www.gevent.org/)、[kivy](https://kivy.org/) |
| [Boost.Python](https://www.boost.org/doc/libs/1_66_0/libs/python/doc/html/index.html) | 2002 | |
| ctypes | 2003 | [oscrypto](https://github.com/wbond/oscrypto) | 
| SWIG | 1996 | [crfsuite](http://www.chokkan.org/software/crfsuite/) | 
| cffi | 2013 | [cryptography](https://cryptography.io/en/latest/)、[pypy](https://pypy.org/) |
| [cppyy](https://cppyy.readthedocs.io/en/latest/) | 2017 | |

## <a name="see-also"></a>こちらもご覧ください

このチュートリアルで使われているサンプルの完全版は [python-samples-vs-cpp-extension](https://github.com/Microsoft/python-sample-vs-cpp-extension) (GitHub) にあります。
