---
title: ディレクトリを追加する、新しい項目 ダイアログ ボックスの追加 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Add New Item dialog box, extending
ms.assetid: 67ae8af6-3752-49e8-8ce3-007aca5f7982
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: f370d208cb8f7aad88f806983983ccee9f584625
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "58974318"
---
# <a name="adding-directories-to-the-add-new-item-dialog-box"></a>[新しい項目の追加] ダイアログ ボックスへの新しいディレクトリの追加
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

次のコード例は、ディレクトリの新しいセットを登録する方法を示します、**新しい項目の追加** ダイアログ ボックス。 用のディレクトリ、**新しい項目の追加** ダイアログ ボックスは、プロジェクトごとに異なります。 プロジェクト サブキーにあるディレクトリを登録するため、 \<HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp\Projects >:  
  
## <a name="the-registry-script"></a>レジストリ スクリプト  
  
```  
NoRemove Projects  
{  
  NoRemove %GUID_Project%  
  {  
    NoRemove AddItemTemplates  
    {  
      NoRemove TemplateDirs  
      {  
        ForceRemove %CLSID_Package%  
        {  
      ForceRemove /1 = s '#%Folder_Label_ResID%'  
          {  
            val TemplatesDir = s '%Template_Path%'     
            val SortPriority = d 2000  
          }  
        }  
      }  
    }  
  }  
}  
```  
  
 Template_Path 値では、プロジェクト テンプレートを格納するディレクトリの完全なパスを指定します。 これらのテンプレートには、.vsz ファイルまたは複製する典型的なテンプレート ファイルのいずれかを指定できます。  
  
 SortPriority 値では、並べ替えの優先順位を指定します。  
  
## <a name="adding-items-to-an-existing-project"></a>既存のプロジェクトに項目を追加します。  
 既存のプロジェクトに項目を追加することもできます。 たとえば、[!INCLUDE[csprcs](../../includes/csprcs-md.md)]プロジェクトに項目を追加することができます、\<ルート > \Program Files\Microsoft Visual Studio \VC#\CSharpProjectItems\LocalProjectItems フォルダー。 この場合、`%GUID_Project%`は C# プロジェクト ({FAE04EC0-301F-11D3-BF4B-00C04F79EFBC}) の GUID です。  
  
 プロジェクト サブタイプをプログラミングによって既存のプロジェクトを拡張することもできます。 プロジェクト サブタイプの場合は、新しいプロジェクトの種類を記述することがなくプロジェクトを拡張できます。 プロジェクト サブタイプの詳細については、次を参照してください。[プロジェクト サブタイプ](../../extensibility/internals/project-subtypes.md)します。  
  
## <a name="see-also"></a>関連項目  
 [プロジェクトと項目テンプレートを登録します。](../../extensibility/internals/registering-project-and-item-templates.md)   
 [項目を追加、新しい項目の追加 ダイアログ ボックス](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md)   
 [[新しいプロジェクト] ダイアログ ボックスへの新しいディレクトリの追加](../../extensibility/internals/adding-directories-to-the-new-project-dialog-box.md)
