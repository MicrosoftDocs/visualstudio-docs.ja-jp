---
title: CA2132:既定のコンストラクターは、基本型の既定コンストラクターと同程度以上、重要であることが必要
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA2132
ms.assetid: e758afa1-8bde-442a-8a0a-bd1ea7b0ce4d
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6c5ca98219444515d01baf670489120238cb8dda
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/24/2019
ms.locfileid: "71232335"
---
# <a name="ca2132-default-constructors-must-be-at-least-as-critical-as-base-type-default-constructors"></a>CA2132:既定のコンストラクターは、基本型の既定コンストラクターと同程度以上、重要であることが必要

|||
|-|-|
|TypeName|DefaultConstructorsMustHaveConsistentTransparency|
|CheckId|CA2132|
|カテゴリ|Microsoft.Security|
|互換性に影響する変更点|あり|

> [!NOTE]
> この警告は、CoreCLR (Silverlight web アプリケーションに固有の CLR のバージョン) を実行しているコードにのみ適用されます。

## <a name="cause"></a>原因

派生クラスの既定のコンストラクターの透過性属性は、基本クラスの透過性と同じほど重要ではありません。

## <a name="rule-description"></a>規則の説明

を持つ<xref:System.Security.SecurityCriticalAttribute>型およびメンバーを Silverlight アプリケーションコードで使用することはできません。 セキュリティが重要な型やメンバーは、.NET Framework for Silverlight クラス ライブラリの信頼されているコードからのみ使用できます。 派生クラスにおけるパブリックな構築または保護された構築の透過性は、基底クラスと同程度以上である必要があるため、アプリケーション内のクラスを、SecurityCritical としてマークされたクラスから派生させることはできません。

CoreCLR プラットフォームコードの場合、基本型にパブリックまたは保護された非透過的な既定のコンストラクターがある場合、派生型は既定のコンストラクターの継承規則に従う必要があります。 派生型は、既定のコンストラクターを持つ必要があります。また、そのコンストラクターは、少なくとも基本型の重要な既定のコンストラクターである必要があります。

## <a name="how-to-fix-violations"></a>違反の修正方法

違反を修正するには、型を削除するか、透過的セキュリティ以外の型から派生させないようにします。

## <a name="when-to-suppress-warnings"></a>警告を非表示にする場合

この規則からの警告を抑制しないでください。 この規則をアプリケーションコードによって違反すると、CoreCLR はを使用<xref:System.TypeLoadException>して型の読み込みを拒否します。

### <a name="code"></a>コード

[!code-csharp[FxCop.Security.CA2132.DefaultConstructorsMustHaveConsistentTransparency#1](../code-quality/codesnippet/CSharp/ca2132-default-constructors-must-be-at-least-as-critical-as-base-type-default-constructors_1.cs)]