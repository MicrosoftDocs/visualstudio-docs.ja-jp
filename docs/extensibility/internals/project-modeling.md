---
title: プロジェクトのモデリング | Microsoft Docs
description: 新しいプロジェクト タイプに対するオートメーションを作成するために必要な標準プロジェクト オブジェクトと、プロジェクト オートメーションが従うパスについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- automation [Visual Studio SDK], implementing project objects
- project models, automation
ms.assetid: c8db8fdb-88c1-4b12-86fe-f3c30a18f9ee
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 506606291996c94ff10514c6c57f83c6e1133862
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105062825"
---
# <a name="project-modeling"></a>プロジェクトのモデリング
プロジェクトのオートメーションを実現する次のステップでは、標準のプロジェクト オブジェクト (<xref:EnvDTE.Projects> および `ProjectItems` コレクション、`Project` および <xref:EnvDTE.ProjectItem> オブジェクト、実装に固有の残りのオブジェクト) を実装します。 これらの標準オブジェクトは、Dteinternal.h ファイルで定義されています。 標準オブジェクトの実装は、BscPrj サンプルに用意されています。 これらのクラスをモデルとして使用して、他のプロジェクト タイプのプロジェクト オブジェクトと両立する独自の標準プロジェクト オブジェクトを作成できます。

 オートメーション コンシューマーは、<xref:EnvDTE.Solution>("`<UniqueProjName>")` および <xref:EnvDTE.ProjectItems> (`n`) を呼び出せることを前提としています。ここで、n は、ソリューション内の特定のプロジェクトを取得するためのインデックス番号です。 このオートメーション呼び出しを行うと、環境では、ItemID パラメーターとして VSITEMID_ROOT が、VSHPROPID パラメーターとして VSHPROPID_ExtObject が渡されて、適切なプロジェクト階層で <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.GetProperty%2A> が呼び出されます。 `IVsHierarchy::GetProperty` により、実装したコア `Project` インターフェイスを提供するオートメーション オブジェクトへの `IDispatch` ポインターが返されます。

 `IVsHierarchy::GetProperty` の構文を次に示します。

 `HRESULT GetProperty (`

 `VSITEMID` `itemid`,

 `VSHPROPID` `propid`,

 `VARIANT` `*pvar`

 `);`

 プロジェクトでは、入れ子に対応し、コレクションを使用して、プロジェクト項目のグループを作成します。 この階層構造は次のようになっています。

```
Projects
  |- Project
      |- ProjectItems (a collection of ProjectItem)
          |- ProjectItem (single object) or ProjectItems (another collection)
```

 入れ子とは、入れ子になったオブジェクトを `ProjectItems` コレクションに含めることができるため、<xref:EnvDTE.ProjectItem> オブジェクトが同時に <xref:EnvDTE.ProjectItems> コレクションにもなれることを意味します。 基本的なプロジェクトのサンプルでは、この入れ子については説明しません。 `Project` オブジェクトを実装して、オートメーション モデル全体の設計を特徴付けるツリー状の構造に参加します。

 プロジェクト オートメーションは、次の図のパスに従います。

 ![Visual Studio プロジェクト オブジェクト](../../extensibility/internals/media/projectobjects.gif "ProjectObjects") プロジェクト オートメーション

 `Project` オブジェクトを実装しない場合でも、プロジェクトの名前のみを含む汎用の `Project` オブジェクトが環境によって返されます。

## <a name="see-also"></a>関連項目
- <xref:EnvDTE.Projects>
- <xref:EnvDTE.ProjectItem>
- <xref:EnvDTE.ProjectItems>
