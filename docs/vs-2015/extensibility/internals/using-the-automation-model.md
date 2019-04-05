---
title: オートメーション モデルを使用して |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- automation [Visual Studio SDK], automation model
ms.assetid: 0c7f7889-fbfb-4b19-804f-b742138baecd
caps.latest.revision: 16
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: d0e628b1e920031aa447485536863c1b563bc1c7
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "58962745"
---
# <a name="using-the-automation-model"></a>オートメーション モデルの使用
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

プロパティとメソッドを入手して、VSPackage を automation に接続した後、<xref:EnvDTE.DTEClass.GetObject%2A>メソッドを<xref:EnvDTE._DTE>オブジェクトを取得するオブジェクトを表す文字列を渡します。  
  
## <a name="obtaining-project-objects"></a>プロジェクト オブジェクトを取得します。  
 取得する方法、コンシューマーをオートメーション プロジェクト オートメーション オブジェクトを示す 2 つのコード例を次に示します。 DTE オブジェクトを取得する方法については、次を参照してください。[方法。DTE と DTE2 オブジェクトへの参照を取得](http://msdn.microsoft.com/library/c92e3c8e-82e6-4a67-85da-e43c50ffd8e4)します。  
  
```vb  
Sub DoAutomation()  
    Dim MyProjects As Projects  
    MyProjects = DTE.GetObject("AcmeProject")  
End Sub  
```  
  
```cpp#  
void DoAutomation(void)  
{  
  CComQIPtr<Projects> pMyPkg; // Use an IDispatch-derived object type.  
    pMyPkg = pDTE->GetObject("AcmeProjects");   
  
   // The '=' performs a Query Interface.  
   // Assumes pDTE is already available as a global.  
   // Use pMyPkg to access your projects object's properties and methods.  
}  
  
```  
  
 この時点では、階層モデルの下に移動する特定の VSPackage の一部である標準的なプロジェクト オブジェクトを使用することができます。  
  
 次のコード例は、カスタムのプロジェクトの種類のプロパティであるカスタム オブジェクトを取得する方法を示します。  
  
```vb  
Dim MyPrj As Project  
Dim MyPrjItem As ProjectItem  
Dim objMyObject as MyExtendedObject  
  
MyPrj = MyProjects.Item(1) 'use the Projects collection to get a project  
objMyObject = MyPrj.Object 'You call .Object to get to special Project  
                           'implementation  
objMyObject.MySpecialMethodOrProperty  
```  
  
 次のコードは、すべてのプロパティの名前を一覧表示されます、[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]環境**全般**オプション、**ツール**メニュー。  
  
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
 <xref:EnvDTE.DTEClass.GetObject%2A>
