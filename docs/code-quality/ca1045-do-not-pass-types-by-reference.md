---
title: CA1045:型を参照によって渡しません
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA1045
- DoNotPassTypesByReference
helpviewer_keywords:
- CA1045
- DoNotPassTypesByReference
ms.assetid: bcc3900a-e092-4bb8-896f-cb83f6289968
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c6a8fda526647a1a9f7f999928cb08978a61bd04
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/24/2019
ms.locfileid: "71235776"
---
# <a name="ca1045-do-not-pass-types-by-reference"></a>CA1045:型を参照によって渡しません

|||
|-|-|
|TypeName|DoNotPassTypesByReference|
|CheckId|CA1045|
|カテゴリ|Microsoft.Design|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
パブリック型のパブリックメソッドまたはプロテクトメソッドには`ref` 、プリミティブ型、参照型、または組み込み型の1つではない値型を受け取るパラメーターがあります。

## <a name="rule-description"></a>規則の説明
型を参照渡しで渡す`out` ( `ref`またはを使用) には、ポインターの使用経験、値型と参照型の違いの理解、および複数の戻り値を持つメソッドの処理が必要です。 また、パラメーターと`out` `ref`パラメーターの違いは広く認識されていません。

参照型が "参照渡し" されると、メソッドは、パラメーターを使用してオブジェクトの別のインスタンスを返すようにします。 参照型を参照渡しで渡すことは、double ポインター、ポインターへのポインター、または二重の間接参照とも呼ばれます。既定の呼び出し規約 ("値渡し") を使用すると、参照型を受け取るパラメーターは既にオブジェクトへのポインターを受け取ります。 ポインターが指すオブジェクトではなく、値によって渡されます。 値渡しでは、メソッドが参照型の新しいインスタンスを指すようにポインターを変更することはできませんが、ポイントするオブジェクトの内容を変更することができます。 ほとんどのアプリケーションでは十分であり、必要な動作が得られます。

メソッドが別のインスタンスを返す必要がある場合は、メソッドの戻り値を使用してこれを実行します。 文字列を操作し、文字列の新しいインスタンスを返すさまざまなメソッドについては、クラスを参照してください。<xref:System.String?displayProperty=fullName> このモデルを使用すると、元のオブジェクトが保持されているかどうかを判断するために呼び出し元に残されます。

戻り値は一般的であり、頻繁に使用されます`out`が`ref` 、パラメーターとパラメーターを正しく適用するには、中間の設計とコーディングのスキルが必要です。 一般ユーザー向けに設計されたライブラリアーキテクトは、ユーザーがまたは`out` `ref`パラメーターをマスターに使用することを想定しないでください。

> [!NOTE]
> 大規模な構造のパラメーターを使用する場合、これらの構造をコピーするために必要な追加リソースによって、値渡しによってパフォーマンスが低下する可能性があります。 このような場合は、または`ref` `out`パラメーターを使用することを検討してください。

## <a name="how-to-fix-violations"></a>違反の修正方法
値の型に起因するこの規則違反を修正するには、メソッドが戻り値としてオブジェクトを返すようにします。 メソッドが複数の値を返す必要がある場合は、値を保持するオブジェクトの1つのインスタンスを返すように再設計します。

参照型に起因するこの規則違反を修正するには、必要な動作が参照の新しいインスタンスを返すことを確認します。 この値がの場合、メソッドは戻り値を使用してこれを実行する必要があります。

## <a name="when-to-suppress-warnings"></a>警告を非表示にする場合
このルールからの警告を抑制するのは安全です。ただし、この設計ではユーザビリティの問題が発生する可能性があります。

## <a name="example"></a>例
次のライブラリは、ユーザーのフィードバックへの応答を生成するクラスの2つの実装を示しています。 最初の実装 (`BadRefAndOut`) では、ライブラリユーザーが3つの戻り値を管理するように強制します。 2番目の`RedesignedRefAndOut`実装 () は、データを1つの単位として`ReplyData`管理するコンテナークラス () のインスタンスを返すことによって、ユーザーエクスペリエンスを簡略化します。

[!code-csharp[FxCop.Design.NoRefOrOut#1](../code-quality/codesnippet/CSharp/ca1045-do-not-pass-types-by-reference_1.cs)]

## <a name="example"></a>例
次のアプリケーションは、ユーザーのエクスペリエンスを示しています。 再設計されたライブラリ (`UseTheSimplifiedClass`メソッド) の呼び出しはより簡単で、メソッドによって返される情報は簡単に管理できます。 2つのメソッドからの出力は同じです。

[!code-csharp[FxCop.Design.TestNoRefOrOut#1](../code-quality/codesnippet/CSharp/ca1045-do-not-pass-types-by-reference_2.cs)]

## <a name="example"></a>例
次のライブラリ例は、 `ref`参照型のパラメーターの使用方法を示しています。また、この機能を実装するためのより良い方法を示しています。

[!code-csharp[FxCop.Design.RefByRefNo#1](../code-quality/codesnippet/CSharp/ca1045-do-not-pass-types-by-reference_3.cs)]

## <a name="example"></a>例
次のアプリケーションは、ライブラリ内の各メソッドを呼び出して、動作を示します。

[!code-csharp[FxCop.Design.TestRefByRefNo#1](../code-quality/codesnippet/CSharp/ca1045-do-not-pass-types-by-reference_4.cs)]

この例を実行すると、次の出力が生成されます。

```txt
Changing pointer - passed by value:
12345
12345
Changing pointer - passed by reference:
12345
12345 ABCDE
Passing by return value:
12345 ABCDE
```

## <a name="related-rules"></a>関連するルール
[CA1021Out パラメーターを回避する](../code-quality/ca1021-avoid-out-parameters.md)