---
title: ProjectTemplateLink 要素 (Visual Studio テンプレート) |Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#ProjectTemplateLink
helpviewer_keywords:
- <ProjectTemplateLink> element [Visual Studio Templates]
- ProjectTemplateLink element [Visual Studio Templates]
ms.assetid: b0449111-8b48-45a1-a031-ea24b765e969
caps.latest.revision: 16
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 792c89b7c4a804a91a0c6e07ed4e9a1f2244ba7d
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/16/2018
ms.locfileid: "51738845"
---
# <a name="projecttemplatelink-element-visual-studio-templates"></a>ProjectTemplateLink 要素 (Visual Studio テンプレート)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

複数プロジェクトのテンプレートにある プロジェクトの .vstemplate ファイル パスを指定します。  
  
 \<VSTemplate>  
 \<TemplateContent >  
 \<ProjectCollection >  
 \<ProjectTemplateLink >  
- または -  
\<VSTemplate>  
 \<TemplateContent >  
 \<ProjectCollection >  
 \<SolutionFolder >  
 \<ProjectTemplateLink >  
  
## <a name="syntax"></a>構文  
  
```  
<ProjectTemplateLink ProjectName="Name">  
    PathToTemplateFile  
</ProjectTemplateLink>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|`ProjectName`|省略可能な属性です。<br /><br /> 複数プロジェクトのテンプレートにある各プロジェクトに個別の名前を指定します。 **新しいプロジェクト** ダイアログ ボックスは、個々 のプロジェクトに名前を割り当てることはできません。|  
|`CopyParameters`|メインのグループ テンプレート内のすべての変数を、リンクされたテンプレートそれぞれにコピーできるようにします。<br /><br /> リンクされたテンプレート内のパラメーターには、プレフィックス `"$ext_*$"` が付きます。 たとえば、親グループのテンプレート パラメーターの場合`$projectname$`の値を持つ**ExampleProject1**、リンクされたテンプレートを実行する順番を取得するときに、パラメーターを取得`$ext_projectname$`、のコピーである`$projectname$`、親グループのテンプレートのパラメーター。<br /><br /> これにより、リンクされたテンプレートは、親のグループ テンプレートでのみ簡単に作成できる一部の共通パラメーターを共有できるようになります。<br /><br /> この属性は省略可能であり、省略した場合は自動的に `false` に設定されます。<br /><br /> Visual Studio 2013 更新プログラム 2 で導入されました。 製品の正しいバージョンを参照するを参照してください。[を参照する、Visual Studio 2013 SDK の更新プログラム 2 で提供されるアセンブリ](http://msdn.microsoft.com/en-us/42b65c3e-e42b-4c39-98c8-bea285f25ffb)します。|  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|[ProjectCollection](../extensibility/projectcollection-element-visual-studio-templates.md)|複数プロジェクトのテンプレートの構成と内容を指定します。|  
|[SolutionFolder](../extensibility/solutionfolder-element-visual-studio-templates.md)|複数プロジェクトのテンプレートをグループ化します。|  
  
## <a name="text-value"></a>テキスト値  
 テキスト値が必要です。  
  
 これは、テンプレートの .vstemplate ファイルのパスを示します。  
  
## <a name="remarks"></a>Remarks  
 複数プロジェクトのテンプレートは、2 つ以上のプロジェクトのコンテナーとして機能します。 `ProjectTemplateLink` 要素は、テンプレート内にあるプロジェクトの .vstemplate ファイルの場所を指定するために使用します。 複数プロジェクトのテンプレートの .vstemplate ファイルには、1 プロジェクトにつき 1 つの `ProjectTemplateLink` 要素があります。 複数プロジェクトのテンプレートの詳細については、[方法: 複数プロジェクトのテンプレートの作成](../ide/how-to-create-multi-project-templates.md)を参照してください。  
  
## <a name="example"></a>例  
 簡単なマルチプロジェクトのルート .vstemplate ファイルの例を次に示します。 この例では、テンプレートには `My Windows Application` と `My Class Library` の 2 つのプロジェクトが含まれています。 `ProjectName` 要素の `ProjectTemplateLink` 属性は、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] がこのプロジェクトに割り当てる名前を設定します。 `ProjectName` 属性が存在しない場合、.vstemplate ファイルの名前がプロジェクト名として使用されます。  
  
```  
<VSTemplate Version="3.0.0" Type="ProjectGroup"  
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">  
    <TemplateData>  
        <Name>Multi-Project Template Sample</Name>  
        <Description>An example of a multi-project template</Description>  
        <Icon>Icon.ico</Icon>  
        <ProjectType>VisualBasic</ProjectType>  
    </TemplateData>  
    <TemplateContent>  
        <ProjectCollection>  
            <ProjectTemplateLink ProjectName="My Windows Application">  
                WindowsApp\MyTemplate.vstemplate  
            </ProjectTemplateLink>  
            <ProjectTemplateLink ProjectName="My Class Library" CopyParameters="true">  
                ClassLib\MyTemplate.vstemplate  
            </ProjectTemplateLink>  
        </ProjectCollection>  
    </TemplateContent>  
</VSTemplate>  
```  
  
## <a name="see-also"></a>関連項目  
 [Visual Studio テンプレート スキーマ参照](../extensibility/visual-studio-template-schema-reference.md)   
 [プロジェクトと項目テンプレートの作成](../ide/creating-project-and-item-templates.md)   
 [方法 : 複数プロジェクトのテンプレートを作成する](../ide/how-to-create-multi-project-templates.md)

