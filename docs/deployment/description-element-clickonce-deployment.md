---
title: '&lt;description&gt; 要素 (ClickOnce 配置) | Microsoft Docs'
description: description 要素では、シェルに表示する内容とコントロール パネルの [プログラムの追加と削除] 項目を作成するために使用されるアプリケーション情報を指定します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- urn:schemas-microsoft-com:asm.v2#description
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- <description> element [ClickOnce deployment manifest]
ms.assetid: 18f6919e-a3ab-4942-a57d-167fabfac44e
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 8dee33fca027ce47ede8315f7956479ee2394382
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99893088"
---
# <a name="ltdescriptiongt-element-clickonce-deployment"></a>&lt;description&gt; 要素 (ClickOnce 配置)
シェルに表示する内容とコントロール パネルの **[プログラムの追加と削除]** 項目を作成するために使用されるアプリケーション情報を指定します。

## <a name="syntax"></a>構文

```xml

      <description 
   publisher 
   product
   suiteName
   supportUrl
/>
```

## <a name="elements-and-attributes"></a>要素と属性
 `description` 要素は必須です。この要素は `urn:schemas-microsoft-com:asm.v1` 名前空間にあります。 子要素は含まれず、次の属性があります。

|属性|説明|
|---------------|-----------------|
|`publisher`|必須。 配置がインストール用に構成されている場合に、Windows の **[スタート]** メニューとコントロール パネルの **[プログラムの追加と削除]** 項目で、アイコンの配置に使用される会社名を指定します。|
|`product`|必須。 完全な製品名を指定します。 Windows の **[スタート]** メニューで、インストールされているアイコンのタイトルとして使用されます。|
|`suiteName`|省略可能。 Windows の **[スタート]** メニューの `publisher` フォルダー内のサブフォルダーを指定します。|
|`supportUrl`|省略可能。 コントロール パネルの **[プログラムの追加と削除]** 項目に表示されるサポート URL を指定します。 配置がインストール用に構成されている場合は、Windows の **[スタート]** メニューでのアプリケーションのサポート用に、この URL へのショートカットも作成されます。|

## <a name="remarks"></a>解説
 description 要素はすべての配置構成で必須です。

## <a name="example"></a>例
 次のコード例は、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 配置マニフェストの `description` 要素を示しています。 このコード例は、「[ClickOnce 配置マニフェスト](../deployment/clickonce-deployment-manifest.md)」に記載されている、より大きな例の一部です。

```xml
<description
  asmv2:publisher="My Company Name"
  asmv2:product="My Application"
  xmlns="urn:schemas-microsoft-com:asm.v1" />
```

## <a name="see-also"></a>関連項目
- [ClickOnce 配置マニフェスト](../deployment/clickonce-deployment-manifest.md)