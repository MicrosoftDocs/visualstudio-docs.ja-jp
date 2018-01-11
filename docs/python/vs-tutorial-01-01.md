---
title: "Visual Studio での Python の使用、手順 1 | Microsoft Docs"
ms.custom: 
ms.date: 09/26/2017
ms.reviewer: 
ms.suite: 
ms.technology: devlang-python
ms.devlang: python
ms.tgt_pltfrm: 
ms.topic: get-started-article
caps.latest.revision: "1"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.workload: python
ms.openlocfilehash: adb49bb6070fee611a2ba67913943e68ee938d29
ms.sourcegitcommit: 32f1a690fc445f9586d53698fc82c7debd784eeb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/22/2017
---
# <a name="working-with-python-in-visual-studio"></a>Visual Studio での Python の使用

Python は、信頼性と柔軟性に優れ、簡単に学ぶことができ、すべてのオペレーティング システムで自由に使える一般的なプログラミング言語であり、強力な開発者コミュニティと多くの無料ライブラリによってサポートされています。 この言語は、Web アプリケーション、Web サービス、デスクトップ アプリ、スクリプト、科学技術計算などのすべての開発方法をサポートし、多くの大学、科学者、一般の開発者、プロの開発者によって同様に使われています。

Visual Studio は、Python 言語の最上のサポートを提供しています。 このチュートリアルに従って操作すると、以下の作業を実行できます。

- [手順 0: インストール](vs-tutorial-01-00.md)
- [手順 1: Python プロジェクトの作成 (このトピック)](#step-1-create-a-new-python-project)
- [手順 2: 動作中の Visual Studio IntelliSense を確認するためのコードの記述と実行](vs-tutorial-01-02.md)
- [手順 3: 対話型 REPL ウィンドウでの追加のコードの作成](vs-tutorial-01-03.md)
- [手順 4: 完成したプログラムの Visual Studio デバッガーでの実行](vs-tutorial-01-04.md)
- [手順 5: パッケージのインストールと Python 環境の管理](vs-tutorial-01-05.md)
- [手順 6: Git の使用](vs-tutorial-01-06.md)

## <a name="prerequisites"></a>必須コンポーネント

- Python のワークロードがインストールされた Visual Studio 2017。 手順については、「[手順 0](vs-tutorial-01-00.md)」を参照してください。

## <a name="step-1-create-a-new-python-project"></a>手順 1: 新しい Python プロジェクトの作成

*プロジェクト*とは、ソース コード、リソース、構成など、1 つのアプリケーションを生成する、1 つのまとまりとなるすべてのファイルの、Visual Studio での管理方法です。 プロジェクトでは、すべてのプロジェクト ファイル間の関係や、複数のプロジェクト間で共有されている外部リソースが形式化され、維持されます。 これにより、アドホック フォルダー、スクリプト、テキスト ファイル、またはユーザーの頭の中で単にプロジェクトの関係を管理するよりも、プロジェクトで、アプリケーションを楽に拡張し大きくすることができます。

このチュートリアルでは、簡単な空のコード ファイルを含むプロジェクトから開始します。

1. Visual Studio で **[ファイル] > [新規] > [プロジェクト]** (Ctrl + Shift + N) を選択し、**[新しいプロジェクト]** ダイアログを開きます。 ここでは、さまざまな言語のテンプレートを参照して、プロジェクト用に 1 つ選択して、Visual Studio がそのファイルをどこに配置するか指定します。

1. Python テンプレートを参照するには、左側で **[インストール済み]、[Python]** の順に選択するか、"Python" を検索します。 言語のツリー内の場所が思い出せない場合、検索はテンプレートを探す優れた方法です。

    ![Python プロジェクトが表示されている [新しいプロジェクト] ダイアログ](media/vs-getting-started-python-01-new-project.png)

    Python がサポートされている Visual Studio では、Bottle、Flask、および Django フレームワークを使用した Web アプリケーションを含む、多数のプロジェクト テンプレートが含まれていることに注目してください。 ただし、このチュートリアルでは、空のプロジェクトを作成することから始めます。

1. **[Python アプリケーション]** テンプレートを選択し、プロジェクト名を指定して、**[OK]** を選択します。 

1. しばらくすると、**ソリューション エクスプローラー** ウィンドウ (1) にプロジェクトの構造が表示されます。 既定のコード ファイルが、エディター (2) で開きます。 ソリューション エクスプローラーで選択された項目の追加情報を表示する、[プロパティ] ウィンドウ (3) も表示されます。ディスク上の正確な場所も表示されます。

    ![Python プロジェクトが表示されたソリューション エクスプローラー](media/vs-getting-started-python-02-windows.png)

1. プロジェクトのファイルとフォルダーを参照するためのソリューション エクスプローラーに、少し時間を割いて慣れてください。

    ![さまざまな機能が表示され展開されているソリューション エクスプローラー](media/vs-getting-started-python-03-solution-explorer.png)

    (1) [新しいプロジェクト] ダイアログ ボックスに指定した名前が使用され、太字で強調表示されているのがあなたのプロジェクトです。 ディスク上では、このプロジェクトは、プロジェクト フォルダーの `.pyproj` ファイルに該当します。

    (2) 最上位レベルにあるのは、*ソリューション*です。既定では、名前はプロジェクトと同じです。 ディスク上の `.sln` ファイルで表されるソリューションは、1 つ以上の関連プロジェクトのコンテナーです。 たとえば、Python アプリケーション用に C++ の拡張機能を記述した場合、その C++ プロジェクトは同じソリューション内に存在します。 ソリューションには、専用のテスト プログラム用のプロジェクトと共に、Web サービス用のプロジェクトも含まれる可能性があります。 

    (3) プロジェクトの下には、ソース ファイルがあります。この場合は、`.py` ファイルが 1 つだけあります。 ファイルを選択すると、[プロパティ] ウィンドウにそのプロパティが表示されます。 ファイルをダブルクリックすると、そのファイルに適した方法でファイルが開きます。

    (4) プロジェクトの下には、**[Python の環境]** ノードもあります。 これを展開すると、使用可能な Python インタープリターが表示されます。 インタープリター ノードを展開し、その環境 (5) にインストールされているライブラリを参照してください。

    ソリューション エクスプローラーで、いずれかのノードまたは項目を右クリックすると、適切なコマンドのメニューを表示できます。 たとえば、**[名前の変更]** コマンドを使用すると、プロジェクトとソリューションを含む、任意のノードまたは項目の名前を変更できます。

## <a name="next-steps"></a>次の手順

> [!div class="nextstepaction"]
> [コードを記述して実行する](vs-tutorial-01-02.md)

## <a name="going-deeper"></a>詳しい説明

- [Visual Studio の Python プロジェクト](python-projects.md)。
- [python.org で Python 言語を学習する](https://www.python.org)
- [初心者向けの Python](https://www.python.org/about/gettingstarted/) (python.org)
- [Microsoft Virtual Academy の無料 Python コース](https://mva.microsoft.com/search/SearchResults.aspx#!q=python)
- [Python に関して寄せられることの多い質問 (Microsoft Virtual Academy)](https://aka.ms/mva-top-python-questions)
