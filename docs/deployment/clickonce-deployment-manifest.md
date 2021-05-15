---
title: ClickOnce 配置マニフェスト | Microsoft Docs
description: 配置する ClickOnce アプリケーションの現在のバージョンなど、ClickOnce の配置に関する情報を記述した XML ファイルである配置マニフェストについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce, deployment manifests
- deployment manifests [ClickOnce]
ms.assetid: 8457e615-e3b6-4990-8dcf-11bc590e4e9b
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: c3e8737a29fed109e82240a74569011be60a586c
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99840861"
---
# <a name="clickonce-deployment-manifest"></a>ClickOnce 配置マニフェスト
配置マニフェストは、配置する [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションの現在のバージョンの識別など、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] の配置に関する情報を記述した XML ファイルです。

 配置マニフェストには、次の要素および属性があります。

| 要素 | 説明 | 属性 |
| - | - | - |
| [\<assembly> 要素](../deployment/assembly-element-clickonce-deployment.md) | 必須。 最上位の要素です。 | `manifestVersion` |
| [\<assemblyIdentity> 要素](../deployment/assemblyidentity-element-clickonce-deployment.md) | 必須。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションのアプリケーション マニフェストを指定します。 | `name`<br /><br /> `version`<br /><br /> `publicKeyToken`<br /><br /> `processorArchitecture`<br /><br /> `culture` |
| [\<description> 要素](../deployment/description-element-clickonce-deployment.md) | 必須。 シェルに表示する内容、およびコントロール パネルの **[プログラムの追加と削除]** 項目を作成するために使用される、アプリケーション情報を指定します。 | `publisher`<br /><br /> `product`<br /><br /> `supportUrl` |
| [\<deployment> 要素](../deployment/deployment-element-clickonce-deployment.md) | 省略可能。 更新プログラムの配置とシステムへの公開に使用される属性を指定します。 | `install`<br /><br /> `minimumRequiredVersion`<br /><br /> `mapFileExtensions`<br /><br /> `disallowUrlActivation`<br /><br /> `trustUrlParameters` |
| [\<compatibleFrameworks> 要素](../deployment/compatibleframeworks-element-clickonce-deployment.md) | 必須。 このアプリケーションをインストールして実行できる .NET Framework のバージョンを指定します。 | `SupportUrl` |
| [\<dependency> 要素](../deployment/dependency-element-clickonce-deployment.md) | 必須。 配置でインストールするアプリケーションのバージョンおよびアプリケーション マニフェストの場所を指定します。 | `preRequisite`<br /><br /> `visible`<br /><br /> `dependencyType`<br /><br /> `codebase`<br /><br /> `size` |
| [\<publisherIdentity> 要素](../deployment/publisheridentity-element-clickonce-deployment.md) | 署名されたマニフェストに対しては必ず指定します。 この配置マニフェストに署名した発行元についての情報が含まれます。 | `Name`<br /><br /> `issuerKeyHash` |
| [\<Signature> 要素](../deployment/signature-element-clickonce-deployment.md) | 省略可能。 この配置マニフェストにデジタル署名するために必要な情報が含まれます。 | なし |
| [\<customErrorReporting> 要素](../deployment/customerrorreporting-element-clickonce-deployment.md) | 省略可能。 エラー発生時に表示する URI を指定します。 | Uri |

## <a name="remarks"></a>解説
 配置マニフェスト ファイルには、現在のバージョンや配置に関するその他の設定など、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションの配置に関する情報を指定します。 配置マニフェストでは、アプリケーション マニフェストを参照します。アプリケーション マニフェストには、アプリケーションの現在のバージョンおよび配置に含められるすべてのファイルが記述されています。

 詳細については、「 [ClickOnce Security and Deployment](../deployment/clickonce-security-and-deployment.md)」を参照してください。

## <a name="file-location"></a>ファイルの場所
 配置マニフェスト ファイルでは、アプリケーションの現在のバージョンに対応する適切なアプリケーション マニフェストを参照します。 新しいバージョンのアプリケーション配置を使用可能にした場合は、新しいアプリケーション マニフェストを参照するように配置マニフェストを更新する必要があります。

 配置マニフェスト ファイルには、厳密な名前を付ける必要があります。また、発行元を検証するための証明書を含めることもできます。

## <a name="file-name-syntax"></a>ファイル名の構文
 配置マニフェスト ファイルの名前は *.application* という拡張子で終わる必要があります。

## <a name="examples"></a>例
 次のコード例は、配置マニフェストを示しています。

```xml
<?xml version="1.0" encoding="utf-8"?>
<asmv1:assembly xsi:schemaLocation="urn:schemas-microsoft-com:asm.v1 assembly.adaptive.xsd"
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
  <assemblyIdentity
    name="My Application Deployment.app"
    version="1.0.0.0"
    publicKeyToken="43cb1e8e7a352766"
    language="neutral"
    processorArchitecture="x86"
    xmlns="urn:schemas-microsoft-com:asm.v1" />
  <description
    asmv2:publisher="My Company Name"
    asmv2:product="My Application"
    xmlns="urn:schemas-microsoft-com:asm.v1" />
  <deployment install="true">
    <subscription>
      <update>
        <expiration maximumAge="0" unit="days" />
      </update>
    </subscription>
    <deploymentProvider codebase="\\myServer\sampleDeployment\MyApplicationDeployment.application" />
  </deployment>
  <compatibleFrameworks xmlns="urn:schemas-microsoft-com:clickonce.v2">
    <framework targetVersion="4.0" profile="Full" supportedRuntime="4.0.20506" />
    <framework targetVersion="4.0" profile="Client" supportedRuntime="4.0.20506" />
  </compatibleFrameworks>
  <dependency>
    <dependentAssembly
      dependencyType="install"
      codebase="1.0.0.0\My Application Deployment.exe.manifest"
      size="6756">
      <assemblyIdentity
        name="My Application Deployment.exe"
        version="1.0.0.0"
        publicKeyToken="43cb1e8e7a352766"
        language="neutral"
        processorArchitecture="x86"
        type="win32" />
      <hash>
        <dsig:Transforms>
          <dsig:Transform Algorithm="urn:schemas-microsoft-com:HashTransforms.Identity" />
        </dsig:Transforms>
        <dsig:DigestMethod Algorithm="http://www.w3.org/2000/09/xmldsig#sha1" />
        <dsig:DigestValue>E506x9FwNauks7UjQywmzgtd3FE=</dsig:DigestValue>
      </hash>
    </dependentAssembly>
  </dependency>
<publisherIdentity name="CN=DOMAIN\MyUsername" issuerKeyHash="18312a18a21b215ecf4cdb20f5a0e0b0dd263c08" /><Signature Id="StrongNameSignature" xmlns="http://www.w3.org/2000/09/xmldsig#">
...
</Signature></asmv1:assembly>
```

## <a name="see-also"></a>関連項目
- [ClickOnce アプリケーションの発行](../deployment/publishing-clickonce-applications.md)