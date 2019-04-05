---
title: SafeControl 要素 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SafeControl element
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: e6b47254a80c9cdadab6ca18f2fb8c3e8540fbd0
ms.sourcegitcommit: 3d37c2460584f6c61769be70ef29c1a67397cf14
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/21/2019
ms.locfileid: "58324566"
---
# <a name="safecontrol-element"></a>SafeControl 要素
  ASPX コントロールまたは SharePoint サイトのいずれかの ASPX ページにアクセスするすべてのユーザーに対してセキュリティで保護されたとして指定されている Web パーツを表します。

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
|**Assembly**|省略可能な**xs:string**属性。<br /><br /> ASPX コントロールまたは Web パーツが定義されているアセンブリの名前。 既定では、この属性を使用して、 **$SharePoint.Project.AssemblyFullName$** アセンブリ名の置き換え可能パラメーター。 詳細については、[置き換え可能パラメーター](../sharepoint/replaceable-parameters.md)を参照してください。|
|**IsSafe**|省略可能な**xs:boolean**属性。<br /><br /> ASPX コントロールまたは Web パーツが信頼されていないユーザーにアクセスするセキュリティで保護されたかどうかを指定します。|
|**IsSafeAgainstScript**|省略可能な**xs:boolean**属性。<br /><br /> 信頼されていないユーザーを表示したり、ASPX コントロールまたは Web パーツのプロパティの編集にかどうかを指定します。|
|**Name**|省略可能な**xs:string**属性。<br /><br /> このコレクション内の安全なコントロール エントリの名前。|
|**Namespace**|省略可能な**xs:string**属性。<br /><br /> ASPX コントロールまたは Web パーツの名前空間。|
|**TypeName**|省略可能な**xs:string**属性。<br /><br /> ASPX コントロールまたは Web パーツの型名。|

### <a name="child-elements"></a>子要素
 なし。

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[SafeControls](../sharepoint/safecontrols-element.md)|ASPX コントロールと、SharePoint サイト上のいずれかの ASPX ページにアクセスするすべてのユーザーに対してセキュリティで保護されたとして指定されている Web パーツのコレクションを表します。|

## <a name="remarks"></a>Remarks
 安全なコントロールの詳細については、[プロジェクト項目でパッケージ化と配置の情報を提供](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md)を参照してください。

## <a name="element-information"></a>要素情報

|||
|-|-|
|**Namespace**|http:\/\/schemas.microsoft.com/VisualStudio/<br>SharePointProjectItemModel SharePointTools/2010/|
|**スキーマ名**|SharePoint プロジェクト項目のスキーマ|
|**ファイルの検証**|ProjectItemModelSchema.xsd|
|**空にすることができます。**|いいえ|

## <a name="see-also"></a>関連項目
- [SharePoint プロジェクト項目スキーマのリファレンス](../sharepoint/sharepoint-project-item-schema-reference.md)
- [プロジェクト項目でパッケージ化と配置の情報を提供します。](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md)
