---
title: CA1016:アセンブリに AssemblyVersionAttribute を設定します
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- MarkAssembliesWithAssemblyVersion
- CA1016
helpviewer_keywords:
- CA1016
- MarkAssembliesWithAssemblyVersion
ms.assetid: 4340aed8-d92b-4cde-a398-cb6963c6da5a
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CPP
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 140037b025db88230762bc0d540d933cec7a5119
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/24/2019
ms.locfileid: "71236309"
---
# <a name="ca1016-mark-assemblies-with-assemblyversionattribute"></a>CA1016:アセンブリに AssemblyVersionAttribute を設定します

|||
|-|-|
|TypeName|MarkAssembliesWithAssemblyVersion|
|CheckId|CA1016|
|カテゴリ|Microsoft.Design|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因

アセンブリにバージョン番号がありません。

## <a name="rule-description"></a>規則の説明

アセンブリの id は、次の情報で構成されます。

- [アセンブリ名]

- バージョン番号

- カルチャ

- 公開キー (厳密な名前を持つアセンブリの場合)。

.NET では、バージョン番号を使用してアセンブリを一意に識別し、厳密な名前を持つアセンブリの型にバインドします。 バージョン番号は、バージョンと発行者のポリシーと共に使用されます。 既定で、アプリケーションは、ビルドされたアセンブリのバージョンでのみ実行されます。

## <a name="how-to-fix-violations"></a>違反の修正方法

この規則違反を修正するには、 <xref:System.Reflection.AssemblyVersionAttribute?displayProperty=fullName>属性を使用してバージョン番号をアセンブリに追加します。

## <a name="when-to-suppress-warnings"></a>警告を非表示にする場合

サードパーティまたは運用環境で使用されているアセンブリについては、この規則による警告を抑制しないでください。

## <a name="example"></a>例

次の例は、 <xref:System.Reflection.AssemblyVersionAttribute>属性が適用されているアセンブリを示しています。

[!code-csharp[FxCop.Design.AssembliesVersion#1](../code-quality/codesnippet/CSharp/ca1016-mark-assemblies-with-assemblyversionattribute_1.cs)]
[!code-vb[FxCop.Design.AssembliesVersion#1](../code-quality/codesnippet/VisualBasic/ca1016-mark-assemblies-with-assemblyversionattribute_1.vb)]
[!code-cpp[FxCop.Design.AssembliesVersion#1](../code-quality/codesnippet/CPP/ca1016-mark-assemblies-with-assemblyversionattribute_1.cpp)]

## <a name="see-also"></a>関連項目

- [アセンブリのバージョン管理](/dotnet/framework/app-domains/assembly-versioning)
- [方法: 発行者ポリシーを作成する](/dotnet/framework/configure-apps/how-to-create-a-publisher-policy)