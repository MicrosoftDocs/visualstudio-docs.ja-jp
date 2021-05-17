---
title: '&lt;fileAssociation&gt; 要素 (ClickOnce アプリケーション) | Microsoft Docs'
description: fileAssociation 要素では、アプリケーションに関連付けられるファイル拡張子を識別します。 fileAssociation 要素は省略可能です。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- <fileAssociation> element [ClickOnce application manifest]
- manifests [ClickOnce], fileAssociation element
ms.assetid: 8f951b4f-54f9-412e-a9e5-af4e379fcf08
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 7435a4e4973ee0a000555e9508328a76f7aa59a6
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99889149"
---
# <a name="ltfileassociationgt-element-clickonce-application"></a>&lt;fileAssociation&gt; 要素 (ClickOnce アプリケーション)
アプリケーションに関連付けられるファイル拡張子を識別します。

## <a name="syntax"></a>構文

```xml
<fileAssociation
    xmlns="urn:schemas-microsoft-com:clickonce.v1"
    extension
    description
    progid
    defaultIcon
/>
```

## <a name="elements-and-attributes"></a>要素と属性
 `fileAssociation` 要素は省略可能です。 要素には、次の属性があります。

|属性|説明|
|---------------|-----------------|
|`extension`|必須。 アプリケーションに関連付けられるファイル拡張子。|
|`description`|必須。 シェルで使用されるファイルの種類の説明。|
|`progid`|必須。 ファイルの種類を一意に識別する名前。|
|`defaultIcon`|必須。 この拡張子を持つファイルで使用するアイコンを指定します。 アイコン ファイルは、この要素を含む [\<assembly> 要素](../deployment/assembly-element-clickonce-application.md)内の [\<file> 要素](../deployment/file-element-clickonce-application.md)を使用して指定する必要があります。|

## <a name="remarks"></a>解説
 この要素には、"urn:schemas-microsoft-com:clickonce.v1" への XML 名前空間参照が含まれている必要があります。 `<fileAssociation>` 要素を使用する場合は、親の [\<assembly> 要素](../deployment/assembly-element-clickonce-application.md)内の、`<application>` 要素の後に置く必要があります。

 既存のファイルの関連付けは、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] によって上書きされません。 ただし、ClickOnce アプリケーションでは、現在のユーザーに対してのみ、ファイル拡張子をオーバーライドできます。 ClickOnce アプリケーションがアンインストールされた後は、ClickOnce によってこのユーザーのファイル関連付けが削除され、マシンごとの関連付けがもう一度アクティブになります。

## <a name="example"></a>例
 次のコード例は、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] を使用して配置されるテキスト エディター アプリケーションのアプリケーション マニフェスト内にある `fileAssociation` 要素を示しています。 このコード例には、`defaultIcon` 属性では必須の [\<file> 要素](../deployment/file-element-clickonce-application.md)も含まれています。

```xml
<file name="text.ico" size="4286">
  <hash>
    <dsig:Transforms>
      <dsig:Transform Algorithm="urn:schemas-microsoft-com:HashTransforms.Identity" />
    </dsig:Transforms>
    <dsig:DigestMethod Algorithm="http://www.w3.org/2000/09/xmldsig#sha1" />
    <dsig:DigestValue>0joAqhmfeBb93ZneZv/oTMP2brY=</dsig:DigestValue>
  </hash>
</file>
<file name="writing.ico" size="9662">
  <hash>
    <dsig:Transforms>
      <dsig:Transform Algorithm="urn:schemas-microsoft-com:HashTransforms.Identity" />
    </dsig:Transforms>
    <dsig:DigestMethod Algorithm="http://www.w3.org/2000/09/xmldsig#sha1" />
    <dsig:DigestValue>2cL2U7cm13nG40v9MQdxYKazIwI=</dsig:DigestValue>
  </hash>
</file>
<fileAssociation xmlns="urn:schemas-microsoft-com:clickonce.v1" extension=".text" description="Text  Document (ClickOnce)" progid="Text.Document" defaultIcon="text.ico" />
<fileAssociation xmlns="urn:schemas-microsoft-com:clickonce.v1" extension=".writing" description="Writings (ClickOnce)" progid="Writing.Document" defaultIcon="writing.ico" />
```

## <a name="see-also"></a>関連項目
- [ClickOnce アプリケーション マニフェスト](../deployment/clickonce-application-manifest.md)