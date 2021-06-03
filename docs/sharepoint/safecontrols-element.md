---
title: SafeControls 要素 | Microsoft Docs
description: SafeControls 要素に関する情報を取得します。これには、SharePoint サイトの ASPX ページでのアクセスからセキュリティで保護されるとしてマークされた ASPX コントロールまたは Web パーツのコレクションが保持されます。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SafeControls element
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 23e31e3df59d6d580ac94ffcb83f7a17e186a267
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99889448"
---
# <a name="safecontrols-element"></a>SafeControls 要素
  SharePoint サイトの任意の ASPX ページでの任意のユーザーによるアクセスからセキュリティで保護されるとして指定された ASPX コントロールおよび Web パーツのコレクション。

## <a name="syntax"></a>構文

```xml
<SafeControls>
  <SafeControl.../>
</SafeControls>
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性
 なし。

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|[SafeControl](../sharepoint/safecontrol-element.md)|省略可能な要素です。<br /><br /> SharePoint サイトの任意の ASPX ページでの任意のユーザーによるアクセスからセキュリティで保護されるとして指定された ASPX コントロールまたは Web パーツを表します。|

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[ProjectItem](../sharepoint/projectitem-element.md)|SharePoint プロジェクト項目を表します。 この要素は、 *.spdata* ファイルの必須のルート要素です。|

## <a name="remarks"></a>解説
 安全なコントロールの詳細については、「[プロジェクト項目でのパッケージ化と配置の情報を提供する](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md)」を参照してください。

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
