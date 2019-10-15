---
title: CA2207:値型のスタティック フィールドのインラインを初期化します
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- InitializeValueTypeStaticFieldsInline
- CA2207
helpviewer_keywords:
- CA2207
- InitializeValueTypeStaticFieldsInline
ms.assetid: d1ea9d8b-ecc2-46ca-86e2-c41dd0e76658
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 695f15c73120f766157fabb09193d32115dda588
ms.sourcegitcommit: 034c503ae04e22cf840ccb9770bffd012e40fb2d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2019
ms.locfileid: "72305932"
---
# <a name="ca2207-initialize-value-type-static-fields-inline"></a>CA2207:値型のスタティック フィールドのインラインを初期化します

|||
|-|-|
|TypeName|InitializeValueTypeStaticFieldsInline|
|CheckId|CA2207|
|カテゴリ|Microsoft.Usage|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因
値型は、明示的な静的コンストラクターを宣言します。

## <a name="rule-description"></a>規則の説明
値型が宣言されている場合、すべての値型フィールドがゼロに設定され、すべての参照型フィールドが `null` (Visual Basic の `Nothing`) に設定されている場合、既定の初期化が行われます。 明示的な静的コンストラクターは、その型のインスタンスコンストラクターまたは静的メンバーが呼び出される前にのみ実行されることが保証されます。 したがって、インスタンスコンストラクターを呼び出さずに型が作成された場合、静的コンストラクターの実行は保証されません。

すべての静的データがインラインで初期化され、明示的な静的コンストラクター C#が宣言されていない場合、および Visual Basic コンパイラは、MSIL クラス定義に `beforefieldinit` フラグを追加します。 コンパイラは、静的初期化コードを含むプライベートな静的コンストラクターも追加します。 このプライベート静的コンストラクターは、型の静的フィールドにアクセスする前に実行することが保証されています。

## <a name="how-to-fix-violations"></a>違反の修正方法
この規則違反を修正するには、宣言時にすべての静的データを初期化し、静的コンストラクターを削除します。

## <a name="when-to-suppress-warnings"></a>警告を非表示にする場合
この規則による警告は抑制しないでください。

## <a name="related-rules"></a>関連するルール
[CA1810:参照型の静的フィールドを初期化します。インライン @ no__t-0