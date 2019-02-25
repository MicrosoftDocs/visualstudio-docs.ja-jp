---
title: ProjectItemFile 要素 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ProjectItemFile element
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 76da5221d8f5bbdeb40f22559c6fabba727986b4
ms.sourcegitcommit: d0425b6b7d4b99e17ca6ac0671282bc718f80910
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/21/2019
ms.locfileid: "56645356"
---
# <a name="projectitemfile-element"></a>ProjectItemFile 要素
  機能の要素ファイルが SharePoint に展開するときに、プロジェクト項目に含めるなど、SharePoint のファイルを表します。

## <a name="syntax"></a>構文

```xml
<ProjectItemFile Source = "Name of the file"
    Target = "Deployment path of the file"
    Type = "Type of deployment for the file" />
```

## <a name="type"></a>型
 **ProjectItemFileType**

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|**ソース**|必要な**xs:string**属性。<br /><br /> プロジェクト項目で展開するファイルの名前。|
|**Target**|省略可能な**xs:string**属性。<br /><br /> ファイルが配置される、SharePoint のデプロイ ルート フォルダーの相対パス。 配置ルート フォルダーがで指定された展開の種類によって決まりますが、**型**属性。 場合、**ターゲット**属性が指定されていない、ファイルがで指定された名前のフォルダーに配置する、**ソース**属性。<br /><br /> 詳細については、の説明を参照してください、**配置パス**と**Deployment Root** SharePoint のプロパティ内の項目をプロジェクト[SharePoint の開発ソリューション](../sharepoint/developing-sharepoint-solutions.md)します。|
|**Type**|必要な**xs:string**属性。<br /><br /> ファイルの展開の種類。 使用可能な値の詳細については、の説明を参照して、**展開の種類**で SharePoint プロジェクト アイテムのプロパティ[SharePoint の開発ソリューション](../sharepoint/developing-sharepoint-solutions.md)します。|

### <a name="child-elements"></a>子要素
 なし。

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[ファイル](../sharepoint/files-element.md)|SharePoint に配置されるときに、SharePoint プロジェクト項目に含めるファイルを指定します。|

## <a name="remarks"></a>Remarks
 SharePoint ファイルで参照される通常**ProjectItemFile**要素がフィーチャー要素ファイルが含まれます (*Elements.xml*)、リスト定義のスキーマ ファイル (*Schema.xml*)、および Web パーツの Web パーツの定義ファイル (*.webpart*)。

## <a name="element-information"></a>要素情報

|||
|-|-|
|**Namespace**|http<nolink>://schemas.microsoft.com/VisualStudio/<br>SharePointProjectItemModel SharePointTools/2010/|
|**スキーマ名**|SharePoint プロジェクト項目のスキーマ|
|**ファイルの検証**|ProjectItemModelSchema.xsd|
|**空にすることができます。**|いいえ|

## <a name="see-also"></a>関連項目
- [SharePoint プロジェクト項目スキーマのリファレンス](../sharepoint/sharepoint-project-item-schema-reference.md)
