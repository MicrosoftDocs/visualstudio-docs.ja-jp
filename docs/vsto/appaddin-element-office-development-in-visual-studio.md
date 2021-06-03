---
title: '&lt;appAddin&gt; 要素 (Visual Studio での Office 開発)'
description: vstov4 名前空間の appAddin 要素に、VSTO アドイン用のカスタマイズ固有の情報がどのように格納されるかについて説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application manifests [Office development in Visual Studio], <appAddin> element
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 427d7bc0ec59b98394b292745985be7fdf69b904
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99950511"
---
# <a name="ltappaddingt-element-office-development-in-visual-studio"></a>&lt;appAddin&gt; 要素 (Visual Studio での Office 開発)
  `vstov4` 名前空間の **appAddin** 要素には、VSTO アドイン用のカスタマイズ固有の情報が格納されます。

## <a name="syntax"></a>構文

```xml
<appAddin
  application
  loadBehavior
  keyName>
  <friendlyName>
  <description>
  <formRegions></formRegions>
</appAddin>
```

## <a name="elements-and-attributes"></a>要素と属性
 **appAddin** 要素は必須で、`vstov4` 名前空間に属します。 アプリケーション マニフェストで定義される **appAddin** 要素が 1 つだけあります。

 **appAddin** 要素には、次の属性があります。

|属性|説明|
|---------------|-----------------|
|**application**|必須。 Microsoft Office アプリケーションを指定します。 この値は、Excel、InfoPath、Outlook、PowerPoint、Project、Visio、Word のいずれか 1 つになります。|
|**loadBehavior**|省略可能。 既定では、この値が 3 に設定され、**loadBehavior** が有効になっています。 デバッグする場合は、この値を 2 に設定して VSTO アドインを無効にできます。 詳細については、「[VSTO アドインのレジストリ エントリ](../vsto/registry-entries-for-vsto-add-ins.md)」の「LoadBehavior の値」の表を参照してください。|
|**keyName**|必須。 この値は、アプリケーションが VSTO アドインを読み込むのに使用するレジストリ キーの名前です。 詳細については、「[VSTO アドインのレジストリ エントリ](../vsto/registry-entries-for-vsto-add-ins.md)」を参照してください。|

 **appAddin** 要素には、次の子要素があります。

### <a name="friendlyname"></a>friendlyName
 省略可能。 **friendlyName** 要素は、「[&#60;friendlyName&#62; 要素 &#40;Visual Studio での Office 開発&#41;](../vsto/friendlyname-element-office-development-in-visual-studio.md)」で説明されています。

### <a name="description"></a>description
 省略可能。 **description** 要素は、「[&#60;description&#62; 要素 &#40;Visual Studio での Office 開発&#41;](../vsto/description-element-office-development-in-visual-studio.md)」で説明されています。

### <a name="formregions"></a>formRegions
 フォーム領域を含んでいる Outlook VSTO アドインでのみ必須です。 **formRegions** 要素は、「[&#60;formRegions&#62; 要素 &#40;Visual Studio での Office 開発&#41;](../vsto/formregions-element-office-development-in-visual-studio.md)」で説明されています。

## <a name="vsto-add-in-example"></a>VSTO アドインの例

### <a name="description"></a>説明
 次のコード例は、[!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] を使用して配置される Outlook ソリューションの **appAddin** 要素を示しています。 このコード例は、「[Office ソリューション用アプリケーション マニフェスト](../vsto/application-manifests-for-office-solutions.md)」に記載されている例から一部を抜粋したものです。

### <a name="code"></a>コード

```xml
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
```

## <a name="see-also"></a>関連項目

- [Office ソリューション用アプリケーション マニフェスト](../vsto/application-manifests-for-office-solutions.md)
- [Office ソリューション用配置マニフェスト](../vsto/deployment-manifests-for-office-solutions.md)
- [ClickOnce アプリケーション マニフェスト](../deployment/clickonce-application-manifest.md)