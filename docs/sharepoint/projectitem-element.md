---
title: ProjectItem 要素 | Microsoft Docs
description: ProjectItem 要素に関する参照情報を取得します。これは、SharePoint プロジェクト項目の XML スキーマ リファレンス内の SharePoint プロジェクト項目を表します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ProjectItem element
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 2b94b44bfa442805c4c785a48c9f60f56eb8e002
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99950589"
---
# <a name="projectitem-element"></a>ProjectItem 要素
  SharePoint プロジェクト項目を表します。 この要素は、 *.spdata* ファイルの必須のルート要素です。

## <a name="syntax"></a>構文

```xml
<ProjectItem DefaultFile = "File that opens in the editor when you open the project item"
    FeatureReceiverClass = "Class that implements a feature receiver for the project item"
    FeatureReceiverAssembly = "Assembly that defines a feature receiver for the project item"
    SupportedTrustLevels = "Trust levels that the project item supports"
    SupportedDeploymentScopes = "Deployment scopes that the project item supports"
    Type="Identifier for the project item">
  <Files>...</Files>
  <ProjectItemFolder>...</ProjectItemFolder>
  <SafeControls>...</SafeControls>
  <FeatureProperties>...</FeatureProperties>
  <ExtensionData>...</ExtensionData>
</ProjectItem>
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|**DefaultFile**|省略可能な **xs: string** 属性。<br /><br /> **ソリューション エクスプローラー** で SharePoint プロジェクト項目を開いたときに Visual Studio エディターで開くファイルの相対パス (ファイル名を含む)。 このパスは、 *.spdata* ファイルが含まれているフォルダーからの相対パスです。|
|**FeatureReceiverClass**|省略可能な **xs:string** 属性。<br /><br /> この SharePoint プロジェクト項目のフィーチャー レシーバー クラスの完全修飾名。 フィーチャー レシーバーの詳細については、「[プロジェクト項目でのパッケージ化と配置の情報を提供する](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md)」を参照してください。|
|**FeatureReceiverAssembly**|省略可能な **xs:string** 属性。<br /><br /> この SharePoint プロジェクト項目のフィーチャー レシーバーを定義するアセンブリの完全修飾名を指定します。 フィーチャー レシーバーの詳細については、「[プロジェクト項目でのパッケージ化と配置の情報を提供する](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md)」を参照してください。 完全修飾アセンブリ名の詳細については、「[アセンブリ名](/dotnet/framework/app-domains/assembly-names)」を参照してください。|
|**SupportedTrustLevels**|省略可能な **xs:string** 属性。<br /><br /> この SharePoint プロジェクト項目でサポートされる信頼レベルを指定します。 この値には、次の文字列のいずれかを指定できます: Sandboxed、FullTrust、または All。 値 All は、Sandboxed と FullTrust の両方を指定します。<br /><br /> カスタムの SharePoint プロジェクト項目の種類では、この属性の値は、<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider.InitializeType%2A> メソッドの実装で <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeDefinition.SupportedTrustLevels%2A> プロパティに割り当てる値に相当します。 この属性に別の値を指定すると、Visual Studio により、<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeDefinition.SupportedTrustLevels%2A> プロパティで指定したのと同じ信頼レベルが指定されるように値が上書きされます。|
|**SupportedDeploymentScopes**|省略可能な **xs:string** 属性。<br /><br /> この SharePoint プロジェクト項目でサポートされる配置スコープを指定します。 この値は、Farm、Site、Web、WebApplication、または Package の 1 つ以上の文字列で構成されるコンマ区切りの文字列です。 例: `Web, Site`<br /><br /> カスタムの SharePoint プロジェクト項目の種類では、この属性の値は、<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider.InitializeType%2A> メソッドの実装で <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeDefinition.SupportedDeploymentScopes%2A> プロパティに割り当てる値に相当します。 この属性に別の値を指定すると、Visual Studio により、<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeDefinition.SupportedDeploymentScopes%2A> プロパティで指定したのと同じ信頼レベルが指定されるように値が上書きされます。|
|**Type**|必須の **xs: string** 属性。<br /><br /> SharePoint プロジェクト項目の識別子。 カスタムの SharePoint プロジェクト項目の種類では、識別子は <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemTypeAttribute> に渡す文字列です。 詳細については、「[方法: SharePoint プロジェクト項目の種類を定義する](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)」を参照してください。<br /><br /> Visual Studio に含まれている組み込みの SharePoint プロジェクト項目の識別子の一覧については、「[SharePoint プロジェクト項目の拡張](../sharepoint/extending-sharepoint-project-items.md)」を参照してください。|

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|[ExtensionData](../sharepoint/extensiondata-element.md)|省略可能な要素です。<br /><br /> SharePoint プロジェクト項目に関連付けられているカスタム データ項目のコレクションを表します。<br /><br /> 1 つの **ExtensionData** 要素だけを含めることができます。|
|[FeatureProperties](../sharepoint/featureproperties-element.md)|省略可能な要素です。<br /><br /> フィーチャーが SharePoint に配置されるときに一緒に含まれるプロパティ値のコレクションを表します。<br /><br /> 1 つの **FeatureProperties** 要素だけを含めることができます。|
|[ファイル](../sharepoint/files-element.md)|省略可能な **FileCollectionType** 要素です。<br /><br /> Feature 要素のファイルや従属の非 SharePoint プロジェクトの出力など、SharePoint プロジェクト項目と共に配置するファイルを指定します。<br /><br /> **Files** または **ProjectItemFolder** 要素の両方ではなく、いずれかが含まれます。|
|[ProjectItemFolder](../sharepoint/projectitemfolder-element.md)|省略可能な **ProjectItemFolderType** 要素です。<br /><br /> マップされたフォルダーを表します。<br /><br /> **Files** または **ProjectItemFolder** 要素の両方ではなく、いずれかが含まれます。|
|[SafeControls](../sharepoint/safecontrols-element.md)|省略可能な要素です。<br /><br /> SharePoint サイトの任意の ASPX ページで任意のユーザーがアクセスしても安全であると指定された ASPX コントロールおよび Web パーツのコレクションを表します。<br /><br /> 1 つの **SafeControls** 要素だけを含めることができます。|

### <a name="parent-elements"></a>親要素
 [なし] :

## <a name="element-information"></a>要素情報

|プロパティ|値|
|-|-|
|**Namespace**|http:\/\/schemas.microsoft.com/VisualStudio/<br>2010/SharePointTools/SharePointProjectItemModel|
|**スキーマ名**|SharePoint プロジェクト項目スキーマ|
|**検証ファイル**|ProjectItemModelSchema.xsd|
|**空の場合もあります**|いいえ|

## <a name="see-also"></a>関連項目
[SharePoint プロジェクト項目スキーマのリファレンス](../sharepoint/sharepoint-project-item-schema-reference.md)
