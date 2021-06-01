---
title: Visual Studio でのテンプレート検出に関するトラブルシューティング | Microsoft Docs
description: Visual Studio SDK でのカスタム プロジェクトとテンプレートの配置に関するトラブルシューティングのために、診断ログを有効にする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 01/02/2018
ms.topic: troubleshooting
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 82b7b3f5eced4c8e24830fba34e47d224186949d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105072950"
---
# <a name="troubleshooting-template-installation"></a>テンプレート インストールのトラブルシューティング

プロジェクトまたは項目テンプレートの配置時に問題が発生した場合は、診断ログを有効にすることができます。

::: moniker range="vs-2017"

1. インストール用の *Common7\IDE\CommonExtensions* フォルダーに pkgdef ファイルを作成します。 たとえば、*C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise\Common7\IDE\CommonExtensions\EnablePkgDefLogging.pkgdef* です。

::: moniker-end

::: moniker range=">=vs-2019"

1. インストール用の *Common7\IDE\CommonExtensions* フォルダーに pkgdef ファイルを作成します。 たとえば、*C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise\Common7\IDE\CommonExtensions\EnablePkgDefLogging.pkgdef* です。

::: moniker-end

2. 次の内容を pkgdef ファイルに追加します。

    ```
    [$RootKey$\VsTemplate]
    "EnableTemplateDiscoveryLog"=dword:00000001
    ```

3. インストールの [[開発者コマンド プロンプト]](../ide/reference/command-prompt-powershell.md) を開き、`devenv /updateConfiguration` を実行します。

::: moniker range="vs-2017"

4. Visual Studio を開き、[新しいプロジェクト] ダイアログ ボックスと [新しい項目] ダイアログ ボックスを起動して、両方のテンプレート ツリーを初期化します。

   テンプレート ログが **%LOCALAPPDATA%\Microsoft\VisualStudio\15.0_[instanceid]\VsTemplateDiagnosticsList.csv** に表示されます (instanceid は Visual Studio のインスタンスのインストール ID に対応します)。 各テンプレート ツリーの初期化により、このログにエントリが追加されます。

::: moniker-end

::: moniker range=">=vs-2019"

4. Visual Studio を開き、 **[新しいプロジェクトの作成]** ダイアログ ボックスと **[新しい項目]** ダイアログ ボックスを起動して、両方のテンプレート ツリーを初期化します。

   テンプレート ログが **%LOCALAPPDATA%\Microsoft\VisualStudio\16.0_[instanceid]\VsTemplateDiagnosticsList.csv** に表示されます (instanceid は Visual Studio のインスタンスのインストール ID に対応します)。 各テンプレート ツリーの初期化により、このログにエントリが追加されます。

::: moniker-end

このログ ファイルには、次の列が含まれています。

- **FullPathToTemplate**。次の値があります。

  - マニフェストベースの配置の場合は 1

  - ディスクベースの配置の場合は 0

- **TemplateFileName**

- その他のテンプレートのプロパティ

> [!NOTE]
> ログを無効にするには、pkgdef ファイルを削除するか、`EnableTemplateDiscoveryLog` の値を `dword:00000000` に変更してから、`devenv /updateConfiguration` を再度実行します。

## <a name="see-also"></a>こちらもご覧ください

- [カスタム プロジェクト テンプレートと項目テンプレートの作成](creating-custom-project-and-item-templates.md)
- [Visual Studio トラブルシューティング](/troubleshoot/visualstudio/welcome-visual-studio/)
