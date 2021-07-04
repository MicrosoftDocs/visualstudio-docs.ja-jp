---
title: '[新しいプロジェクト] ダイアログ ボックスへの新しいディレクトリの追加 | Microsoft Docs'
description: 新しいプロジェクトの種類を作成してテンプレートとして使用できるように、Visual Studio の [新しいプロジェクト] ダイアログ ボックスでディレクトリを追加する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- New Project dialog box, extending
ms.assetid: 53b328f5-20bb-49a3-bf9e-1818f4fbdf50
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 44554c8bd7b758f1bf191d1a4bef9ba07941191d
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112901839"
---
# <a name="add-directories-to-the-new-project-dialog-box"></a>[新しいプロジェクト] ダイアログ ボックスへの新しいディレクトリの追加
新しいプロジェクトの種類を作成するときに、 **[新しいプロジェクト]** ダイアログ ボックスで新しいディレクトリを登録して、テンプレートとして使用できるように表示することもできます。 次のコード例では、新しいディレクトリ (ノードとも呼ばれる) を登録する方法について説明します。 この例では、VSPackage である *CLSID_Package* によって公開されているテンプレートが登録されています。 結果として、 **[新しいプロジェクト]** ダイアログ ボックスの左側には、追加したノードが、*Folder_Label_ResID* リソースによって決定される名前と共に提供されます。 このリソースは、VSPackage サテライト DLL から読み込まれます。

 **Folder** の値は、*Folder_Label_ResID* ノードが表示されるフォルダーの GUID を表します。 この例では、GUID は **[新しいプロジェクト]** ダイアログ ボックスの **[プロジェクトの種類]** ペインにある **[その他のプロジェクト]** フォルダーを表します。 **[その他のプロジェクト]** の値が存在しない場合、ラベルは最上位レベルに配置されます。

 `TemplatesDir` の値は、プロジェクト テンプレートが格納されているディレクトリの完全パスを指定します。 これらのファイルには、複製する *.vsz* ファイルまたは一般的なテンプレート ファイルを指定できます。

 `TemplatesLocalizedSubDir` を指定する場合、ローカライズされたテンプレートを保持する `TemplatesDir` のサブディレクトリに名前を指定する文字列のリソース ID にする必要があります。 サテライト DLL がある場合、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ではそこから文字列リソースを読み込むため、サテライト DLL ごとに異なるサブディレクトリ名を含めることができます。 `SortPriority` の値は並べ替えの優先度を指定します。

```
NoRemove NewProjectTemplates
{
    NoRemove TemplateDirs
  {
    ForceRemove %CLSID_Package%
    {
      ForceRemove /1 = s '#%Folder_Label_ResID%'
      {
        val Folder = s '{DCF2A94A-45B0-11D1-ADBF-00C04FB6BE4C}'
        val TemplatesDir = s '%Template_Path%'
        val TemplatesLocalizedSubDir = s '#100'
        val SortPriority = d 1000
      }
    }
  }
}
```

## <a name="see-also"></a>関連項目
- [プロジェクトと項目テンプレートの登録](../../extensibility/internals/registering-project-and-item-templates.md)
- [[新しい項目の追加] ダイアログ ボックスへの項目の追加](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md)
- [[新しい項目の追加] ダイアログ ボックスへの新しいディレクトリの追加](../../extensibility/internals/adding-directories-to-the-add-new-item-dialog-box.md)
