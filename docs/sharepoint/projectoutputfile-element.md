---
title: ProjectOutputFile 要素 | Microsoft Docs
description: ProjectOutputFile 要素に関する参照情報を取得します。これは、SharePoint プロジェクト項目の XML スキーマ参照内の別のプロジェクトの出力を表します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ProjectOutputFile element
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: a3b5a0f6474231fdc8f7617040ec4aa57056d9c0
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99966956"
---
# <a name="projectoutputfile-element"></a>ProjectOutputFile 要素
  SharePoint に配置するとき、プロジェクト項目と共に含める別のプロジェクトの出力を表します。

## <a name="syntax"></a>構文

```xml
<ProjectOutputFile ProjectId = "GUID of the project"
    ProjectPath = "Relative path of the project"
    Target = "Deployment path of the project output"
    Type = "Type of deployment for the project output" />
```

## <a name="type"></a>種類
 **ProjectOutputFileType**

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|**ProjectId**|必須の **xs: string** 属性。<br /><br /> 含める出力がある依存プロジェクトの GUID。 これは、依存プロジェクト ファイル内の **ProjectGuid** 要素に対応します。|
|**ProjectPath**|必須の **xs: string** 属性。<br /><br /> 含める出力がある依存プロジェクトの、プロジェクト ファイル名を含む相対パス。 このパスは、SharePoint プロジェクト項目が含まれている SharePoint プロジェクトのルート フォルダーに相対となります。|
|**移行先**|省略可能な **xs:string** 属性。<br /><br /> 配置ルート フォルダーを基準とした、SharePoint サーバーに依存プロジェクトの出力が配置されるパス。 配置ルート フォルダーは、**Type** 属性によって指定された配置の種類によって決定されます。<br /><br /> 詳細については、「[SharePoint ソリューションの開発](../sharepoint/developing-sharepoint-solutions.md)」の SharePoint プロジェクト項目の **[配置パス]** および **[配置ルート]** プロパティの説明を参照してください。|
|**Type**|必須の **xs: string** 属性。<br /><br /> 依存プロジェクトの出力に使用する配置の種類。 使用可能な値の詳細については、「[SharePoint ソリューションの開発](../sharepoint/developing-sharepoint-solutions.md)」の SharePoint プロジェクト項目の **[配置の種類]** プロパティの説明を参照してください。|

### <a name="child-elements"></a>子要素
 なし。

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[ファイル](../sharepoint/files-element.md)|SharePoint に配置されるときに SharePoint プロジェクト項目と共に含めるファイルを指定します。|

## <a name="remarks"></a>解説
 **ProjectOutputFile** 要素を使用して、SharePoint プロジェクト項目の配置にプロジェクトの出力を含めます。 別のプロジェクト、またはプロジェクト項目が含まれている同じプロジェクトを指定できます。 詳細については、[プロジェクト項目のパッケージ化および配置情報の提供](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md)に関するページを参照してください。

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
- [SharePoint ソリューションの開発](../sharepoint/developing-sharepoint-solutions.md)
