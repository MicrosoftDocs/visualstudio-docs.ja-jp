---
title: Descendants (XElement 動的プロパティ) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-designers
ms.topic: conceptual
ms.assetid: 9611d00f-23bf-444b-ab0c-f30701bfc13d
caps.latest.revision: 4
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 8c89e04346a4b08d6ee7bbc0012ef52f3b648512
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "68178204"
---
# <a name="descendants-xelement-dynamic-property"></a>Descendants (XElement 動的プロパティ)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

現在の要素の子孫要素のうち指定された拡張名に一致するすべての子孫要素を取得するためのインデクサーを取得します。  
  
## <a name="syntax"></a>構文  
  
```  
elem.Descendants[{namespaceName}localName]  
```  
  
## <a name="property-valuereturn-value"></a>プロパティ値/戻り値  
 `IEnumerable<XElement> Item(String expandedName)` 型のインデクサー。 このインデクサーは、指定された子孫要素の拡張名を受け取り、<xref:System.Collections.IEnumerable>`<`<xref:System.Xml.Linq.XElement>`>` コレクション内の一致する子要素を返します。  
  
## <a name="remarks"></a>Remarks  
 このプロパティは、<xref:System.Xml.Linq.XContainer.Descendants%28System.Xml.Linq.XName%29?displayProperty=fullName> クラスの <xref:System.Xml.Linq.XContainer> メソッドに相当します。  
  
 返されるコレクション内の要素は、XML ソース ドキュメント順になります。  
  
 このプロパティは、遅延実行を使用します。  
  
## <a name="see-also"></a>関連項目  
 [XElement クラスの動的プロパティ](../designers/xelement-class-dynamic-properties.md)   
 [要素](../designers/elements-xelement-dynamic-property.md)
