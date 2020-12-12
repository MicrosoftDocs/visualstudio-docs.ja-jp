---
title: クイック スタート - Python コードのフォルダーを開く
description: このクイック スタートでは、Visual Studio プロジェクトを使用せずに、フォルダーから Python コードを開いて実行します (Visual Studio 2019 のみ)。
ms.date: 03/12/2019
ms.topic: quickstart
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.custom: seodec18
ms.workload:
- python
- data-science
monikerRange: '>= vs-2019'
ms.openlocfilehash: a7bf174191a6a2fb013aa3d25880b01bc2e7f070
ms.sourcegitcommit: a801ca3269274ce1de4f6b2c3f40b58bbaa3f460
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/25/2020
ms.locfileid: "88801673"
---
# <a name="quickstart-open-and-run-python-code-in-a-folder"></a>クイック スタート: フォルダー内の Python コードを開いて実行する

[Visual Studio 2019 に Python のサポートをインストール](installing-python-support-in-visual-studio.md)した後は、Visual Studio プロジェクトを作成しなくても、Visual Studio 2019 で既存の Python コードを簡単に実行できます。

> [!Note]
> Visual Studio 2017 以前では、Python コードを実行するには Visual Studio プロジェクトを作成する必要がありますが、組み込みのプロジェクト テンプレートを使用すれば簡単に行うことができます。 例については、「[クイック スタート:既存のコードから Python プロジェクトを作成する](quickstart-01-python-in-visual-studio-project-from-existing-code.md)」をご覧ください

1. このチュートリアルでは、Python コードが含まれるフォルダーであれば好きなものを使用できます。 以下の例を進めるには、`git clone https://github.com/gregmalcolm/python_koans` コマンドを使用して、gregmalcolm/python_koans GitHub リポジトリをお使いのコンピューターの適当なフォルダーにクローンします。

1. Visual Studio 2019 を起動し、スタート ウィンドウで **[作業の開始]** 列の下部にある **[開く]** を選択します。 または、Visual Studio を既に実行している場合は、代わりに **[ファイル]**  >  **[開く]**  >  **[フォルダー]** コマンドを選択します。

    ![Visual Studio のスタートアップ画面](media/quickstart-open-folder/01-open-local-folder.png)

1. Python コードが格納されているフォルダーに移動し、 **[フォルダーの選択]** を選択します。 python_koans コードを使用している場合は、クローンしたフォルダー内の `python3` フォルダーを選択します。

    ![フォルダーを開くコマンドからの [フォルダーの選択] ダイアログ](media/quickstart-open-folder/02-select-folder.png)

1. Visual Studio の**ソリューション エクスプローラー**の**フォルダー ビュー**にフォルダーが表示されます。 フォルダー名の左端にある矢印を使用して、フォルダーを展開したり折りたたんだりできます。

    ![ソリューション エクスプローラーでフォルダーの展開や折りたたみを行うコントロール](media/quickstart-open-folder/03-expand-collapse-folders.png)

1. Python フォルダーを開くと、Visual Studio により、プロジェクトに関連する設定を管理するために、いくつかの隠しフォルダーが作成されます。 これらのフォルダー (および、 *.git* フォルダーなどの他の非表示ファイルや隠しフォルダー) を表示するには、 **[すべてのファイルを表示]** ツール バー ボタンを選択します。

    ![ソリューション エクスプローラーでの隠しフォルダーの表示](media/quickstart-open-folder/05-view-hidden-folders.png)

1. コードを実行するには、最初にスタートアップ ファイルまたはプライマリ プログラム ファイルを識別する必要があります。 この例では、スタートアップ ファイルは *contemplate-koans.py* です。 そのファイルを右クリックして、 **[スタートアップ アイテムとして設定]** を選択します。

    ![ソリューション エクスプローラーでのスタートアップ アイテムの設定](media/quickstart-open-folder/06-set-as-startup-item-command.png)

    > [!Important]
    > スタートアップ アイテムが開いたフォルダーのルートにない場合は、「[作業ディレクトリを設定する](#set-a-working-directory)」セクションで説明されているように、起動構成 JSON ファイルに行を追加する必要もあります。

1. **Ctrl**+**F5** キーを押すか、 **[デバッグ]**  >  **[デバッグなしで開始]** を選択して、コードを実行します。 再生ボタンの付いたスタートアップ アイテムを示すツール バーのボタンを選択することもできます。このようにすると、Visual Studio デバッガーでコードが実行されます。 どの場合でも、Visual Studio でスタートアップ アイテムが Python ファイルであることが検出されて、既定の Python 環境でコードが自動的に実行されます。 (その環境は、ツール バーのスタートアップ アイテムの右側に示されます。)

    ![デバッガー開始ツール バー ボタン](media/quickstart-open-folder/07-start-debug-toolbar.png)

1. プログラムの出力は、独立したコマンド ウィンドウに表示されます。

    ![Python コードを実行したときの出力ウィンドウ](media/quickstart-open-folder/08-result-window.png)

1. 別の環境でコードを実行するには、ツール バーのドロップダウン コントロールでその環境を選択し、スタートアップ アイテムをもう一度起動します。

1. Visual Studio でフォルダーを閉じるには、 **[ファイル]**  >  **[フォルダーを閉じる]** メニュー コマンドを選択します。

## <a name="set-a-working-directory"></a>作業ディレクトリを設定する

既定では、フォルダーとして開かれた Python プロジェクトはその同じフォルダーのルートで実行されます。 ただし、プロジェクトのコードでは、Python がサブフォルダーで実行されているものと想定される場合があります。 たとえば、python_koans リポジトリのルート フォルダーを開き、*python3/contemplate-koans.py* ファイルをスタートアップ アイテムとして設定するものとします。 それからコードを実行すると、*koans.txt* ファイルが見つからないというエラーが表示されます。 このエラーが発生するのは、*contemplate-koans.py* では Python がリポジトリのルートではなく *python3* フォルダーで実行されているものと想定されるためです。

そのような場合は、作業ディレクトリを指定する行を起動構成 JSON ファイルに追加する必要もあります。

1. **ソリューション エクスプローラー**で Python ( *.py*) スタートアップ ファイルを右クリックして、 **[デバッグ設定と起動設定]** を選択します。

    ![Python ファイルの [デバッグ設定と起動設定] コマンド](media/quickstart-open-folder/09-debug-launch-settings-menu-command.png)

1. **[デバッガーの選択]** ダイアログ ボックスが表示されたら、 **[既定]** 、 **[選択]** の順に選択します。

    ![Python ファイルの [デバッグ設定と起動設定] コマンド](media/quickstart-open-folder/10-select-debugger.png)

    > [!Note]
    > 選択肢として **[既定]** が表示されない場合は、 **[デバッグ設定と起動設定]** コマンドを選択するときに Python の *.py* ファイルを選択したことを確認してください。 Visual Studio では、ファイルの種類を使用して、表示するデバッガー オプションが決定されます。

1. Visual Studio で *launch.vs.json* という名前のファイルが開かれます。このファイルは隠しフォルダー *.vs* にあります。 このファイルでは、プロジェクトのデバッグ コンテキストが記述されています。 作業ディレクトリを指定するには、python-koans の例での `"workingDirectory": "python3"` のように、`"workingDirectory"` の値を追加します。

    ```json
    {
      "version": "0.2.1",
      "defaults": {},
      "configurations": [
        {
          "type": "python",
          "interpreter": "(default)",
          "interpreterArguments": "",
          "scriptArguments": "",
          "env": {},
          "nativeDebug": false,
          "webBrowserUrl": "",
          "project": "python3\\contemplate_koans.py",
          "name": "contemplate_koans.py",
          "workingDirectory": "python3"
        }
      ]
    }
    ```

1. ファイルを保存してプログラムを再び起動すると、指定したフォルダーで実行されるようになります。

## <a name="next-steps"></a>次の手順

> [!div class="nextstepaction"]
> [チュートリアル: Visual Studio での Python の使用](tutorial-working-with-python-in-visual-studio-step-01-create-project.md)

## <a name="see-also"></a>関連項目

- [クイック スタート:既存のコードから Python プロジェクトを作成する](quickstart-01-python-in-visual-studio-project-from-existing-code.md)」をご覧ください
- [クイック スタート:リポジトリから Python プロジェクトを作成する](quickstart-03-python-in-visual-studio-project-from-repository.md)
- [既存の Python インタープリターを手動で識別する](managing-python-environments-in-visual-studio.md#manually-identify-an-existing-environment)
