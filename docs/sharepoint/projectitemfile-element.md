---
title: ProjectItemFile 要素 | Microsoft Docs
description: ProjectItemFile 要素に関する参照情報を取得します。これは、SharePoint プロジェクト項目の XML スキーマ リファレンス内のプロジェクト項目ファイルを表します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ProjectItemFile element
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: a7c6dd7fc46dc8616eddc164bcf2ec801657cb00
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99955139"
---
# <a name="projectitemfile-element"></a>ProjectItemFile 要素
  Feature 要素ファイルなど、SharePoint に配置するとき、プロジェクト ファイルと共に追加する SharePoint ファイルを表します。

## <a name="syntax"></a>構文

```xml
<ProjectItemFile Source = "Name of the file"
    Target = "Deployment path of the file"
    Type = "Type of deployment for the file" />
```

## <a name="type"></a>種類
 **ProjectItemFileType**

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|**ソース**|必須の **xs: string** 属性。<br /><br /> プロジェクト項目と共に配置するファイルの名前。|
|**移行先**|省略可能な **xs:string** 属性。<br /><br /> 配置ルート フォルダーを基準とした、SharePoint 上でのファイルの配置先のパス。 配置ルート フォルダーは、**Type** 属性によって指定された配置の種類によって決定されます。 **Target** 属性が指定されていない場合、ファイルは、**Source** 属性で指定された名前のフォルダーに配置されます。<br /><br /> 詳細については、「[SharePoint ソリューションの開発](../sharepoint/developing-sharepoint-solutions.md)」の SharePoint プロジェクト項目の **[配置パス]** および **[配置ルート]** プロパティの説明を参照してください。|
|**Type**|必須の **xs: string** 属性。<br /><br /> ファイルの配置の種類。 使用可能な値の詳細については、「[SharePoint ソリューションの開発](../sharepoint/developing-sharepoint-solutions.md)」の SharePoint プロジェクト項目の **[配置の種類]** プロパティの説明を参照してください。|

### <a name="child-elements"></a>子要素
 なし。

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[ファイル](../sharepoint/files-element.md)|SharePoint に配置されるときに SharePoint プロジェクト項目と共に含めるファイルを指定します。|

## <a name="remarks"></a>解説
 通常、**ProjectItemFile** 要素で参照される SharePoint ファイルには、Feature 要素ファイル (*Elements.xml*)、リスト定義のスキーマ ファイル (*Schema.xml*)、および Web パーツの Web パーツ定義ファイル ( *.webpart*) が含まれています。

## <a name="element-information"></a>要素情報

|プロパティ|値|
|-|-|
|**Namespace**|http:\/\/schemas.microsoft.com/VisualStudio/<br>2010/SharePointTools/SharePointProjectItemModel|
|**スキーマ名**|SharePoint プロジェクト項目スキーマ|
|**検証ファイル**|ProjectItemModelSchema.xsd|
|**空の場合もあります**|いいえ|

## <a name="see-also"></a>関連項目
- [SharePoint プロジェクト項目スキーマのリファレンス](../sharepoint/sharepoint-project-item-schema-reference.md)
