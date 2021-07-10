---
title: DebuggerTypeProxy を使用してカスタム型を表示する | Microsoft Docs
description: DebuggerTypeProxyAttribute のインスタンスを使用して型のプロキシ (代理) を指定して、デバッガー ウィンドウでの型の表示方法を変更します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- attributes [C#], debugger
- DebuggerTypeProxyAttribute class
- DebuggerTypeProxy attribute
ms.assetid: 943f3bb1-993e-4800-a47e-0af78b063014
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 532850f8bb4ac6198481188c2a57a8db15a13873
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112389281"
---
# <a name="tell-the-debugger-what-type-to-show-using-debuggertypeproxy-attribute-c-visual-basic-ccli"></a>DebuggerTypeProxy 属性を使用して、デバッガーにどの型を表示するかを通知する (C#、Visual Basic、C++/CLI)

<xref:System.Diagnostics.DebuggerTypeProxyAttribute> では、ある型のプロキシ (代理) を指定し、その型をデバッガー ウィンドウで表示する方法を変更します。 プロキシを指定した変数を表示すると、元の型の代理としてプロキシが **表示** されます。 デバッガーの変数ウィンドウには、プロキシ型のパブリック メンバーのみが表示されます。 プライベート メンバーは表示されません。

この属性は次の対象に適用できます。

- 構造体
- クラス
- アセンブリ

> [!NOTE]
> ネイティブ コードの場合、この属性は C++/CLI コードでのみサポートされます。

型プロキシ クラスには、プロキシで置換される型の引数を使用するコンストラクターが必要です。 デバッガーでは、対象となる型の変数を表示するときに、毎回、新しい型プロキシ クラスのインスタンスが作成されます。 その結果、パフォーマンスが低下する可能性があります。 そのため、コンストラクターでの作業は必要最小限に抑えます。

パフォーマンスの低下を最小限にするために、式エバリュエーターでは、型の表示プロキシに関する属性はチェックされません。ただし、デバッガー ウィンドウで + 記号をクリックして型を展開したときや、<xref:System.Diagnostics.DebuggerBrowsableAttribute> を使用するときはチェックされます。 そのため、表示型に属性を指定するのは避けます。 属性は、表示型の本体で使用できるようにします。

型プロキシは、属性の対象となるクラスに入れ子にした、プライベート クラスにすることをお勧めします。 こうすることで、内部のメンバーに簡単にアクセスできます。

<xref:System.Diagnostics.DebuggerTypeProxyAttribute> は継承することができるため、基底クラスで型プロキシが指定されている場合は、派生クラスで独自の型プロキシが指定されていない限り、それが派生クラスにも適用されます。

<xref:System.Diagnostics.DebuggerTypeProxyAttribute> をアセンブリ レベルで使用する場合は、プロキシに置換される型を `Target` パラメーターで指定します。

<xref:System.Diagnostics.DebuggerDisplayAttribute> および <xref:System.Diagnostics.DebuggerTypeProxyAttribute> と共にこの属性を使用する方法の例については、[DebuggerDisplay 属性の使用](../debugger/using-the-debuggerdisplay-attribute.md)に関する記事を参照してください。

## <a name="using-generics-with-debuggertypeproxy"></a>ジェネリックと DebuggerTypeProxy の使用

ジェネリックのサポートは限定的です。 C# では、`DebuggerTypeProxy` はオープン型のみをサポートします。 オープン型 (構築されていない型とも呼ばれます) とは、その型パラメーターの引数によってインスタンス化されていないジェネリック型のことです。 クローズ型 (構築された型とも呼ばれます) は、サポートされていません。

オープン型の構文は次のようになります。

`Namespace.TypeName<,>`

`DebuggerTypeProxy` 内でジェネリック型を対象として使用する場合は、この構文を使用する必要があります。 `DebuggerTypeProxy` の機構は、型パラメーターを推論します。

C# のオープン型とクローズ型の詳細については、[C# 言語仕様](/dotnet/csharp/language-reference/language-specification)の「セクション 20.5.2 オープン型とクローズ型」を参照してください。

Visual Basic にはクローズ型の構文はないため、Visual Basic で同じ処理はできません。 代わりに、オープン型の名前の文字列形式を使用する必要があります。

`"Namespace.TypeName'2"`

## <a name="see-also"></a>関連項目

- [DebuggerDisplay 属性の使用](../debugger/using-the-debuggerdisplay-attribute.md)
- [.managed オブジェクトのカスタム ビューの作成](../debugger/create-custom-views-of-managed-objects.md)
- [デバッガー表示属性によるデバッグ機能の拡張](/dotnet/framework/debug-trace-profile/enhancing-debugging-with-the-debugger-display-attributes)
