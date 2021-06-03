---
title: フィーチャーおよびパッケージ マニフェストでの XML のマージ | Microsoft Docs
description: SharePoint のフィーチャーおよびパッケージ マニフェストに、デザイナーで生成された XML コードとユーザーが追加した XML コードをマージします。 フィーチャーおよびパッケージ マニフェスト要素とマージ例外について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, packaging
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 8be6adfedeabaea236e4dcb2cd969e6023a7f3ec
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99889565"
---
# <a name="merge-xml-in-feature-and-package-manifests"></a>フィーチャーおよびパッケージ マニフェストでの XML のマージ
  フィーチャーとパッケージは、[!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] マニフェスト ファイルによって定義されます。 これらのパッケージ化されたマニフェストは、デザイナーで生成されたデータと、ユーザーによってマニフェスト テンプレートに入力されたカスタム [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] を組み合わせたものです。 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] では、パッケージ化の際に、カスタム [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] ステートメントとデザイナーから提供された [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] をマージして、パッケージ化された [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] マニフェスト ファイルを作成します。 SharePoint にファイルを配置した後で [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] 検証エラーが発生しないようにし、マニフェスト ファイルを小さく効率的なものにするため、後の「マージ例外」で説明されている場合を除き、同様の要素もマージされます。

## <a name="modify-the-manifests"></a>マニフェストを変更する
 パッケージ化されたマニフェスト ファイルは、フィーチャーまたはパッケージ デザイナーを無効にするまで、直接変更できません。 ただし、フィーチャーおよびパッケージ デザイナーまたは [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] エディターを使用して、手動でマニフェスト テンプレートにカスタム [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] 要素を追加できます。 詳細については、「[方法: SharePoint フィーチャーをカスタマイズする](../sharepoint/how-to-customize-a-sharepoint-feature.md)」と「[方法: SharePoint ソリューション パッケージをカスタマイズする](../sharepoint/how-to-customize-a-sharepoint-solution-package.md)」を参照してください。

## <a name="feature-and-package-manifest-merge-process"></a>フィーチャーおよびパッケージ マニフェストのマージ プロセス
 カスタム要素とデザイナーから提供される要素を組み合わせる場合、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] では次のプロセスを使用します。 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] では、各要素に一意のキー値があるかどうかを確認します。 要素に一意のキー値がない場合、それはパッケージ化されたマニフェスト ファイルに追加されます。 同様に、複数のキーを持つ要素はマージできません。 したがって、それらはマニフェスト ファイルに追加されます。

 要素に一意のキーがある場合、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ではデザイナーのキーとカスタム キーの値を比較します。 値が一致する場合、それらは 1 つの値にマージされます。 値が異なる場合、デザイナーのキー値は破棄され、カスタム キー値が使用されます。 コレクションもマージされます。 たとえば、デザイナーで生成された [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] とカスタム [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] の両方にアセンブリ コレクションが含まれている場合、パッケージ化されたマニフェストにはアセンブリ コレクションが 1 つだけ含まれます。

## <a name="merge-exceptions"></a>マージ例外
 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] では、単一の一意識別属性が存在する限り、ほとんどのデザイナー [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] 要素を類似したカスタム [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] 要素とマージします。 ただし、[!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] マージに必要な一意識別子を持たない要素もあります。 これらの要素は "*マージ例外*" と呼ばれます。 このような場合、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] では、カスタム [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] 要素とデザイナーから提供される [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] 要素をマージせずに、パッケージ化されたマニフェスト ファイルに追加します。

 フィーチャーおよびパッケージ [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] マニフェスト ファイルのマージ例外の一覧を次に示します。

|デザイナー|XML 要素|
|--------------|-----------------|
|フィーチャー デザイナー|ActivationDependency|
|フィーチャー デザイナー|UpgradeAction|
|パッケージ デザイナー|SafeControl|
|パッケージ デザイナー|CodeAccessSecurity|

## <a name="feature-manifest-elements"></a>フィーチャー マニフェスト要素
 次の表に、マージできるすべてのフィーチャー マニフェスト要素と、一致に使用される一意のキーの一覧を示します。

|要素名|一意キー|
|------------------|----------------|
|Feature (すべての属性)|<*属性名*> (Feature 要素の各属性名は一意のキーです。)|
|ElementFile|場所|
|ElementManifests/ElementManifest|場所|
|Properties/Property|キー|
|CustomUpgradeAction|名前|
|CustomUpgradeActionParameter|名前|

> [!NOTE]
> CustomUpgradeAction 要素を変更する唯一の方法はカスタム [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] エディターであるため、マージしない効果は低いです。

## <a name="package-manifest-elements"></a>パッケージ マニフェスト要素
 次の表に、マージできるすべてのパッケージ マニフェスト要素と、一致に使用される一意のキーの一覧を示します。

|要素名|一意キー|
|------------------|----------------|
|Solution (すべての属性)|<*属性名*> (Solution 要素の各属性名は一意のキーです。)|
|ApplicationResourceFiles/ApplicationResourceFile|場所|
|Assemblies/Assembly|場所|
|ClassResources/ClassResource|場所|
|DwpFiles/DwpFile|場所|
|FeatureManifests/FeatureManifest|場所|
|Resources/Resource|場所|
|RootFiles/RootFile|場所|
|SiteDefinitionManifests/SiteDefinitionManifest|場所|
|WebTempFile|場所|
|TemplateFiles/TemplateFile|場所|
|SolutionDependency|SolutionID|

## <a name="manually-add-deployed-files"></a>配置されたファイルを手動で追加する
 マニフェスト要素の中には、ファイル名を含む場所を指定するものがあります (ApplicationResourceFile や DwpFiles など)。 ただし、マニフェスト テンプレートにファイル名のエントリを追加しても、基になるファイルはパッケージに追加されません。 ファイルをプロジェクトに追加してパッケージに含め、その配置の種類プロパティを適宜設定する必要があります。

## <a name="see-also"></a>関連項目
- [SharePoint ソリューションのパッケージ化と配置](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
- [SharePoint ソリューションのビルドとデバッグ](../sharepoint/building-and-debugging-sharepoint-solutions.md)
