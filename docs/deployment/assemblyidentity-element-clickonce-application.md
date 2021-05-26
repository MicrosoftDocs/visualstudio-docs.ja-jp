---
title: '&lt;assemblyIdentity&gt; 要素 (ClickOnce アプリケーション) | Microsoft Docs'
description: assemblyIdentity 要素は ClickOnce アプリケーションで必須です。 子要素は含まれず、この記事で説明する属性があります。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- urn:schemas-microsoft-com:asm.v2#assemblyIdentity
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- <assemblyIdentity> element [ClickOnce application manifest]
ms.assetid: f48e9531-efac-4d11-8166-f63a5ece1ac5
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 92b5c1d323634bbb242cdccb54890908d5668803
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99911371"
---
# <a name="ltassemblyidentitygt-element-clickonce-application"></a>&lt;assemblyIdentity&gt; 要素 (ClickOnce アプリケーション)
[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 配置に配置されたアプリケーションを識別します。

## <a name="syntax"></a>構文

```xml

      <assemblyIdentity
   name
   version
   publicKeyToken
   processorArchitecture
   language
/>
```

## <a name="elements-and-attributes"></a>要素と属性
 `assemblyIdentity` 要素は必須です。 子要素は含まれず、次の属性があります。

|属性|説明|
|---------------|-----------------|
|`Name`|必須。 アプリケーションの名前を指定します。<br /><br /> `Name` に一重引用符や二重引用符などの特殊文字が含まれている場合、アプリケーションのアクティブ化に失敗する可能性があります。|
|`Version`|必須。 `major.minor.build.revision` の形式で、アプリケーションのバージョン番号を指定します。|
|`publicKeyToken`|省略可能。 アプリケーションまたはアセンブリの署名に使用される公開キーの、`SHA-1` ハッシュ値の最後の 8 バイトを表す 16 文字の 16 進数文字列を指定します。 カタログの署名に使用する公開キーは、2048 ビット以上である必要があります。<br /><br /> アセンブリへの署名は推奨されますが任意です。ただし、この属性は必須です。 アセンブリが署名されていない場合は、自己署名アセンブリから値をコピーするか、すべてゼロの "ダミー" 値を使用する必要があります。|
|`processorArchitecture`|必須。 プロセッサを指定します。 有効な値は、すべてのプロセッサでは `msil`、32 ビット Windows では `x86`、64 ビット Windows では `IA64`、Intel 64 ビット Itanium プロセッサでは `Itanium` です。|
|`language`|必須。 アセンブリの、2 つの部分から成る言語コード (例: `en-US`) を指定します。 この要素は `asmv2` 名前空間内にあります。 指定しない場合、既定値は `neutral` です。|

## <a name="examples"></a>例

### <a name="description"></a>説明
 次のコード例は、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーション マニフェストの `assemblyIdentity` 要素を示しています。 このコード例は、「[ClickOnce アプリケーション マニフェスト](../deployment/clickonce-application-manifest.md)」に記載されている、より大きな例の一部です。

### <a name="code"></a>コード

```xml
<asmv1:assemblyIdentity
  name="My Application Deployment.exe"
  version="1.0.0.0"
  publicKeyToken="43cb1e8e7a352766"
  language="neutral"
  processorArchitecture="x86"
  type="win32" />
```

## <a name="see-also"></a>関連項目
- [ClickOnce アプリケーション マニフェスト](../deployment/clickonce-application-manifest.md)
- [\<assemblyIdentity> 要素](../deployment/assemblyidentity-element-clickonce-deployment.md)