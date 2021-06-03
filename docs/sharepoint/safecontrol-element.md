---
title: SafeControl 要素 | Microsoft Docs
description: SafeControl 要素に関する情報を取得します。これは、SharePoint サイトの ASPX ページでのユーザーによるアクセスからセキュリティで保護されるとしてマークされた ASPX コントロールまたは Web パーツを表します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SafeControl element
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: f08046666ff00d4a0e5489bc78c0c70967774f08
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99889474"
---
# <a name="safecontrol-element"></a>SafeControl 要素
  SharePoint サイトの任意の ASPX ページでの任意のユーザーによるアクセスからセキュリティで保護されるとして指定された ASPX コントロールまたは Web パーツを表します。

## <a name="syntax"></a>構文

```xml
<SafeControl Assembly = "Name of assembly that contains the safe control"
    IsSafe = "true/false"
    IsSafeAgainstScript = "true/false"
    Name = "Name of this safe control entry"
    Namespace = "Namespace of the safe control"
    TypeName = "Type of the safe control" />
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|**Assembly**|省略可能な **xs:string** 属性。<br /><br /> ASPX コントロールまたは Web パーツが定義されているアセンブリの名前。 この属性では、既定でアセンブリ名に対して **$SharePoint.Project.AssemblyFullName$** という置き換え可能パラメーターが使用されます。 詳細については、「[置き換え可能パラメーター](../sharepoint/replaceable-parameters.md)」を参照してください。|
|**IsSafe**|省略可能な **xs:boolean** 属性。<br /><br /> ASPX コントロールまたは Web パーツが信頼されていないユーザーによるアクセスからセキュリティで保護されるかどうかを指定します。|
|**IsSafeAgainstScript**|省略可能な **xs:boolean** 属性。<br /><br /> 信頼されていないユーザーが ASPX コントロールまたは Web パーツのプロパティを表示または編集できるかどうかを指定します。|
|**名前**|省略可能な **xs:string** 属性。<br /><br /> コレクション内のこの安全なコントロール エントリの名前。|
|**Namespace**|省略可能な **xs:string** 属性。<br /><br /> ASPX コントロールまたは Web パーツの名前空間。|
|**TypeName**|省略可能な **xs:string** 属性。<br /><br /> ASPX コントロールまたは Web パーツの種類名。|

### <a name="child-elements"></a>子要素
 なし。

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[SafeControls](../sharepoint/safecontrols-element.md)|SharePoint サイトの任意の ASPX ページで任意のユーザーがアクセスしても安全であると指定された ASPX コントロールおよび Web パーツのコレクションを表します。|

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
