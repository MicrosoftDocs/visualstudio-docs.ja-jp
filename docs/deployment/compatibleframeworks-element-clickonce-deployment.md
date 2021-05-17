---
title: '&lt;compatibleFrameworks&gt; 要素 (ClickOnce 配置) | Microsoft Docs'
description: compatibleFrameworks 要素では、このアプリケーションをインストールして実行できる .NET Framework のバージョンを識別します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- <compatibleFrameworks> element [ClickOnce deployment manifest]
ms.assetid: f6c3ee55-9e65-403d-8664-3ebde872c7d4
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 6b0a87e36a176a01b8f243c4646e2711220f807f
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99881179"
---
# <a name="ltcompatibleframeworksgt-element-clickonce-deployment"></a>&lt;compatibleFrameworks&gt; 要素 (ClickOnce 配置)
このアプリケーションをインストールして実行できる .NET Framework のバージョンを指定します。

> [!NOTE]
> [*MageUI.exe*](/dotnet/framework/tools/mageui-exe-manifest-generation-and-editing-tool-graphical-client) では、[*MageUI.exe*](/dotnet/framework/tools/mageui-exe-manifest-generation-and-editing-tool-graphical-client) を使用して証明書で既に署名されているアプリケーション マニフェストを保存するときには、`compatibleFrameworks` 要素がサポートされません。 代わりに [*Mage.exe*](/dotnet/framework/tools/mage-exe-manifest-generation-and-editing-tool) を使用する必要があります。

## <a name="syntax"></a>構文

```xml
<compatibleFrameworks
      SupportUrl> 
   <framework
      targetVersion
      profile
      supportedRuntime
   /> 
</ compatibleFrameworks>
```

## <a name="elements-and-attributes"></a>要素と属性
 `compatibleFrameworks` 要素は、.NET Framework 4 以降で提供されている [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ランタイムをターゲットとしている配置マニフェストでは必須です。 `compatibleFrameworks` 要素には、このアプリケーションを実行できる .NET Framework バージョンを指定する `framework` 要素が 1 つ以上含まれています。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ランタイムは、この一覧で使用可能な最初の `framework` でアプリケーションを実行します。

 次の表は、`compatibleFrameworks` 要素でサポートされている属性の一覧です。

|属性|説明|
|---------------|-----------------|
|`S` `upportUrl`|省略可能。 優先される、互換性のある .NET Framework バージョンをダウンロードできる URL を指定します。|

## <a name="framework"></a>フレームワーク
 必須。 次の表に、`framework` 要素でサポートされている属性の一覧を示します。

|属性|説明|
|---------------|-----------------|
|`targetVersion`|必須。 ターゲット .NET Framework のバージョン番号を指定します。|
|`profile`|必須。 ターゲット .NET Framework のプロファイルを指定します。|
|`supportedRuntime`|必須。 ターゲット .NET Framework に関連付けられているランタイムのバージョン番号を指定します。|

## <a name="remarks"></a>解説

## <a name="example"></a>例
 次のコード例は、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 配置マニフェストの `compatibleFrameworks` 要素を示しています。 この配置は、[!INCLUDE[net_client_v40_long](../deployment/includes/net_client_v40_long_md.md)] で実行できます。 これは [!INCLUDE[net_client_v40_long](../deployment/includes/net_client_v40_long_md.md)] のスーパーセットであるため、.NET Framework 4 で実行することもできます。

```xml
<compatibleFrameworks xmlns="urn:schemas-microsoft-com:clickonce.v2">
  <framework
      targetVersion="4.0"
      profile="Client"
      supportedRuntime="4.0.30319" />
</compatibleFrameworks>
```

## <a name="see-also"></a>関連項目
- [ClickOnce 配置マニフェスト](../deployment/clickonce-deployment-manifest.md)