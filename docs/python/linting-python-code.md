---
title: PyLint を使用した Python コードの lint
description: Visual Studio で PyLint を使って、Python コードの問題を調べる方法を説明します。
ms.date: 07/12/2017
ms.prod: visual-studio-dev15
ms.technology: vs-python
ms.topic: conceptual
author: kraigb
ms.author: kraigb
manager: douge
ms.workload:
- python
- data-science
ms.openlocfilehash: 4e47de7be6587f0e8c967ba458a65906c80f2e5b
ms.sourcegitcommit: 42ea834b446ac65c679fa1043f853bea5f1c9c95
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/19/2018
---
# <a name="using-pylint-to-check-python-code"></a>PyLint を使用した Python コードのチェック

Visual Studio for Python プロジェクトには [PyLint](https://www.pylint.org/) が組み込まれています。これは広く用いられている Python コードのエラー チェックツールで、優れた Python のコード パターンを作成するのに役立ちます。

使用するには、ソリューション エクスプローラーで Python プロジェクトを右クリックし、**[Python] > [Run PyLint (PyLint の実行)]** を選択するだけです。

![Python プロジェクトのコンテキスト メニューに表示された PyLint コマンド](media/code-pylint-command.png)

このコマンドを使用すると、PyLint が存在しない場合は、アクティブな環境内に PyLint をインストールするように求められます。

PyLint の警告とエラーが [エラー一覧] ウィンドウに表示されます。

![PyLint のエラー一覧](media/code-pylint-error-list.png)

エラーをダブルクリックすると、問題が発生したソース コードに直接移動できます。

> [!Tip]
> PyLint のすべての出力メッセージの詳細な一覧については、[PyLint の機能のリファレンス](https://pylint.readthedocs.io/en/latest/technical_reference/features.html)に関するページをご覧ください。

## <a name="setting-pylint-command-line-options"></a>PyLint コマンド ライン オプションの設定

PyLint ドキュメントの[コマンド ライン オプション](https://pylint.readthedocs.io/en/latest/user_guide/run.html#command-line-options)のセクションでは、`.pylintrc` 構成ファイルを使用して PyLint の動作を制御する方法が説明されています。 このようなファイルは Visual Studio 内の Python プロジェクトのルートに配置するか、設定を適用したい範囲に応じて他の場所に配置します (詳しくは、[コマンドライン オプション](https://pylint.readthedocs.io/en/latest/user_guide/run.html#command-line-options)に関するページをご覧ください)。

たとえば、前の画像に表示されている "docstring が見つかりません" という警告がプロジェクト内の `.pylintrc` ファイルに対して表示されないようにするには、次の手順を実行します。

1. コマンド ラインで、プロジェクトのルート (`.pyproj` ファイルが含まれる) に移動し、次のコマンドを実行してコメント付きの構成ファイルを生成します。

   ```command
   pylint --generate-rcfile > .pylintrc
   ```

1. Visual Studio のソリューション エクスプローラーでプロジェクトを右クリックし、**[追加] > [既存の項目]** を選択します。新しい `.pylintrc` ファイルを見つけて選択し、**[追加]** を選択します。

1. ファイルを編集のために開くと、操作できる各種の設定が表示されます。 警告を無効にするには、`[MESSAGES CONTROL]` セクションを探し、そのセクションの `disable` 設定を見つけます。 特定のメッセージからなる長い文字列が表示されます。ここに目的の警告を追加できます。 この例では、`,missing-docstring` (区切りコンマを含む) を追加します。

1. `.pylintrc` ファイルを保存し、PyLint をもう一度実行して、警告が表示されなくなったことを確認します。

> [!Tip]
> ネットワーク共有から `.pylintrc` ファイルを使用するには、「`PYLINTRC`」という名前の環境変数を作成します。ネットワーク共有のファイル名の値には、UNC パスまたはマッピングされたドライブ文字を使用します。 たとえば、`PYLINTRC=\\myshare\python\.pylintrc` のようにします。
