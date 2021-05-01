---
title: Python インタープリターの選択とインストール
description: Visual Studio でサポートされている Python インタープリターの詳細な一覧です。インストーラーを入手できる場所についても簡単に説明します。
ms.date: 06/05/2019
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: 8070bb93a1dd76ad29832afae15d83788300ae7a
ms.sourcegitcommit: 925db7adb9cb554b081c7e727d09680d4863feed
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2021
ms.locfileid: "107941111"
---
# <a name="install-python-interpreters"></a>Python インタープリターのインストール

既定では、Visual Studio 2017 以降に Python 開発ワークロードをインストールすると、Python 3 (64 ビット) もインストールされます。 [インストール](installing-python-support-in-visual-studio.md)に関する記事で説明されているように、必要に応じて、32 ビットおよび 64 ビット版の Python 2 および Python 3 と共に、Miniconda (Visual Studio 2019) または Anaconda 2/Anaconda 3 (Visual Studio 2017) をインストールできます。

::: moniker range=">=vs-2019"
または、標準の Python インタープリターを **[環境の追加]** ダイアログからインストールできます。 **[Python 環境]** ウィンドウまたは Python ツール バーで **[環境の追加]** コマンドを選択し、**[Python インストール]** タブを選択して、インストールするインタープリターを指定し、**[インストール]** を選択します。
::: moniker-end

以下の表のインタープリターは、Visual Studio インストーラーを使用せずに手動でインストールすることもできます。 たとえば、Visual Studio をインストールする前に Anaconda 3 がインストールされている場合、Visual Studio インストーラーでそれを再度インストールする必要はありません。 また、たとえば Visual Studio インストーラーに利用可能な新しいバージョンがまだ表示されていない場合なども、手動でインタープリターをインストールできます。

::: moniker range=">=vs-2019"
> [!Note]
> Visual Studio では、Python バージョン 2.7 のほか、バージョン 3.5 ～ 3.7 をサポートしています。 Visual Studio を使って、他のバージョンの Python で記述されたコードを編集することはできますが、それらのバージョンは公式にはサポートされておらず、IntelliSense やデバッグなどの機能が動作しない可能性があります。
::: moniker-end

**Visual Studio 2015 以前** では、いずれかのインタープリターを手動でインストールする必要があります。

Visual Studio (すべてのバージョン) でレジストリ (「[PEP 514 - Python registration in the Windows registry](https://www.python.org/dev/peps/pep-0514/)」(PEP 514 - Windows レジストリでの Python の登録) に従って) が確認され、インストールされている各 Python インタープリターとその環境が自動的に検出されます。 Python のインストールは、通常、**HKEY_LOCAL_MACHINE\SOFTWARE\Python** (32 ビット) および **HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Python** (64 ビット) 以下の、**PythonCore** (CPython) や **ContinuumAnalytics** (Anaconda) などの配布用ノード内にあります。

Visual Studio でインストール済みの環境が検出されない場合は、「[既存の環境を手動で識別する](managing-python-environments-in-visual-studio.md#manually-identify-an-existing-environment)」をご覧ください。

Visual Studio の [ **[Python 環境]** ](managing-python-environments-in-visual-studio.md#the-python-environments-window) ウィンドウには既知の環境がすべて表示され、既存のインタープリターの更新プログラムが自動的に検出されます。

| インタープリター | Description |
| --- | --- |
| [CPython](https://www.python.org/) | "ネイティブ" で最もよく使われるインタープリターであり、32 ビット バージョンと 64 ビット バージョンがあります (32 ビットを推奨)。 最新の言語機能、Python パッケージの最大限の互換性、完全なデバッグ サポート、および [IPython](https://ipython.org/) との相互運用性が含まれています。 「[Should I use Python 2 or Python 3?](https://wiki.python.org/moin/Python2orPython3)」(Python 2 と Python 3 のどちらを使うか) もご覧ください。 Visual Studio 2015 以前では、Python 3.6 以降がサポートされていないため、**Python バージョン 3.6 はサポートされていません** というようなエラーが発生する場合があることに注意してください。 代わりに 3.5 以前の Python を使用します。 |
| [IronPython](https://github.com/IronLanguages/ironpython2) | Python の .NET の実装であり (32 ビット バージョンと 64 ビット バージョン)、C#/F#/Visual Basic の相互運用機能、.NET API へのアクセス、標準 Python デバッグ (ただし、C++ 混合モードのデバッグはありません)、IronPython/C# の混合デバッグが提供されます。 ただし、IronPython は仮想環境をサポートしていません。 |
| [Anaconda](https://www.continuum.io) | Python を利用するオープン データ サイエンス プラットフォームであり、最新バージョンの CPython と、インストールが困難なパッケージのほとんどを含みます。 他のインタープリターに決定できない場合にお勧めします。 |
| [PyPy](https://www.pypy.org/) | Python の高パフォーマンスなトレースの JIT 実装であり、実行時間の長いプログラム、およびパフォーマンスに問題があるが他の解決策が見つからない場合に、適しています。 Visual Studio で動作しますが、高度なデバッグ機能のサポートには制限があります。 |
| [Jython](https://www.jython.org/) | Java 仮想マシン (JVM) での Python の実装です。 IronPython に似ており、Jython で実行されるコードは Java のクラスおよびライブラリとやり取りできますが、CPython 用の多くのライブラリは使用できない場合があります。 Visual Studio で動作しますが、高度なデバッグ機能のサポートには制限があります。 |

Python 環境用に新しい検出形式を提供したい開発者は、「[PTVS Environment Detection](https://github.com/Microsoft/PTVS/wiki/Extensibility-Environments)」(PTVS 環境の検出) (github.com) をご覧ください。

## <a name="move-an-interpreter"></a>インタープリターを移動する

ファイル システムを使用して既存のインタープリターを新しい場所に移動すると、Visual Studio は変更を自動的に検出しません。

- 元々 **[Python 環境]** ウィンドウでインタープリターの場所を指定している場合は、そのウィンドウの **[構成]** タブを使用して環境を編集して新しい場所を特定します。 「[既存の環境を手動で識別する](managing-python-environments-in-visual-studio.md#manually-identify-an-existing-environment)」をご覧ください。

- インストーラー プログラムを使用してインタープリターをインストールした場合は、次の手順でインタープリターを新しい場所に再インストールします。

  1. Python インタープリターを元の場所に復元します。
  2. インストーラーを使用してインタープリターをアンインストールします。これで、レジストリ エントリがクリアされます。
  3. 目的の場所にインタープリターを再インストールします。
  4. Visual Studio を再起動します。これで、古い場所ではなく新しい場所が自動的に検出されます。

このプロセスを実行すると、Visual Studio が使用するインタープリターの場所を特定するレジストリ エントリが正しく更新されます。 インストーラーを使用すると、他にも存在する可能性のある副作用も処理されます。

## <a name="see-also"></a>こちらもご覧ください

- [Python 環境を管理する](managing-python-environments-in-visual-studio.md)
- [プロジェクトのインタープリターの選択](selecting-a-python-environment-for-a-project.md)
- [依存関係の requirements.txt の使用](managing-required-packages-with-requirements-txt.md)
- [検索パス](search-paths.md)
- [[Python 環境] ウィンドウ リファレンス](python-environments-window-tab-reference.md)
