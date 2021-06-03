---
title: ExtensionDataItem 要素 | Microsoft Docs
description: SharePoint プロジェクト項目スキーマの要素である ExtensionDataItem 要素に関する参照情報を表示します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ExtensionDataItem element
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: add1a119283635f9cfd9bebddfe18228f1976703
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99876824"
---
# <a name="extensiondataitem-element"></a>ExtensionDataItem 要素
  SharePoint プロジェクト項目に関連付けられているカスタム データ項目 (キー/値形式)。 キーと値は、どちらも文字列である必要があります。

## <a name="syntax"></a>構文

```xml
<ExtensionDataItem Key = "Key of the data item"
    Value = "Value of the data item" />
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|**キー**|必須の **xs: string** 属性。<br /><br /> データ項目を格納および取得するために使用されるキー。|
|**Value**|必須の **xs: string** 属性。<br /><br /> データ項目の値。|

### <a name="child-elements"></a>子要素
 なし。

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[ExtensionData](../sharepoint/extensiondata-element.md)|SharePoint プロジェクト項目に関連付けられているカスタム データ項目のコレクションを表します。|

## <a name="remarks"></a>解説
 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem> オブジェクトの <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem.ExtensionData%2A> プロパティを使用してカスタム データを SharePoint プロジェクト項目に関連付けると、Visual Studio では、そのデータがプロジェクト項目の `.spdata` ファイルの新しい **ExtensionDataItem** 要素に保存されます。 詳細については、「[SharePoint プロジェクト システムの拡張機能にデータを保存する](../sharepoint/saving-data-in-extensions-of-the-sharepoint-project-system.md)」を参照してください。

## <a name="element-information"></a>要素情報

|プロパティ|値|
|-|-|
|**Namespace**|http:\/\/schemas.microsoft.com/VisualStudio/<br>2010/SharePointTools/SharePointProjectItemModel|
|**スキーマ名**|SharePoint プロジェクト項目スキーマ|
|**検証ファイル**|ProjectItemModelSchema.xsd|
|**空の場合もあります**|いいえ|

## <a name="see-also"></a>関連項目
- [SharePoint プロジェクト項目スキーマのリファレンス](../sharepoint/sharepoint-project-item-schema-reference.md)
