---
title: '[新しい項目の追加] ダイアログ ボックスへの投稿 | Microsoft Docs'
description: Projects レジストリ サブキーの下に Add Item テンプレートを登録して、Visual Studio の [新しい項目の追加] ダイアログ ボックスに投稿する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Add New Item dialog box, contributing to
ms.assetid: b2e53175-9372-4d17-8c2b-9264c9e51e9c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8186f25f8e1631f0e13aa7a8f43620812c4c7693
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105057053"
---
# <a name="contribute-to-the-add-new-item-dialog-box"></a>[新しい項目の追加] ダイアログ ボックスへの投稿
プロジェクトのサブタイプでは、**Projects** レジストリ サブキーの下に **Add Item** テンプレートを登録することにより、 **[新しい項目の追加]** ダイアログ ボックスの項目の新しい完全なディレクトリを提供できます。

## <a name="register-add-new-item-templates"></a>[新しい項目の追加] テンプレートの登録
 このセクションは、レジストリの **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0\Projects** の下にあります。 以下のレジストリ エントリでは、仮定のプロジェクト サブタイプによって集計された [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] プロジェクトが想定されています。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] プロジェクトのエントリを、以下に示します。

```
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0\Projects\{F184B08F-C81C-45F6-A57F-5ABD9991F28F}]
@="#2143"
"DefaultProjectExtension"="vbproj"
"PossibleProjectExtensions"="vbproj;vbp"
"ProjectTemplatesDir"="visualStudioInstallPath\\Vb\\.\\VBProjects"

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0\Projects\{F184B08F-C81C-45F6-A57F-5ABD9991F28F}\AddItemTemplates\TemplateDirs\{12345678-1234-1234-1122334455667788}\/1]
@="#100"
"TemplatesDir"="projectSubTypeTemplatesDir\\VBProjectItems"
```

 **AddItemTemplates\TemplateDirs** サブキーには、 **[新しい項目の追加]** ダイアログ ボックスで使用できるようになった項目が配置されるディレクトリへのパスを含むレジストリ エントリが含まれています。

 環境では、**Projects** レジストリ サブキーの下に、すべての **AddItemTemplates** データが自動的に読み込まれます。 このデータには、基本プロジェクトの実装のデータと、特定のプロジェクト サブタイプ タイプのデータを含めることができます。 各プロジェクト サブタイプは、プロジェクト タイプの **GUID** によって識別されます。 プロジェクト サブタイプでは、<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A> 実装内の <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2> から `VSHPROPID_ AddItemTemplatesGuid` 列挙をサポートすることで、特定のフレーバー プロジェクト インスタンスに対して、**Add Item** テンプレートの代替セットを使用するように指定して、プロジェクト サブタイプの GUID 値を返すことができます。 `VSHPROPID_AddItemTemplatesGuid` プロパティが指定されていない場合は、基本プロジェクト GUID が使用されます。

 プロジェクト サブタイプ アグリゲーター オブジェクト上に <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg> インターフェイスを実装することで、 **[新しい項目の追加]** ダイアログ ボックスで項目をフィルター処理できます。 たとえば、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] プロジェクトの集計によってデータベース プロジェクトを実装するプロジェクト サブタイプでは、フィルター処理を実装することで、 **[新しい項目の追加]** ダイアログ ボックスから [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 特定の項目をフィルター処理できます。また、逆に、<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A> で `VSHPROPID_ AddItemTemplatesGuid` をサポートすることにより、データベース プロジェクト固有の項目を追加できます。 **[新しい項目の追加]** ダイアログ ボックスでの項目のフィルター処理と追加の方法の詳細については、[[新しい項目の追加] ダイアログ ボックスへの項目の追加](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md)に関するページを参照してください。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2>
- [プロジェクトの拡張に通常使用されるオブジェクトの CATID](../../extensibility/internals/catids-for-objects-that-are-typically-used-to-extend-projects.md)
