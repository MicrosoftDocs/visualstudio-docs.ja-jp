---
title: Files 要素 | Microsoft Docs
description: SharePoint プロジェクト項目スキーマの要素である Files 要素に関する参照情報を表示します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Files element
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 653e48a2e9b6a68db94fd66660da85f4dec20927
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99876648"
---
# <a name="files-element"></a>Files 要素
  Feature 要素のファイルや従属の非 SharePoint プロジェクトの出力など、SharePoint プロジェクト項目と共に配置するファイルを指定します。

## <a name="syntax"></a>構文

```xml
<Files>
  <ProjectItemFile.../>
  <ProjectOutputFile.../>
</Files>
```

## <a name="type"></a>種類
 **FileCollectionType**

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性
 なし。

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|[ProjectItemFile](../sharepoint/projectitemfile-element.md)|省略可能な **ProjectItemFileType** 要素。<br /><br /> Feature 要素ファイルなど、SharePoint に配置するとき、プロジェクト ファイルと共に追加する SharePoint ファイルを表します。|
|[ProjectOutputFile](../sharepoint/projectoutputfile-element.md)|省略可能な **ProjectOutputFileType** 要素。<br /><br /> SharePoint に配置するとき、プロジェクト項目と共に追加するプロジェクトの出力を表します。|

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[ProjectItem](../sharepoint/projectitem-element.md)|SharePoint プロジェクト項目を表します。 この要素は、`.spdata` ファイルの必須のルート要素です。|

## <a name="element-information"></a>要素情報

|プロパティ|値|
|-|-|
|**Namespace**|http:\/\/schemas.microsoft.com/VisualStudio/<br>2010/SharePointTools/SharePointProjectItemModel|
|**スキーマ名**|SharePoint プロジェクト項目スキーマ|
|**検証ファイル**|ProjectItemModelSchema.xsd|
|**空の場合もあります**|いいえ|

## <a name="see-also"></a>関連項目
- [SharePoint プロジェクト項目スキーマのリファレンス](../sharepoint/sharepoint-project-item-schema-reference.md)
