---
title: CA1062:パブリック メソッドの引数の検証
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
ms.openlocfilehash: 3868061a01572d0b1adadec6619f88269d353dff
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68922438"
---
# <a name="ca1062-validate-arguments-of-public-methods"></a>CA1062:パブリック メソッドの引数の検証

|||
|-|-|
|TypeName|ValidateArgumentsOfPublicMethods|
|CheckId|CA1062|
|カテゴリ|Microsoft.Design|
|互換性に影響する変更点|中断なし|

## <a name="cause"></a>原因

外部から参照できるメソッドは、その引数が`null` (`Nothing` Visual Basic) であるかどうかを確認せずに、参照引数の1つを逆参照します。

## <a name="rule-description"></a>規則の説明

外部から参照できるメソッドに渡されるすべての参照引数を照合`null`する必要があります。 必要に応じて、 <xref:System.ArgumentNullException>引数が`null`の場合にをスローします。

パブリックまたは protected として宣言されているために不明なアセンブリからメソッドを呼び出すことができる場合は、メソッドのすべてのパラメーターを検証する必要があります。 メソッドが既知のアセンブリによってのみ呼び出されるように設計されている場合は、メソッド<xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute>を内部にし、メソッドを含むアセンブリに属性を適用する必要があります。

## <a name="how-to-fix-violations"></a>違反の修正方法

この規則違反を修正するには、各参照引数を`null`に対して検証します。

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
                throw new ArgumentNullException("input");
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
                Throw New ArgumentNullException("input")
            End If

            If input.Length <> 0 Then
                Console.WriteLine(input)
            End If

        End Sub

    End Class

End Namespace
```

## <a name="example"></a>例

フィールドまたは参照オブジェクトであるプロパティを設定するコピーコンストラクターも、CA1062 の規則に違反する可能性があります。 コピーコンストラクターに渡されるコピーさ`null`れたオブジェクトが (`Nothing` Visual Basic) である可能性があるため、違反が発生します。 違反を解決するには、静的 (Visual Basic では Shared) メソッドを使用して、コピーされたオブジェクトが null でないことを確認します。

次`Person`のクラスの例`other`では、 `Person`コピーコンストラクターに渡されるオブジェクトがで`null`ある可能性があります。

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

次`Person`の例では`other` 、コピーコンストラクターに渡されたオブジェクトが、最初に`PassThroughNonNull`メソッドで null であるかどうかがチェックされます。

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
            throw new ArgumentNullException("person");
        return person;
    }
}
```