---
title: '&lt;RelatedProducts&gt; 要素 (ブートストラップ) |Microsoft Docs'
description: RelatedProducts 要素は、現在の製品に依存しているか、または現在の製品に含まれている他の製品を定義します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- MSBuild.GenerateBootstrapper.MissingDependency
- MSBuild.GenerateBootstrapper.DuplicateItems
- MSBuild.GenerateBootstrapper.IncludedProductIncluded
- MSBuild.GenerateBootstrapper.DependencyNotFound
- MSBuild.GenerateBootstrapper.PackageFileNotFound
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- <RelatedProducts> element [bootstrapper]
ms.assetid: bf152712-4c1e-48bd-9b7f-311cf0fdb832
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: a7987306d9f7fc25f9f9b783d5b0966ac5015ce0
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99949689"
---
# <a name="ltrelatedproductsgt-element-bootstrapper"></a>&lt;RelatedProducts&gt; 要素 (ブートストラップ)
`RelatedProducts` 要素は、現在の製品に依存しているか、または現在の製品に含まれている他の製品を定義します。

## <a name="syntax"></a>構文

```xml
<RelatedProducts>
    <DependsOnProduct
        Code
    />
    <EitherProducts>
        <DependsOnProduct
            Code
        />
    </EitherProducts>
    <IncludesProduct
        Code
    />
</RelatedProducts>
```

## <a name="elements-and-attributes"></a>要素と属性
 `RelatedProducts` 要素は、`Product` 要素の子です。 属性はありません。

## <a name="dependsonproduct"></a>DependsOnProduct
 `DependsOnProduct` 要素は、現在の製品が指定された製品に依存していること、および指定された製品を現在の製品より前にインストールする必要があることを示します。 `RelatedProducts` 要素の子です。 `RelatedProducts` 要素には、1 つまたは複数の `DependsOnProduct` 要素が含まれます。

 `DependsOnProduct` には、以下の属性があります。

|属性|説明|
|---------------|-----------------|
|`Code`|含まれる製品のコード名。`Product` 要素の `ProductCode` 属性によって指定されます。 詳細については、[\<Product> 要素](../deployment/product-element-bootstrapper.md)に関するページを参照してください。|

## <a name="eitherproducts"></a>EitherProducts
 `EitherProducts` 要素は、0 個以上の `DependsOnProduct` 要素を定義し、属性はありません。 このセット内の少なくとも 1 つの `DependsOnProduct` を、現在の製品よりも前にインストールする必要があります。 `RelatedProducts` 要素には、1 つ以上の `EitherProducts` 要素を含めることができます。

## <a name="includesproduct"></a>IncludesProduct
 `IncludesProduct` 要素は、製品が現在のインストールに含まれ、個別インストールが必要ないことを示します。 `RelatedProducts` 要素の子です。 `RelatedProducts` 要素には、1 つまたは複数の `IncludesProduct` 要素が含まれます。

 `IncludesProduct` には、以下の属性があります。

|属性|説明|
|---------------|-----------------|
|`Code`|含まれる製品のコード名。`Product` 要素の `ProductCode` 属性によって指定されます。 詳細については、[\<Product> 要素](../deployment/product-element-bootstrapper.md)に関するページを参照してください。|

## <a name="example"></a>例
 次のコード例では、Microsoft インストーラーが .NET Framework と共にインストールされるため、個別にインストールする必要がないことを指定します。

```xml
<RelatedProducts>
    <IncludesProduct Code="Microsoft.Windows.Installer.2.0" />
</RelatedProducts>
```

## <a name="see-also"></a>関連項目
- [\<Product> 要素](../deployment/product-element-bootstrapper.md)