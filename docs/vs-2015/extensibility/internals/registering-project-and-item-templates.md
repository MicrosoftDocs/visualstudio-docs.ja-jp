---
title: プロジェクトと項目テンプレートの登録 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], adding items
- registry, Add New Item dialog box
- Add New Item dialog box
- Add New Project dialog box
- registry, Add New Project dialog box
ms.assetid: 6b909f93-d7f5-4aec-81c6-ee9ff0f31638
caps.latest.revision: 28
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a06e7a292d960e675ad4b0de97499557542fef1c
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "58973657"
---
# <a name="registering-project-and-item-templates"></a>プロジェクトと項目テンプレートの登録
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

プロジェクトの種類には、そのプロジェクトとプロジェクト項目テンプレートが配置されるディレクトリを登録する必要があります。 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 表示するものを決定する、プロジェクトの種類に関連付けられている登録情報を使用して、**新しいプロジェクトの追加**と**新しい項目の追加** ダイアログ ボックス。  
  
 テンプレートの詳細については、次を参照してください。[プロジェクトに追加するとプロジェクト項目テンプレート](../../extensibility/internals/adding-project-and-project-item-templates.md)します。  
  
## <a name="registry-entries-for-projects"></a>プロジェクトのレジストリ エントリ  
 次の例では、hkey_local_machine \software\microsoft\visualstudio の下にレジストリ エントリ\\<*バージョン*>。 付随するテーブルでは、例で使用される要素について説明します。  
  
```  
[Projects\{ProjectGUID}]  
@="MyProjectType"  
"DisplayName"="#2"  
"Package"="{VSPackageGUID}"  
"ProjectTemplatesDir"="C:\\MyProduct\\MyProjectTemplates"  
```  
  
|名前|種類|説明|  
|----------|----------|-----------------|  
|@|REG_SZ|この種類のプロジェクトの既定の名前。|  
|DisplayName|REG_SZ|パッケージ サテライト DLL から取得する名前のリソース ID が登録されます。|  
|Package|REG_SZ|パッケージの下に登録されているパッケージのクラス ID。|  
|ProjectTemplatesDir|REG_SZ|プロジェクト テンプレート ファイルの既定のパス。 プロジェクト テンプレート ファイルがによって表示される、**新しいプロジェクト**テンプレート。|  
  
### <a name="registering-item-templates"></a>項目テンプレートを登録します。  
 項目テンプレートを格納するディレクトリを登録する必要があります。  
  
```  
[Projects\{ProjectGUID}\AddItemTemplates\TemplateDirs\{VSPackageGUID}\1]  
@="#7"  
"TemplatesDir"="C:\\MyProduct\\MyProjectItemTemplates "  
"TemplatesLocalizedSubDir"="#10"  
"SortPriority"=dword:00000064  
```  
  
|名前|種類|説明|  
|----------|----------|-----------------|  
|@|REG_SZ|項目の追加テンプレートのリソース ID。|  
|TemplatesDir|REG_SZ|ダイアログ ボックスに表示されるプロジェクト項目のパス、**新しい項目の追加**ウィザード。|  
|TemplatesLocalizedSubDir|REG_SZ|TemplatesDir のサブディレクトリの名前を示す文字列のリソース ID は、ローカライズされたテンプレートを保持します。 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]負荷から文字列リソース サテライト Dll に存在する場合、各サテライト DLL が別のローカライズされたサブディレクトリ名を含めることができます。|  
|SortPriority|REG_DWORD|テンプレートを表示する順序を制御する SortPriority の設定、**新しい項目の追加** ダイアログ ボックス。 テンプレートの一覧に以前 SortPriority のより大きな値が表示されます。|  
  
### <a name="registering-file-filters"></a>ファイル フィルターを登録します。  
 必要に応じて、フィルターを登録することができますを[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]ファイル名を要求するときに使用します。 たとえば、[!INCLUDE[csprcs](../../includes/csprcs-md.md)]のフィルター処理、**ファイルを開く** ダイアログ ボックスは。  
  
 **Visual C# ファイル (\*.cs、\*.resx、\*.settings、\*.xsd、\*.wsdl);\*します。cs、\*.resx、\*.settings、\*.xsd、\*.wsdl)**  
  
 独自のサブキー hkey_local_machine \software\microsoft\visualstudio 下で複数のフィルターの登録をサポートする各フィルターが登録されている\\<*バージョン*> \Projects\\{\< *ProjectGUID*>} \Filters\\<*サブキー*>。 サブキーの名前は任意です。[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]サブキーの名前を無視し、その値だけを使用します。  
  
 次の表に示すようにフラグを設定してフィルターを使用するコンテキストを制御できます。 フィルターでは、フラグを設定することはない場合の一般的なフィルターの後に表示されます、**既存項目の追加** ダイアログ ボックスおよび**ファイルを開く** ダイアログ ボックスがないで使用される、**ファイル内の検索**  ダイアログ ボックス。  
  
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
  
|名前|種類|説明|  
|----------|----------|-----------------|  
|CommonFindFilesFilter|REG_DWORD|一般的なフィルターの 1 つのフィルターにより、**ファイル内の検索** ダイアログ ボックス。 一般的なフィルターは、一般的でマークされていないフィルターの前に、フィルター一覧に表示されます。|  
|CommonOpenFilesFilter|REG_DWORD|一般的なフィルターの 1 つのフィルターにより、**ファイルを開く** ダイアログ ボックス。 一般的なフィルターは、一般的でマークされていないフィルターの前に、フィルター一覧に表示されます。|  
|FindInFilesFilter|REG_DWORD|一般的なフィルターの後にフィルターを一覧表示、**ファイル内の検索** ダイアログ ボックス。|  
|NotOpenFileFilter|REG_DWORD|フィルターが使用されないことを示します、**ファイルを開く** ダイアログ ボックス。|  
|NotAddExistingItemFilter|REG_DWORD|フィルターが使用されないことを示します、**既存項目の追加** ダイアログ ボックス。|  
|SortPriority|REG_DWORD|フィルターを表示する順序を制御する SortPriority を設定します。 フィルターの一覧に以前 SortPriority のより大きな値が表示されます。|  
  
## <a name="directory-structure"></a>ディレクトリの構造  
 Vspackage テンプレート ファイルとフォルダーどこでも配置できます、ローカルまたはリモート ディスクの場所が統合開発環境 (IDE) で登録されている限り、します。 ただし、容易にするための組織、製品のインストール パスでは、次のディレクトリ構造を推奨します。  
  
 \Templates  
  
 \Projects (プロジェクト テンプレートが含まれています)  
  
 \Applications  
  
 \Components  
  
 \ ...  
  
 \ProjectItems (プロジェクト項目が含まれています)  
  
 \Class  
  
 \Form  
  
 \Web Page  
  
 \HelperFiles (複数のファイル プロジェクト項目で使用されるファイルが含まれています)  
  
 \WizardFiles  
  
## <a name="see-also"></a>関連項目  
 [プロジェクトとプロジェクト項目テンプレートを追加します。](../../extensibility/internals/adding-project-and-project-item-templates.md)   
 [ウィザード](../../extensibility/internals/wizards.md)   
 [アプリケーションのローカライズ](../../ide/localizing-applications.md)   
 [プロジェクトの拡張に通常使用されるオブジェクトの CATID](../../extensibility/internals/catids-for-objects-that-are-typically-used-to-extend-projects.md)
