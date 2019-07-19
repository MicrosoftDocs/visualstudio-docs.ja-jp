---
title: Attribute (XElement 動的プロパティ) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-designers
ms.topic: conceptual
ms.assetid: 8440fc7d-b3b4-4726-8ec8-492e6af79642
caps.latest.revision: 4
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: ced05b8da63f9a7a242b166fe64e9e44f78b8065
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "68162672"
---
# <a name="attribute-xelement-dynamic-property"></a>Attribute (XElement 動的プロパティ)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

指定された展開名に対応する属性のインスタンスの取得に使用するインデクサーを取得します。  
  
## <a name="syntax"></a>構文  
  
```  
elem.Attribute[{namespaceName}attribName]  
```  
  
## <a name="property-valuereturn-value"></a>プロパティ値/戻り値  
 `XAttribute Item(String expandedName)` 型のインデクサー。 このインデクサーは、指定された属性の展開名を受け取り、対応する <xref:System.Xml.Linq.XAttribute> を返します。指定された名前を持つ属性がない場合は、`null` を返します。  
  
## <a name="remarks"></a>Remarks  
 このプロパティは、<xref:System.Xml.Linq.XElement.Attribute%2A> クラスの <xref:System.Xml.Linq.XElement?displayProperty=fullName> メソッドに相当します。  
  
## <a name="see-also"></a>関連項目  
 <xref:System.Xml.Linq.XElement.Attribute%2A?displayProperty=fullName>   
 [XElement クラスの動的プロパティ](../designers/xelement-class-dynamic-properties.md)   
 [[値]](../designers/value-xattribute-dynamic-property.md)
