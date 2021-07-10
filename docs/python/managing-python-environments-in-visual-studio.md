---
title: Python 環境とインタープリターを管理する
description: '[Python 環境] ウィンドウを使用して、グローバル環境、仮想環境、および conda 環境を管理し、Python インタープリターとパッケージをインストールし、環境を Visual Studio プロジェクトに割り当てます。'
ms.date: 08/06/2019
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.workload:
- python
- data-science
ms.openlocfilehash: 26bcf0fa4d56d4e8df100a0d3e65904d065d8757
ms.sourcegitcommit: 4908561809ad397c99cf204f52d5e779512e502c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2021
ms.locfileid: "112254876"
---
# <a name="how-to-create-and-manage-python-environments-in-visual-studio"></a>Visual Studio で Python 環境を作成および管理する方法

**Python 環境** は、その中で Python コードを実行するコンテキストであり、グローバル環境、仮想環境、および conda 環境が含まれます。 1 つの環境は、インタープリター、ライブラリ (通常は Python 標準ライブラリ)、およびインストールされているパッケージのセットで構成されます。 これらのコンポーネントがすべて合わさって、有効な言語の構造と構文、アクセスできるオペレーティング システム機能、使用できるパッケージが決まります。

Windows 上の Visual Studio では、この記事で説明するように、 **[Python 環境]** ウィンドウで環境を管理し、新しいプロジェクトの既定値として 1 つの環境を選択します。 環境の他の側面については、以下の記事を参照してください。

- 特定のプロジェクトに対して、既定ではなく、[特定の環境を選択](selecting-a-python-environment-for-a-project.md)することができます。

- Python プロジェクトの仮想環境の作成と使用の詳細については、「[仮想環境を使用する](selecting-a-python-environment-for-a-project.md#use-virtual-environments)」を参照してください。

- 環境にパッケージをインストールする場合は、[[パッケージ] タブのリファレンス](python-environments-window-tab-reference.md#packages-tab)を参照してください。

- Python インタープリターをインストールする場合は、「[Python インタープリターのインストール](installing-python-interpreters.md)」を参照してください。 一般的に、主流の Python ディストリビューションのインストーラーをダウンロードして実行すると、Visual Studio でその新しいインストールが検出され、環境が **[Python 環境]** ウィンドウに表示され、プロジェクトに選択できるようになります。

Visual Studio で Python を初めて使用する場合は、以下の記事で一般的な背景を確認してください。

- [Visual Studio での Python の使用](overview-of-python-tools-for-visual-studio.md)
- [Visual Studio での Python サポートのインストール](installing-python-support-in-visual-studio.md)

::: moniker range="vs-2017"
> [!Note]
> **[ファイル]**  >  **[開く]**  >  **[フォルダー]** コマンドを使用してフォルダーとしてのみ開かれた Python コードの環境は管理できません。 Visual Studio の環境機能を使用するには、[既存のコードから Python プロジェクトを作成](quickstart-01-python-in-visual-studio-project-from-existing-code.md)します。
::: moniker-end

::: moniker range=">=vs-2019"
> [!Note]
> **[ファイル]**  >  **[開く]**  >  **[フォルダー]** コマンドを使用して、フォルダーとして開いた Python コードの環境を管理できす。 Python ツールバーを使用すると、検出したすべての環境の中で環境を切り替えたり、新しい環境を追加したりできます。 環境情報は、ワークスペース .vs フォルダー内の PythonSettings.json ファイルに格納されています。
::: moniker-end

## <a name="the-python-environments-window"></a>[Python 環境] ウィンドウ

Visual Studio が認識した環境が **[Python 環境]** ウィンドウに表示されます。 ウィンドウを開くには、次のいずれかの方法を使用します。

- **[表示]**  >  **[その他のウィンドウ]**  >  **[Python 環境]** メニュー コマンドを選びます。
- **ソリューション エクスプローラー** でプロジェクトの **[Python 環境]** ノードを右クリックし、 **[すべての Python 環境の表示]** を選択します。

    ::: moniker range="vs-2017"
    ![ソリューション エクスプローラーの [View All Python Environments (すべての Python 環境の表示)] コマンド](media/environments/environments-view-all.png)
    ::: moniker-end
    ::: moniker range=">=vs-2019"
    ![ソリューション エクスプローラーの [View All Python Environments (すべての Python 環境の表示)] コマンド](media/environments/environments-view-all-2019.png)
    ::: moniker-end

いずれの場合も、 **[Python 環境]** ウィンドウは **ソリューション エクスプローラー** と共に表示されます。

::: moniker range="vs-2017"
![[Python Environments (Python 環境)] ウィンドウ](media/environments/environments-default-view.png)
::: moniker-end
::: moniker range=">=vs-2019"
![[Python Environments (Python 環境)] ウィンドウ](media/environments/environments-default-view-2019.png)
::: moniker-end

Visual Studio では、仮想環境と conda 環境 (「[環境の種類](#types-of-environments)」を参照してください) と共に、([PEP 514](https://www.python.org/dev/peps/pep-0514/) に従って) レジストリを使用してインストールされているグローバル環境が検索されます。 一覧に想定した環境が見つからない場合は、「[既存の環境を手動で識別する](#manually-identify-an-existing-environment)」を参照してください。

一覧から環境を選択すると、Visual Studio の **[概要]** タブにはその環境のさまざまなプロパティとコマンドが表示されます。たとえば、上の図では、インタープリターの場所が *C:\Python36-32* であることがわかります。 **[概要]** タブの一番下にある 4 つのコマンドを実行すると、いずれの場合も、コマンド プロンプトが開き、インタープリターが実行されます。 詳細については、[[環境] ウィンドウ タブ リファレンスの [概要]](python-environments-window-tab-reference.md#overview-tab) に関するページを参照してください。

以下の環境の一覧のドロップダウン リストを使用して、**Package** や **IntelliSense** など異なるタブに切り替えることができます。 これらのタブの説明は、「[[Python 環境] ウィンドウ タブ リファレンス](python-environments-window-tab-reference.md)」でもご覧いただけます。

環境を選択しても、どのプロジェクトとの関係も変わりません。 この一覧で太字で表示されている既定の環境は、Visual Studio ですべての新しいプロジェクトに使用されている環境です。 新しいプロジェクトに別の環境を使用するには、 **[これを新しいプロジェクトに対する既定の環境にする]** コマンドを使用します。 プロジェクトのコンテキスト内では、特定の環境を常に選択できます。 詳細については、[プロジェクト用の環境の選択](selecting-a-python-environment-for-a-project.md)に関するページを参照してください。

一覧表示されている各環境の右側に、その環境の **対話型** ウィンドウを開くコントロールがあります (Visual Studio 2017 15.5 以前では、その環境の IntelliSense データベースを更新する別のコントロールが表示されます。 データベースの詳細については、「[[Python 環境] ウィンドウ タブ リファレンス](python-environments-window-tab-reference.md)」参照してください)。

::: moniker range="vs-2017"
> [!Tip]
> **[Python 環境]** ウィンドウを大きく広げると、環境の表示が拡張され、より操作しやすくなります。
>
> ![[Python Environments (Python 環境)] ウィンドウを広げた表示](media/environments/environments-expanded-view.png)
::: moniker-end

::: moniker range=">=vs-2019"
> [!Tip]
> **[Python 環境]** ウィンドウを大きく広げると、環境の表示が拡張され、より操作しやすくなります。
>
> ![[Python Environments (Python 環境)] ウィンドウを広げた表示](media/environments/environments-expanded-view-2019.png)
::: moniker-end

> [!Note]
> Visual Studio はシステム サイト パッケージのオプションを尊重しますが、Visual Studio 内からそれを変更する方法は用意されていません。

### <a name="what-if-no-environments-appear"></a>環境が表示されない場合

環境が表示されない場合は、Visual Studio が標準的な場所で Python インストールを検出できなかったことを意味します。 たとえば、Visual Studio 2017 以降をインストールしたが、Python ワークロードのインストーラー オプションですべてのインタープリター オプションを選択解除している場合があります。 同様に、Visual Studio 2015 以前をインストールしているが、インタープリターを手動でインストールしなかった場合があります (「[Python インタープリターのインストール](installing-python-interpreters.md)」を参照)。

コンピューター上に Python インタープリターがあることがわかっているが、Visual Studio (すべてのバージョン) で検出されなかった場合は、 **[+ カスタム]** コマンドを使用して、その場所を手動で指定します。 次のセクション「[既存の環境を手動で識別する](#manually-identify-an-existing-environment)」を参照してください。

> [!Tip]
> python.org からのインストーラーを使用することによる Python 2.7.11 から Python 2.7.14 へのアップグレードなど、既存のインタープリターに対する更新プログラムを検出します。インストール プロセス中に、古くなった環境が **Python 環境** の一覧から消え、その場所に更新プログラムが表示されます。
>
> ただし、ファイル システムを使用してインタープリターとその環境を手動で移動している場合、Visual Studio は新しい場所がわかりません。 詳細については、「[インタープリターの移動](installing-python-interpreters.md#move-an-interpreter)」を参照してください。

### <a name="types-of-environments"></a>環境の種類

Visual Studio は、グローバル環境、仮想環境、および conda 環境で動作します。

#### <a name="global-environments"></a>グローバル環境

各 Python インストール (Python 2.7、Python 3.6、Python 3.7、Anaconda 4.4.0 など。「[Python インタープリターのインストール](installing-python-interpreters.md)」を参照) で、独自の *グローバル環境* が保持されます。 各環境は、特定の Python インタープリター、その標準ライブラリ、プレインストールされたパッケージ セット、その環境がアクティブなときにインストールした追加のパッケージで構成されています。 グローバル環境にパッケージをインストールすると、グローバル環境を使用するすべてのプロジェクトでパッケージが使用できるようになります。 環境がファイル システムの保護領域にある場合 (*c:\program files* 内など)、パッケージをインストールするには管理者特権が必要です。

グローバル環境は、コンピューター上のすべてのプロジェクトで使用できます。 Visual Studio では、1 つのグローバル環境を既定の環境として選択します。プロジェクトに対して別の環境を特に選ばない限り、すべてのプロジェクトでこれが使用されます。 詳細については、[プロジェクト用の環境の選択](selecting-a-python-environment-for-a-project.md)に関するページを参照してください。

#### <a name="virtual-environments"></a>仮想環境

グローバル環境での作業は簡単に始めることができますが、異なるプロジェクトのためにさまざまなパッケージがインストールされると、時間の経過と共に混乱が生じます。 このような混乱があると、既知のバージョンで、ビルド サーバーや Web サーバー上に設定した環境とまったく同じ種類の特定のパッケージ セットに対してアプリケーションを完全にテストすることが困難になります。 競合は、2 つのプロジェクトに互換性のないパッケージまたは同じパッケージの異なるバージョンが必要な場合にも発生します。

このため、開発者は 1 つのプロジェクト用に *仮想環境* を作成することがよくあります。 仮想環境は、特定のインタープリターのコピーを含むプロジェクトのサブフォルダーです。 仮想環境をアクティブにすると、インストールするパッケージはその環境のサブフォルダーにのみインストールされます。 その環境内で Python プログラムを実行すると、そうした特定のパッケージに対してのみ実行されていることがわかります。

Visual Studio には、プロジェクトの仮想環境を作成するための直接的なサポートが提供されています。 たとえば、*requirements.txt* を含むプロジェクトを開く場合、またはそのファイルを含むテンプレートからプロジェクトを作成する場合、Visual Studio では、自動的に仮想環境が作成され、それらの依存関係がインストールされるというメッセージが表示されます。

開いているプロジェクト内には、いつでも新しい仮想環境を作成できます。 **ソリューション エクスプローラー** でプロジェクト ノードを展開し、 **[Python 環境]** ノードを右クリックし、[仮想環境を追加] を選択します。 詳細については、「[仮想環境を作成する](./selecting-a-python-environment-for-a-project.md?view=vs-2019&preserve-view=true#create-a-virtual-environment-1)」を参照してください。

Visual Studio には、仮想環境から *requirements.txt* ファイルを生成し、他のコンピューターで環境を簡単に再作成するためのコマンドも用意されています。 詳しくは、「[仮想環境を使用する](selecting-a-python-environment-for-a-project.md#use-virtual-environments)」をご覧ください。

#### <a name="conda-environments"></a>conda 環境

conda 環境は `conda` ツールを使用して作成される環境です。Visual Studio 2017 バージョン 15.7 以降では、統合 conda 管理が使用されます (Anaconda または Miniconda が必要です。これらは Visual Studio インストーラーを通して利用できるようになります。[インストール](installing-python-support-in-visual-studio.md#visual-studio-2019-and-visual-studio-2017)に関するページを参照してください)。

::: moniker range="vs-2017"

1. **[Python 環境]** ウィンドウの **[+ conda 環境の作成]** を選択します。これにより、 **[新しい conda 環境の作成]** タブが開きます。

    ![新しい conda 環境のためのタブを作成する](media/environments/environments-conda-1.png)

1. **[名前]** フィールドに環境の名前を入力し、 **[Python]** フィールドで基本的な Python インタープリターを選択し、 **[作成]** を選択します。

1. **[出力]** ウィンドウに新しい環境の進捗状況が表示され、環境が作成されると CLI に関する指示がいくつか表示されます。

    ![conda 環境の正常な作成](media/environments/environments-conda-2.png)

1. Visual Studio 内では、[プロジェクト用の環境の選択](selecting-a-python-environment-for-a-project.md)に関するページの説明に従って、他の環境の場合と同様にプロジェクト用の conda 環境をアクティブにすることができます。

1. 環境にパッケージをインストールするには、[[パッケージ] タブ](python-environments-window-tab-reference.md#packages-tab)を使用します。
::: moniker-end

::: moniker range=">=vs-2019"

1. **[Python 環境]** ウィンドウで (または、Python ツール バーから) **[+ 環境の追加]** を選択し、 **[環境の追加]** ダイアログ ボックスを開きます。 そのダイアログ ボックスで、 **[Conda 環境]** タブを選択します。

    ![[環境の追加] ダイアログの [Conda 環境] タブ](media/environments/environments-conda-1-2019.png)

1. 次のフィールドを構成します。

    | フィールド | 説明 |
    | --- | --- |
    | Project | 環境を作成するプロジェクト (同じ Visual Studio ソリューションに複数のプロジェクトがある場合)。 |
    | 名前 | Conda 環境の名前。 |
    | パッケージの追加元 | 依存関係が記述されている *environment.yml* ファイルがある場合は、 **[環境ファイル]** を選択します。または、 **[1 つ以上の Anaconda パッケージ名]** を選択して、下のフィールドに少なくとも 1 つの Pythonパッケージまたは Python のバージョンを一覧表示します。 パッケージ一覧では、Python 環境を作成するよう Conda に指示されます。 最新バージョンの Python をインストールするには、`python` を使用します。特定のバージョンをインストールするには、`python=3.7` のように `python=,major>.<minor>` を使用します。 また、パッケージ ボタンを使用して、一連のメニューから Python のバージョンと一般的なパッケージを選択することもできます。 |
    | 現在の環境として設定 | 環境を作成した後、選択したプロジェクトで新しい環境をアクティブ化します。 |
    | 新しいプロジェクトの既定の環境として設定 | Visual Studio で作成されるすべての新しいプロジェクトで、Conda 環境を自動的に設定してアクティブにします。 このオプションは、 **[Python 環境]** ウィンドウの **[これを新しいプロジェクトに対する既定の環境にする]** を使用する場合と同じです。 |
    | Python 環境ウィンドウで表示 | 環境の作成後、 **[Python 環境]** ウィンドウを表示するかどうかを指定します。 |

    > [!Important]
    > Conda 環境を作成するときは、`environments.yml` またはパッケージ一覧を使用して、少なくとも 1 つの Python バージョンまたは Python パッケージを必ず指定してください。そうすれば、環境には Python ランタイムが確実に含まれます。 そうしないと、Visual Studio では環境が無視されます。そのような環境は、 **[Python 環境]** ウィンドウのどこにも表示されず、プロジェクトの現在の環境として設定されず、グローバル環境として使用できません。
    >
    > Python のバージョンを指定しないで Conda 環境を作成してしまった場合は、`conda info` コマンドを使用して Conda 環境フォルダーの場所を確認した後、その場所から環境のサブフォルダーを手動で削除します。

1. **[作成]** を選択し、 **[出力]** ウィンドウで進行状況を確認します。 作成が完了すると、出力にいくつかの CLI 命令が含まれます。

    ![conda 環境の正常な作成](media/environments/environments-conda-2-2019.png)

1. Visual Studio 内では、[プロジェクト用の環境の選択](selecting-a-python-environment-for-a-project.md)に関するページの説明に従って、他の環境の場合と同様にプロジェクト用の conda 環境をアクティブにすることができます。

1. 環境に追加パッケージをインストールするには、[[パッケージ] タブ](python-environments-window-tab-reference.md#packages-tab)を使用します。
::: moniker-end

> [!Note]
> conda 環境で最適な結果を得るためには、conda 4.4.8 以降 (conda バージョンは Anaconda バージョンとは異なります) をご使用ください。 Visual Studio インストーラーを使用して、適切なバージョンの Miniconda (Visual Studio 2019) および Anaconda (Visual Studio 2017) をインストールすることができます。

conda 環境が格納されている conda バージョンや、その他の情報を参照するには、Anaconda コマンド プロンプト (つまり、Anaconda がパス内に存在するコマンド プロンプト) で `conda info` を実行します。

```cli
conda info
```

conda 環境フォルダーは次のように表示されます。

```output
       envs directories : C:\Users\user\.conda\envs
                          c:\anaconda3\envs
                          C:\Users\user\AppData\Local\conda\conda\envs
```

conda 環境はプロジェクトと共に格納されないことから、グローバル環境と同じように機能します。 たとえば、conda 環境に新しいパッケージをインストールすると、その環境を使用するすべてのプロジェクトでパッケージが使用できるようになります。

Visual Studio 2017 バージョン 15.6 以前の場合、conda 環境は、「[既存の環境を手動で識別する](#manually-identify-an-existing-environment)」に記載の説明に従って手動でポイントすることにより使用できます。

Visual Studio 2017 バージョン 15.7 以降では、次のセクションに説明するように、conda 環境が自動的に検出され、 **[Python 環境]** ウィンドウに表示されます。

## <a name="manually-identify-an-existing-environment"></a>既存の環境を手動で識別する

標準と異なる場所にインストールされている環境 (Visual Studio 2017 バージョン 15.6 以前の conda 環境など) を識別するには、次の手順を使用します。

::: moniker range="vs-2017"

1. **[Python 環境]** ウィンドウで **[+ カスタム]** を選択します。 **[構成]** タブが開きます。

    ![新しいカスタム環境の既定のビュー](media/environments/environments-custom-1.png)

1. **[Description (説明)]** フィールドに環境の名前を入力します。

1. **[プレフィックス パス]** フィールドで、インタープリターのパスを入力するか参照します ( **...** を使用)。

1. Visual Studio がその場所 (次の図に示した conda 環境用のパスなど) で Python インタープリターを検出した場合は、 **[自動検出]** コマンドが有効になります。 **[自動検出]** を選択すると、残りのフィールドが入力されます。 これらのフィールドは、手動で入力することもできます。

    ![[自動検出] コマンドの有効化](media/environments/environments-custom-2.png)

    ![[自動検出] 使用後の環境フィールドの入力](media/environments/environments-custom-3.png)

1. フィールドに目的の値が入力されたら、 **[適用]** を選択して構成を保存します。 これで、他の環境と同じように、Visual Studio 内で使用できます。

1. 手動で識別した環境を削除する必要がある場合は、 **[構成]** タブの **[削除]** コマンドを選択します。自動検出された環境ではこのオプションは提供されません。 詳細については、「[タブを構成する](python-environments-window-tab-reference.md#configure-tab)」を参照してください。

::: moniker-end

::: moniker range=">=vs-2019"

1. **[Python 環境]** ウィンドウで (または、Python ツール バーから) **[+ 環境の追加]** を選択し、 **[環境の追加]** ダイアログ ボックスを開きます。 そのダイアログで、 **[既存の環境]** タブを選択します。

    ![[環境の追加] ダイアログの [既存の環境] タブ](media/environments/environments-custom-1-2019.png)

1. **[環境]** ドロップダウンを選択して、 **[カスタム]** を選択します。

    ![[環境の追加] ダイアログのカスタム環境オプション](media/environments/environments-custom-2-2019.png)

1. ダイアログ ボックスの **[プレフィックス パス]** フィールドで、インタープリターのパスを入力または参照 ( **[...]** を使用) します。これにより、他のほとんどのフィールドが設定されます。 それらの値を確認し、必要に応じて変更した後、 **[追加]** を選択します。

    ![[環境の追加] ダイアログのカスタム環境オプションの詳細を指定するためのフィールド](media/environments/environments-custom-3-2019.png)

1. 環境の詳細は、 **[Python 環境]** ウィンドウでいつでも確認および変更できます。 そのウィンドウで、環境を選択し、 **[構成]** タブを選択します。変更を行った後、 **[適用]** コマンドを選択します。 **[削除]** コマンドを使用して環境を削除することもできます (自動検出された環境には使用できません)。 詳細については、「[タブを構成する](python-environments-window-tab-reference.md#configure-tab)」を参照してください。
::: moniker-end

## <a name="fix-or-delete-invalid-environments"></a>無効な環境を修正または削除する

Visual Studio で環境のレジストリ エントリが検出されたものの、インタープリターへのパスが無効である場合、 **[Python 環境]** ウィンドウに取り消し線の付いた名前が表示されます。

::: moniker range="vs-2017"
![無効な環境を示す [Python 環境] ウィンドウ](media/environments/environments-invalid-entry.png)
::: moniker-end
::: moniker range=">=vs-2019"
![無効な環境を示す [Python 環境] ウィンドウ](media/environments/environments-invalid-entry-2019.png)
::: moniker-end

保持する環境を修正するには、まず、そのインストーラーの **修復** プロセスを使用してみます。 たとえば、標準的な Python 3.x のインストーラーにはそのオプションが含まれます。

修復オプションがない環境を修正する場合や、無効な環境を削除する場合は、次の手順を使用して直接レジストリを変更します。 Visual Studio では、レジストリの変更時に **[Python 環境]** ウィンドウが自動的に更新されます。

1. *regedit.exe* を実行します。
1. **HKEY_LOCAL_MACHINE\SOFTWARE\Python** または **HKEY_CURRENT_USER\SOFTWARE\Python** に移動します。 IronPython の場合は、代わりに **IronPython** を検索します。
1. **Python Core** (CPython の場合) や **ContinuumAnalytics** (Anaconda の場合) など、ディストリビューションと一致するノードを展開します。 IronPython の場合は、バージョン番号のノードを展開します。
1. **InstallPath** ノードの下の値を検査します。

    ![CPython の標準インストールのレジストリ エントリ](media/environments/environments-registry-entries.png)

    - コンピューター上にまだ環境が存在する場合は、**ExecutablePath** の値を正しい場所に変更します。 また、必要に応じて、 **(Default)** と **WindowedExecutablePath** の値を修正します。
    - コンピューター上に環境が既に存在せず、 **[Python 環境]** ウィンドウから削除する場合は、上のイメージの **3.6** など、**InstallPath** の親ノードを削除します。
    - **HKEY_CURRENT_USER\SOFTWARE\Python** の無効な設定で、**HKEY_LOCAL_MACHINE\SOFTWARE\Python** の設定が上書きされます

## <a name="see-also"></a>関連項目

- [Python インタープリターのインストール](installing-python-interpreters.md)
- [プロジェクトのインタープリターの選択](selecting-a-python-environment-for-a-project.md)
- [依存関係の requirements.txt の使用](managing-required-packages-with-requirements-txt.md)
- [検索パス](search-paths.md)
- [[Python 環境] ウィンドウ リファレンス](python-environments-window-tab-reference.md)