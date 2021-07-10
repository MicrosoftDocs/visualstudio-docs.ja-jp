---
title: Visual Studio の削除
titleSuffix: ''
description: コンピューターから Visual Studio を完全に削除する詳細な手順を説明します。
ms.date: 12/19/2019
ms.custom: seodec18
ms.topic: how-to
f1_keywords:
- uninstall
- uninstall Visual Studio
- remove
- remove Visual Studio
- cleanup
- cleanup Visual Studio
- clean up
- clean up Visual Studio
ms.assetid: 9c81a777-9c95-4934-b517-c60c6dc78799
author: j-martens
ms.author: jmartens
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: 5af0cf31d3a53b12910ea8108c93a99cbaf3e87f
ms.sourcegitcommit: 5fb4a67a8208707e79dc09601e8db70b16ba7192
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2021
ms.locfileid: "112306957"
---
# <a name="remove-visual-studio"></a>Visual Studio の削除

致命的なエラーが発生して Visual Studio の修復またはアンインストールができない場合は、`InstallCleanup.exe` ツールを実行して Visual Studio 2017、Visual Studio 2019、Visual Studio 2022 のすべてのインストール済みインスタンスのインストール ファイルと製品情報を削除することができます。

> [!WARNING]
> InstallCleanup ツールは、修復またはアンインストールが失敗した場合の **最終手段としてのみ** 使用してください。 このツールを使うと、他の Visual Studio インストールまたは他の製品の機能がアンインストールされ、場合によっては修復や再インストールが必要になる可能性があります。

## <a name="run-installcleanupexe"></a>InstallCleanup.exe を実行する

`InstallCleanup.exe` ツールでは、次のいずれかのコマンドライン スイッチを使用できます。

| Switch | 動作                                                                                                                                                                                                                                                                                                                 |
|--------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `-i`   | このスイッチは、他のスイッチが渡されない場合の既定値です。 メインのインストール ディレクトリと製品情報のみが削除されます。 `InstallCleanup.exe` ツールを実行した後に同じバージョンの Visual Studio を再インストールする場合は、このスイッチを使用します。                                                              |
| `-f`   | このスイッチを指定すると、メインのインストール ディレクトリ、製品情報、インストール ディレクトリ以外にインストールされているその他の多くの機能 (他の Visual Studio のインストールまたは他の製品とも共有されている可能性があります) が削除されます。 このスイッチは、Visual Studio を削除し、後で再インストールしない場合に使用します。 |

`InstallCleanup.exe` ツールの実行方法は次のとおりです。

1. Visual Studio インストーラーを閉じます。
1. 管理者のコマンド プロンプトを開きます。 管理者のコマンド プロンプトを開くには、以下の手順に従います。
   * [検索するテキストをここに入力] ボックスに、「**cmd**」と入力します。
   * **[コマンド プロンプト]** を右クリックしてから、 **[管理者として実行]** を選択します。
1. `InstallCleanup.exe` ツールの完全パスを入力し、必要なコマンドライン スイッチを追加します。 既定では、ツールのパスは次のようになります。 スペースを含むコマンドは二重引用符で囲みます。

   ```shell
   "C:\Program Files (x86)\Microsoft Visual Studio\Installer\resources\app\layout\InstallCleanup.exe"
   ```

   > [!NOTE]
   > Visual Studio インストーラー ディレクトリ以下に `InstallCleanup.exe` が見つからない場合は (常に `%ProgramFiles(x86)%\Microsoft Visual Studio` にあります)、次の手順を行います。 指示に従って [Visual Studio をインストール](install-visual-studio.md)します。 次にワークロードの選択画面が表示されたら、ウィンドウを閉じて、このページの手順に従います。

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>関連項目

* [Visual Studio のインストール](install-visual-studio.md)
* [Visual Studio の更新](update-visual-studio.md)
* [Visual Studio の変更](modify-visual-studio.md)
* [Visual Studio のアンインストール](uninstall-visual-studio.md)
