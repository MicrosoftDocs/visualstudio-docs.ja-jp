---
title: Visual Studio 2022 Preview における API の破壊的変更
description: Visual Studio 2022 Preview に拡張機能を移行する場合に、既存の VS 拡張機能のコンパイルに失敗する原因となる API の変更について学習します。
ms.date: 06/08/2021
ms.topic: reference
author: leslierichardson95
ms.author: lerich
manager: jmartens
monikerRange: vs-2022
ms.workload:
- vssdk
ms.openlocfilehash: 9427b7a75ad53fc9a0795b249d96431113aba36d
ms.sourcegitcommit: 5fb4a67a8208707e79dc09601e8db70b16ba7192
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2021
ms.locfileid: "112309225"
---
# <a name="breaking-api-changes-in-visual-studio-2022"></a>Visual Studio 2022 での API の破壊的変更

[!INCLUDE [preview-note](../includes/preview-note.md)]

Visual Studio 2022 に拡張機能を移行する場合、ここに一覧表示されている破壊的変更が影響する可能性があります。

## <a name="reference-assemblies-no-longer-installed"></a>参照アセンブリがインストールされなくなった

Visual Studio のインストール ディレクトリから解決された、その MSBuild を参照していた可能性のあるアセンブリの多くはインストールされなくなりました。 必要な Visual Studio SDK ref アセンブリを取得するには、NuGet を使用する必要があります。 これを行う詳細な手順については、[プロジェクトの最新化](update-visual-studio-extension.md#modernize-your-vsix-project)に関するページを参照してください。

## <a name="removed-apis"></a>API の削除

Visual Studio 2022 では、今後の Visual Studio の移行の一環としていくつかの API が削除されています。 削除された API のリストは、[削除された API のリスト](removed-api-list.md)に関するページで確認できます。

## <a name="interop-breaking-changes"></a>相互運用性の破壊的変更

Visual Studio 2022 では多くの API が変更されています。通常はコードで簡単に対応できる単純な変更です。

破壊的変更を管理するために、相互運用機能アセンブリを配布するための新しいメカニズムを提供する予定です。 具体的には、Visual Studio 2022 以降では、多くの一般的なパブリック Visual Studio インターフェイスの定義を含む単一の相互運用機能アセンブリを提供します。 そのアセンブリには、複数の相互運用機能アセンブリから移行する多くの Visual Studio インターフェイスのマネージド定義が含まれています。 新しい相互運用機能アセンブリは、`Microsoft.VisualStudio.Interop` NuGet パッケージを使用して配布されます。

しかし、主にネイティブ コンテキストで使用され、破壊的変更の数が少ない Visual Studio コンポーネントには、引き続き独自の相互運用機能アセンブリが含まれることになります (たとえば、デバッガー アセンブリは引き続き、現在の場合と同じように VisualStudio.Debugger.Interop.dll となります)。 いずれにせよ、現在の場合と同じように、アセンブリをアプリケーションから参照することができます。

これは重大な変更であり、この新しいアプローチでビルドされた API とアセンブリを使用する拡張機能は、前の相互運用機能アセンブリを使用している古いバージョンの Visual Studio と互換性がないことを意味します。

これには、拡張機能を Visual Studio 2022 により簡単に更新できるようになる非常に重要な利点がいくつかあります。

- 破損した API はビルド時エラーとなり、それらを見つけて修正しやすくなります。
- Visual Studio 2022 では破損した API を使用するコードのみを更新する必要があります。
- 古くなり、破損した API を誤って使用できなくなります。

全体として、これらの変更により、すべてのユーザーに対して Visual Studio がより安定したバージョンとなります。 このアプローチの大きな欠点は、ターゲットの Visual Studio バージョンごとに 1 回コードをコンパイルしないとマネージド アセンブリを Visual Studio 2019 と Visual Studio 2022 の両方で実行できないことです。

Visual Studio 2019 と Visual Studio 2022 の API の違いによるコンパイル エラーを確認しながら、その API または発生するパターンを参照できます。これらは、その修正方法についてのガイダンスとともに以下に一覧表示されています。

### <a name="int-or-uint-where-intptr-is-expected"></a>`int` または `uint` (`IntPtr` が想定されている場合)

これは非常に一般的なエラーであると考えられます。 Visual Studio 2022 を 64 ビット プロセスにするために、一部の相互運用 API を修正する必要がありました。これは、ポインターが 32 ビット整数に収まり、ポインターサイズの値を実際に使用できることを想定しています。

サンプル エラー:

> 引数 3: 'out uint' から 'out System.IntPtr' に変換できません

コードを更新し、破損を解決するために `IntPtr` または `UIntPtr` (以前は `int` または `uint` だった場合) を想定または指定するだけです。

修正のサンプル:

```diff
-shell.LoadLibrary(myGuid, myFlags, out uint ptrLib);
+shell.LoadLibrary(myGuid, myFlags, out IntPtr ptrLib);
```

### <a name="an-interop-type-defined-in-two-assemblies"></a>相互運用機能型が 2 つのアセンブリで定義されている

使用している型が 2 つのアセンブリで定義されていることを示すエラーが C# コンパイラによって報告された場合は、参照しなくなったはずの SDK の Visual Studio 2019 バージョンのアセンブリを参照していることがあります。

サンプル エラー:

> エラー CS0433: 型 'IVsDpiAware' が、'Microsoft.VisualStudio.Interop, Version=17.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a' と 'Microsoft.VisualStudio.Shell.Interop.16.0.DesignTime, Version=16.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a' の両方に存在します

[参照アセンブリの再マッピング テーブル](migrated-assemblies.md)に関するページを参照し、Visual Studio 2022 で優先名としてどのアセンブリ名が使用されているかを確認します。
上記のサンプル エラーに示されている 2 つのアセンブリを検討し、このテーブルを確認して、`Microsoft.VisualStudio.Interop` が新しいアセンブリ名であることに注目してください。 その後、プロジェクトから `Microsoft.VisualStudio.Shell.Interop.16.0.DesignTime` への参照を削除して修正します。

場合によっては、型フォワーダーを含む非推奨のアセンブリに対して、Visual Studio 2022 でバージョン管理されたパッケージを提供します。 これが使用できる場合は、パッケージ参照を削除するのではなく、Visual Studio 2022 バージョンに ''*アップグレード*'' することもできます。 型フォワーダーによってコンパイラからエラーが解決されます。

これらの参照は、推移的なパッケージ参照によって得られる場合があるため、プロジェクト ファイルで行われる直接参照よりも削除が困難になる可能性があることに注意してください。 そのような場合は、すべての直接パッケージ参照で、Visual Studio 2022 SDK パッケージ自体が使用されていることを確認してください。 *project.assets.js* を参照して、非推奨のアセンブリに取り込むパッケージのチェーンを特定することができます。 推移的なパッケージ参照を Visual Studio 2022 バージョンに更新することは、直接参照としてインストールするのと同様に簡単です。

依存関係ツリーを変更できない場合 (たとえば、サードパーティの依存関係が含まれているため)、Visual Studio 2022 より前のパッケージへの直接パッケージ参照を追加し、その `PackageReference` 項目に `ExcludeAssets="compile"` メタデータを追加してコンパイラ エラーを解決することができます。 しかし、この方法では、拡張機能で Visual Studio 2022 より前のアセンブリに対する依存関係が保持され、実行時に拡張機能が誤動作する場合があることに注意してください。

### <a name="missing-reference-to-an-interop-assembly"></a>相互運用機能アセンブリへの参照が欠落しています

Visual Studio 2022 より前の SDK に対してコンパイルされたアセンブリを参照すると、アセンブリ参照の欠落に関するエラーが発生することがあります。

サンプル エラー:

> エラー CS0012 型 'IVsTextViewFilter' は、参照されていないアセンブリで定義されています。 アセンブリ 'Microsoft.VisualStudio.TextManager.Interop, Version=7.1.40304.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a' への参照を追加する必要があります

[参照アセンブリの再マッピング テーブル](migrated-assemblies.md)を使用して、要求されたアセンブリが実際には参照する必要があるものではないことを確認できます。

最善の修正策は、Visual Studio 2022 SDK に対してコンパイルされたバージョンに依存関係を更新し、削除された相互運用機能アセンブリがコンパイラによって要求されなくなるようにすることです。

場合によっては、型フォワーダーを含む非推奨のアセンブリに対して、Visual Studio 2022 でバージョン管理されたパッケージを提供します。 これを使用できる場合は、古いパッケージの Visual Studio 2022 バージョンにパッケージ参照を追加して、型フォワーダーによってコンパイラからエラーが解決されるようにすることができます。

### <a name="iasyncserviceprovider-is-missing"></a>`IAsyncServiceProvider` が欠落しています

2 つの名前空間に、このインターフェイスの定義が 2 つあります。 これらのうちの 1 つだけが、管理対象の使用を目的としています。

Visual Studio 2019 の名前空間 | Visual Studio 2022 の名前空間 | 使用目的
--|--|--
Microsoft.VisualStudio.Shell.IAsyncServiceProvider | Microsoft.VisualStudio.Shell.IAsyncServiceProvider | マネージド コードの使用
Microsoft.VisualStudio.Shell.Interop.IAsyncServiceProvider | Microsoft.VisualStudio.Shell.COMAsyncServiceProvider.IAsyncServiceProvider | 下位相互運用のみ

`IAsyncServiceProvider` に関するエラーが表示される場合は、ネイティブ コード (2 番目の行) 用のものを使用していた ''*可能性*'' があります。
その場合は、新しい名前空間に更新するか、より管理しやすいインターフェイスに切り替えることができます。

### <a name="dte-and-_dte-type-cast-failures"></a>`DTE` および `_DTE` 型キャストの失敗

`DTE` と `_DTE` はどちらもインターフェイスです。 一方は他方から派生します。 しかし、Visual Studio 2022 では、基本型と派生型が入れ替わります。
これにより、特定の型の割り当てやキャストが失敗します。

これは、以前に `new DTE()` を使用していた場合、今後は `new _DTE()` を使用する必要があることも意味します。

### <a name="missing-argument-on-a-method-invocation"></a>メソッド呼び出しの引数が欠落しています

いくつかのメソッドでは、相互運用 API の省略可能なパラメーターとして既定の引数が宣言されなくなりました。
COM 相互運用呼び出しに対する引数の欠落に関するエラーが発生し、パラメーターで `object` 型を呼び出した場合、Visual Studio 2019 相互運用 API によって定義された以前の既定値が `""` であった可能性があります。そのため、コンパイル エラーを解決するために引数として `""` を追加することを検討してください。

既定の引数がどのように使用されているかがわからない場合は、言語サービス コンテキストを Visual Studio 2022 から Visual Studio 2019 に切り替えてみて、古い相互運用機能アセンブリを使用して Intellisense を取得し、既定の引数の内容を確認してから、コードに明示的に追加してください。 Visual Studio 2019 用にコンパイルされている場合は引き続き正常に動作しますが、Visual Studio 2022 に対してコンパイルされるようになります。

修正のサンプル:

```diff
-process4.Attach2();
+process4.Attach2("");
```
