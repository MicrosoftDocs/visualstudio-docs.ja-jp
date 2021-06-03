---
title: FeatureProperty 要素 | Microsoft Docs
description: SharePoint プロジェクト項目スキーマの要素である FeatureProperty 要素に関する参照情報を表示します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- FeatureProperty element
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 070866b9dd14d974eb976b22bf7a79907e2c5d9e
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99876668"
---
# <a name="featureproperty-element"></a>FeatureProperty 要素
  フィーチャーが SharePoint に配置されるときに一緒に含まれるカスタム プロパティを表します。 フィーチャーが配置された後は、そのプロパティにコードでアクセスできます。

## <a name="syntax"></a>構文

```xml
<FeatureProperty Key = "Key of the property value"
    Value = "Property value" />
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|**キー**|必須の **xs: string** 属性。<br /><br /> プロパティ値を格納および取得するために使用されるキー。 各プロパティには、フィーチャー内で一意のキーが必要です。|
|**Value**|必須の **xs: string** 属性。<br /><br /> プロパティ値。|

### <a name="child-elements"></a>子要素
 なし。

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[FeatureProperties](../sharepoint/featureproperties-element.md)|フィーチャーが SharePoint に配置されるときに一緒に含まれるプロパティ値のコレクションを表します。|

## <a name="remarks"></a>解説
 フィーチャー プロパティの詳細については、「[プロジェクト項目でのパッケージ化と配置の情報を提供する](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md)」を参照してください。

## <a name="element-information"></a>要素情報

|プロパティ|値|
|-|-|
|**Namespace**|http:\/\/schemas.microsoft.com/VisualStudio/<br>2010/SharePointTools/SharePointProjectItemModel|
|**スキーマ名**|SharePoint プロジェクト項目スキーマ|
|**検証ファイル**|ProjectItemModelSchema.xsd|
|**空の場合もあります**|いいえ|

## <a name="see-also"></a>関連項目
- [SharePoint プロジェクト項目スキーマのリファレンス](../sharepoint/sharepoint-project-item-schema-reference.md)
- [プロジェクト項目でのパッケージ化と配置の情報を提供する](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md)
