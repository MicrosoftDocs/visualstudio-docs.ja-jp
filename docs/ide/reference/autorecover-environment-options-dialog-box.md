---
title: '[自動バックアップ] ([オプション] ダイアログ ボックス - [環境])'
description: '[自動バックアップ]、[環境]、[オプション] ダイアログ ボックスの概要、およびそれを使用してファイルを自動的にバックアップするかどうかを指定する方法について説明します。'
ms.custom: SEO-VS-2020
ms.date: 08/14/2020
ms.topic: reference
f1_keywords:
- VS.DialogAutoRestore
- VS.ToolsOptionsPages.Environment.AutoRecover
- VS.ToolsOptionsPages.Environment.Auto_Save_and_Restore
helpviewer_keywords:
- files, recovering
- AutoRecover page
- saving files, automatically
- files, saving automatically
ms.assetid: 397e5e44-4bbe-4289-94d1-642b466c9111
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 007e82ee7c1c2839ba266794432605f1f92a1669
ms.sourcegitcommit: 5fb4a67a8208707e79dc09601e8db70b16ba7192
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2021
ms.locfileid: "112307792"
---
# <a name="autorecover-environment-options-dialog-box"></a>[自動バックアップ]\ ([オプション] ダイアログ ボックス - [環境])

**[オプション]** ダイアログ ボックスのこのページを使用し、ファイルを自動的にバックアップするかどうかを指定します。 Visual Studio が突然終了した場合に、変更したファイルを復元するかどうかを指定することもできます。

このダイアログ ボックスにアクセスするには、 **[ツール]** 、 **[オプション]** 、 **[環境]** 、 **[自動バックアップ]** の順に進みます。

:::image type="content" source="media/autorecover-options.png" alt-text="[オプション] ダイアログ ボックスの [自動バックアップ] セクションのスクリーンショット":::

**自動バックアップの実行間隔: [n] 分**

::: moniker range=">=vs-2022"

このオプションを使用し、エディターでファイルを自動的に保存する頻度をカスタマイズします。 以前に保存したファイルについては、Visual Studio の場合、***%LocalAppData%\Microsoft\VisualStudio\BackupFiles\\[projectname]*** にファイルのコピーが保存されます。 ファイルが新しく、手動でまだ保存していない場合、Visual Studio では、ランダムに生成されたファイル名でファイルが自動保存されます。

::: moniker-end

::: moniker range="vs-2019"

このオプションを使用し、エディターでファイルを自動的に保存する頻度をカスタマイズします。 以前に保存したファイルについては、Visual Studio 2019 バージョン 16.2 以降の場合、***%LocalAppData%\Microsoft\VisualStudio\BackupFiles\\[プロジェクト名]*** にファイルのコピーが保存されます。 ファイルが新しく、手動でまだ保存していない場合、Visual Studio では、ランダムに生成されたファイル名でファイルが自動保存されます。

> [!NOTE]
> Visual Studio 2019 バージョン 16.1 以前を使用している場合、ファイルの場所は *%USERPROFILE%\Documents\Visual Studio [バージョン]\Backup Files\\[プロジェクト名]* です。 詳細については、「[Visual Studio 2019 リリース ノート履歴](/visualstudio/releases/2019/release-notes-history/)」を参照してください。

::: moniker-end

::: moniker range="vs-2017"

このオプションを使用し、エディターでファイルを自動的に保存する頻度をカスタマイズします。 以前に保存したファイルに関しては、Visual Studio 2017 では、 *%USERPROFILE%\Documents\Visual Studio [バージョン]\Backup Files\\[プロジェクト名]* にファイルのコピーが保存されます。 ファイルが新しく、手動でまだ保存していない場合、Visual Studio では、ランダムに生成されたファイル名でファイルが自動保存されます。

::: moniker-end

**自動バックアップした情報の保存期間: [n] 日**

このオプションを使用し、Visual Studio で自動バックアップのために作成したファイルを保存する期間を指定します。

### <a name="see-also"></a>関連項目

- [[オプション] ダイアログ ボックス](../../ide/reference/options-dialog-box-visual-studio.md)
