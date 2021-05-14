---
description: vstov4 名前空間の formRegion 要素は、VSTO アドインに関連付けられている Microsoft Office Outlook フォーム領域を識別します。
title: '&lt;formRegion&gt; 要素 (Visual Studio での Office 開発)'
titleSuffix: ''
ms.custom: seodec18
ms.date: 02/02/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application manifests [Office development in Visual Studio], <formRegion> element
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 0851ba9e117b464d3a2fbb9ad9903af17ceda0c4
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102221081"
---
# <a name="ltformregiongt-element-office-development-in-visual-studio"></a>&lt;formRegion&gt; 要素 (Visual Studio での Office 開発)
  `vstov4` 名前空間の `formRegion` 要素は、VSTO アドインに関連付けられている Microsoft Office Outlook フォーム領域を識別します。

## <a name="syntax"></a>構文

```xml
<formRegion
  name>
  <messageClass
    name/>
</formRegion>
```

## <a name="elements-and-attributes"></a>要素と属性
 `formRegion` 名前空間の `vstov4` 要素は、Outlook VSTO アドインに関連付けられているフォーム領域を識別します。 それは、フォーム領域のある Outlook VSTO アドインにのみ必要です。

 1 つの VSTO アドインに対して、 `formRegion` 要素内で複数の `formRegions` 要素を定義できます。

 `formRegion` 要素には、次の属性があります。

|属性|説明|
|---------------|-----------------|
|`name`|必須。 フォーム領域の名前を識別します。|

 `formRegion` 要素には、次の子要素があります。

### <a name="messageclass"></a>messageClass
 `messageClass` 要素は、フォーム領域に関連付けられる Outlook フォームを指定します。

 `messageClass` 要素には、次の属性があります。

|属性|説明|
|---------------|-----------------|
|`name`|必須。 フォーム領域に関連付けられるフォームを識別します。|

## <a name="example"></a>例
 次のコード例は、 `formRegion` を使用して配置される Outlook VSTO アド インのアプリケーション マニフェスト内の [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)]要素を示しています。 ここでは、1 つのフォーム領域に 3 つのメッセージ クラスが関連付けられています。 このコード例は、「[Office ソリューション用アプリケーション マニフェスト](../vsto/application-manifests-for-office-solutions.md)」に記載されている例から一部を抜粋したものです。

```xml
<vstov4:formRegion
    name="OutlookAddIn1.FormRegion1">
  <vstov4:messageClass name="IPM.Note" />
  <vstov4:messageClass name="IPM.Contact" />
  <vstov4:messageClass name="IPM.Appointment" />
</vstov4:formRegion>
```

## <a name="see-also"></a>関連項目

- [Outlook フォーム領域を作成する](../vsto/creating-outlook-form-regions.md)
- [Office ソリューション用アプリケーション マニフェスト](../vsto/application-manifests-for-office-solutions.md)
- [Office ソリューション用配置マニフェスト](../vsto/deployment-manifests-for-office-solutions.md)
- [ClickOnce アプリケーション マニフェスト](../deployment/clickonce-application-manifest.md)
