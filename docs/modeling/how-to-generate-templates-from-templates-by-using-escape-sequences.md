---
title: テキスト テンプレートからテキスト テンプレートを生成する
description: エスケープ シーケンスを使用して別のテキスト テンプレートからテキスト テンプレートを生成する方法について説明します。
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- text templates, generating templates from templates
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.custom: SEO-VS-2020
ms.workload:
- multiple
ms.openlocfilehash: 9347e32a72e7f590f8f513c4b47a4b7aae699f27
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112387178"
---
# <a name="how-to-generate-templates-from-templates-by-using-escape-sequences"></a>方法: エスケープ シーケンスを使用してテンプレートからテンプレートを生成する
別のテキスト テンプレートを生成テキストの出力として作成するテキスト テンプレートを作成できます。 そのためには、エスケープ シーケンスを使用してテキスト テンプレート タグを記述する必要があります。 エスケープ シーケンスを使用しない場合、生成されたテキスト テンプレートには定義済みの意味があります。 テキスト テンプレートでのエスケープ シーケンスの使用の詳細については、「[テキスト テンプレートでのエスケープ シーケンスの使用](../modeling/using-escape-sequences-in-text-templates.md)」を参照してください。

### <a name="to-generate-a-text-template-from-within-a-text-template"></a>テキスト テンプレートからテキスト テンプレートを生成するには

- 円記号 (\\) をエスケープ文字として使用して、テキスト テンプレート内でディレクティブ、ステートメント、式、およびクラス フィーチャーのために必要なマークアップ タグを別のテキスト テンプレート ファイルに生成します。

    ```
    \<#@ directive \#>
    \<# statement \#>
    \<#= expression \#>
    \<#+ classfeature \#>
    ```

## <a name="example"></a>例
 次の例では、エスケープ文字を使用してテキスト テンプレートからテキスト テンプレートを生成します。 `output` ディレクティブにより、変換先のファイルの種類がテキスト テンプレート ファイルの種類 (.tt) に設定されます。

```csharp
\<#@ output extension=".tt" \#>
\<#@ assembly name="System.Xml.dll" \#>
\<#@ import namespace="System.Xml" \#>
\<#
XmlDocument xDoc = new XmlDocument();
//System.Diagnostics.Debugger.Break();
    xDoc.Load(@"E:\CSharp\Overview.xml");
    XmlAttributeCollection attributes = xDoc.Attributes;
    if (attributes != null)
    {
       foreach (XmlAttribute attr in attributes)
       {\#>
           \<#= attr.Name \#>
       \<#}
     }
\#>
```

 生成されたテキスト出力はテキスト テンプレートです。

```
<#@ output extension=".tt" #>
<#@ assembly name="System.Xml.dll" #>
<#@ import namespace="System.Xml" #>
<#
XmlDocument xDoc = new XmlDocument();
//System.Diagnostics.Debugger.Break();
    xDoc.Load(@"E:\CSharp\Overview.xml");
    XmlAttributeCollection attributes = xDoc.Attributes;
    if (attributes != null)
    {
       foreach (XmlAttribute attr in attributes)
       {#>
           <#= attr.Name #>
       <#}
     }
#>
```
