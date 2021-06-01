---
title: SharePoint プロジェクト項目スキーマ リファレンス | Microsoft Docs
description: .spdata ファイルの内容を検証するために使用される SharePoint プロジェクト項目 XML スキーマ リファレンス (ProjectItemModelSchema.xsd) の概要について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- FeatureProperty element
- SafeControls element
- SafeControl element
- .spdata files
- ExtensionData element
- FeatureProperties element
- ProjectOutputFile element
- Files element
- ProjectItemFolder element
- ProjectItemFile element
- ExtensionDataItem element
- ProjectItem element
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 466bc68ca002914b64698d7cd87f98ff276bfc0e
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99892282"
---
# <a name="sharepoint-project-item-schema-reference"></a>SharePoint プロジェクト項目スキーマ リファレンス
  SharePoint プロジェクト項目スキーマは、 *.spdata* ファイルの内容を検証するために、Visual Studio によって使用されます。 *.spdata* ファイルでは、SharePoint プロジェクト項目の内容と動作が指定されています。 SharePoint プロジェクト項目の内容の詳細については、「[SharePoint プロジェクト項目の項目テンプレートとプロジェクト テンプレートを作成する](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)」を参照してください。

 SharePoint プロジェクト項目スキーマは ProjectItemModelSchema.xsd という名前で、既定では %Program Files (x86)%\Microsoft Visual Studio 11.0\Xml\Schemas にインストールされます。

 ルート要素は [ProjectItem](../sharepoint/projectitem-element.md) 要素です。 次の表では、スキーマで定義されているすべての要素について説明します。

|要素|説明|
|-------------|-----------------|
|[ExtensionData](../sharepoint/extensiondata-element.md)|SharePoint プロジェクト項目に関連付けられているカスタム データ項目のコレクションを表します。|
|[ExtensionDataItem](../sharepoint/extensiondataitem-element.md)|SharePoint プロジェクト項目に関連付けられているカスタム データ項目 (キーと値の形式) を表します。 キーと値は、どちらも文字列である必要があります。|
|[FeatureProperties](../sharepoint/featureproperties-element.md)|SharePoint に配置されるときにフィーチャーに含まれるプロパティ値のコレクションを表します。 フィーチャーが配置されると、そのプロパティ値にコードでアクセスできるようになります。|
|[FeatureProperty](../sharepoint/featureproperty-element.md)|SharePoint に配置されるときにフィーチャーに含まれるカスタム プロパティを表します。 フィーチャーが配置された後は、そのプロパティ値にコードでアクセスできます。|
|[ファイル](../sharepoint/files-element.md)|フィーチャー要素ファイルやプロジェクトの出力など、SharePoint プロジェクト項目と共に配置するファイルを指定します。|
|[ProjectItem](../sharepoint/projectitem-element.md)|SharePoint プロジェクト項目を表します。|
|[ProjectItemFile](../sharepoint/projectitemfile-element.md)|フィーチャー要素ファイルなど、SharePoint に配置するときに、プロジェクト項目と共に含める SharePoint ファイルを表します。|
|[ProjectItemFolder](../sharepoint/projectitemfolder-element.md)|マップされたフォルダーを表します。|
|[ProjectOutputFile](../sharepoint/projectoutputfile-element.md)|SharePoint に配置するとき、プロジェクト項目と共に含めるプロジェクトの出力を表します。|
|[SafeControl](../sharepoint/safecontrol-element.md)|SharePoint サイトの任意の ASPX ページで任意のユーザーがアクセスしても安全であると指定された ASPX コントロールまたは Web パーツを表します。|
|[SafeControls](../sharepoint/safecontrols-element.md)|SharePoint サイトの任意の ASPX ページで任意のユーザーがアクセスしても安全であると指定された ASPX コントロールおよび Web パーツのコレクションを表します。|

## <a name="see-also"></a>こちらもご覧ください
- [SharePoint プロジェクト項目の項目テンプレートとプロジェクト テンプレートを作成する](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)
