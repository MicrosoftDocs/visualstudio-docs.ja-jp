---
title: Visual Studio でテンプレートを整理する
ms.date: 01/02/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- project templates [Visual Studio], locations
- item templates [Visual Studio], locations
- template locations [Visual Studio]
- Visual Studio templates, organizing
- templates [Visual Studio], organizing
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 65d4940e7a7969fe28fe115ec7ef42cfdc645c9a
ms.sourcegitcommit: e13e61ddea6032a8282abe16131d9e136a927984
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
---
# <a name="how-to-locate-and-organize-project-and-item-templates"></a>方法: プロジェクト テンプレートと項目テンプレートを配置して整理する

テンプレートを **[新しいプロジェクト]** ダイアログ ボックスや **[新しい項目の追加]** ダイアログ ボックスに表示するためには、Visual Studio が認識する場所にテンプレート ファイルを配置する必要があります。 ユーザー テンプレートの場所にカスタム サブカテゴリを作成することも可能で、カテゴリは **[新しいプロジェクト]** ダイアログ ボックスと **[新しい項目の追加]** ダイアログ ボックスに表示されます。

## <a name="locate-templates"></a>テンプレートの検索

インストールされたテンプレートとユーザー テンプレートは、2 つの異なる場所に格納されます。

### <a name="user-templates"></a>ユーザー テンプレート

**.vstemplate** ファイルを含む圧縮 (**.zip**) ファイルをユーザー テンプレート ディレクトリに追加すると、そのテンプレートは *[新しいプロジェクト]* ダイアログ ボックスまたは *[新しい項目の追加]* ダイアログ ボックスに表示されます。 既定では、ユーザー テンプレートは次の場所に配置されます。

- *%USERPROFILE%\Documents\Visual Studio \<バージョン\>\Templates\ProjectTemplates*

- *%USERPROFILE%\Documents\Visual Studio \<バージョン\>\Templates\ItemTemplates*

たとえば、次のディレクトリには C# 用のユーザー プロジェクト テンプレートがあります。

- *C:\Users\UserName\Documents\Visual Studio 2017\Templates\ProjectTemplates\Visual C#*

> [!TIP]
> ユーザー テンプレートの場所は、**[ツール]** > **[オプション]** > **[プロジェクトおよびソリューション]** > **[場所]** で設定できます。

### <a name="installed-templates"></a>インストールされたテンプレート

既定では、Visual Studio でインストールされるテンプレートは次の場所にあります。

- *\\<VisualStudioInstallationDirectory\>\Common7\IDE\ItemTemplates\\<プログラミング言語\>\\<Locale ID>*

- *\\<VisualStudioInstallationDirectory\>\Common7\IDE\ProjectTemplates\\<プログラミング言語\>\\<Locale ID>*

たとえば、次のディレクトリには英語 (LCID 1033) 用の Visual Basic 項目テンプレートがあります。

- *C:\\<VisualStudioInstallationDirectory\>\Common7\IDE\ItemTemplates\VisualBasic\1033*

## <a name="organize-templates"></a>テンプレートの整理

**[新しいプロジェクト]** ダイアログ ボックスおよび **[新しい項目の追加]** ダイアログ ボックスのカテゴリには、インストールされたテンプレートおよびユーザー テンプレートの場所に存在するディレクトリ構造が反映されます。 ユーザー テンプレート ディレクトリに新しいフォルダーを追加することで、ユーザー テンプレートを独自のカテゴリに整理できます。 **[新しいプロジェクト]** ダイアログ ボックスと **[新しい項目の追加]** ダイアログ ボックスには、ユーザー テンプレート カテゴリに加えた変更が表示されます。

> [!NOTE]
> プログラミング言語のレベルでは、新しいカテゴリを作成できません。 新しいカテゴリは、各言語内でのみ作成できます。

### <a name="to-create-new-user-project-template-categories"></a>ユーザー プロジェクト テンプレートの新しいカテゴリを作成するには

1. ユーザー プロジェクト テンプレートのディレクトリのプログラミング言語フォルダーに、フォルダーを作成します。 たとえば、C# プロジェクト テンプレートに **HelloWorld** カテゴリを設定するには、次のディレクトリを作成します。

    - *\%USERPROFILE%\Documents\Visual Studio \<バージョン\>\Templates\ProjectTemplates\Visual C#\HelloWorld*

1. このカテゴリのすべてのテンプレートを新しいフォルダーに配置します。

1. **[ファイル]** メニューで、**[新規]** > **[プロジェクト]** の順に選択します。

   **HelloWorld** カテゴリが、**[新しいプロジェクト]** ダイアログ ボックスの **[インストール済み]** > **[Visual C#]** に表示されます。

### <a name="to-create-new-user-item-template-categories"></a>ユーザー項目テンプレートの新しいカテゴリを作成するには

1. ユーザー項目テンプレートのディレクトリのプログラミング言語フォルダーに、フォルダーを作成します。 たとえば、C# 項目テンプレートに **HelloWorld** カテゴリを設定するには、次のディレクトリを作成します。

    - *\%USERPROFILE%\Documents\Visual Studio \<バージョン\>\Templates\ItemTemplates\Visual C#\HelloWorld*

1. このカテゴリのすべてのテンプレートを新しいフォルダーに配置します。

1. プロジェクトを作成するか、既存のプロジェクトを開きます。 その後、**[プロジェクト]** メニューの **[新しい項目の追加]** を選択します。

   **HelloWorld** カテゴリが、**[新しい項目の追加]** ダイアログ ボックスの **[インストール済み]** > **[Visual C# アイテム]** に表示されます。

### <a name="display-templates-in-parent-categories"></a>親カテゴリでのテンプレートの表示

*.vstemplate* ファイルの `NumberOfParentCategoriesToRollUp` 要素を使用して、サブカテゴリのテンプレートを親カテゴリに表示できます。 この手順は、プロジェクト テンプレートと項目テンプレートで同じです。

#### <a name="to-display-templates-in-parent-categories"></a>親カテゴリにテンプレートを表示するには

1. テンプレートを含む *.zip* ファイルを探します。

1. *.zip* ファイルを展開します。

1. Visual Studio で *.vstemplate* ファイルを開きます。

1. `TemplateData` 要素に、`NumberOfParentCategoriesToRollUp` 要素を追加します。 たとえば、次のコードを実行すると、テンプレートが親カテゴリに表示されますが、親カテゴリよりも上のレベルでは表示されません。

    ```xml
    <TemplateData>
        ...
        <NumberOfParentCategoriesToRollUp>
            1
        </NumberOfParentCategoriesToRollUp>
        ...
    </TemplateData>
    ```

1. *.vstemplate* ファイルを保存して、閉じます。

1. テンプレートのファイルを選んで右クリックし、**[送る]** > **[圧縮 (zip 形式) フォルダー]** の順に選択します。

   ファイルは *.zip* ファイルに圧縮されます。

1. 抽出したテンプレート ファイルと古いテンプレート *.zip* ファイルを削除します。

1. 削除した *.zip* ファイルが含まれていたディレクトリに、新しい *.zip* ファイルを配置します。

## <a name="see-also"></a>関連項目

- [テンプレートのカスタマイズ](../ide/customizing-project-and-item-templates.md)
- [Visual Studio テンプレート スキーマ参照 (機能拡張)](../extensibility/visual-studio-template-schema-reference.md)
- [NumberOfParentCategoriesToRollUp (Visual Studio テンプレート)](../extensibility/numberofparentcategoriestorollup-visual-studio-templates.md)
- [方法: プロジェクト テンプレートを作成する](../ide/how-to-create-project-templates.md)
- [方法: 項目テンプレートを作成する](../ide/how-to-create-item-templates.md)