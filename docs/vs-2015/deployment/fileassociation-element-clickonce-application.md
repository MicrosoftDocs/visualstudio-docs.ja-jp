---
title: '&lt;fileAssociation&gt;要素 (ClickOnce アプリケーション) |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- <fileAssociation> element [ClickOnce application manifest]
- manifests [ClickOnce], fileAssociation element
ms.assetid: 8f951b4f-54f9-412e-a9e5-af4e379fcf08
caps.latest.revision: 10
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 4b31ac34627b244cb61b6fdb5c6ca214675ec045
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "58974160"
---
# <a name="ltfileassociationgt-element-clickonce-application"></a>&lt;fileAssociation&gt;要素 (ClickOnce アプリケーション)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

アプリケーションに関連するファイル拡張子を識別します。  
  
## <a name="syntax"></a>構文  
  
```  
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
|`extension`|必須。 アプリケーションに関連するファイル拡張子。|  
|`description`|必須。 シェルによって使用されるファイルの種類の説明。|  
|`progid`|必須。 ファイルの種類を一意に識別する名前。|  
|`defaultIcon`|必須。 この拡張機能でファイルを使用するアイコンを指定します。 使用してアイコン ファイルを指定する必要があります、 [\<ファイル > 要素](../deployment/file-element-clickonce-application.md)内、 [\<アセンブリ > 要素](../deployment/assembly-element-clickonce-application.md)この要素を格納しています。|  
  
## <a name="remarks"></a>Remarks  
 この要素への XML 名前空間参照を含める必要があります"urn: スキーマ-microsoft-com:clickonce.v1"。 場合、`<fileAssociation>`要素を使用して、後に、必要があります、`<application>`では親要素[\<アセンブリ > 要素](../deployment/assembly-element-clickonce-application.md)します。  
  
 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 既存のファイルの関連付けは上書きされません。 ただし、ClickOnce アプリケーションでは、現在のユーザーのみのファイル拡張子を上書きできます。 ClickOnce アプリケーションをアンインストールすると後、ClickOnce は、ユーザーのファイルの関連付けを削除し、コンピューターごとの関連付けがもう一度アクティブです。  
  
## <a name="example"></a>例  
 次のコード例を示しています`fileAssociation`テキスト エディター アプリケーションを使用してデプロイ用のマニフェストをアプリケーション内の要素[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]します。 このコード例も含まれています、 [\<ファイル > 要素](../deployment/file-element-clickonce-application.md)によって必要な`defaultIcon`属性。  
  
```  
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
 [ClickOnce Application Manifest](../deployment/clickonce-application-manifest.md)
