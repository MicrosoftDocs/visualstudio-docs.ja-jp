---
title: MaxFrameworkVersion 要素 (Visual Studio テンプレート) |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- <MaxFrameworkVersion> Element (Visual Studio Templates)
- MaxFrameworkVersion Element (Visual Studio Templates)
ms.assetid: f732a9d3-fc29-405b-9298-01ea83fc58b8
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 4a1c27e42574429dbb6b2eaeb140db484bf29db5
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "58976802"
---
# <a name="maxframeworkversion-element-visual-studio-templates"></a>MaxFrameworkVersion 要素 (Visual Studio テンプレート)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

テンプレートで必要とされる .NET Framework の最大バージョンを指定します。 テンプレートが表示されるかどうかを判断します、**テンプレート**のセクション、**新しいプロジェクトの追加** ダイアログ ボックスで選択されている値に基づいて、 **ターゲットフレームワークのバージョン**のボックス、**新しいプロジェクトの追加** ダイアログ ボックス。  
  
 \<VSTemplate>  
 \<MaxFrameworkVersion >  
  
## <a name="syntax"></a>構文  
  
```  
<MaxFrameworkVersion> ... </MaxFrameworkVersion>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
 なし。  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|必須の要素です。<br /><br /> テンプレートを分類し、いずれかでの表示方法を定義、**新しいプロジェクト**または**新しい項目の追加** ダイアログ ボックス。|  
  
## <a name="text-value"></a>テキスト値  
 テキスト値が必要です。  
  
 テキストは、テンプレートで許可されている .NET Framework の最上位のバージョン番号である必要があります。  
  
## <a name="remarks"></a>Remarks  
 `MaxFrameworkVersion` は、省略可能な要素です。 内の要素、 `TemplateData` .vstemplate ファイルのセクションは、のフィルターとして機能、**テンプレート**のセクション、**新しいプロジェクトの追加** ダイアログ ボックス。 .NET Framework の要件が一致するテンプレートのみより小さい`MaxFrameworkVersion`で選択されている値に基づいて、要素の値を表示するが、**ターゲット フレームワークのバージョン**のボックス、 **の新しいプロジェクトの追加** ダイアログ ボックス。 `MaxFrameworkVersion`から新しいバージョンの .NET Framework を使用している場合に表示されているテンプレートを誤って原因にならないように、必要な場合を除き、要素を省略する必要があります。  
  
## <a name="example"></a>例  
 次の例では、標準のメタデータ[!INCLUDE[csprcs](../includes/csprcs-md.md)]クラス テンプレートです。  
  
```  
<VSTemplate Type="Item" Version="3.0.0"  
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">  
    <TemplateData>  
        <Name>MyClass</Name>  
        <Description>My custom C# class template.</Description>  
        <Icon>Icon.ico</Icon>  
        <ProjectType>CSharp</ProjectType>  
        <MaxFrameworkVersion>3.5</MaxFrameworkVersion>  
        <DefaultName>MyClass</DefaultName>  
    </TemplateData>  
    <TemplateContent>  
        <ProjectItem>MyClass.cs</ProjectItem>  
    </TemplateContent>  
</VSTemplate>  
```  
  
 この例では、テンプレートで必要とされる .NET Framework の最大バージョンで表される`MaxFrameworkVersion`、3.5 です。 3.0 または 3.5 インチのいずれかを選択する場合にのみ、上記のテンプレートが表示されます、**ターゲット フレームワーク バージョン**ボックスに、**新しいプロジェクトの追加** ダイアログ ボックス。  
  
## <a name="see-also"></a>関連項目  
 [Visual Studio テンプレート スキーマ参照](../extensibility/visual-studio-template-schema-reference.md)   
 [プロジェクトと項目テンプレートの作成](../ide/creating-project-and-item-templates.md)
