---
title: CustomParameter 要素 (Visual Studio テンプレート) | Microsoft Docs
description: CustomParameter 要素について示し、プロジェクトまたは項目がテンプレートから作成されるときに使用するカスタム パラメーター名と値がどのように含まれているかを説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#CustomParameter
helpviewer_keywords:
- CustomParameters element [Visual Studio project templates]
ms.assetid: 743c4489-74ac-403a-bbaa-eed7d785a3ac
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 6190dc96501221a31c9a51f59e1bd734b9e08260
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105055597"
---
# <a name="customparameter-element-visual-studio-templates"></a>CustomParameter 要素 (Visual Studio テンプレート)
プロジェクトまたは項目がテンプレートから作成されるときに使用する、カスタム パラメーターの名前と値が含まれます。

## <a name="syntax"></a>構文

```
<CustomParameter Name="name" Value="value">
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|`Name`|必須。 パラメーターの名前。 パラメーターの形式は $*name*$ です。|
|`Value`|必須。 パラメーターの置換値。|

### <a name="child-elements"></a>子要素
 なし。

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[CustomParameters](../extensibility/customparameters-element-visual-studio-templates.md)|テンプレート ウィザードでパラメーターの置換を行うときにウィザードに渡されるカスタム パラメーターをグループ化します。|

## <a name="remarks"></a>解説
 テンプレートに `CustomParameter` 要素が含まれるとき、`Name` 属性のすべてのインスタンスが、作成されたプロジェクトまたは項目ファイルの `Value` 属性で置換されます。

## <a name="example"></a>例
 次の例は、テンプレートでいくつかのカスタム パラメーターを使用する方法を示しています。 次のカスタム パラメーターを使用してテンプレートからプロジェクトまたは項目が作成されると、テンプレート ファイル内の `$color1$` と `$color2$` のすべてのインスタンスがそれぞれ `Red` と `Blue` に置き換えられます。

```
<CustomParameters>
    <CustomParameter Name="$color1$" Value="Red"/>
    <CustomParameter Name="$color2$" Value="Blue "/>
</CustomParameters>
```

## <a name="see-also"></a>こちらもご覧ください
- [CustomParameters 要素 (Visual Studio テンプレート)](../extensibility/customparameters-element-visual-studio-templates.md)
- [テンプレート パラメーター](../ide/template-parameters.md)
- [Visual Studio テンプレート スキーマ参照](../extensibility/visual-studio-template-schema-reference.md)
