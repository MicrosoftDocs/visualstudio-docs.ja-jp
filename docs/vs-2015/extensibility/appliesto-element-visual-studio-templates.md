---
title: AppliesTo 要素 (Visual Studio テンプレート) |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
ms.assetid: 8fb1334b-d78c-405f-98b4-786e9f6b58d7
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 0b5151f739dfe464ae948eb4b4716f659b7a7913
ms.sourcegitcommit: 1fc6ee928733e61a1f42782f832ead9f7946d00c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "60044188"
---
# <a name="appliesto-element-visual-studio-templates"></a>AppliesTo 要素 (Visual Studio テンプレート)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

省略可能な式を 1 つ以上の機能と一致するように指定します  (「<xref:Microsoft.VisualStudio.Shell.Interop.VsProjectCapabilityExpressionMatcher>」を参照してください)。 機能は、<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID5> プロパティとして、階層を介してプロジェクトの種類によって公開されます。 このようにすると、共通の適用可能な機能を持つ複数のプロジェクトの種類によってテンプレートを共有できます。  
  
 この要素は省略可能です。 テンプレート ファイルには、最大で 1 つのインスタンスがあります。 この要素は、現在選択されているアクティブなプロジェクトの機能に基づいて、項目テンプレートを適用可能として利用できるようにするだけです。 項目テンプレートを適用不可にするためには使用できません。 `AppliesTo` が存在しない場合、または式を正常に利用できない場合は、製品の以前のバージョンの場合と同様に、テンプレートを適用可能にするために `TemplateID` または `TemplateGroupID` が使用されます。  
  
 Visual Studio 2013 更新プログラム 2 で導入されました。 正しいバージョンを参照するを参照してください。[を参照する、Visual Studio 2013 SDK の更新プログラム 2 で提供されるアセンブリ](http://msdn.microsoft.com/42b65c3e-e42b-4c39-98c8-bea285f25ffb)します。  
  
 \<VSTemplate>  
 \<TemplateData>  
 \<AppliesTo>  
  
## <a name="syntax"></a>構文  
  
```  
<AppliesTo>Capability1</AppliesTo>   
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
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|テンプレートをカテゴリに分類します。|  
  
## <a name="text-value"></a>テキスト値  
 テキスト値が必要です。 このテキストでプロジェクトの機能を指定します。  
  
 有効な式の構文は次のように定義されます。  
  
- 機能の式など"(Visualc++ &#124; CSharp) + (MSTest &#124; NUnit)"。  
  
- "&#124;"は OR 演算子です。  
  
- "&"と「+」文字は、どちらも AND 演算子。  
  
- "!" 文字は NOT 演算子です。  
  
- かっこで囲むことで、評価の優先順位が強制的に設定されます。  
  
- Null または空の式は、一致として評価されます。  
  
- これらの予約文字を除く任意の文字をプロジェクトの機能があります:"':;,+-*/\\! ~&#124;& %$@^() ={}:operator[] <> でしょうか。 を除く文字を使用できます。  
  
## <a name="example"></a>例  
 次の例に、3 種類のテンプレートを示します。 `Template1` は、C# のすべてのプロジェクトの種類、または `WindowsAppContainer` 機能をサポートする他のプロジェクトの種類に適用されます。 `Template2` は、すべての種類の C# プロジェクトに適用されます。 `Template3` は、`WindowsAppContainer` プロジェクトではない C# プロジェクトに適用されます。  
  
```xml  
<!--  Template 1 -->  
<?xml version="1.0" encoding="utf-8"?>  
<VSTemplate Version="3.0.0" Type="Item" xmlns="http://schemas.microsoft.com/developer/vstemplate/2005" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://schemas.microsoft.com/developer/vstemplate/2005">  
    <TemplateData>  
        <AppliesTo>CSharp | WindowsAppContainer</AppliesTo>   
    </TemplateData>  
</VSTemplate>  
  
<!--  Template 2 -->  
<?xml version="1.0" encoding="utf-8"?>  
<VSTemplate Version="3.0.0" Type="Item" xmlns="http://schemas.microsoft.com/developer/vstemplate/2005" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://schemas.microsoft.com/developer/vstemplate/2005">  
    <TemplateData>  
        <AppliesTo>CSharp</AppliesTo>   
    </TemplateData>  
</VSTemplate>  
  
<!--  Template 1 -->  
<?xml version="1.0" encoding="utf-8"?>  
<VSTemplate Version="3.0.0" Type="Item" xmlns="http://schemas.microsoft.com/developer/vstemplate/2005" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://schemas.microsoft.com/developer/vstemplate/2005">  
    <TemplateData>  
        <AppliesTo>CSharp_Class + (!WindowsAppContainer)</AppliesTo>   
    </TemplateData>  
</VSTemplate>  
  
```  
  
## <a name="see-also"></a>関連項目  
 [Visual Studio テンプレート スキーマ参照](../extensibility/visual-studio-template-schema-reference.md)   
 [プロジェクトと項目テンプレートの作成](../ide/creating-project-and-item-templates.md)
