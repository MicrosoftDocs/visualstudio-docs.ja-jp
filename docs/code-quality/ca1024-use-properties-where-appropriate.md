---
title: CA1024:適切な場所にプロパティを使用します
ms.date: 03/11/2019
ms.topic: reference
f1_keywords:
- UsePropertiesWhereAppropriate
- CA1024
helpviewer_keywords:
- CA1024
- UsePropertiesWhereAppropriate
ms.assetid: 3a04f765-af7c-4872-87ad-9cc29e8e657f
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: d312618c80abb6a4ce6e1a2676903d85867f4989
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/24/2019
ms.locfileid: "71236157"
---
# <a name="ca1024-use-properties-where-appropriate"></a>CA1024:適切な場所にプロパティを使用します

|||
|-|-|
|TypeName|UsePropertiesWhereAppropriate|
|CheckId|CA1024|
|カテゴリ|Microsoft.Design|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因

メソッドの名前はで`Get`始まり、パラメーターを取らず、配列ではない値を返します。

既定では、この規則はパブリックメソッドと保護されたメソッドのみを参照しますが、これは[構成可能](#configurability)です。

## <a name="rule-description"></a>規則の説明

ほとんどの場合、プロパティはデータを表し、メソッドはアクションを実行します。 プロパティはフィールドのようにアクセスされるため、簡単に使用できます。 次の条件のいずれかが存在する場合、メソッドは、プロパティになることをお勧めします。

- 引数を取らず、オブジェクトの状態情報を返します。

- 1つの引数を受け取り、オブジェクトの状態の一部を設定します。

プロパティは、フィールドであるかのように動作します。メソッドがを使用できない場合は、プロパティに変更しないでください。 メソッドは、次のような場合にプロパティよりも優れています。

- メソッドは、時間のかかる操作を実行します。 メソッドの perceivably は、フィールドの値を設定または取得するために必要な時間よりも遅くなります。

- メソッドは、変換を実行します。 フィールドにアクセスしても、格納されているデータの変換バージョンは返されません。

- Get メソッドには、観測可能な副作用があります。 フィールドの値を取得しても、副作用は生成されません。

- 実行の順序は重要です。 フィールドの値を設定しても、他の操作の発生には依存しません。

- メソッドを連続して2回呼び出すと、異なる結果が生成されます。

- メソッドは静的ですが、呼び出し元が変更できるオブジェクトを返します。 フィールドの値を取得しても、フィールドに格納されているデータを呼び出し元が変更することはできません。

- メソッドは配列を返します。

## <a name="how-to-fix-violations"></a>違反の修正方法

この規則違反を修正するには、メソッドをプロパティに変更します。

## <a name="when-to-suppress-warnings"></a>警告を非表示にする場合

メソッドが前述の条件のうち少なくとも1つを満たしている場合、この規則からの警告を非表示にします。

## <a name="configurability"></a>かつ

この規則を[FxCop アナライザー](install-fxcop-analyzers.md) (レガシ分析ではなく) から実行している場合は、ユーザー補助に基づいて、この規則を実行するコードベースの部分を構成できます。 たとえば、パブリックでない API サーフェイスに対してのみルールを実行するように指定するには、プロジェクトの editorconfig ファイルに次のキーと値のペアを追加します。

```ini
dotnet_code_quality.ca1024.api_surface = private, internal
```

このオプションは、この規則、すべての規則、またはこのカテゴリのすべての規則 (デザイン) に対してのみ構成できます。 詳細については、「 [FxCop アナライザーの構成](configure-fxcop-analyzers.md)」を参照してください。

## <a name="control-property-expansion-in-the-debugger"></a>デバッガーでのプロパティの拡張の制御

プログラマがプロパティを使用しないようにする理由の1つは、プログラマがデバッガーを自動展開しないようにするためです。 たとえば、プロパティに大きなオブジェクトの割り当てや P/Invoke の呼び出しが含まれる場合がありますが、実際には観測可能な副作用がない可能性があります。

を適用<xref:System.Diagnostics.DebuggerBrowsableAttribute?displayProperty=fullName>することによって、デバッガーが自動的にプロパティを展開しないようにすることができます。 次の例は、この属性がインスタンスプロパティに適用されていることを示しています。

```vb
Imports System
Imports System.Diagnostics

Namespace Microsoft.Samples

    Public Class TestClass

        ' [...]

        <DebuggerBrowsable(DebuggerBrowsableState.Never)> _
        Public ReadOnly Property LargeObject() As LargeObject
            Get
                ' Allocate large object
                ' [...]
            End Get
        End Property

    End Class

End Namespace
```

```csharp
using System;
using System.Diagnostics;

namespace Microsoft.Samples
{
    publicclass TestClass
    {
        // [...]

        [DebuggerBrowsable(DebuggerBrowsableState.Never)]
        public LargeObject LargeObject
        {
            get
            {
                // Allocate large object
                // [...]
            }
        }
    }
}
```

## <a name="example"></a>例

次の例には、プロパティに変換する必要があるいくつかのメソッドと、フィールドのように動作しないため、いくつかのメソッドが含まれています。

[!code-csharp[FxCop.Design.MethodsProperties#1](../code-quality/codesnippet/CSharp/ca1024-use-properties-where-appropriate_1.cs)]