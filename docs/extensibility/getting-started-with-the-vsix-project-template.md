---
title: VSIX プロジェクトのテンプレートの概要 | Microsoft Docs
description: VSIX プロジェクト テンプレートを使用して拡張機能を作成する方法、または配置用の既存の拡張機能をパッケージ化する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 3/16/2019
ms.topic: how-to
helpviewer_keywords:
- Visual Studio SDK, VSIX project template
ms.assetid: 89fac33e-9380-4723-9b45-048a6e16f0ed
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 56573ee1add273c76ab96657c74207c3e2b620c3
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105057638"
---
# <a name="get-started-with-the-vsix-project-template"></a>VSIX プロジェクト テンプレートの概要

VSIX プロジェクト テンプレートを使用して拡張機能を作成する方法、または配置用の既存の拡張機能をパッケージ化することができます。 VSIX プロジェクト テンプレートには Visual Basic と Visual C# の両方のバージョンがあり、Visual Studio SDK の一部としてインストールされます。

 VSIX プロジェクト テンプレートは、*source.extension.vsixmanifest* ファイルで構成されています。このファイルには、提供する拡張機能とそれに付属するアセットに関する情報が含まれています。

 VSIX プロジェクト テンプレートを見つけるには、Visual Studio SDK をインストールする必要があります。 詳細については、「[Visual Studio SDK](../extensibility/visual-studio-sdk.md)」を参照してください。

## <a name="deploy-a-custom-project-template-using-the-vsix-project-template"></a>VSIX プロジェクト テンプレートを使用したカスタム プロジェクト テンプレートの配置

 次の手順では、VSIX プロジェクトを使用して、他の開発者と共有したり、Visual Studio ギャラリーにアップロードしたりできるプロジェクト テンプレートをパッケージ化する方法について説明します。

1. プロジェクト テンプレートを作成します。

    1. テンプレートを作成するプロジェクトを開きます。 このプロジェクトは、任意のプロジェクト タイプにすることができます。

    2. **[プロジェクト]** メニューの **[テンプレートのエクスポート]** をクリックします。 ウィザードの手順を完了します。

         *%USERPROFILE%\My Documents\Visual Studio {version}\My Exported Templates\\* に *.zip* が作成されます。

2. 空の VSIX プロジェクトを作成します。

     **[File]**  >  **[New]**  >  **[Project]** の順に選択します。 検索ボックスに「vsix」と入力し、**VSIX プロジェクト** の **C#** または **Visual Basic** バージョンを選択します。

3. プロジェクトに *.zip* ファイルを追加します。 **[出力ディレクトリにコピー]** プロパティを `Copy Always` に設定します。

4. **ソリューション エクスプローラー** で、*source.extension.vsixmanifest* ファイルをダブルクリックして **VSIX マニフェスト デザイナー** でそれを開き、次のように変更します。

    - **[製品名]** フィールドを「**My Project Template**」に設定します。

    - **[製品 ID]** フィールドを「**MyProjectTemplate - 1**」に設定します。

    - **[作成者]** フィールドを「**Fabrikam**」に設定します。

    - **[説明]** フィールドを「**マイ プロジェクト テンプレート**」に設定します。

    - **[アセット]** セクションで、**Microsoft.VisualStudio.ProjectTemplate** 型を追加し、そのパスを *.zip* ファイルの名前に設定します。

5. *source.extension.vsixmanifest* ファイルを保存して閉じます。

6. プロジェクトをビルドします。

7. 出力ディレクトリで、 *.vsix* ファイルをダブルクリックします。

8. **VSIX インストーラー** のメッセージ ボックスが表示されます。 手順に従って拡張機能をインストールします。

9. Visual Studio をいったん閉じて開きなおします。

::: moniker range="vs-2017"

10. **[ツール]** メニューの **[拡張機能と更新プログラム]** を選択し、 **[テンプレート]** カテゴリを選択します。 使用可能な拡張機能の 1 つが、**My Project Template** になっているはずです。

::: moniker-end

::: moniker range=">=vs-2019"

10. **[拡張機能]** メニューの **[拡張機能の管理]** を選択し、 **[テンプレート]** カテゴリを選択します。 使用可能な拡張機能の 1 つが、**My Project Template** になっているはずです。

::: moniker-end

11. 新しいプロジェクト テンプレートは、元のプロジェクト テンプレートと同じ場所にある **[新しいプロジェクト]** ダイアログに表示されます。 たとえば、Visual Basic コンソール アプリケーションから **VB Console** という名前のテンプレートを作成した場合、**VB Console** は、Visual Basic **コンソール アプリケーション** テンプレートと同じウィンドウに表示されます。

### <a name="to-specify-the-location-of-the-template-in-the-new-project-dialog-box"></a>[新しいプロジェクト] ダイアログ ボックスでテンプレートの場所を指定する方法

1. テンプレート フォルダーは、 *{Visual Studio インストール パス}\Common7\IDE\ProjectTemplates* と *{Visual studio インストールパス}\Common7\IDE\ItemTemplates* ディレクトリにあります。 **[新しいプロジェクト]** ダイアログ ボックスの最上位セクションの名前は、テンプレート フォルダーの名前と完全には一致しません。 違いがある場合は、テンプレート フォルダーの名前を使用します。

    *.vsix* ファイル拡張子を *.zip* に変更し、ファイルを開きます。

2. テンプレートが表示されるはずの **[新しいプロジェクト]** ダイアログのセクションと同じ名前の新しいフォルダーを作成します。

3. テンプレートがサブセクションに表示される場合は、同じ名前のサブフォルダーを作成します。

4. テンプレートの *.zip* ファイルを新しいフォルダーに移動します。

5. *.zip* 拡張子を *.vsix* に変更します。

6. VSIX マニフェストを開きます。

7. VSIX マニフェストで、テンプレート ファイルを含むディレクトリ ツリーのルートをポイントするように、テンプレートの **アセット** パスを更新します。 たとえば、テンプレートが *\CSharp\Windows* にある場合、参照は *\CSharp* をポイントする必要があります。
