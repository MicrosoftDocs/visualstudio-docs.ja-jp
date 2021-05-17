---
title: '&lt;assembly&gt; 要素 (ClickOnce アプリケーション) | Microsoft Docs'
description: assembly 要素はルート要素であり、ClickOnce アプリケーションに必要です。 最初に含まれる要素は、assemblyIdentity 要素である必要があります。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- urn:schemas-microsoft-com:asm.v2#assembly
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- <assembly> element [ClickOnce application manifest]
ms.assetid: 51410569-10f9-4c0a-96b5-d39185edbefc
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: f86ed604ae6b893f02da1d4f65a816bd05f34f94
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99837789"
---
# <a name="ltassemblygt-element-clickonce-application"></a>&lt;assembly&gt; 要素 (ClickOnce アプリケーション)
アプリケーション マニフェストの最上位要素。

## <a name="syntax"></a>構文

```xml

      <assembly
   manifestVersion
/>
```

## <a name="elements-and-attributes"></a>要素と属性
 `assembly` 要素はルート要素であり、必須です。 最初に含まれる要素は、`assemblyIdentity` 要素である必要があります。 マニフェスト要素は、次の名前空間のいずれかにある必要があります。

 `urn:schemas-microsoft-com:asm.v1`

 `urn:schemas-microsoft-com:asm.v2`

 `http://www.w3.org/2000/09/xmldsig#`

 アセンブリの子要素も、継承またはタグ付けによって、この名前空間に属している必要があります。

 `assembly` 要素には、次の属性があります。

|属性|説明|
|---------------|-----------------|
|`manifestVersion`|必須。 `manifestVersion` 属性は `1.0` に設定する必要があります。|

## <a name="example"></a>例
 次のコード例は、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションのためのアプリケーション マニフェストの `assembly` 要素を示しています。 このコード例は、「[ClickOnce アプリケーション マニフェスト](../deployment/clickonce-application-manifest.md)」に記載されている、より大きな例の一部です。

```xml
<asmv1:assembly
  xsi:schemaLocation="urn:schemas-microsoft-com:asm.v1 assembly.adaptive.xsd"
  manifestVersion="1.0"
  xmlns:asmv3="urn:schemas-microsoft-com:asm.v3"
  xmlns:dsig=http://www.w3.org/2000/09/xmldsig#
  xmlns:co.v2="urn:schemas-microsoft-com:clickonce.v2"
  xmlns="urn:schemas-microsoft-com:asm.v2"
  xmlns:asmv1="urn:schemas-microsoft-com:asm.v1"
  xmlns:asmv2="urn:schemas-microsoft-com:asm.v2"
  xmlns:xsi=http://www.w3.org/2001/XMLSchema-instance
  xmlns:co.v1="urn:schemas-microsoft-com:clickonce.v1">
```

## <a name="see-also"></a>関連項目
- [ClickOnce アプリケーション マニフェスト](../deployment/clickonce-application-manifest.md)
- [\<assembly> 要素](../deployment/assembly-element-clickonce-deployment.md)
