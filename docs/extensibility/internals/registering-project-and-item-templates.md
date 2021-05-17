---
title: プロジェクトと項目テンプレートの登録 | Microsoft Docs
description: Visual Studio でプロジェクト タイプに関する登録情報を使用して、[新しいプロジェクトの追加] および [新しい項目の追加] ダイアログ ボックスに表示する内容を判断する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], adding items
- registry, Add New Item dialog box
- Add New Item dialog box
- Add New Project dialog box
- registry, Add New Project dialog box
ms.assetid: 6b909f93-d7f5-4aec-81c6-ee9ff0f31638
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d6f4abe3a8632f4fe9208922aee1ccd92da3dab5
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105062695"
---
# <a name="registering-project-and-item-templates"></a>プロジェクトと項目テンプレートの登録
プロジェクト タイプでは、プロジェクト テンプレートとプロジェクト項目テンプレートが配置されているディレクトリを登録する必要があります。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] では、プロジェクト タイプに関連付けられた登録情報を使用して、 **[新しいプロジェクトの追加]** および **[新しい項目の追加]** ダイアログ ボックスに表示する内容を判断します。

 詳細については、「[プロジェクト テンプレートとプロジェクト項目テンプレートの追加](../../extensibility/internals/adding-project-and-project-item-templates.md)」を参照してください。

## <a name="registry-entries-for-projects"></a>プロジェクトのレジストリ エントリ
 次の例では、HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\\<*Version*> の下にあるレジストリ エントリを示します。 下の表では、例で使用される要素について説明します。

```
[Projects\{ProjectGUID}]
@="MyProjectType"
"DisplayName"="#2"
"Package"="{VSPackageGUID}"
"ProjectTemplatesDir"="C:\\MyProduct\\MyProjectTemplates"
```

|名前|Type|説明|
|----------|----------|-----------------|
|@|REG_SZ|この種類のプロジェクトの既定の名前。|
|DisplayName|REG_SZ|パッケージに登録されているサテライト DLL から取得する名前のリソース ID。|
|パッケージ|REG_SZ|パッケージに登録されているパッケージのクラス ID。|
|ProjectTemplatesDir|REG_SZ|プロジェクト テンプレート ファイルの既定のパス。 プロジェクト テンプレート ファイルは、 **[新しいプロジェクト]** テンプレートによって表示されます。|

### <a name="registering-item-templates"></a>項目テンプレートの登録
 項目テンプレートを格納するディレクトリを登録する必要があります。

```
[Projects\{ProjectGUID}\AddItemTemplates\TemplateDirs\{VSPackageGUID}\1]
@="#7"
"TemplatesDir"="C:\\MyProduct\\MyProjectItemTemplates "
"TemplatesLocalizedSubDir"="#10"
"SortPriority"=dword:00000064
```

| 名前 | Type | 説明 |
|--------------------------|-----------| - |
| @ | REG_SZ | [項目の追加] テンプレートのリソース ID。 |
| TemplatesDir | REG_SZ | **[新しい項目の追加]** ウィザードのダイアログ ボックスに表示されるプロジェクト項目のパス。 |
| TemplatesLocalizedSubDir | REG_SZ | ローカライズされたテンプレートを保持する TemplatesDir のサブディレクトリに名前を指定する文字列のリソース ID。 サテライト DLL がある場合、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ではそこから文字列リソースを読み込むため、サテライト DLL ごとに異なるローカライズされたサブディレクトリ名を含めることができます。 |
| SortPriority | REG_DWORD | **[新しい項目の追加]** ダイアログ ボックスでのテンプレートの表示順序を制御するには、SortPriority を設定します。 SortPriority 値は大きいほどテンプレート リストの前の方に表示されます。 |

### <a name="registering-file-filters"></a>ファイル フィルターの登録
 必要に応じて、ファイル名の入力が求められたときに [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] で使用されるフィルターを登録できます。 たとえば、 **[ファイルを開く]** ダイアログ ボックスの [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] フィルターは次のとおりです。

 **Visual C# Files (\*.cs,\*.resx,\*.settings,\*.xsd,\*.wsdl);\*.cs,\*.resx,\*.settings,\*.xsd,\*.wsdl)**

 複数のフィルターの登録をサポートするために、各フィルターは HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\\<*Version*>\Projects\\{\<*ProjectGUID*>}\Filters\\<*Subkey*> の下に独自のサブキーとして登録されます。 サブキー名は任意です。[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ではサブキーの名前が無視され、その値だけが使用されます。

 次の表に示すように、フラグを設定して、フィルターを使用するコンテキストを制御できます。 フィルターにフラグが設定されていない場合、 **[既存項目の追加]** ダイアログ ボックスと **[ファイルを開く]** ダイアログ ボックスの共通フィルターの後に一覧表示されますが、 **[フォルダーを指定して検索]** ダイアログ ボックスでは使用されません。

```
[Projects\{ProjectGUID}\Filters\MyLanguageFilter]
@="#3"
"CommonOpenFilesFilter"=dword:00000000
"CommonFindFilesFilter"=dword:00000000
"FindInFilesFilter"=dword:00000000
"NotOpenFileFilter"=dword:00000000
"NotAddExistingItemFilter"=dword:00000000
"SortPriority"=dword:00000064
```

|名前|Type|説明|
|----------|----------|-----------------|
|CommonFindFilesFilter|REG_DWORD|フィルターを、 **[フォルダーを指定して検索]** ダイアログ ボックスの共通フィルターの 1 つにします。 共通フィルターは、フィルター一覧で、共通としてマークが付けられていないフィルターの前に一覧表示されます。|
|CommonOpenFilesFilter|REG_DWORD|フィルターを、 **[ファイルを開く]** ダイアログ ボックスの共通フィルターの 1 つにします。 共通フィルターは、フィルター一覧で、共通としてマークが付けられていないフィルターの前に一覧表示されます。|
|FindInFilesFilter|REG_DWORD|フィルターを、 **[フォルダーを指定して検索]** ダイアログ ボックスの共通フィルターの後にフィルターを一覧表示します。|
|NotOpenFileFilter|REG_DWORD|フィルターが **[ファイルを開く]** ダイアログ ボックスで使用されないことを示します。|
|NotAddExistingItemFilter|REG_DWORD|フィルターが **[既存項目の追加]** ダイアログ ボックスで使用されないことを示します。|
|SortPriority|REG_DWORD|SortPriority を設定して、フィルターを表示する順序を制御します。 SortPriority 値は大きいほどフィルター一覧の前の方に表示されます。|

## <a name="directory-structure"></a>ディレクトリの構造
 VSpackage では、統合開発環境 (IDE) によって場所が登録されていれば、ローカルまたはリモートのディスク上の任意の場所にテンプレート ファイルとフォルダーを配置できます。 ただし、編成しやすくするために、製品のインストール パスの下に次のディレクトリ構造を使用することをお勧めします。

 \Templates

 \Projects (プロジェクト テンプレートを含みます)

 \Applications

 \Components

 \ ...

 \ProjectItems (プロジェクト項目を含みます)

 \Class

 \Form

 \Web Page

 \HelperFiles (複数ファイル プロジェクト項目で使用されるファイルを含みます)

 \WizardFiles

## <a name="see-also"></a>関連項目

- [プロジェクト テンプレートとプロジェクト項目テンプレートの追加](../../extensibility/internals/adding-project-and-project-item-templates.md)
- [ウィザード](../../extensibility/internals/wizards.md)
- [アプリケーションのローカライズ](../../ide/globalizing-and-localizing-applications.md)
- [プロジェクトの拡張に通常使用されるオブジェクトの CATID](../../extensibility/internals/catids-for-objects-that-are-typically-used-to-extend-projects.md)
