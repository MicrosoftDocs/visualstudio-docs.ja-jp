---
title: References 要素 (Visual Studio テンプレート) | Microsoft Docs
description: References 要素と、それを使用して、テンプレートによってプロジェクトに追加されるアセンブリ参照をグループ化する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#References
helpviewer_keywords:
- <References> element [Visual Studio Templates]
- References element [Visual Studio Templates]
ms.assetid: 1969146d-46bf-422d-8d46-0e9493925003
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: be367bbd1b466c5df3051af384ccefdcf93f8b44
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105056572"
---
# <a name="references-element-visual-studio-templates"></a>References 要素 (Visual Studio テンプレート)
テンプレートによってプロジェクトに追加されるアセンブリ参照をグループ化します。

 \<VSTemplate> \<TemplateContent>
 \<References>

## <a name="syntax"></a>構文

```xml
<References>
    <Reference>... </Reference>
    <Reference>... </Reference>
    ...
</References>
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性
 なし。

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|[参照](../extensibility/reference-element-visual-studio-templates.md)|必須の要素です。<br /><br /> 項目がプロジェクトに追加されたときに追加するアセンブリ参照を指定します。 `References` 要素内で 1 個以上の `Reference` 要素を指定する必要があります。|

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[TemplateContent](../extensibility/templatecontent-element-visual-studio-templates.md)|テンプレートの内容を指定します。|

## <a name="remarks"></a>解説
 `References` は、`TemplateContent` の子要素で、省略可能な要素です。

 `Reference` および `References` 要素を使用できるのは、`Item` の `Type` 属性値を含む *.vstemplate* ファイル内のみです。

## <a name="example"></a>例
 次の例は、項目テンプレートの `TemplateContent` 要素を示しています。 この XML を使用すると、*System.dll* および *System.Data.dll* アセンブリへの参照が追加されます。

```xml
<TemplateContent>
    <References>
        <Reference>
            <Assembly>
                System, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089
            </Assembly>
        </Reference>
        <Reference>
            <Assembly>
                System.Data, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089
            </Assembly>
        </Reference>
    </References>
    ...
</TemplateContent>
```

## <a name="see-also"></a>関連項目
- [Visual Studio テンプレート スキーマ参照](../extensibility/visual-studio-template-schema-reference.md)
- [プロジェクトと項目テンプレートの作成](../ide/creating-project-and-item-templates.md)
