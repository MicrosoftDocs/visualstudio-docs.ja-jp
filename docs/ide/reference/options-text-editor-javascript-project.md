---
title: '[オプション]、[テキスト エディター]、[JavaScript]、[プロジェクト]'
ms.date: 1/15/2019
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.JavaScript.Project.General
- VS.ToolsOptionsPages.Text_Editor.JavaScript.Project
- VS.ToolsOptionsPages.Text_Editor.TypeScript.Project.General
- VS.ToolsOptionsPages.Text_Editor.TypeScript.Project
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ff2fc32a173f1c05fc200c9acd9b37ad2307a3a3
ms.sourcegitcommit: 2193323efc608118e0ce6f6b2ff532f158245d56
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/25/2019
ms.locfileid: "55031813"
---
# <a name="options-text-editor-javascript-project"></a>[オプション]、[テキスト エディター]、[JavaScript]、[プロジェクト]

**[オプション]** ダイアログ ボックスの **[プロジェクト]** ページを使用して、コード エディターで JavaScript プロジェクトに適用されるオプションを指定します。 このページにアクセスするには、メニュー バーで **[ツール]** > **[オプション]** をクリックし、**[テキスト エディター]** > **[JavaScript]** > **[プロジェクト]** を展開します。

## <a name="project-analysis-options"></a>プロジェクト解析オプション

これらのオプションは、エディターでプロジェクトの分析、診断のレポート、および機能強化の提案をどのように実行するかを決定します。 これらの状況をエディターでどのように処理するかを指定するには、オプションを選択するか、選択解除します。

### <a name="uielement-list"></a>UIElement の一覧

- **エディターで開いているファイルを含むプロジェクトのみ分析する**
- **エディターで開いているファイルの診断のみ報告する**
- **修正ではなく、実行できる機能強化を提案する**

## <a name="virtual-projects-in-solution-explorer"></a>ソリューション エクスプローラーの仮想プロジェクト

これらのオプションを使用して、ソリューションが読み込まれているか読み込まれていないときに、仮想プロジェクトを表示するかどうかを選択できます。

## <a name="compile-on-save"></a>保存時にコンパイル

これらのオプションは、プロジェクトの一部ではない TypeScript ファイルが自動的にコンパイルされるかどうかを決定します。 チェック ボックスをオンにした後、使用するコード生成の種類を選択します。

### <a name="uielement-list"></a>UIElement の一覧

- **プロジェクトの一部ではないモジュールでは AMD コード生成を使用する**
- **プロジェクトの一部ではないモジュールでは CommonJS コード生成を使用する**
- **プロジェクトの一部ではないモジュールでは UMD コード生成を使用する**
- **プロジェクトの一部ではないモジュールではシステム コード生成を使用する**
- **プロジェクトの一部ではないモジュールでは ES2015 コード生成を使用する**

## <a name="ecmascript-version-for-files-that-are-not-part-of-a-project"></a>プロジェクトの一部ではないファイル用の ECMAScript のバージョン

これらのオプションを使用して、プロジェクトの一部ではないファイル用の ECMAScript のバージョンを選択できます。 **[ECMAScript 3]**、**[ECMAScript 5]**、または **[ECMAScript 6]** から選択できます。

## <a name="jsx-emit-for-tsx-files-that-are-not-part-of-a-project"></a>プロジェクトの一部ではない TSX ファイルに対する JSX の発行

これらのオプションは、プロジェクトの一部ではない TypeScript ファイルをエディターでどのように処理するかを決定します。

### <a name="uielement-list"></a>UIElement の一覧

|オプション|説明|
|------------|-----------------|
|**React フレームワーク**|このオプションをオンにすると、コード エディターによって *.js* ファイル拡張子が出力されます。|
|**Preserve**|このオプションを選択すると、コード エディターでは出力の一部として JSX が保持され、*.jsx* ファイル拡張子が出力されます。|

## <a name="see-also"></a>関連項目

- [[全般]、[環境]、[オプション] ダイアログ ボックス](../../ide/reference/general-environment-options-dialog-box.md)