---
title: '&lt;assembly&gt; 要素 (ClickOnce 配置) | Microsoft Docs'
description: assembly 要素はルート要素であり、ClickOnce 配置に必要です。 最初に含まれる要素は、assemblyIdentity 要素である必要があります。
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
- <assembly> element [ClickOnce deployment manifest]
ms.assetid: b8e3362a-f821-4696-b98d-571d4bbfe431
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: b7838e0a212bbc1e743783255106bb44561fbe62
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99837763"
---
# <a name="ltassemblygt-element-clickonce-deployment"></a>&lt;assembly&gt; 要素 (ClickOnce 配置)
配置マニフェストの最上位要素。

## <a name="syntax"></a>構文

```xml

      <assembly  
   manifestVersion
/>
```

## <a name="elements-and-attributes"></a>要素と属性
 `assembly` 要素はルート要素であり、必須です。 最初に含まれる要素は、`assemblyIdentity` 要素である必要があります。 マニフェスト要素は、`urn:schemas-microsoft-com:asm.v1`、`urn:schemas-microsoft-com:asm.v2`、および `http://www.w3.org/2000/09/xmldsig#` の名前空間にある必要があります。 アセンブリの子要素も、継承またはタグ付けによって、この名前空間に属している必要があります。

 `assembly` 要素には、次の属性があります。

|属性|説明|
|---------------|-----------------|
|`manifestVersion`|必須。 この属性は `1.0` に設定する必要があります。|

## <a name="example"></a>例
 次のコード例は [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] を使用して配置されるアプリケーションの配置マニフェストの `assembly` 要素を示しています。 このコード例は、「[ClickOnce 配置マニフェスト](../deployment/clickonce-deployment-manifest.md)」トピックに記載されている、より大きな例の一部です。

```xml
<asmv1:assembly
  xsi:schemaLocation="urn:schemas-microsoft-com:asm.v1 assembly.adaptive.xsd"
  manifestVersion="1.0"
  xmlns:asmv3="urn:schemas-microsoft-com:asm.v3"
  xmlns:dsig=http://www.w3.org/2000/09/xmldsig#
  xmlns:co.v1="urn:schemas-microsoft-com:clickonce.v1"
  xmlns:co.v2="urn:schemas-microsoft-com:clickonce.v2"
  xmlns="urn:schemas-microsoft-com:asm.v2"
  xmlns:asmv1="urn:schemas-microsoft-com:asm.v1"
  xmlns:asmv2="urn:schemas-microsoft-com:asm.v2"
  xmlns:xrml="urn:mpeg:mpeg21:2003:01-REL-R-NS"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
```

## <a name="see-also"></a>関連項目
- [ClickOnce 配置マニフェスト](../deployment/clickonce-deployment-manifest.md)
- [\<assembly> 要素](../deployment/assembly-element-clickonce-application.md)