---
title: '&lt;assembly &gt; 要素 (ClickOnce アプリケーション) |Microsoft Docs'
description: Assembly 要素はルート要素であり、ClickOnce アプリケーションで必要です。 最初に含まれる要素は、assemblyIdentity 要素である必要があります。
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
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0c3614cd2d4fc0e6a5eebfb8dc6911e6eb183c01
ms.sourcegitcommit: 0893244403aae9187c9375ecf0e5c221c32c225b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/09/2020
ms.locfileid: "94383223"
---
# <a name="ltassemblygt-element-clickonce-application"></a>&lt;assembly &gt; 要素 (ClickOnce アプリケーション)
アプリケーションマニフェストの最上位要素。

## <a name="syntax"></a>構文

```xml

      <assembly
   manifestVersion
/>
```

## <a name="elements-and-attributes"></a>要素と属性
 `assembly`要素はルート要素であり、必須です。 最初に含まれる要素は、要素である必要があり `assemblyIdentity` ます。 マニフェスト要素は、次のいずれかの名前空間にある必要があります。

 `urn:schemas-microsoft-com:asm.v1`

 `urn:schemas-microsoft-com:asm.v2`

 `http://www.w3.org/2000/09/xmldsig#`

 アセンブリの子要素は、継承またはタグ付けによって、これらの名前空間にも存在する必要があります。

 `assembly` 要素には、次の属性があります。

|属性|説明|
|---------------|-----------------|
|`manifestVersion`|必須。 `manifestVersion`属性をに設定する必要があり `1.0` ます。|

## <a name="example"></a>例
 次のコード例は、アプリケーションマニフェストの要素を示してい `assembly` [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ます。 このコード例は、 [ClickOnce アプリケーションマニフェスト](../deployment/clickonce-application-manifest.md)に用意されている大規模な例の一部です。

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
- [ClickOnce アプリケーションマニフェスト](../deployment/clickonce-application-manifest.md)
- [\<assembly> element](../deployment/assembly-element-clickonce-deployment.md)
