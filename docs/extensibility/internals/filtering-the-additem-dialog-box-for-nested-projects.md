---
title: 入れ子になったプロジェクトのための [AddItem] ダイアログ ボックスのフィルター処理 | Microsoft Docs
description: 親プロジェクトの IVsFilterAddProjectItemDlg インターフェイスを実装することによって、Visual Studio で入れ子になったプロジェクトの [AddItem] ダイアログ ボックスをフィルター処理する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- filtering, nested projects
- nested projects, AddItem dialog box filtering
ms.assetid: 5b3e352e-7f18-4f66-be16-b0ad55637ce5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 59ae3c229ba359af0349ad93edc75e53c2cc3557
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105069583"
---
# <a name="filter-the-additem-dialog-box-for-nested-projects"></a>入れ子になったプロジェクトの [AddItem] ダイアログ ボックスをフィルター処理する
入れ子になったプロジェクトの **[AddItem]** ダイアログボックスを表示するときに、ダイアログ ボックスに表示される項目を親プロジェクトで制御できます。

 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2> インターフェイスを使用すると、 **[AddItem]** ダイアログ ボックスに表示されるノードをフィルター処理できます。 子プロジェクトで **[AddItem]** ダイアログボックスが表示される場合、親では、子のプロジェクトに表示される `IVsFilterAddProjectItemDlg` インターフェイスとフィルター項目を実装できます。

 プロジェクトが特定の親プロジェクトの関数によってグループ化されている場合は、入れ子になったプロジェクトのショートカットメニューにある **[プロジェクト項目の追加]** をユーザーが選択したときに `IVsFilterAddProjectItemDlg` を実装できます。 プロジェクト項目またはそのグループに固有のファイルのみ `IvsFilterAddProjectItemDlg displays` を実装します。 他のグループのプロジェクト項目は、同じディレクトリに格納されている場合でも、ダイアログ ボックスからフィルターで除外されます。

 ユーザーが子の **[AddItem]** ダイアログ ボックスを開くと、親プロジェクトの `IVsFilterAddProjectItemDlg` インターフェイスの実装が呼び出されます。

 `IVsFilterAddProjectItemDlg` インターフェイスでは、カテゴリによるフィルター処理を実装することもできます。 詳細については、「[[新しい項目の追加] ダイアログ ボックスへの項目の追加](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md)」および「[プロジェクトと項目テンプレートの登録](../../extensibility/internals/registering-project-and-item-templates.md)」を参照してください。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2>
- [[新しい項目の追加] ダイアログ ボックスへの項目の追加](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md)
- [プロジェクトと項目テンプレートの登録](../../extensibility/internals/registering-project-and-item-templates.md)
- [プロジェクトを入れ子にする](../../extensibility/internals/nesting-projects.md)
