---
title: '&lt;カスタマイズ &gt; 要素 (Visual Studio での Office 開発)'
description: Vstov4 名前空間のカスタマイズ要素に、各 Office ソリューションのインストールおよび読み込みに関するすべての情報が含まれていることを確認します。
titleSuffix: ''
ms.custom: seodec18, SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- <customizations> element
- customizations element
- application manifests [Office development in Visual Studio], <customizations> element
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 27b20a13d96b8fc23fcde2dbb8f14d1f1f27ceea
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99849932"
---
# <a name="ltcustomizationsgt-element-office-development-in-visual-studio"></a>&lt;カスタマイズ &gt; 要素 (Visual Studio での Office 開発)
  `customizations` 名前空間の `vstov4` 要素には、各 Office ソリューションのインストールおよび読み込みに関するすべての情報が含まれています。

## <a name="syntax-for-document-level-customizations"></a>ドキュメントレベルのカスタマイズの構文

```xml
<customizations>
  <customization
    id
    <document
      solutionId
    />
  </customization>
</customizations>
```

## <a name="syntax-for-vsto-add-ins"></a>VSTO アドインの構文

```xml
<customizations>
  <customization
    id
    <appAddin
      application
      loadBehavior
      keyName>
    <friendlyName></friendlyName>
    <description></description>
    <formRegions></formRegions>
  </customization>
</customizations>
```

## <a name="elements-and-attributes"></a>要素と属性
 `customizations` 要素には、各 Office ソリューションに関する特定の情報が含まれています。 この要素は、名前空間 `vstov4=urn:schemas-microsoft-com:vsto.v4`に存在する必要があります。 アセンブリの子要素もこの名前空間に属している必要があります。

 `customizations` 要素に属性はありません。

 `customizations` 要素には、次の子要素があります。

### <a name="customization"></a>カスタマイズ
 必須。 `customization`名前空間の要素 `vstov4` は[&#60;カスタマイズ&#62; 要素 &#40;Visual Studio&#41;での Office 開発](../vsto/customization-element-office-development-in-visual-studio.md)に定義されています。

## <a name="example-of-a-document-level-customization"></a>ドキュメントレベルのカスタマイズの例

### <a name="description"></a>Description
 次のコード例は、ドキュメント レベルのカスタマイズの `customizations` 要素を示しています。

> [!NOTE]
> このコード例は、 [Office ソリューションのアプリケーションマニフェスト](../vsto/application-manifests-for-office-solutions.md)に用意されている大規模な例の一部です。

### <a name="code"></a>コード

```xml
<vstov4:customizations
  xmlns:vstov4="urn:schemas-microsoft-com:vsto.v4">
  <vstov4:customization>
    <vstov4:document
      solutionId="73e" />
  </vstov4:customization>
</vstov4:customizations>
```

## <a name="example-of-a-vsto-add-in"></a>VSTO アドインの例

### <a name="description"></a>Description
 次のコード例は、 `customizations` VSTO アドインの要素を示しています。 この例は、フォーム領域が含まれた Outlook VSTO アドインです。 このコード例は、 [Office ソリューションのアプリケーションマニフェスト](../vsto/application-manifests-for-office-solutions.md)に用意されている大規模な例の一部です。

### <a name="code"></a>コード

```xml
<vstov4:customizations
  xmlns:vstov4="urn:schemas-microsoft-com:vsto.v4">
  <vstov4:customization>
    <vstov4:appAddIn
      application="Outlook"
      loadBehavior="3"
      keyName="ContosoOutlookAddIn">
      <vstov4:friendlyName>
        ContosoOutlookAddIn
      </vstov4:friendlyName>
      <vstov4:description>
        ContosoOutlookAddIn - Outlook VSTO Add-in
        created with Visual Studio Tools for Office
      </vstov4:description>
      <vstov4:formRegions>
        <vstov4:formRegion
            name="OutlookAddIn1.FormRegion1">
          <vstov4:messageClass name="IPM.Note" />
          <vstov4:messageClass name="IPM.Contact" />
          <vstov4:messageClass name="IPM.Appointment" />
        </vstov4:formRegion>
      </vstov4:formRegions>
    </vstov4:appAddIn>
  </vstov4:customization>
</vstov4:customizations>
```

## <a name="see-also"></a>関連項目

- [Office ソリューション用アプリケーションマニフェスト](../vsto/application-manifests-for-office-solutions.md)
- [Office ソリューションの配置マニフェスト](../vsto/deployment-manifests-for-office-solutions.md)
- [ClickOnce アプリケーションマニフェスト](../deployment/clickonce-application-manifest.md)