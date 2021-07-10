---
title: Python 用の C++ 拡張機能の記述
description: この記事では、混合モードのデバッグなど、Visual Studio、CPython、および PyBind11 を使用して Python 用の C++ 拡張機能を作成する方法について説明します。
ms.date: 05/11/2021
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: ce80ab6647ffc1043bcc452c387abcbdb80a2def
ms.sourcegitcommit: 162be102d2c22a1c4ad2c447685abd28e0e85d15
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "109973441"
---
# <a name="create-a-c-extension-for-python"></a>Python 用 C++ 拡張機能の作成

Python インタープリターの機能を拡張するために、C++ (または C) で記述されたモジュールがよく使われます。 また、低レベルのオペレーティング システム機能へのアクセスを有効にするためにも使用されます。 

モジュールには次の 3 つの主な種類があります。

- **アクセラレータ モジュール**: Python はインタープリター言語であるため、C++ でアクセラレータ モジュールを記述してパフォーマンスを向上させることができます。
- **ラッパー モジュール**: これらのモジュールでは、既存の C/C++ インターフェイスを Python コードに公開するか、Python から使いやすい、より "Python らしい" API を公開します。
- **低レベル システム アクセス モジュール**: これらのモジュールを作成し、`CPython` ランタイム、オペレーティング システム、または基になるハードウェアの低レベル機能にアクセスできます。

この記事では、双曲正接を計算する `CPython` 用の C++ 拡張モジュールを作成し、Python コードからそれを呼び出す手順について説明します。 Python では最初にルーチンを実装して、C++ で同じルーチンを実装した場合の相対的なパフォーマンス向上を示します。

この記事では、Python で C++ 拡張機能を使用できるようにする 2 つの方法も示します。

- [Python のドキュメント](https://docs.python.org/3/c-api/)で説明されている標準の `CPython` 拡張機能を使用する。
- その簡潔さから C++ 11 に推奨される [PyBind11](https://github.com/pybind/pybind11) を使用する。

このチュートリアルのサンプルの完全版は、GitHub の [python-samples-vs-cpp-extension](https://github.com/Microsoft/python-sample-vs-cpp-extension) にあります。

## <a name="prerequisites"></a>前提条件

- Python 開発ワークロードがインストールされた Visual Studio 2017 以降。 ワークロードには Python ネイティブ開発ツールが含まれており、ネイティブ拡張機能に必要な C++ ワークロードとツールセットが提供されます。

    ![Python ネイティブ開発ツール オプションが強調表示された、Python 開発オプションのリストのスクリーンショット。](media/cpp-install-native.png)

    > [!NOTE]
    > **データ サイエンスと分析アプリケーション** ワークロードをインストールすると、Python と **Python ネイティブ開発ツール** オプションが既定でインストールされます。

インストール オプションの詳細については、[Visual Studio 用の Python サポートのインストール](installing-python-support-in-visual-studio.md)に関するページを参照してください。 Python を別個にインストールする場合は、そのインストーラーの **[詳細オプション]** で **[Download debugging symbols]\(デバッグ シンボルのダウンロード\)** を必ず選択してください。 このオプションは、Python コードとネイティブ コードの間で混合モードのデバッグを使用する場合に必要です。

## <a name="create-the-python-application"></a>Python アプリケーションを作成する

1. Visual Studio で **[ファイル]**  >  **[新規]**  >  **[プロジェクト]** の順に選択して、新しい Python プロジェクトを作成します。 **Python** を検索し、**Python アプリケーション** テンプレートを選んで、名前と場所を入力してから、 **[OK]** を選択します。

1. プロジェクトの *.py* ファイルに、次のコードを貼り付けます。 [Python の編集機能](editing-python-code-in-visual-studio.md)をいくつか体験する場合は、コードを手動で入力してみてください。  

   このコードでは、数値演算ライブラリを使用せずに双曲正接が計算されます。これは、ネイティブ拡張機能を使用して高速化する対象です。

    > [!Tip]
    > C++ で書き換える前に、純粋な Python でコードを記述します。 このようにすることで、ネイティブ コードが確実に正しいことをより簡単に確認できます。

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

1. 結果を表示するには、 **[デバッグ]**  >  **[デバッグなしで開始]** の順に選択するか、Ctrl + F5 キーを押してプログラムを実行します。 

   `COUNT` 変数を調整して、ベンチマークの実行にかかる時間を変更することができます。 このチュートリアルの目的は、ベンチマークの所要時間を約 2 秒にするように、カウントを設定することです。

   > [!TIP]
   > ベンチマークを実行する場合は、常に **[デバッグ]**  >  **[デバッグなしで開始]** を使用します。 このようにすると、Visual Studio デバッガー内でコードを実行したときに発生するオーバーヘッドを回避するのに役立ちます。

## <a name="create-the-core-c-projects"></a>C++ のコア プロジェクトを作成する

*superfastcode* と *superfastcode2* という 2 つの同じ C++ プロジェクトを作成するには、このセクションの手順に従います。 後で、各プロジェクトで別の手段を使用して C++ コードを Python に公開します。

1. **ソリューション エクスプローラー** で、ソリューションを右クリックしてから、 **[追加]**  >  **[新しいプロジェクト]** の順に選択します。 Visual Studio ソリューションには、Python および C++ プロジェクトの両方を含めることができます (これは Visual Studio for Python を使用する利点の 1 つです)。

1. **C++** を検索し、 **[空のプロジェクト]** を選び、**superfastcode** (1 つ目のプロジェクトの場合) または **superfastcode2** (2 つ目のプロジェクトの場合) を指定してから、 **[OK]** を選択します。

    > [!Tip]
    > Visual Studio で Python ネイティブ開発ツールをインストールしたので、Python 拡張モジュール テンプレートから始めることもできます。 このテンプレートには、ここで説明するものの多くが既に配置されています。 
    > 
    > ただし、このチュートリアルでは、拡張モジュールの作成手順を実際に示すため、空のプロジェクトから始めます。 プロセスを理解したら、テンプレートを使用して、独自の拡張機能を作成するときの時間を節約できます。

1. 新しいプロジェクトに C++ ファイルを作成するには、 **[ソース ファイル]** ノードを右クリックしてから、 **[追加]**  >  **[新しい項目]** の順に選択します。

1. **[C++ ファイル]** を選択し、*module.cpp* という名前を付けてから、 **[OK]** を選択します。

    > [!Important]
    > 後続の手順で C++ プロパティ ページを有効にするには、*.cpp* 拡張子を持つファイルが必要です。

1. メイン ツールバーのドロップダウン メニューを使用して、次のいずれかの操作を行います。

   * 64 ビットの Python ランタイムの場合は、**x64** 構成をアクティブにします。 
   * 32 ビットの Python ランタイムの場合は、**Win32** 構成をアクティブにします。

1. **ソリューション エクスプローラー** で、C++ プロジェクトを右クリックし、 **[プロパティ]** を選択してから次の操作を行います。 

   a. **[構成]** には、 **[アクティブ (デバッグ)]** を入力します。  
   b. **[プラットフォーム]** には、前の手順で選択した内容に応じて、 **[アクティブ (x64)]** または **[アクティブ (Win32)]** を入力します。

    > [!NOTE]
    > 独自のプロジェクトを作成する場合は、''*デバッグ*'' と ''*リリース*'' の両方の構成を行う必要があります。 このユニットでは、デバッグの構成のみを行い、CPython のリリース ビルドを使用するように設定します。 この構成により、アサーションを含む、C++ ランタイムの一部のデバッグ機能が無効になります。 CPython デバッグ バイナリ (*python_d.exe*) を使用する場合は、異なる設定が必要になります。

1. 次の表で説明されているようにプロパティを設定します。

    ::: moniker range=">=vs-2019"

    | タブ | プロパティ | 値 |
    | --- | --- | --- |
    | **全般** | **ターゲット名** | `from...import` ステートメントで Python から参照するモジュールの名前を指定します。 この名前は、Python のモジュールを定義するときに C++ コードでも使用します。 プロジェクトの名前をモジュール名として使用するには、既定値の **$\<ProjectName>** のままにします。  `python_d.exe` では、名前の末尾に `_d` を追加します。 |
    | | **[構成の種類]** | **ダイナミック ライブラリ (.dll)** |
    | | **詳細** > **ターゲット ファイル拡張子** | **.pyd** |
    | | **[プロジェクトの既定値]** > **[構成の種類]** | **ダイナミック ライブラリ (.dll)** |
    | **[C/C++]** > **[全般]** | **追加のインクルード ディレクトリ** | インストールに合わせて Python の *include* フォルダーを追加します (例: `c:\Python36\include`)。  |
    | **[C/C++]** > **[プリプロセッサ]** | **プリプロセッサの定義** | **_DEBUG** 値を **NDEBUG** に変更して、CPython の非デバッグ バージョンに一致させます (存在する場合)。 *python_d.exe* を使用する場合は、この値を変更せずにそのままにしておきます。 |
    | **[C/C++]** > **[コード生成]** | **ランタイム ライブラリ** | CPython の非デバッグ バージョンに一致する **[マルチスレッド DLL (/MD)]** 。 *python_d.exe* を使用する場合は、この値を **[マルチスレッド デバッグ DLL (/MDd)]** のままにします。 |
    | **[リンカー]** > **[全般]** | **追加のライブラリ ディレクトリ** | インストールに合わせて、 *.lib* ファイルが含まれる Python の *libs* フォルダーを追加します (例:*c:\Python36\libs*)。 *.py* ファイルが含まれる *Lib* フォルダー ''*ではなく*''、必ず、 *.lib* ファイルが含まれる *libs* フォルダーをポイントするようにしてください。 |
    | | |

    ::: moniker-end

    ::: moniker range="=vs-2017"

    | タブ | プロパティ | 値 |
    | --- | --- | --- |
    | **全般** | **[全般]** > **[ターゲット名]** | `from...import` ステートメントで Python から参照するモジュールの名前を指定します。 この名前は、Python のモジュールを定義するときに C++ コードでも使用します。 プロジェクトの名前をモジュール名として使用するには、既定値の **$\<ProjectName>** のままにします。 `python_d.exe` では、名前の末尾に `_d` を追加します。 |
    | | **[全般]** > **[ターゲットの拡張子]** | **.pyd** |
    | | **[プロジェクトの既定値]** > **[構成の種類]** | **ダイナミック ライブラリ (.dll)** |
    | **[C/C++]** > **[全般]** | **追加のインクルード ディレクトリ** | インストールに合わせて Python の *include* フォルダーを追加します (例: *c:\Python36\include*)。  |
    | **[C/C++]** > **[プリプロセッサ]** | **プリプロセッサの定義** | **_DEBUG** 値を **NDEBUG** に変更して、`CPython` の非デバッグ バージョンに一致させます (存在する場合)。 `python_d.exe` を使用する場合は、この値を変更せずにそのままにしておきます。 |
    | **[C/C++]** > **[コード生成]** | **ランタイム ライブラリ** | `CPython` の非デバッグ バージョンに一致する **[マルチスレッド DLL (/MD)]** 。 `python_d.exe` を使用する場合は、この値を変更せずにそのままにしておきます。 |
    | **[リンカー]** > **[全般]** | **追加のライブラリ ディレクトリ** | インストールに合わせて、 *.lib* ファイルが含まれる Python の *libs* フォルダーを追加します (例:*c:\Python36\libs*)。 *.py* ファイルが含まれる *Lib* フォルダー ''*ではなく*''、必ず、 *.lib* ファイルが含まれる *libs* フォルダーをポイントするようにしてください。 |
    | | |

    ::: moniker-end
    
    > [!NOTE]
    > **[C/C++]** タブがプロジェクトのプロパティに表示されない場合、プロジェクトには C/C++ ソース ファイルとして識別されるファイルは含まれません。 このような条件は、 *.c* または *.cpp* ファイル拡張子を付けずにソース ファイルを作成すると発生する場合があります。 
    > 
    > たとえば、前に新しい項目のダイアログで「*module.cpp*」ではなく誤って「*module.coo*」と入力した場合、Visual Studio ではこのファイルが作成されますが、ファイルの種類は C/C++ のプロパティ タブをアクティブにする *[C/C+ コード]* に設定されません。このような誤った識別は、このファイルの名前を *.cpp* ファイル拡張子を使用して変更した場合でもそのままになります。 
    > 
    > ファイルの種類を正しく設定するには、**ソリューション エクスプローラー** でファイルを右クリックし、 **[プロパティ]** を選択します。 次に、 **[ファイルの種類]** で **[C/C++ コード]** を選択します。

1. **[OK]** を選択します。

1. 構成 (''*デバッグ*'' と ''**リリース**'' の両方) をテストするには、C++ プロジェクトを右クリックしてから、 *[ビルド]* を選択します。 

   *.pyd* ファイルは、C++ のプロジェクト フォルダー自体ではなく、*Debug* および *Release* の下の *solution* フォルダーにあります。

1. C++ プロジェクトの *module.cpp* ファイルで、次のコードを追加します。

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

1. まだ行っていない場合は、前の手順を繰り返して、同じ構成を持つ *superfastcode2* という名前の 2 つ目のプロジェクトを作成します。

## <a name="convert-the-c-projects-to-extensions-for-python"></a>C++ プロジェクトを Python の拡張機能に変換する

C++ DLL を Python の拡張機能にするには、まず、エクスポートしたメソッドを Python の型とやりとりするように変更します。 その後、モジュールのメソッドの定義と共に、モジュールをエクスポートする関数を追加します。

次のセクションでは、CPython の拡張機能と PyBind11 の両方を使用して、これらの手順を行う方法について説明します。

### <a name="use-cpython-extensions"></a>CPython の拡張機能を使用する

このセクションで示されているコードの詳しい背景については、「[Python/C API リファレンス マニュアル](https://docs.python.org/3/c-api/index.html)」と、特に「[モジュール オブジェクト](https://docs.python.org/3/c-api/module.html)」ページを参照してください。 必ず、右上のドロップダウン リストで Python のバージョンを選択してください。

1. *module.cpp* ファイルの上部に、*Python.h* を含めます。

    ```cpp
    #include <Python.h>
    ```

1. Python の型 (つまり、`PyObject*`) を受け入れて戻すように、`tanh_impl` メソッドを変更します。

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

1. Python コードで参照するモジュールを定義する構造体を追加します (具体的には、`from...import` ステートメントを使用する場合)。 

   このコードでインポートされる名前は、 **[構成プロパティ]**  >  **[全般]**  >  **[ターゲット名]** のプロジェクト プロパティの値と一致する必要があります。 

   次の例では、`"superfastcode"` というモジュール名は Python で `from superfastcode import fast_tanh` を使用できることを意味します。これは、`fast_tanh` が `superfastcode_methods` 内で定義されているためです。 *module.cpp* など、C++ プロジェクトの内部にあるファイル名は重要ではありません。

    ```cpp
    static PyModuleDef superfastcode_module = {
        PyModuleDef_HEAD_INIT,
        "superfastcode",                        // Module name to use with Python import statements
        "Provides some functions, but faster",  // Module description
        0,
        superfastcode_methods                   // Structure that defines the methods of the module
    };
    ```

1. モジュールを読み込むときに Python で呼び出すメソッドを追加します。`PyInit_<module-name>` という名前にする必要があります。ここで、 *\<module-name>* は C++ プロジェクトの **[全般]**  >  **[ターゲット名]** プロパティと完全に一致します。 つまり、プロジェクトによってビルドされた *.pyd* ファイルのファイル名と一致します。

    ```cpp
    PyMODINIT_FUNC PyInit_superfastcode() {
        return PyModule_Create(&superfastcode_module);
    }
    ```

1. もう一度 C++ プロジェクトをビルドして、コードを検証します。 エラーが発生した場合は、[トラブルシューティング](#troubleshoot-compiling-failures)に関するセクションを参照してください。

### <a name="use-pybind11"></a>PyBind11 を使用する

前のセクションの手順を完了すると、C++ コードに必要なモジュール構造を作成するために多数の定型コードを使用したことに気付きます。 PyBind11 では、同じ結果が得られる (ただし、はるかに少ないコードで) C++ ヘッダー ファイルのマクロを使用してプロセスを簡略化します。 

このセクションのコードの詳細については、[PyBind11 の基本](https://github.com/pybind/pybind11/blob/master/docs/basics.rst)を参照してください。

1. pip (`pip install pybind11` または `py -m pip install pybind11`) を使用して、PyBind11 をインストールします。 

   または、[Python 環境] ウィンドウを使って PyBind11 をインストールしてから、次の手順のために **[PowerShell で開く]** コマンドを使用できます。

1. 同じターミナルで `python -m pybind11 --includes` または `py -m pybind11 --includes` を実行します。 

   これにより、プロジェクトの **[C/C++]**  >  **[全般]**  >  **[追加のインクルード ディレクトリ]** プロパティに追加する必要があるパスのリストが出力されます。 `-I` プレフィックスが存在する場合は、必ず削除してください。

1. 前のセクションの変更が含まれていない新しい *module.cpp* の上部に、*pybind11.h* を含めます。

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

1. C++ プロジェクトをビルドして、コードを検証します。 エラーが発生した場合は、次のセクションの「コンパイル エラーのトラブルシューティングを行う」を参照して解決方法をご確認ください。

### <a name="troubleshoot-compiling-failures"></a>コンパイル エラーのトラブルシューティングを行う

C++ モジュールでは、次の理由でコンパイルに失敗する場合があります。

- エラー: *Python.h* が見つかりません (**E1696: ソース ファイル "Python.h" を開けません** かつ/または **C1083: インクルード ファイルを開けません: "Python.h": 該当するファイルまたはディレクトリがありません**) 

  解決方法: プロジェクトのプロパティの **[C/C++]**  >  **[全般]**  >  **[追加のインクルード ディレクトリ]** のパスが、Python インストールの *include* フォルダーを指していることを確認します。 「[C++ のコア プロジェクトを作成する](#create-the-core-c-projects)」の手順 6 をご覧ください。

- エラー: Python ライブラリが見つかりません 
 
   解決方法: プロジェクトのプロパティの **[リンカー]**  >  **[全般]**  >  **[追加のライブラリ ディレクトリ]** のパスが、Python インストールの *libs* フォルダーを指していることを確認します。 「[C++ のコア プロジェクトを作成する](#create-the-core-c-projects)」の手順 6 をご覧ください。

- ターゲット アーキテクチャに関連するリンカー エラー
   
   解決方法: C++ プロジェクトのターゲット アーキテクチャを、Python インストールのものと一致するように変更します。 たとえば、C++ プロジェクトで Win32 をターゲットとする一方で、Python インストールが 64 ビットの場合は、C++ プロジェクトを x64 に変更します。

## <a name="test-the-code-and-compare-the-results"></a>コードをテストして結果を比較する

これで、Python 拡張機能の構造の DLL ができたので、Python プロジェクトからそれらを参照し、モジュールをインポートして、それらのメソッドを使うことができます。

### <a name="make-the-dll-available-to-python"></a>Python で DLL を使用できるようする

いくつかの方法で DLL を Python で使用できるようにすることができます。 検討すべき 2 つの方法を以下に示します。 

* Python プロジェクトと C++ プロジェクトが同じソリューション内にある場合は、この 1 つ目の方法を使用します。 次の操作を行います。 

   1. **ソリューション エクスプローラー** で、Python プロジェクト内の **[参照設定]** ノードを右クリックしてから、 **[参照の追加]** を選択します。 
   1. 表示されるダイアログで **[プロジェクト]** タブを選択し、**superfastcode** プロジェクトと **superfastcode2** プロジェクトの両方を選択し、**[OK]** を選択します。

      !["superfastcode" プロジェクトに参照を追加する方法を示すスクリーンショット。](media/cpp-add-reference.png)

* 別の方法では、モジュールを Python 環境にインストールします。これにより、他の Python プロジェクトでもモジュールを使用できるようになります。 詳細については、[**setuptools** プロジェクトのドキュメント](https://setuptools.readthedocs.io/)を参照してください。 次の操作を行います。

    1. プロジェクトを右クリックし、**[追加]** > **[新しい項目]** を選択して、C++ プロジェクトに *setup.py* という名前のファイルを作成します。 
    
    1. **[C++ ファイル (.cpp)]** を選択し、そのファイルに *setup.py* という名前を付けてから、 **[OK]** を選択します。
    
       *.py* 拡張子を使ってファイルに名前を付けることで、C++ ファイル テンプレートを使用していても、Visual Studio で Python ファイルとして認識されるようにします。 

       ファイルがエディターに表示されたら、拡張メソッドに応じて、そこに次のコードを貼り付けます。
    
        **`CPython` 拡張機能 (superfastcode プロジェクト) の場合**:
    
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
    
        **`PyBind11` (superfastcode2 プロジェクト) の場合**:
    
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
    
    1. C++ プロジェクトで *pyproject.toml* という名前の 2 つ目のファイルを作成し、次のコードを貼り付けます。
    
        ```toml
        [build-system]
        requires = ["setuptools", "wheel", "pybind11"]
        build-backend = "setuptools.build_meta"
        ```
    
    1. 拡張機能をビルドするには、開いている *pyproject.toml* タブを右クリックしてから、 **[完全なパスのコピー]** を選択します。 *pyproject.toml* 名は、使用する前にパスから削除します。
    
    1. **ソリューション エクスプローラー** で、アクティブな Python 環境を右クリックしてから、 **[Python パッケージの管理]** を選択します。
    
        > [!Tip]
        > パッケージが既にインストールされている場合は、ここで一覧表示されます。 続行する前に、 **[X]** をクリックしてアンインストールします。
    
    1. 検索ボックスにコピーしたパスを貼り付け、末尾から *pyproject.toml* を削除し、Enter キーを押してそのディレクトリからモジュールをインストールします。
    
        > [!Tip]
        > アクセス許可エラーによりインストールが失敗した場合は、 *--user* を末尾に追加し、コマンドを再試行します。


### <a name="call-the-dll-from-python"></a>Python から DLL を呼び出す

前のセクションで説明したように、Python で DLL を使用できるようにすると、Python コードから `superfastcode.fast_tanh` および `superfastcode2.fast_tanh2` 関数を呼び出して、それらのパフォーマンスを Python の実装と比較できます。 DLL を呼び出すには、次の操作を行います。

1. 次の行を *.py* ファイルに追加して、DLL からエクスポートされたメソッドを呼び出してその出力を表示します。

    ```python
    from superfastcode import fast_tanh
    test(lambda d: [fast_tanh(x) for x in d], '[fast_tanh(x) for x in d] (CPython C++ extension)')

    from superfastcode2 import fast_tanh2
    test(lambda d: [fast_tanh2(x) for x in d], '[fast_tanh2(x) for x in d] (PyBind11 C++ extension)')
    ```

1. **[デバッグ]**  >  **[デバッグなしで開始]** の順に選択するか、Ctrl + F5 キーを押して Python プログラムを実行します。

    > [!NOTE]
    > **[デバッグなしで開始]** コマンドが無効な場合は、**ソリューション エクスプローラー** で Python プロジェクトを右クリックしてから、 **[スタートアップ プロジェクトに設定]** を選択します。  

    Python の実装よりも約 5 から 20 倍高速で C++ のルーチンが実行されることを確認します。 通常、次のような出力が表示されます。

    ```output
    Running benchmarks with COUNT = 500000
    [tanh(x) for x in d] (Python implementation) took 0.758 seconds

    [fast_tanh(x) for x in d] (CPython C++ extension) took 0.076 seconds

    [fast_tanh2(x) for x in d] (PyBind11 C++ extension) took 0.204 seconds
    ```

1. 違いがより顕著になるように `COUNT` 変数を増やしてみてください。 

    また、C++ モジュールの ''*デバッグ*'' ビルドの実行は、''*リリース*'' ビルドよりも低速になります。これは、デバッグ ビルドが十分に最適化されず、さまざまなエラー チェックが含まれるためです。 比較のために、これらの構成を自由に切り替えることができます。ただし、必ず前に戻って、リリース構成に対して前に設定したプロパティを更新してください。

出力で、PyBind11 拡張機能が CPython 拡張機能ほど高速ではないものの、純粋な Python 実装よりも大幅に高速であることが確認できます。 この違いの主な原因は、複数のパラメーター、パラメーター名、またはキーワード引数をサポートしていない `METH_O` 呼び出しを使用したことです。 PyBind11 では、より Python に類似したインターフェイスを呼び出し元に提供するために、少し複雑なコードを生成します。 しかし、テスト コードで関数が 50 万回呼び出されるため、結果的にオーバーヘッドが大幅に増加する可能性があります。

`for` ループをネイティブ コードに移動することで、オーバーヘッドをさらに軽減できます。 この方法では、[反復子プロトコル](https://docs.python.org/c-api/iter.html) (または[関数パラメーター](https://pybind11.readthedocs.io/en/stable/advanced/functions.html#python-objects-as-args)用の PyBind11 の `py::iterable` 型) を使用して、各要素を処理する必要があります。 Python と C++ の間で繰り返される切り替えを削除することは、シーケンスの処理にかかる時間を短縮する効果的な方法です。

### <a name="troubleshoot-importing-errors"></a>インポート エラーのトラブルシューティングを行う

モジュールをインポートしようとしたときに `ImportError` メッセージを受け取った場合は、次のいずれかの方法で解決できます。

* プロジェクト参照を使用してビルドする場合は、C++ プロジェクトのプロパティが、Python プロジェクトでアクティブになっている Python 環境と確実に一致するようにします (特に *Include* および *Library* ディレクトリ)。

* 出力ファイルには、必ず *superfastcode.pyd* という名前を付けます。 他の名前や拡張子を使用すると、インポートできなくなります。

* *setup.py* ファイルを使用してモジュールをインストールした場合は、Python プロジェクト用にアクティブ化された Python 環境で確実に *pip* コマンドを実行したことを確認します。 ソリューション エクスプローラーで Python 環境を展開すると、*superfastcode* のエントリが表示されるはずです。

## <a name="debug-the-c-code"></a>C++ コードをデバッグする

Visual Studio では、Python と C++ コードを一緒にデバッグすることをサポートしています。 このセクションでは、*superfastcode* プロジェクトを使用してプロセスについて説明します。 プロセスは *superfastcode2* プロジェクトでも同じです。

1. **ソリューション エクスプローラー** で Python プロジェクトを右クリックして、 **[プロパティ]** 、 **[デバッグ]** タブの順に選択します。その後、 **[デバッグ]**  >  **[ネイティブ コードのデバッグを有効にする]** オプションをオンにします。

    > [!Tip]
    > ネイティブ コードのデバッグを有効にすると、プログラムが通常の **[続行するには、任意のキーを押してください]** で一時停止せずに終了した直後に、Python の出力ウィンドウが閉じることがあります。 
    >
    > 解決方法: ネイティブ コードのデバッグを有効にした後で強制的に一時停止するには、 **[デバッグ]** タブの **[実行]**  >  **[インタープリター引数]** フィールドに `-i` オプションを追加します。この引数を使用すると、Python インタープリターはコードの実行後に対話モードになり、この時点でユーザーが Ctrl + Z キー、Enter キーの順に押してウィンドウを閉じるまで待機します。 
    >
    > または、Python コードを変更してもよい場合は、プログラムの最後に `import os` および `os.system("pause")` ステートメントを追加できます。 このコードで、元の一時停止プロンプトが複製されます。

1. **[ファイル]**  >  **[保存]** を選択して、プロパティの変更を保存します。

1. Visual Studio ツール バーで、ビルド構成を **[デバッグ]** に設定します。

    ![Visual Studio ツール バーの [デバッグ] 設定のスクリーンショット。](media/cpp-set-debug.png)

1. 通常、デバッガーでコードを実行するとより時間がかかるため、 *.py* ファイルの `COUNT` 変数を、既定値より約 5 倍小さい値に変更できます。 たとえば、**500000** から **100000** に変更します。

1. C++ コードで `tanh_impl` メソッドの先頭行にブレークポイントを設定してから、**F5** キーを押すか、 **[デバッグ]**  >  **[デバッグの開始]** の順に選択してデバッガーを開始します。 

    ブレークポイント コードが呼び出されるとデバッガーが停止します。 ブレークポイントがヒットしない場合は、構成が確実に **[デバッグ]** に設定されていることと、プロジェクトを保存していること (これはデバッガーの開始時に自動的に行われません) を確認します。

    ![ブレークポイントを含む C++ コードのスクリーンショット。](media/cpp-debugging.png)

1. ブレークポイントで、C++ コードをステップ実行したり、変数を調べたりすることができます。 これらの機能の詳細については、「[Python と C++ を同時にデバッグする](debugging-mixed-mode-c-cpp-python-in-visual-studio.md)」を参照してください。

## <a name="alternative-approaches"></a>他の方法

次の表で説明されているように、さまざまな方法で Python の拡張機能を作成することができます。 最初の 2 行 (`CPython` と `PyBind11`) については、この記事で説明されています。

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

このチュートリアルのサンプルの完全版は、GitHub の [python-samples-vs-cpp-extension](https://github.com/Microsoft/python-sample-vs-cpp-extension) にあります。
