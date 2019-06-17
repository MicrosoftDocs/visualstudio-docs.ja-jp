---
title: 入れ子になったプロジェクト |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project nesting
- nested projects
- projects [Visual Studio SDK], child projects
- projects [Visual Studio SDK], nesting
ms.assetid: 12cce037-9840-4761-845e-5abd5fb317b0
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 209d3ca013e72ff709d0bd581dd460205d8e347d
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66326687"
---
# <a name="nesting-projects"></a>入れ子になったプロジェクト
VS パッケージを使用するエンタープライズ アプリケーション開発者が類似した種類のプロジェクトでまとめてを便利にグループ[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]を使用して*プロジェクトの入れ子*します。 たとえば、エンタープライズ テンプレート プロジェクトは、カテゴリにプロジェクトをグループ化の入れ子になったプロジェクトを使用します。 ビジネス ファサード プロジェクトや Web UI プロジェクトの場合は、1 つのカテゴリにグループ化。

 このシナリオでは、開発者は、各親プロジェクトの下で入れ子にできますプロジェクトの数に制限、開発者が制限をプログラムで提供できます。 この種類のグループ化もできる再帰的で、下に子は、親のサブプロジェクトのサブプロジェクト子場合に子プロジェクトと同じ型のプロジェクトを入れ子にすることができます。

 プロジェクトの入れ子の組み込みの一部でない[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]します。 入れ子を有効にして、子プロジェクト内の入れ子のサブプロジェクトにコードを記述する必要があります。 親プロジェクトは、特別な VSPackage は、またはプロジェクトの種類を作成し、プロジェクトの入れ子の実装に必要なコードが含まれる、独自の GUID に登録されています。

 C# Example.Nested プロジェクト サンプルでは、入れ子になったプロジェクトの例が見つかります。

## <a name="nested-projects-example"></a>入れ子になったプロジェクトの例
 ![プロジェクトのソリューションを入れ子になった](../../extensibility/internals/media/vsnestedprojects.gif "vsNestedProjects")入れ子になったプロジェクトの例

## <a name="see-also"></a>関連項目
- [方法: 入れ子になったプロジェクトの実装](../../extensibility/internals/how-to-implement-nested-projects.md)
- [入れ子になったプロジェクトのアンロードと再ロードに関する考慮事項](../../extensibility/internals/considerations-for-unloading-and-reloading-nested-projects.md)
- [入れ子になったプロジェクト向けのウィザード サポート](../../extensibility/internals/wizard-support-for-nested-projects.md)
- [プロジェクトと項目テンプレートの登録](../../extensibility/internals/registering-project-and-item-templates.md)
- [入れ子になったプロジェクト向けのコマンド処理の実装](../../extensibility/internals/implementing-command-handling-for-nested-projects.md)
- [入れ子になったプロジェクトのための [AddItem] ダイアログ ボックスのフィルター処理](../../extensibility/internals/filtering-the-additem-dialog-box-for-nested-projects.md)
- [チェックリスト: 新しいプロジェクト タイプの作成](../../extensibility/internals/checklist-creating-new-project-types.md)
- [コンテキスト パラメーター](../../extensibility/internals/context-parameters.md)
- [ウィザード (.Vsz) ファイル](../../extensibility/internals/wizard-dot-vsz-file.md)