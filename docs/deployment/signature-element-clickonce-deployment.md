---
title: '&lt;Signature&gt; 要素 (ClickOnce 配置) | Microsoft Docs'
description: Signature 要素には、この配置マニフェストにデジタル署名するために必要な情報が含まれています。 配置マニフェストへの署名は、省略可能ですが推奨されています。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- <Signature> element [ClickOnce deployment manifest]
ms.assetid: c99b07ad-e8ba-43f2-b0d6-3745e7a7c8b3
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 5d95398285d9106719f3c2444d54202b81cfee4a
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99877500"
---
# <a name="ltsignaturegt-element-clickonce-deployment"></a>&lt;Signature&gt; 要素 (ClickOnce 配置)
この配置マニフェストにデジタル署名するために必要な情報が含まれます。

## <a name="syntax"></a>構文

```xml

<Signature> 
   XML signature information 
</Signature>
```

## <a name="remarks"></a>解説
 エンベロープ署名を使用した配置マニフェストへの署名は、省略可能ですが推奨されています。 XML ファイルへの署名の詳細については、[http://www.w3.org/TR/xmldsig-core/](https://www.w3.org/TR/xmldsig-core/) で説明されている、World Wide Web コンソーシアムの推奨事項「XML 署名の構文と処理」を参照してください。

 マニフェストに署名する場合は、すべてのファイルにハッシュを提供する必要があります。 ユーザーはハッシュされていないファイルの内容を検証できないため、ハッシュされていないファイルが含まれるマニフェストには署名できません。

## <a name="example"></a>例
 次のコード例は、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 配置で使用される配置マニフェストの `Signature` 要素を示しています。

```xml
<Signature xmlns="http://www.w3.org/2000/09/xmldsig#">
  <SignedInfo>
    <CanonicalizationMethod Algorithm=
           "http://www.w3.org/TR/2001/REC-xml-c14n-20010315" />
    <SignatureMethod Algorithm=
           "http://www.w3.org/2000/09/xmldsig#rsa-sha1" />
    <Reference URI="">
      <Transforms>
        <Transform Algorithm=
           "http://www.w3.org/2000/09/xmldsig#enveloped-signature" />
      </Transforms>
      <DigestMethod Algorithm="http://www.w3.org/2000/09/xmldsig#sha1" />
      <DigestValue>d2z5AE...</DigestValue>
    </Reference>
  </SignedInfo>
  <SignatureValue>
4PHj6SaopoLp...
  </SignatureValue>
  <KeyInfo>
    <X509Data>
      <X509Certificate>
MIIHnTCCBoWgAwIBAgIKJY9+nwAHAAB...
      </X509Certificate>
    </X509Data>
  </KeyInfo>
</Signature>
```

## <a name="see-also"></a>関連項目
- [ClickOnce 配置マニフェスト](../deployment/clickonce-deployment-manifest.md)
