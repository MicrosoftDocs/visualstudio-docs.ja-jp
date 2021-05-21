---
description: vstov4 名前空間の formRegions 要素には、VSTO アドインに関連付けられている Microsoft Office Outlook フォーム領域が格納されます。
title: '&lt;formRegions&gt; 要素 (Visual Studio での Office 開発)'
titleSuffix: ''
ms.custom: seodec18
ms.date: 02/02/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- formRegions element
- <formRegions> element
- application manifests [Office development in Visual Studio], <formRegions> element
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 7c8fd7e0ced0fadcd945388a9730513b2a591ed0
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102223460"
---
# <a name="ltformregionsgt-element-office-development-in-visual-studio"></a>&lt;formRegions&gt; 要素 (Visual Studio での Office 開発)
  `vstov4` 名前空間の `formRegions` 要素には、VSTO アドインに関連付けられている Microsoft Office Outlook フォーム領域が格納されます。

## <a name="syntax"></a>構文

```xml
<formRegions>
  <formRegion>
  </formRegion>
</formRegions>
```

## <a name="elements-and-attributes"></a>要素と属性
 `formRegions` 名前空間の `vstov4` 要素には、Outlook VSTO アドインの `formRegion` 要素がすべて含まれています。 それは、フォーム領域のある Outlook VSTO アドインにのみ必要です。

 アプリケーション マニフェストで定義できる `formRegions` 要素は 1 つだけです。

 `formRegions` 要素に属性はありません。

 `formRegions` 要素には次の要素があります。

### <a name="formregion"></a>formRegion
 フォーム領域のある Outlook VSTO アドインに必要です。 `formRegion` 要素は、「[&#60;formRegion&#62; 要素 &#40;Visual Studio での Office 開発&#41;](../vsto/formregion-element-office-development-in-visual-studio.md)」で定義されています。

## <a name="vsto-add-in-example"></a>VSTO アドインの例

### <a name="description"></a>説明
 次のコード例は、 `formRegions` を使用して展開したアプリケーション レベルの Office ソリューションに対するアプリケーション マニフェストの [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)]要素を示しています。 このコード例は、「[Office ソリューション用アプリケーション マニフェスト](../vsto/application-manifests-for-office-solutions.md)」で提供されている大きな例の一部です。

### <a name="code"></a>コード

```xml
<vstov4:formRegions>
  <vstov4:formRegion
      name="OutlookAddIn1.FormRegion1">
    <vstov4:messageClass name="IPM.Note" />
    <vstov4:messageClass name="IPM.Contact" />
    <vstov4:messageClass name="IPM.Appointment" />
  </vstov4:formRegion>
</vstov4:formRegions>
```

## <a name="see-also"></a>関連項目

- [Office ソリューション用アプリケーション マニフェスト](../vsto/application-manifests-for-office-solutions.md)
- [Office ソリューション用配置マニフェスト](../vsto/deployment-manifests-for-office-solutions.md)
- [ClickOnce アプリケーション マニフェスト](../deployment/clickonce-application-manifest.md)
