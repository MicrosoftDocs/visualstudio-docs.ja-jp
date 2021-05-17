---
title: プロジェクトを入れ子にする | Microsoft Docs
description: プロジェクトの入れ子化について説明します。VSPackage を使用するアプリケーション開発者は、これによって、類似したタイプのプロジェクトを Visual Studio でグループ化できます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project nesting
- nested projects
- projects [Visual Studio SDK], child projects
- projects [Visual Studio SDK], nesting
ms.assetid: 12cce037-9840-4761-845e-5abd5fb317b0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 30b562cac794b7ab960f055fe67a5d0cc4ec871f
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105063222"
---
# <a name="nesting-projects"></a>入れ子になったプロジェクト
VSPackage を使用するエンタープライズ アプリケーション開発者は、*プロジェクトの入れ子化* を使用して、類似したタイプのプロジェクトを [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] で簡単にグループ化できます。 たとえば、エンタープライズ テンプレート プロジェクトでは、入れ子になったプロジェクトを使用して、プロジェクトをカテゴリにグループ化します。 ビジネス ファサード プロジェクト、Web UI プロジェクトなどは、1 つのカテゴリにグループ化されます。

 このシナリオでは、開発者がそれぞれの親プロジェクトの下に入れ子化できるプロジェクトの数に制限はありませんが、開発者がプログラムで制限を指定することはできます。 このようなグループ化を再帰的に行うこともできます。その場合、子プロジェクトと同じタイプのプロジェクトを子の下に入れ子化して、親のサブプロジェクトである子のサブプロジェクトにすることができます。

 プロジェクトの入れ子化は、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] の組み込み部分ではありません。 子プロジェクト内で入れ子化とサブプロジェクトの入れ子化を有効にするには、コードを記述する必要があります。 親プロジェクトは、独自の GUID を使用して作成および登録された特別な VSPackage またはプロジェクト タイプであり、プロジェクトの入れ子化を実装するために必要なコードが含まれています。

 プロジェクトを入れ子にする方法の例については、「[方法: 入れ子になったプロジェクトを実装する](../../extensibility/internals/how-to-implement-nested-projects.md)」を参照してください。

## <a name="nested-projects-example"></a>入れ子になったプロジェクトの例
 ![入れ子になったプロジェクトのソリューション](../../extensibility/internals/media/vsnestedprojects.gif "vsNestedProjects") 入れ子になったプロジェクトの例

## <a name="see-also"></a>関連項目
- [入れ子になったプロジェクトのアンロードと再ロードに関する考慮事項](../../extensibility/internals/considerations-for-unloading-and-reloading-nested-projects.md)
- [入れ子になったプロジェクト向けのウィザード サポート](../../extensibility/internals/wizard-support-for-nested-projects.md)
- [プロジェクトと項目テンプレートの登録](../../extensibility/internals/registering-project-and-item-templates.md)
- [入れ子になったプロジェクト向けのコマンド処理の実装](../../extensibility/internals/implementing-command-handling-for-nested-projects.md)
- [入れ子になったプロジェクトのための [AddItem] ダイアログ ボックスのフィルター処理](../../extensibility/internals/filtering-the-additem-dialog-box-for-nested-projects.md)
- [チェックリスト: 新しいプロジェクト タイプの作成](../../extensibility/internals/checklist-creating-new-project-types.md)
- [コンテキスト パラメーター](../../extensibility/internals/context-parameters.md)
- [ウィザード (.Vsz) ファイル](../../extensibility/internals/wizard-dot-vsz-file.md)
