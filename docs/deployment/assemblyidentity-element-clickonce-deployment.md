---
title: '&lt;assemblyIdentity&gt; 要素 (ClickOnce 配置) | Microsoft Docs'
description: assemblyIdentity 要素は ClickOnce 配置で必須です。 子要素は含まれず、この記事で説明する属性があります。
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
- <assemblyIdentity> element [ClickOnce deployment manifest]
ms.assetid: f4a3bb83-c800-47d0-9905-9a5ae2486838
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: bc689c80d033c6b92178f020c0d3273f6ec86ca7
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99911354"
---
# <a name="ltassemblyidentitygt-element-clickonce-deployment"></a>&lt;assemblyIdentity&gt; 要素 (ClickOnce 配置)
[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションのプライマリ アセンブリを識別します。

## <a name="syntax"></a>構文

```xml

      <assemblyIdentity  
   name 
   version
   publicKeyToken
   processorArchitecture
    type
/>
```

## <a name="elements-and-attributes"></a>要素と属性
 `assemblyIdentity` 要素は必須です。 子要素は含まれず、次の属性があります。

|属性|説明|
|---------------|-----------------|
|`name`|必須。 情報提供を目的として、人が判読できる配置名を指定します。<br /><br /> `name` に一重引用符や二重引用符などの特殊文字が含まれている場合、アプリケーションのアクティブ化に失敗する可能性があります。|
|`version`|必須。 `major.minor.build.revision` の形式で、アセンブリのバージョン番号を指定します。<br /><br /> アプリケーションの更新をトリガーするために、更新されたマニフェストでこの値をインクリメントする必要があります。|
|`publicKeyToken`|必須。 配置マニフェストの署名に使用される公開キーの、SHA-1 ハッシュ値の最後の 8 バイトを表す 16 文字の 16 進数文字列を指定します。 署名に使用する公開キーは、2048 ビット以上である必要があります。<br /><br /> アセンブリへの署名は推奨されますが任意です。ただし、この属性は必須です。 アセンブリが署名されていない場合は、自己署名アセンブリから値をコピーするか、すべてゼロの "ダミー" 値を使用する必要があります。|
|`processorArchitecture`|必須。 プロセッサを指定します。 有効な値は、すべてのプロセッサでは `msil`、32 ビット Windows では `x86`、64 ビット Windows では `IA64`、Intel 64 ビット Itanium プロセッサでは `Itanium` です。|
|`type`|必須。 Windows のサイド バイ サイド インストール テクノロジとの互換性を確保するためのものです。 使用できる値は `win32` のみです。|

## <a name="remarks"></a>解説

## <a name="example"></a>例
 次のコード例は、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 配置マニフェストの `assemblyIdentity` 要素を示しています。 このコード例は、「[ClickOnce 配置マニフェスト](../deployment/clickonce-deployment-manifest.md)」に記載されている、より大きな例の一部です。

```xml
<!-- Identify the deployment. -->
<assemblyIdentity
  name="My Application Deployment.app"
  version="1.0.0.0"
  publicKeyToken="43cb1e8e7a352766"
  language="neutral"
  processorArchitecture="x86"
  xmlns="urn:schemas-microsoft-com:asm.v1" />
```

## <a name="see-also"></a>関連項目
- [ClickOnce 配置マニフェスト](../deployment/clickonce-deployment-manifest.md)
- [\<assemblyIdentity> 要素](../deployment/assemblyidentity-element-clickonce-application.md)