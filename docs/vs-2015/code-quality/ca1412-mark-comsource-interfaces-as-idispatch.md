---
title: CA1412:ComSource インターフェイスを IDispatch として |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- MarkComSourceInterfacesAsIDispatch
- CA1412
helpviewer_keywords:
- CA1412
- MarkComSourceInterfacesAsIDispatch
ms.assetid: 131a7563-0410-443c-a8f5-52104250cfb4
caps.latest.revision: 18
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 59fec1fddb16296f1238deb5c2f9bbf0c350cdd2
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "58977233"
---
# <a name="ca1412-mark-comsource-interfaces-as-idispatch"></a>CA1412:ComSource インターフェイスを IDispatch として設定します
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|MarkComSourceInterfacesAsIDispatch|
|CheckId|CA1412|
|カテゴリ|Microsoft.Interoperability|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 型が付いて、<xref:System.Runtime.InteropServices.ComSourceInterfacesAttribute>属性と少なくとも 1 つの指定したインターフェイスでマークされていない、<xref:System.Runtime.InteropServices.InterfaceTypeAttribute>属性に設定、`InterfaceIsDispatch`値。

## <a name="rule-description"></a>規則の説明
 <xref:System.Runtime.InteropServices.ComSourceInterfacesAttribute> クラスは、コンポーネント オブジェクト モデル (COM) クライアントに公開するイベント インターフェイスを識別するために使用されます。 これらのインターフェイスとして公開する必要があります`InterfaceIsIDispatch`イベント通知を受信する Visual Basic 6 COM クライアントを有効にします。 インターフェイスが設定されていない場合、既定で、<xref:System.Runtime.InteropServices.InterfaceTypeAttribute>属性、デュアル インターフェイスとして公開されます。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するのには、追加または変更、<xref:System.Runtime.InteropServices.InterfaceTypeAttribute>属性で指定されたすべてのインターフェイスの InterfaceIsIDispatch にその値が設定されるように、<xref:System.Runtime.InteropServices.ComSourceInterfacesAttribute>属性。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告は抑制しないでください。

## <a name="example"></a>例
 次の例では、規則に違反する場所、インターフェイスの 1 つのクラスを示します。

 [!code-csharp[FxCop.Interoperability.MarkIDispatch#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Interoperability.MarkIDispatch/cs/FxCop.Interoperability.MarkIDispatch.cs#1)]
 [!code-vb[FxCop.Interoperability.MarkIDispatch#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Interoperability.MarkIDispatch/vb/FxCop.Interoperability.MarkIDispatch.vb#1)]

## <a name="related-rules"></a>関連規則
 [CA 1408:AutoDual ClassInterfaceType を使用します。](../code-quality/ca1408-do-not-use-autodual-classinterfacetype.md)

## <a name="see-also"></a>関連項目
 [方法: COM シンクによって処理されるイベントを発生させる](http://msdn.microsoft.com/7c9944b2-e951-4c3e-a0a1-59b2ae37d7fd)[アンマネージ コードと相互運用](http://msdn.microsoft.com/library/ccb68ce7-b0e9-4ffb-839d-03b1cd2c1258)
