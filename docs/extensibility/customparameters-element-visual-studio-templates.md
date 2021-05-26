---
title: CustomParameters 要素 (Visual Studio テンプレート) | Microsoft Docs
description: CustomParameters 要素と、テンプレート ウィザードでパラメーターの置換を行うときにウィザードに渡されるカスタム パラメーターをその要素でグループ化する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#CustomParameters
helpviewer_keywords:
- CustomParameters element [Visual Studio project templates]
ms.assetid: cf3efc91-1532-4022-bbb8-a18658424fee
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: cabb3d04276f95d48fa6ecae14acd46246537762
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105055571"
---
# <a name="customparameters-element-visual-studio-templates"></a>CustomParameters 要素 (Visual Studio テンプレート)
テンプレート ウィザードでパラメーターの置換を行うときにウィザードに渡されるカスタム パラメーターをグループ化します。

## <a name="syntax"></a>構文

```
<CustomParameters>
    <CustomParameter/>
    <CustomParameter/>
</CustomParameters>
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性
 なし。

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|[CustomParameter](../extensibility/customparameter-element-visual-studio-templates.md)|省略可能な要素です。<br /><br /> プロジェクトまたは項目がテンプレートから作成されるときに使用する、カスタム パラメーターの名前と値を含めます。 `CustomParameter` 要素に 0 個以上の `CustomParameters` 要素があります。|

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[TemplateContent](../extensibility/templatecontent-element-visual-studio-templates.md)|テンプレートの内容を指定します。|

## <a name="remarks"></a>解説

## <a name="example"></a>例
 次の例は、テンプレートでいくつかのカスタム パラメーターを使用する方法を示しています。 次のカスタム パラメーターを使用してテンプレートからプロジェクトまたは項目が作成されると、テンプレート ファイル内の `$color1$` と `$color2$` のすべてのインスタンスがそれぞれ `Red` と `Blue` に置き換えられます。

```
<CustomParameters>
    <CustomParameter Name="$color1$" Value="Red"/>
    <CustomParameter Name="$color2$" Value="Blue "/>
</CustomParameters>
```

## <a name="see-also"></a>関連項目
- [CustomParameter 要素 (Visual Studio テンプレート)](../extensibility/customparameter-element-visual-studio-templates.md)
- [テンプレート パラメーター](../ide/template-parameters.md)
- [Visual Studio テンプレート スキーマ参照](../extensibility/visual-studio-template-schema-reference.md)
