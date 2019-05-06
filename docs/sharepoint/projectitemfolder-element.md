---
title: ProjectItemFolder 要素 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ProjectItemFolder element
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 124716f8c40a8adc0a0ae1a28cda21dcb5e00ddf
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62562703"
---
# <a name="projectitemfolder-element"></a>ProjectItemFolder 要素
  マップされたフォルダーを表します。

## <a name="syntax"></a>構文

```xml
<ProjectItemFolder Target = "Path of SharePoint folder the mapped folder corresponds to"
    Type = "Type of deployment for the mapped folder" />
```

## <a name="type"></a>型
 **ProjectItemFolderType**

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|**Target**|必要な**xs: 文字列**属性。<br /><br /> マップされたフォルダーが配置ルート フォルダーを基準とした、対応する SharePoint のインストール フォルダーのパス。 配置ルート フォルダーがで指定された展開の種類によって決まりますが、**型**属性。<br /><br /> 詳細については、の説明を参照してください、**配置パス**と**Deployment Root** SharePoint のプロパティ内の項目をプロジェクト[SharePoint の開発ソリューション](../sharepoint/developing-sharepoint-solutions.md)します。|
|**Type**|必要な**xs:string**属性。<br /><br /> マップされたフォルダーの展開の種類。 使用可能な値の詳細については、の説明を参照して、**展開の種類**で SharePoint プロジェクト アイテムのプロパティ[SharePoint の開発ソリューション](../sharepoint/developing-sharepoint-solutions.md)します。|

### <a name="child-elements"></a>子要素
 なし。

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[ProjectItem](../sharepoint/projectitem-element.md)|SharePoint プロジェクト項目を表します。 この要素は、必要なルート要素の *.spdata*ファイル。|

## <a name="remarks"></a>Remarks
 マップされたフォルダーの詳細については、次を参照してください。[方法: 追加すると、マップされたフォルダーを削除する](../sharepoint/how-to-add-and-remove-mapped-folders.md)します。

## <a name="element-information"></a>要素情報

|||
|-|-|
|**Namespace**|http:\/\/schemas.microsoft.com/VisualStudio/2010/<br>SharePointTools/SharePointProjectItemModel|
|**スキーマ名**|SharePoint プロジェクト項目のスキーマ|
|**ファイルの検証**|ProjectItemModelSchema.xsd|
|**空にすることができます。**|いいえ|

## <a name="see-also"></a>関連項目
- [SharePoint プロジェクト項目スキーマのリファレンス](../sharepoint/sharepoint-project-item-schema-reference.md)
- [方法: 追加して、マップされたフォルダーを削除します。](../sharepoint/how-to-add-and-remove-mapped-folders.md)
