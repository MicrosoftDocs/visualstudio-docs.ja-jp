---
title: ProjectType 要素 (Visual Studio テンプレート) |Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-general
ms.topic: conceptual
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#ProjectType
helpviewer_keywords:
- ProjectType element [Visual Studio project templates]
ms.assetid: ccf9d83f-c7f3-49c7-a31f-e1f22bec004c
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 0452f6bbee3232c757c2a5483d9c08fca220ad01
ms.sourcegitcommit: 06db1892fff22572f0b0a11994dc547c2b7e2a48
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/08/2018
ms.locfileid: "39636757"
---
# <a name="projecttype-element-visual-studio-templates"></a>ProjectType 要素 (Visual Studio テンプレート)
指定されたグループの下に表示されるように、プロジェクト テンプレートの分類、**新しいプロジェクト**または**新しい項目の追加** ダイアログ ボックス。  
  
> [!WARNING]
>  プロジェクト テンプレートは、Visual Studio 2012 以降の C++ でサポートされています。 これらは、Visual Studio 2010 以前のバージョンの C++ ではサポートされていません。  
  
 \<VSTemplate>  
 \<TemplateData>  
 \<ProjectType >  
  
## <a name="syntax"></a>構文  
  
```xml  
<ProjectType> CSharp/VisualBasic/VC/Web </ProjectType>  
```  
  
## <a name="attributes-and-elements"></a>属性と要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
 なし。  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|テンプレートをカテゴリに分類し、 **[新しいプロジェクト]** ダイアログ ボックス、または **[新しい項目の追加]** ダイアログ ボックスでどのように表示させるかを定義します。|  
  
## <a name="text-value"></a>テキスト値  
 テキスト値が必要です。  
  
 この値で、テンプレートから作成されるプロジェクトの種類を指定します。値には、次のいずれかの値を含める必要があります。  
  
-   `CSharp` : テンプレートが [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] のプロジェクトまたはアイテムを作成するよう指定します。  
  
-   `VisualBasic` : テンプレートが [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] のプロジェクトまたはアイテムを作成するよう指定します。  
  
-   `Web` : テンプレートが Web プロジェクトまたは Web アイテムを作成するよう指定します。 場合、`ProjectType`要素には、この値が含まれていますでプロジェクトまたはアイテムの言語が定義されている、 [ProjectSubType 要素 (Visual Studio テンプレート)](../extensibility/projectsubtype-element-visual-studio-templates.md)します。  
  
## <a name="remarks"></a>Remarks  
 `ProjectType` は `TemplateData` に必須の子要素です。  
  
 値、`ProjectType`要素は、テンプレートが存在場所を指定します、**新しいプロジェクト**または**新しい項目の追加** ダイアログ ボックス。 テンプレートなど、`ProjectType`の値`CSharp`下に表示されます、 **Visual c#** 内のノード、**新しいプロジェクト** ダイアログ ボックス。  
  
 使用してテンプレートのサブタイプを指定することができます、 [ProjectSubType](../extensibility/projectsubtype-element-visual-studio-templates.md)要素。  
  
## <a name="example"></a>例  
 [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] アプリケーションでのプロジェクト テンプレートのメタデータの例を次に示します。  
  
```  
<VSTemplate Type="Project" Version="3.0.0"  
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">  
    <TemplateData>  
        <Name>My template</Name>  
        <Description>A basic starter kit</Description>  
        <Icon>TemplateIcon.ico</Icon>  
        <ProjectType>CSharp</ProjectType>  
    </TemplateData>  
    <TemplateContent>  
        <Project File="MyStarterKit.csproj">  
            <ProjectItem>Form1.cs<ProjectItem>  
            <ProjectItem>Form1.Designer.cs</ProjectItem>  
            <ProjectItem>Program.cs</ProjectItem>  
            <ProjectItem>Properties\AssemblyInfo.cs</ProjectItem>  
            <ProjectItem>Properties\Resources.resx</ProjectItem>  
            <ProjectItem>Properties\Resources.Designer.cs</ProjectItem>  
            <ProjectItem>Properties\Settings.settings</ProjectItem>  
            <ProjectItem>Properties\Settings.Designer.cs</ProjectItem>  
        </Project>  
    </TemplateContent>  
</VSTemplate>  
```  
  
## <a name="see-also"></a>関連項目  
 [Visual Studio テンプレート スキーマ参照](../extensibility/visual-studio-template-schema-reference.md)   
 [プロジェクトと項目テンプレートを作成します。](../ide/creating-project-and-item-templates.md)   
 [ProjectSubType 要素 (Visual Studio テンプレート)](../extensibility/projectsubtype-element-visual-studio-templates.md)