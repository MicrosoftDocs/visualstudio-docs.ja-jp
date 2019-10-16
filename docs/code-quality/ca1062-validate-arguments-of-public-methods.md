---
title: 'CA1062: パブリック メソッドの引数の検証'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA1062
- ValidateArgumentsOfPublicMethods
- Validate arguments of public methods
helpviewer_keywords:
- CA1062
- ValidateArgumentsOfPublicMethods
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 43aa94f67e17a3de51635840419e36ef38db41df
ms.sourcegitcommit: e82baa50bf5a65858c410882c2e86a552c2c1921
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2019
ms.locfileid: "72381011"
---
# <a name="ca1062-validate-arguments-of-public-methods"></a>CA1062: パブリック メソッドの引数の検証

|||
|-|-|
|TypeName|ValidateArgumentsOfPublicMethods|
|CheckId|CA1062|
|カテゴリ|Microsoft Design|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因

外部から参照可能なメソッドは、その引数が `null` (Visual Basic の `Nothing`) かどうかを検証せずに、参照引数の1つを逆参照します。

## <a name="rule-description"></a>規則の説明

外部から参照できるメソッドに渡されるすべての参照引数は、@no__t 0 に対してチェックする必要があります。 必要に応じて、引数が-1 @no__t の場合に @no__t 0 をスローします。

パブリックまたは protected として宣言されているために不明なアセンブリからメソッドを呼び出すことができる場合は、メソッドのすべてのパラメーターを検証する必要があります。 メソッドが既知のアセンブリによってのみ呼び出されるように設計されている場合は、メソッドを内部にし、メソッドを含むアセンブリに <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> 属性を適用する必要があります。

## <a name="how-to-fix-violations"></a>違反の修正方法

この規則違反を修正するには、各参照引数を `null` に対して検証します。

## <a name="when-to-suppress-warnings"></a>警告を非表示にする場合

逆参照パラメーターが関数内の別のメソッド呼び出しによって検証されていることが確実である場合は、この規則からの警告を非表示にすることができます。

## <a name="example"></a>例

次の例は、規則に違反するメソッドと、規則を満たすメソッドを示しています。

```csharp
using System;

namespace DesignLibrary
{
    public class Test
    {
        // This method violates the rule.
        public void DoNotValidate(string input)
        {
            if (input.Length != 0)
            {
                Console.WriteLine(input);
            }
        }

        // This method satisfies the rule.
        public void Validate(string input)
        {
            if (input == null)
            {
                throw new ArgumentNullException(nameof(input));
            }
            if (input.Length != 0)
            {
                Console.WriteLine(input);
            }
        }
    }
}
```

```vb
Imports System

Namespace DesignLibrary

    Public Class Test

        ' This method violates the rule.
        Sub DoNotValidate(ByVal input As String)

            If input.Length <> 0 Then
                Console.WriteLine(input)
            End If

        End Sub

        ' This method satisfies the rule.
        Sub Validate(ByVal input As String)

            If input Is Nothing Then
                Throw New ArgumentNullException(NameOf(input))
            End If

            If input.Length <> 0 Then
                Console.WriteLine(input)
            End If

        End Sub

    End Class

End Namespace
```

## <a name="example"></a>例

フィールドまたは参照オブジェクトであるプロパティを設定するコピーコンストラクターも、CA1062 の規則に違反する可能性があります。 コピーコンストラクターに渡されるコピーされたオブジェクトは @no__t 0 (Visual Basic では `Nothing`) である可能性があるため、違反が発生します。 違反を解決するには、静的 (Visual Basic では Shared) メソッドを使用して、コピーされたオブジェクトが null でないことを確認します。

次の `Person` クラスの例では、`Person` コピーコンストラクターに渡される `other` オブジェクトは `null` である可能性があります。

```csharp
public class Person
{
    public string Name { get; private set; }
    public int Age { get; private set; }

    public Person(string name, int age)
    {
        Name = name;
        Age = age;
    }

    // Copy constructor CA1062 fires because other is dereferenced
    // without being checked for null
    public Person(Person other)
        : this(other.Name, other.Age)
    {
    }
}
```

## <a name="example"></a>例

次の変更後の `Person` の例では、コピーコンストラクターに渡された `other` オブジェクトが、最初に `PassThroughNonNull` メソッドで null であるかどうかがチェックされます。

```csharp
public class Person
{
    public string Name { get; private set; }
    public int Age { get; private set; }

    public Person(string name, int age)
    {
        Name = name;
        Age = age;
    }

    // Copy constructor
    public Person(Person other)
        : this(PassThroughNonNull(other).Name,
          PassThroughNonNull(other).Age)
    {
    }

    // Null check method
    private static Person PassThroughNonNull(Person person)
    {
        if (person == null)
            throw new ArgumentNullException(nameof(person));
        return person;
    }
}
```