---
title: '[新しい項目の追加] ダイアログ ボックスにディレクトリを追加する | Microsoft Docs'
description: レジストリ スクリプトを使用してディレクトリを登録することにより、Visual Studio の [新しい項目の追加] ダイアログ ボックスにディレクトリを追加する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Add New Item dialog box, extending
ms.assetid: 67ae8af6-3752-49e8-8ce3-007aca5f7982
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 131c04d1025885c59a884220a61098b2c85dd5a1
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105079151"
---
# <a name="add-directories-to-the-add-new-item-dialog-box"></a>[新しい項目の追加] ダイアログ ボックスにディレクトリを追加する
次のコード例は、 **[新しい項目の追加]** ダイアログ ボックスに一連の新しいディレクトリを登録する方法を示しています。 **[新しい項目の追加]** ダイアログ ボックスのディレクトリは、プロジェクトごとに異なります。 そのため、ディレクトリは、**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp\Projects** にある **Projects** サブキーの下に登録されます。

## <a name="registry-script"></a>レジストリ スクリプト

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

 `%Template_Path%` の値によって、プロジェクト テンプレートが格納されているディレクトリの完全なパスが指定されます。 これらのテンプレートには、 *.vsz* ファイルまたは複製されるテンプレート ファイルのひな形を指定できます。

 `SortPriority` の値によって、並べ替えの優先度が指定されます。

## <a name="add-items-to-an-existing-project"></a>既存のプロジェクトに項目を追加する
 既存のプロジェクトに項目を追加することもできます。 たとえば、[!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] プロジェクトの場合は、 *\<root>\Program Files\Microsoft Visual Studio\VC#\CSharpProjectItems\LocalProjectItems* フォルダーに項目を追加できます。 この場合、`%GUID_Project%` は C# プロジェクトの GUID ({FAE04EC0-301F-11D3-BF4B-00C04F79EFBC}) です。

 また、プロジェクトのサブタイプをプログラミングすることによって、既存のプロジェクトを拡張することもできます。 プロジェクトのサブタイプを使用すると、新しいプロジェクトの種類を記述することなくプロジェクトを拡張できます。 プロジェクトのサブタイプの詳細については、「[プロジェクト サブタイプ](../../extensibility/internals/project-subtypes.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [プロジェクトと項目テンプレートの登録](../../extensibility/internals/registering-project-and-item-templates.md)
- [[新しい項目の追加] ダイアログ ボックスへの項目の追加](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md)
- [[新しいプロジェクト] ダイアログ ボックスにディレクトリを追加する](../../extensibility/internals/adding-directories-to-the-new-project-dialog-box.md)
