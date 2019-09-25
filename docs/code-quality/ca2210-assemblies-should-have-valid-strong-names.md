---
title: CA2210:アセンブリには有効な厳密な名前が必要です
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- AssembliesShouldHaveValidStrongNames
- CA2210
helpviewer_keywords:
- AssembliesShouldHaveValidStrongNames
- CA2210
ms.assetid: 8ed33d1c-8ec6-4b47-a692-e22dc8693088
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 54f7d3a0efc2f6199c030c8dd488de3b5b158240
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/24/2019
ms.locfileid: "71231722"
---
# <a name="ca2210-assemblies-should-have-valid-strong-names"></a>CA2210:アセンブリには有効な厳密な名前が必要です

|||
|-|-|
|TypeName|AssembliesShouldHaveValidStrongNames|
|CheckId|CA2210|
|カテゴリ|Microsoft.Design|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因

アセンブリが厳密な名前で署名されていないか、厳密な名前を確認できなかったか、またはコンピューターの現在のレジストリ設定がないと厳密な名前が有効ではありません。

## <a name="rule-description"></a>規則の説明

このルールは、アセンブリの厳密な名前を取得して検証します。 次のいずれかに該当する場合は、違反が発生します。

- アセンブリに厳密な名前がありません。

- 署名後にアセンブリが変更されました。

- アセンブリは遅延署名されています。

- アセンブリが正しく署名されていないか、署名に失敗しました。

- アセンブリには、検証に合格するためのレジストリ設定が必要です。 たとえば、アセンブリの検証をスキップするために、厳密な名前ツール (Sn.exe) が使用されていました。

厳密な名前によって、改ざんされたアセンブリを、クライアントが無意識のうちに読み込む問題を防ぐことができます。 厳密な名前のないアセンブリが配置される状況は、限定されます。 適切に署名されていないアセンブリを共有または配布すると、アセンブリが改ざんされる場合、共通言語ランタイムでアセンブリを読み込むことができない場合、またはユーザーのコンピューターで検証を無効にする必要がある場合などの問題が考えられます。 厳密な名前を持たないアセンブリには、次のような欠点があります。

- そのオリジンを検証できません。

- 共通言語ランタイムは、アセンブリの内容が変更されている場合、ユーザーに警告することはできません。

- グローバルアセンブリキャッシュに読み込むことはできません。

遅延署名されたアセンブリを読み込んで分析するには、アセンブリの検証を無効にする必要があることに注意してください。

## <a name="how-to-fix-violations"></a>違反の修正方法

### <a name="create-a-key-file"></a>キーファイルを作成する

次の手順のいずれかを使用します。

- [アセンブリリンカーツール (al.exe)](/dotnet/framework/tools/al-exe-assembly-linker)を使用します。

- .NET Framework `/keyfile` 2.0 の場合は、 `/keycontainer`コンパイラオプション[/keyfile (アセンブリに署名するためのキーまたはキーペアの指定)](/cpp/build/reference/keyfile-specify-key-or-key-pair-to-sign-an-assembly)または[/KEYCONTAINER (アセンブリに署名するためのキーコンテナーの指定)](/cpp/build/reference/keycontainer-specify-a-key-container-to-sign-an-assembly)リンカーオプションC++のいずれかを使用します。

- .NET Framework v1.0 または v1.1 の場合<xref:System.Reflection.AssemblyKeyFileAttribute?displayProperty=fullName>は、属性または<xref:System.Reflection.AssemblyKeyNameAttribute?displayProperty=fullName>属性のいずれかを使用します。

### <a name="sign-your-assembly-with-a-strong-name-in-visual-studio"></a>Visual Studio で厳密な名前でアセンブリに署名する

1. Visual Studio でソリューションを開きます。

2. **ソリューションエクスプローラー**で、プロジェクトを右クリックし、[プロパティ] をクリックし**ます。**

3. **[署名]** タブをクリックし、 **[アセンブリの署名]** チェックボックスをオンにします。

4. **[厳密な名前のキーファイルを選択**してください] で、 **[新規]** を選択します。

   **[厳密な名前キーの作成]** ウィンドウが表示されます。

5. **[キーファイル名]** に、厳密な名前のキーの名前を入力します。

6. パスワードを使用してキーを保護するかどうかを選択し、[ **OK]** をクリックします。

7. **ソリューションエクスプローラー**で、プロジェクトを右クリックし、 **[ビルド]** をクリックします。

### <a name="sign-your-assembly-with-a-strong-name-outside-visual-studio"></a>Visual Studio の外部の厳密な名前でアセンブリに署名する

[厳密名ツール (sn.exe)](/dotnet/framework/tools/sn-exe-strong-name-tool)を使用します。

## <a name="when-to-suppress-warnings"></a>警告を非表示にする場合

コンテンツの改ざんが心配でない環境でアセンブリが使用されている場合にのみ、この規則の警告を非表示にします。

## <a name="see-also"></a>関連項目

- <xref:System.Reflection.AssemblyKeyFileAttribute?displayProperty=fullName>
- <xref:System.Reflection.AssemblyKeyNameAttribute?displayProperty=fullName>
- [方法: 厳密な名前でアセンブリに署名する](/dotnet/framework/app-domains/how-to-sign-an-assembly-with-a-strong-name)
- [Sn.exe (厳密名ツール)](/dotnet/framework/tools/sn-exe-strong-name-tool)