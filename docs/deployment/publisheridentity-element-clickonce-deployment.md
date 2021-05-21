---
title: '&lt;publisherIdentity&gt; 要素 (ClickOnce 配置) | Microsoft Docs'
description: publisherIdentity 要素には、配置マニフェストに署名した発行元についての情報が含まれます。 この要素は、署名されたマニフェストに必要です。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- publisherIdentity Element [ClickOnce deployment manifest], introduction
- required element for signed manifests [ClickOnce], publisherIdentity Element
- publisherIdentity Element [ClickOnce deployment manifest], syntax, elements, and attributes
ms.assetid: 34c579db-d2f2-4b66-b9c8-47207f33d950
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 65f225f8e3dd3f6d2b3afb2d2a5284d172d4fab1
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99891294"
---
# <a name="ltpublisheridentitygt-element-clickonce-deployment"></a>&lt;publisherIdentity&gt; 要素 (ClickOnce 配置)
この配置マニフェストに署名した発行元についての情報が含まれます。

## <a name="syntax"></a>構文

```xml
<publisherIdentity
   name
   issuerKeyHash
/>
```

## <a name="elements-and-attributes"></a>要素と属性
 `publisherIdentity` 要素は、署名されたマニフェストに必要です。 次の表は、`publisherIdentity` 要素によってサポートされている属性を示しています。

|属性|説明|
|---------------|-----------------|
|`name`|必須。 このアプリケーションを発行したパーティの ID について説明します。|
|`issuerKeyHash`|必須。 証明書の公開キーの SHA-1 ハッシュが含まれます。|

#### <a name="parameters"></a>パラメーター

## <a name="property-valuereturn-value"></a>プロパティ値/戻り値

## <a name="exceptions"></a>例外

## <a name="remarks"></a>解説

## <a name="requirements"></a>必要条件

## <a name="subhead"></a>小見出し