---
title: プロジェクト タイプの登録 | Microsoft Docs
description: 新しいプロジェクト タイプを Visual Studio で認識して使用できるようにするレジストリ エントリの作成について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], new project registry entries
- registry, new project types
- registration, new project types
ms.assetid: dfc0e231-6b4e-447d-9d64-0e66dea3394a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e54f62a90ece61fc2dd8f3cc2b242957f249ed33
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105062773"
---
# <a name="registering-a-project-type"></a>プロジェクト タイプの登録
新しいプロジェクト タイプを作成する場合は、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] でプロジェクト タイプを認識して使用できるようにするレジストリ エントリを作成する必要があります。 通常、これらのレジストリ エントリを作成するには、レジストリ スクリプト (.rgs) ファイルを使用します。

 次の例では、レジストリのステートメントによって、該当する場合は既定のパスとデータが指定され、それに続いて各ステートメントのレジストリ スクリプトのエントリを含むテーブルが指定されます。 これらのテーブルには、ステートメントに関するスクリプト エントリと追加情報が記載されます。

> [!NOTE]
> 次のレジストリ情報は、プロジェクト タイプを登録するために記述するレジストリ スクリプトのエントリの種類と目的の例となるように意図されています。 実際のエントリとその使用は、プロジェクト タイプの特定の要件によって異なる場合があります。 開発しているプロジェクト タイプによく似たものを見つけるために使用可能なサンプルを調べ、そのサンプルのレジストリ スクリプトを確認する必要があります。

 次に HKEY_CLASSES_ROOT の例を示します。

## <a name="example-1"></a>例 1

```
\.figp
   @="FigPrjFile"
   "Content Type"="text/plain"
\.figp\ShellNew
   "NullFile"=""
\FigPrjFile
   @="Figure Project File"
\DefaultIcon
   @="<Visual Studio SDK installation path>\\9.0VSIntegration\\SomeFolder\\FigPkgs\\FigPrj\\Debug\\FigPrj.dll,-206"
\shell\open
   @="&Open in Visual Studio"
\shell\open\command
   @="devenv.exe \"%1\""
```

|名前|種類|データ|説明|
|----------|----------|----------|-----------------|
|`@`|REG_SZ|`FigPrjFile`|拡張子が .figp であるプロジェクト タイプ ファイルの名前と説明。|
|`Content Type`|REG_SZ|`Text/plain`|プロジェクト ファイルのコンテンツ タイプ。|
|`NullFile`|REG_SZ|`Null`||
|`@`|REG_SZ|`%MODULE%,-206`|この種類のプロジェクトに使用される既定のアイコン。 %MODULE% ステートメントは、プロジェクト タイプ DLL の既定の場所に対してレジストリ内で完了されます。|
|`@`|REG_SZ|`&Open in Visual Studio`|このプロジェクト タイプが開かれる既定のアプリケーション。|
|`@`|REG_SZ|`devenv.exe "%1"`|この種類のプロジェクトが開かれたときに実行される既定のコマンド。|

 次の例は HKEY_LOCAL_MACHINE からのものであり、レジストリ内でキー [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\99.0Exp\Packages] の下にあります。

## <a name="example-2"></a>例 2

```
\{ACEF4EB2-57CF-11D2-96F4-000000000000} (The CLSID for the VSPackage)
   @="FigPrj Project Package"
   "InprocServer32"="9.0<Visual Studio SDK installation path>\\VSIntegration\\Archive\\FigPkgs\\FigPrj\\                      Debug\\FigPrj.dll"
   "CompanyName"="Microsoft"
   "ProductName"="Figure Project Sample"
   "ProductVersion"="9.0"
   "MinEdition"="professional"
   "ID"=dword:00000001
\{ACEF4EB2-57CF-11D2-96F4-000000000000}\SatelliteDLL
   "DllName"="FigPrjUI.dll"
   "Path"="9.0<Visual Studio SDK installation path>\\VSIntegration\\Archive\\FigPkgs\\FigPrj\\Debug\\"
\{ACEF4EB2-57CF-11D2-96F4-000000000000}\Automation
   "FigProjects"=""
\{ACEF4EB2-57CF-11D2-96F4-000000000000}\AutomationEvents
   "FigProjectsEvents"="Returns the FigProjectsEvents Object"
   "FigProjectItemsEvents"="Returns the FigProjectItemsEvents Object"
```

|名前|種類|データ|説明|
|----------|----------|----------|-----------------|
|`@` (既定値)|REG_SZ|`FigPrj Project VSPackage`|この登録された VSPackage のローカライズ可能な名前 (プロジェクト タイプ)。|
|`InprocServer32`|REG_SZ|`%MODULE%`|プロジェクト タイプ DLL のパス。 IDE ではこの DLL を読み込み、VSPackage CLSID を `DllGetClassObject` に渡し、<xref:Microsoft.VisualStudio.OLE.Interop.IClassFactory> を取得して、<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage> オブジェクトを構築します。|
|`CompanyName`|REG_SZ|`Microsoft`|プロジェクト タイプを開発した会社の名前。|
|`ProductName`|REG_SZ|`Figure Project Sample`|プロジェクト タイプの名前。|
|`ProductVersion`|REG_SZ|`9.0`|プロジェクト タイプ リリースのバージョン番号。|
|`MinEdition`|REG_SZ|`professional`|登録されている VSPackage のエディション。|
|`ID`|REG_DWORD|`%IDS_PACKAGE_LOAD_KEY%`|プロジェクト VSPackage のパッケージ読み込みキー。 このキーは、環境が起動してからプロジェクトが読み込まれるときに検証されます。|
|`DllName`|REG_SZ|`%RESOURCE_DLL%`|プロジェクト タイプのローカライズされたリソースを含むサテライト DLL のファイル名。|
|`Path`|REG_SZ|`%RESOURCE_PATH%`|サテライト DLL のパス。|
|`FigProjectsEvents`|REG_SZ|値についてはステートメントを参照してください。|このオートメーション イベントに対して返されるテキスト文字列を決定します。|
|`FigProjectItemsEvents`|REG_SZ|値についてはステートメントを参照してください。|このオートメーション イベントに対して返されるテキスト文字列を決定します。|

 次の例はすべて、レジストリ内でキー [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\9.0Exp\Projects] の下にあります。

## <a name="example-3"></a>例 3

```
\{C061DB26-5833-11D2-96F5-000000000000} (The CLSID for projects of this type)
   @="FigPrj Project"
   "DisplayName"="#2"
   "Package"="{ACEF4EB2-57CF-11D2-96F4-000000000000}"
   "ProjectTemplatesDir"="C:\\Program Files\\VSIP 9.0\\EnvSDK\\FigPkgs\\                           FigPrj\\FigPrjProjects"
   "ItemTemplatesDir"="<Visual Studio SDK installation path>\\VSIntegration\\Archive9.0\\FigPkgs\\FigPrj\\                           FigPrjProjectItems"
   "DisplayProjectFileExtensions"="#3"
   "PossibleProjectExtensions"="figp"
   "DefaultProjectExtension"=".figp"
\{C061DB26-5833-11D2-96F5-000000000000}\Filters\1       (Folder 1 contains settings for Open Files filters.)
   @="#4"
   "CommonOpenFilesFilter"=dword:00000000
   "CommonFindFilesFilter"=dword:00000000
   "NotAddExistingItemFilter"=dword:00000000
   "FindInFilesFilter"=dword:00000000
   "NotOpenFileFilter"=dword:00000000
   "SortPriority"=dword:000003e8
\{C061DB26-5833-11D2-96F5-000000000000}\Filters\2
      (Folder 2 contains settings for Find in Files filters.)
   @="#5"
   "CommonOpenFilesFilter"=dword:00000000
   "CommonFindFilesFilter"=dword:00000000
   "NotAddExistingItemFilter"=dword:00000001
   "FindInFilesFilter"=dword:00000001
   "NotOpenFileFilter"=dword:00000000
   "SortPriority"=dword:000003e8
\{C061DB26-5833-11D2-96F5-000000000000}\AddItemTemplates\TemplateDirs\ {ACEF4EB2-57CF-11D2-96F4-000000000000}\1 (Second GUID indicates the registered project type for the Add Items templates.)
   @="#6"
   "TemplatesDir"="<Visual Studio SDK installation path>\\VSIntegration\\Archive9.0\\FigPkgs\\FigPrj\\                    FigPrjProjectItems"
   "SortPriority"=dword:00000064
```

|名前|種類|データ|説明|
|----------|----------|----------|-----------------|
|`@`|REG_SZ|`FigPrj Project`|この種類のプロジェクトの既定の名前。|
|`DisplayName`|REG_SZ|`#%IDS_PROJECT_TYPE%`|パッケージに登録されているサテライト DLL から取得する名前のリソース ID。|
|`Package`|REG_SZ|`%CLSID_Package%`|パッケージに登録されている VSPackage のクラス ID。|
|`ProjectTemplatesDir`|REG_SZ|`%TEMPLATE_PATH%\FigPrjProjects`|プロジェクト テンプレート ファイルの既定のパス。 これらのファイルは、[新しいプロジェクト] テンプレートによって表示されます。|
|`ItemTemplatesDir`|REG_SZ|`%TEMPLATE_PATH% \FigPrjProjectItems`|プロジェクト項目テンプレート ファイルの既定のパス。 これらのファイルは、[新しい項目の追加] テンプレートによって表示されます。|
|`DisplayProjectFileExtensions`|REG_SZ|`#%IDS_DISPLAY_PROJ_FILE_EXT%`|IDE で **[開く]** ダイアログ ボックスを実装できるようにします。|
|`PossibleProjectExtensions`|REG_SZ|`figp`|開いているプロジェクトがこのプロジェクト タイプ (プロジェクト ファクトリ) で処理されるかどうかを判断するために IDE で使用されます。 複数のエントリは、セミコロンで区切られたリストの形式で指定します。 たとえば、"vdproj;vdp" のようになります。|
|`DefaultProjectExtension`|REG_SZ|`.figp`|[名前を付けて保存] 操作の既定のファイル名拡張子として IDE で使用されます。|
|`Filter Settings`|REG_DWORD|さまざま。表に続くステートメントとコメントを参照してください。|これらの設定は、UI ダイアログ ボックスでファイルを表示するためのさまざまなフィルターを設定するために使用されます。|
|`@`|REG_SZ|`#%IDS_ADDITEM_TEMPLATES_ENTRY%`|[項目の追加] テンプレートのリソース ID。|
|`TemplatesDir`|REG_SZ|`%TEMPLATE_PATH%\FigPrjProjectItems`|**[新しい項目の追加]** テンプレートのダイアログ ボックスに表示されるプロジェクト項目のパス。|
|`SortPriority`|REG_DWORD|`100 (vcprx64)`|**[新しい項目の追加]** ダイアログ ボックスに表示されるファイルのツリー ノード内の並べ替え順序を決定します。|

 次の表は、前のコード セグメントで使用できるフィルター オプションを示しています。

|フィルター オプション|説明|
|-------------------|-----------------|
|`CommonFindFilesFilter`|フィルターが **[フォルダーを指定して検索]** ダイアログ ボックスの共通フィルターの 1 つであることを示します。 共通フィルターは、フィルター一覧で、共通としてマークが付けられていないフィルターの前に一覧表示されます。|
|`CommonOpenFilesFilter`|フィルターが **[ファイルを開く]** ダイアログ ボックスの共通フィルターの 1 つであることを示します。 共通フィルターは、フィルター一覧で、共通としてマークが付けられていないフィルターの前に一覧表示されます。|
|`FindInFilesFilter`|フィルターが **[フォルダーを指定して検索]** ダイアログ ボックスのフィルターの 1 つであり、共通フィルターの後に一覧表示されることを示します。|
|`NotOpenFileFilter`|フィルターが **[ファイルを開く]** ダイアログ ボックスで使用されないことを示します。|
|`NotAddExistingItemFilter`|フィルターが **[既存項目の追加]** ダイアログ ボックスで使用されないことを示します。|

 既定では、フィルターにこれらのフラグの 1 つ以上が設定されていない場合、このフィルターは、共通フィルターが一覧表示された後で、 **[既存項目の追加]** ダイアログ ボックスと **[ファイルを開く]** ダイアログ ボックスで使用されます。 フィルターは、 **[フォルダーを指定して検索]** ダイアログ ボックスでは使用されません。

 次の例はすべて、レジストリ内でキー [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\9.0Exp\Projects] の下にあります。

## <a name="example-4"></a>例 4

```
{FE3BBBB6-72D5-11d2-9ACE-00C04F79A2A4} (The CLSID for Enterprise Projects)
\{FE3BBBB6-72D5-11d2-9ACE-00C04F79A2A4}\AddItemTemplates\TemplateDirs\ {ACEF4EB2-57CF-11D2-96F4-000000000000}\1 (CLSID for projects of this type)
   @="#7"
   "TemplatesDir"="<Visual Studio SDK installation path>\\VSIntegration\\Archive9.0\\FigPrj\\FigPrjProjects"
   "SortPriority"=dword:00000029
   "NewProjectDialogOnly"=dword:00000000
```

|名前|種類|データ|説明|
|----------|----------|----------|-----------------|
|`@`|REG_SZ|`#%IDS_NEWPROJ_ TEMPLATES_ENTRY%`|新しいプロジェクト テンプレートのリソース ID。|
|`TemplatesDir`|REG_SZ|`%TEMPLATE_PATH%\FigPrjProjects`|登録されているプロジェクト タイプのプロジェクトの既定のパス。|
|`SortPriority`|REG_DWORD|`41 (x29)`|[新しいプロジェクト ウィザード] ダイアログ ボックスに表示されるプロジェクトの並べ替え順序を設定します。|
|`NewProjectDialogOnly`|REG_DWORD|`0`|0 は、この種類のプロジェクトが [新しいプロジェクト] ダイアログ ボックスにのみ表示されることを示します。|

 次の例はすべて、レジストリ内でキー [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\9.0Exp\Projects] の下にあります。

## <a name="example-5"></a>例 5

```
\{A2FE74E1-B743-11d0-AE1A-00A0C90FFFC3} (CLSID for Miscellaneous Files projects)
   @="Miscellaneous Files Project"
\AddItemTemplates\TemplateDirs\{ACEF4EB2-57CF-11D2-96F4-000000000000}\1
                                 (CLSID for Figures Project projects)
   @="#6"
   "TemplatesDir"="<Visual Studio SDK installation path>\\VSIntegration\\Archive9.0\\FigPkgs\\FigPrj\\                    FigPrjProjectItems"
   "SortPriority"=dword:00000064
```

|名前|種類|データ|説明|
|----------|----------|----------|-----------------|
|`@`|REG_SZ|なし|次のエントリが [その他のファイル] プロジェクト エントリ用であることを示す既定値。|
|`@`|REG_SZ|`#%IDS_ADDITEM_TEMPLATES_ENTRY%`|[新しい項目の追加] テンプレート ファイルのリソース ID 値。|
|`TemplatesDir`|REG_SZ|`%TEMPLATE_PATH%\FigPrjProjectItems`|**[新しい項目の追加]** ダイアログ ボックスに表示される項目の既定のパス。|
|`SortPriority`|REG_DWORD|`100 (vcprx64)`|**[新しい項目の追加]** ダイアログ ボックスのツリー ノードに表示される並べ替え順序を設定します。|

 次の例は、レジストリ内でキー [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\9.0Exp\Menus] の下にあります。

## <a name="example-6"></a>例 6

```
"{ACEF4EB2-57CF-11D2-96F4-000000000000}"=",1000,1"
```

 メニュー エントリにより、メニュー情報の取得に使用されたリソースが IDE で参照されます。 このデータがメニュー データベースにマージされると、レジストリの MenusMerged セクションに同じキーが追加されます。 MenusMerged セクションの下にあるものを直接、VSPackage で変更することはできません。 次の表のデータ フィールドには、3 つのコンマ区切りのフィールドがあります。 最初のフィールドは、メニュー リソース ファイルの完全パスを示します。

- 最初のフィールドを省略した場合、メニュー リソースは VSPackage GUID で識別されるサテライト DLL から読み込まれます。

  2 番目のフィールドは、型 CTMENU のメニュー リソース ID を識別します。

- リソース ID が指定されていて、ファイル パスが最初のパラメーターで指定されている場合、メニュー リソースは完全なファイル パスから読み込まれます。

- リソース ID が指定されていても、ファイル パスが指定されていない場合、メニュー リソースはサテライト DLL から読み込まれます。

- 完全なファイル パスが指定されていて、リソース ID が省略されている場合は、読み込まれるファイルは CTO ファイルである必要があります。

  最後のフィールドは、CTMENU リソースのバージョン番号を識別します。 バージョン番号を変更して、もう一度メニューをマージできます。

|名前|種類|データ|説明|
|----------|----------|----------|-----------------|
|%CLSID_Package%|REG_SZ|`,1000,1`|メニュー情報を取得するリソース。|

 次の例はすべて、レジストリ内でキー [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\9.0Exp\NewProjectTemplates] の下にあります。

```
\TemplateDirs\{ACEF4EB2-57CF-11D2-96F4-000000000000}\1                (CLSID for Figures Project projects)
   @="#7"
   "TemplatesDir"="<Visual Studio SDK installation path>\\VSIntegration\\Archive9.0\\FigPkgs\\FigPrj\\FigPrjProjects"
   "SortPriority"=dword:00000029
   "NewProjectDialogOnly"=dword:00000000
```

|名前|種類|データ|説明|
|----------|----------|----------|-----------------|
|`@`|REG_SZ|`#%IDS_NEWPROJ_TEMPLATES_ENTRY%`|[図プロジェクトの新しいプロジェクト] テンプレートのリソース ID 値。|
|`TemplatesDir`|REG_SZ|`%TEMPLATE_PATH%\FigPrjProjects`|[新しいプロジェクト] ディレクトリの既定のパス。 このディレクトリ内の項目は、 **[新規プロジェクト ウィザード]** ダイアログ ボックスに表示されます。|
|`SortPriority`|REG_DWORD|`41 (x29)`|**[新しいプロジェクト]** ダイアログ ボックスのツリー ノードにプロジェクトを表示する順序を設定します。|
|`NewProjectDialogOnly`|REG_DWORD|`0`|0 は、この種類のプロジェクトが **[新しいプロジェクト]** ダイアログ ボックスにのみ表示されることを示します。|

 次の例は、レジストリ内でキー [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\9.0Exp\InstalledProducts] の下にあります。

```
\FiguresProductSample
   "Package"="{ACEF4EB2-57CF-11D2-96F4-000000000000}"
   "UseInterface"=dword:00000001
```

|名前|種類|データ|説明|
|----------|----------|----------|-----------------|
|`Package`|REG_SZ|`%CLSID_Package%`|登録されている VSPackage のクラス ID。|
|`UseInterface`|REG_DWORD|`1`|1 は、このプロジェクトとの対話に UI が使用されることを示します。 0 は、UI インターフェイスがないことを示します。|

 新しいプロジェクト タイプを制御する .vsz ファイルには、多くの場合 RELATIVE_PATH エントリが含まれています。 このパスは、次のセットアップ キーで、プロジェクト タイプの \ProductDir エントリの下で指定されたパスに対する相対パスです。

 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\7.0Exp\Setup

 たとえば、エンタープライズ フレームワーク プロジェクト テンプレートでは、次のレジストリ エントリが追加されます。

 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\7.0Exp\Setup\EF\ProductDir = C:\Program Files\Microsoft Visual Studio\EnterpriseFrameworks\

 つまり、.vsz ファイルに PROJECT_TYPE=EF エントリを含めると、環境では、前に指定した ProductDir ディレクトリにある .vsz ファイルが検索されます。

## <a name="see-also"></a>関連項目
- [チェックリスト: 新しいプロジェクト タイプの作成](../../extensibility/internals/checklist-creating-new-project-types.md)
- [プロジェクト モデルの要素](../../extensibility/internals/elements-of-a-project-model.md)
- [プロジェクト ファクトリを使用したプロジェクト インスタンスの作成](../../extensibility/internals/creating-project-instances-by-using-project-factories.md)
