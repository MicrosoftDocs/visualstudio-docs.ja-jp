---
title: 'CA1409: Com 参照可能な型は作成可能でなければなりません |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- ComVisibleTypesShouldBeCreatable
- CA1409
helpviewer_keywords:
- ComVisibleTypesShouldBeCreatable
- CA1409
ms.assetid: 9f59569b-de15-4a38-b7cb-cff152972243
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: feb50f576fbff656acaa10b70bb4d8adbca1d6c3
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72602392"
---
# <a name="ca1409-com-visible-types-should-be-creatable"></a>CA1409: COM 参照可能な型は作成可能でなければなりません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|ComVisibleTypesShouldBeCreatable|
|CheckId|CA1409|
|カテゴリ|Microsoft. 相互運用性|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因
 コンポーネントオブジェクトモデル (COM) に対して表示されるように明示的にマークされている参照型は、パブリックなパラメーター化されたコンストラクターを含んでいますが、パブリックな既定 (パラメーターなし) コンストラクターを含んでいません。

## <a name="rule-description"></a>規則の説明
 パブリックな既定のコンストラクターを持たない型は、COM クライアントで作成できません。 ただし、型を作成し、それをクライアントに渡す (たとえば、メソッド呼び出しの戻り値を使用して) 場合、COM クライアントからもこの型にアクセスできます。

 このルールは、<xref:System.Delegate?displayProperty=fullName> から派生した型を無視します。

 既定では、アセンブリ、パブリック型、パブリック型のパブリックインスタンスメンバー、およびパブリック値型のすべてのメンバーに対して、COM から参照できます。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、パブリックの既定のコンストラクターを追加するか、型から <xref:System.Runtime.InteropServices.ComVisibleAttribute?displayProperty=fullName> を削除します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 オブジェクトを作成して COM クライアントに渡すために他の方法が提供されている場合は、この規則による警告を抑制しても安全です。

## <a name="related-rules"></a>関連規則
 [CA1017: アセンブリに ComVisibleAttribute を設定します](../code-quality/ca1017-mark-assemblies-with-comvisibleattribute.md)

## <a name="see-also"></a>参照
 [相互運用に対応する .Net 型を](https://msdn.microsoft.com/library/4b8afb52-fb8d-4e65-b47c-fd82956a3cdd)[アンマネージコードと相互運用](https://msdn.microsoft.com/library/ccb68ce7-b0e9-4ffb-839d-03b1cd2c1258)する
