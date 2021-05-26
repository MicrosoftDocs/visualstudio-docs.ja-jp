---
title: オートメーション モデルの使用 | Microsoft Docs
description: オートメーション モデルに接続した後に VSPackage のプロパティとメソッドを取得する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- automation [Visual Studio SDK], automation model
ms.assetid: 0c7f7889-fbfb-4b19-804f-b742138baecd
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: a25936e0be16231bbe315a2bd29a0d495115f392
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105085807"
---
# <a name="using-the-automation-model"></a>オートメーション モデルの使用
VSPackage をオートメーションに接続した後、<xref:EnvDTE._DTE> オブジェクトの <xref:EnvDTE.DTEClass.GetObject%2A> メソッドを呼び出して、取得するオブジェクトを表す文字列を渡すことによって、プロパティとメソッドを取得できます。

## <a name="obtaining-project-objects"></a>プロジェクト オブジェクトの取得
 次の 2 つのコード例は、オートメーション コンシューマーでプロジェクト オートメーション オブジェクトを取得する方法を示しています。 DTE オブジェクトを取得する方法については、「[方法: DTE オブジェクトおよび DTE2 オブジェクトへの参照を取得する](/previous-versions/68shb4dw(v=vs.140))」を参照してください。

```vb
Sub DoAutomation()
    Dim MyProjects As Projects
    MyProjects = DTE.GetObject("AcmeProject")
End Sub
```

```cpp
void DoAutomation(void)
{
  CComQIPtr<Projects> pMyPkg; // Use an IDispatch-derived object type.
    pMyPkg = pDTE->GetObject("AcmeProjects");

   // The '=' performs a Query Interface.
   // Assumes pDTE is already available as a global.
   // Use pMyPkg to access your projects object's properties and methods.
}

```

 この時点で、特定の VSPackage の一部である標準のプロジェクト オブジェクトを使用して、階層モデルを下に移動できます。

 次のコード例は、カスタム プロジェクト タイプのプロパティであるカスタム オブジェクトを取得する方法を示しています。

```vb
Dim MyPrj As Project
Dim MyPrjItem As ProjectItem
Dim objMyObject as MyExtendedObject

MyPrj = MyProjects.Item(1) 'use the Projects collection to get a project
objMyObject = MyPrj.Object 'You call .Object to get to special Project
                           'implementation
objMyObject.MySpecialMethodOrProperty
```

 次のコードは、 **[ツール]** メニューの [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 環境の **[全般]** オプションにあるすべてのプロパティの名前を一覧表示します。

```vb
dim objDTE
dim objEnv
set objDTE = CreateObject("VisualStudio.DTE")
set objEnv = objDTE.Properties("Environment", "General")
for each obj in ObjEnv
MsgBox obj.Name
Next

```

## <a name="see-also"></a>関連項目
- <xref:EnvDTE.DTEClass.GetObject%2A>