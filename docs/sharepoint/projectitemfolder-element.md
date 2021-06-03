---
title: ProjectItemFolder 要素 | Microsoft Docs
description: ProjectItemFolder 要素に関する参照情報を取得します。これは、SharePoint プロジェクト項目の XML スキーマ リファレンス内のマップされたフォルダーを表します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ProjectItemFolder element
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: d1a5b5086ef90b9d8399a6f0f76bdee77c07288e
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99950576"
---
# <a name="projectitemfolder-element"></a>ProjectItemFolder 要素
  マップされたフォルダーを表します。

## <a name="syntax"></a>構文

```xml
<ProjectItemFolder Target = "Path of SharePoint folder the mapped folder corresponds to"
    Type = "Type of deployment for the mapped folder" />
```

## <a name="type"></a>種類
 **ProjectItemFolderType**

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|**移行先**|必須の **xs: string** 属性。<br /><br /> 配置ルート フォルダーを基準とした、マップされたフォルダーが対応する SharePoint インストール内のフォルダーのパス。 配置ルート フォルダーは、**Type** 属性によって指定された配置の種類によって決定されます。<br /><br /> 詳細については、「[SharePoint ソリューションの開発](../sharepoint/developing-sharepoint-solutions.md)」の SharePoint プロジェクト項目の **[配置パス]** および **[配置ルート]** プロパティの説明を参照してください。|
|**Type**|必須の **xs: string** 属性。<br /><br /> マップされたフォルダーの配置の種類。 使用可能な値の詳細については、「[SharePoint ソリューションの開発](../sharepoint/developing-sharepoint-solutions.md)」の SharePoint プロジェクト項目の **[配置の種類]** プロパティの説明を参照してください。|

### <a name="child-elements"></a>子要素
 なし。

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[ProjectItem](../sharepoint/projectitem-element.md)|SharePoint プロジェクト項目を表します。 この要素は、 *.spdata* ファイルの必須のルート要素です。|

## <a name="remarks"></a>解説
 マップされたフォルダーの詳細については、「[方法: マップされたフォルダーの追加と削除を行う](../sharepoint/how-to-add-and-remove-mapped-folders.md)」を参照してください。

## <a name="element-information"></a>要素情報

|プロパティ|値|
|-|-|
|**Namespace**|http:\/\/schemas.microsoft.com/VisualStudio/2010/<br>SharePointTools/SharePointProjectItemModel|
|**スキーマ名**|SharePoint プロジェクト項目スキーマ|
|**検証ファイル**|ProjectItemModelSchema.xsd|
|**空の場合もあります**|いいえ|

## <a name="see-also"></a>関連項目
- [SharePoint プロジェクト項目スキーマのリファレンス](../sharepoint/sharepoint-project-item-schema-reference.md)
- [方法: マップされたフォルダーの追加と削除を行う](../sharepoint/how-to-add-and-remove-mapped-folders.md)
