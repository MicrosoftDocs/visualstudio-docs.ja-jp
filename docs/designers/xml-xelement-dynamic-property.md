---
title: XML (XElement 動的プロパティ)
ms.date: 11/04/2016
ms.topic: reference
apiname:
- XElement.Xml
ms.assetid: 69ab2a33-4fe7-4cfa-97f8-eaf063decb18
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 7d58dea02a45ccc84e7829da2acdb479eb17dda3
ms.sourcegitcommit: 21d667104199c2493accec20c2388cf674b195c3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2019
ms.locfileid: "55931248"
---
# <a name="xml-xelement-dynamic-property"></a>Xml (XElement 動的プロパティ)

要素について、書式設定されていない XML コンテンツを取得します。

## <a name="syntax"></a>構文

```xaml
elem.Xml
```

## <a name="property-valuereturn-value"></a>プロパティ値/戻り値

要素に関する書式設定されていない XML コンテンツを表す <xref:System.String>。

## <a name="remarks"></a>コメント

このプロパティは、<xref:System.Xml.Linq.XNode.ToString(System.Xml.Linq.SaveOptions)> パラメーターが <xref:System.Xml.Linq.XNode?displayProperty=fullName> に設定されている、`SaveOptions` クラスの <xref:System.Xml.Linq.SaveOptions> メソッドに相当します。

## <a name="see-also"></a>関連項目

- [XElement クラスの動的プロパティ](../designers/xelement-class-dynamic-properties.md)
- [[値]](../designers/value-xelement-dynamic-property.md)