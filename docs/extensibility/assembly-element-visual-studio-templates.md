---
title: Assembly 要素 (Visual Studio テンプレート) | Microsoft Docs
titleSuffix: ''
description: Assembly 要素について説明し、そこでアセンブリに関する情報を指定する方法について説明します。テンプレートでは、その情報を使用して、そのアセンブリの参照をプロジェクトに追加します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#Assembly
helpviewer_keywords:
- Assembly element [Visual Studio templates]
- <Assembly> element [Visual Studio templates]
ms.assetid: 9242f76a-1273-4b8a-8f26-6606f91829ef
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 54fc5cfccde99776136f0cb904d02bf6a4971045
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105097319"
---
# <a name="assembly-element-visual-studio-templates"></a>Assembly 要素 (Visual Studio テンプレート)
アセンブリに関する情報を指定します。テンプレートでは、これを使用して、そのアセンブリの参照をプロジェクトに追加します。

 \<VSTemplate> \<TemplateContent>
 \<References>
 \<Reference>
 \<Assembly>

## <a name="syntax"></a>構文

```
<Assembly> AssemblyName </Assembly>
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
|[参照](../extensibility/reference-element-visual-studio-templates.md)|項目がプロジェクトに追加されたときに追加するアセンブリ参照を指定します。|

## <a name="text-value"></a>テキスト値
 テキスト値が必要です。

 このテキストでは、項目テンプレートがインスタンス化されるときにプロジェクトに追加するアセンブリを指定します。 このアセンブリの名前は、次のいずれかの方法で指定する必要があります。

- 完全なアセンブリ名として。 次に例を示します。

    ```
    <Assembly>
        MyAssembly, Version=1.0.3300.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a, Custom = null.
    </Assembly>
    ```

- 単純なテキスト参照として。 次に例を示します。

    ```
    <Assembly> System </Assembly>
    ```

## <a name="remarks"></a>解説
 `Assembly` は `Reference` に必須の子要素です。

 `Reference`、`References,`、`Assembly` の各要素は、`Type` 属性値が `Item` である *.vstemplate* ファイル内でのみ使用できます。

## <a name="example"></a>例
 次の例は、項目テンプレートの `TemplateContent` 要素を示しています。 この XML では、*System.dll* および *System.Data.dll* アセンブリへの参照を追加します。

```
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
- [プロジェクト テンプレートと項目テンプレートを作成する](../ide/creating-project-and-item-templates.md)
