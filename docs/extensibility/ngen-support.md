---
title: VSIX v3 での Ngen のサポート | Microsoft Docs
description: ネイティブ イメージ ジェネレーターを有効にする方法について説明します。これは、拡張機能の開発者がマネージド アプリケーションのパフォーマンスを向上させるために使用できるツールです。
ms.custom: SEO-VS-2020
ms.date: 11/09/2016
ms.topic: conceptual
ms.assetid: 1472e884-c74e-4c23-9d4a-6d8bdcac043b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 0f8de3b662875a4af0423930eecfdd77e4e05b08
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105090591"
---
# <a name="ngen-support-in-vsix-v3"></a>VSIX v3 での Ngen のサポート

Visual Studio 2017 および新しい VSIX v3 (バージョン 3) 拡張機能マニフェスト形式を使用して、拡張機能の開発者は、インストール時にアセンブリを "ngen" できるようになりました。

下に、"ngen" の機能について説明している MSDN の抜粋を示します。

>ネイティブ イメージ ジェネレーター (*Ngen.exe*) は、マネージド アプリケーションのパフォーマンスを向上させるツールです。 *Ngen.exe* では、コンパイルされたプロセッサ固有のマシン コードを含むファイルであるネイティブ イメージを作成して、ローカル コンピューターのネイティブ イメージ キャッシュにインストールします。 ランタイムは、Just-In-Time (JIT) コンパイラを使用してオリジナルのアセンブリをコンパイルする代わりに、キャッシュにあるネイティブ イメージを使用できます。
>
>[Ngen.exe (ネイティブ イメージ ジェネレーター)](/dotnet/framework/tools/ngen-exe-native-image-generator) より

アセンブリを "ngen" するには、VSIX を "インスタンス単位、コンピューター単位" でインストールする必要があります。 これを有効にするには、`extension.vsixmanifest` デザイナーで [すべてのユーザー] チェック ボックスをオンにします。

![[すべてのユーザー] をオンにする](media/check-all-users.png)

## <a name="how-to-enable-ngen"></a>Ngen を有効にする方法

アセンブリに対して ngen を有効にするには、Visual Studio の **[プロパティ]** ウィンドウを使用します。

次の 4 つのプロパティを設定できます。

1. **Ngen** (ブール値) - True の場合、Visual Studio インストーラーによってアセンブリが "ngen" されます。
2. **Ngen アプリケーション** (文字列) - Ngen では、アセンブリの依存関係を解決するために、アプリケーションの *app.config* ファイルを使用できます。 この値は、(Visual Studio のインストール ディレクトリを基準として) 使用する *app.config* を持つアプリケーションに設定する必要があります。
3. **Ngen アーキテクチャ** (列挙型) - アセンブリをネイティブにコンパイルするためのアーキテクチャ。 オプションは、a. NotSpecified、b. X86、c. X64、d. NotSpecified b. X86 c. X64 d. All
4. **Ngen の優先度** (1 から 3 の整数) - Ngen の優先度レベルは [Ngen.exe の優先度レベル](/dotnet/framework/tools/ngen-exe-native-image-generator#priority-levels)に関するページに記載されています。

次に、 **[プロパティ]** ウィンドウの動作を見てみましょう。

![[プロパティ] の ngen](media/ngen-in-properties.png)

これで、VSIX プロジェクトの *.csproj* ファイル内のプロジェクト参照にメタデータが追加されます。

```xml
 <ProjectReference Include="..\ClassLibrary1\ClassLibrary1.csproj">
    <Project>{69a979f1-eba2-43e7-9346-0e56e803508b}</Project>
    <Name>ClassLibrary1</Name>
    <Ngen>True</Ngen>
    <NgenApplication>vsn.exe</NgenApplication>
    <NgenArchitecture>X86</NgenArchitecture>
    <NgenPriority>2</NgenPriority>
</ProjectReference>
```

> [!NOTE]
> 必要に応じて、.csproj ファイルを直接編集できます。

## <a name="extra-information"></a>追加情報

プロパティ デザイナーの変更は、プロジェクト参照以外にも適用されます。プロジェクト内の項目についても、項目が .NET アセンブリである限り、上記と同じ方法を使用して Ngen メタデータを設定できます。
