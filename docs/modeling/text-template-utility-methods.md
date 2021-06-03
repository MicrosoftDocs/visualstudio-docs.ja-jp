---
title: テキスト テンプレートのユーティリティ メソッド
description: Visual Studio でコードを記述するときに使用できるさまざまなテキスト テンプレートのユーティリティ メソッドについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- text templates, utility methods
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: fcc879a19d3dfcd9e1e8e1bcd79f0488a312e96c
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99924574"
---
# <a name="text-template-utility-methods"></a>テキスト テンプレートのユーティリティ メソッド

Visual Studio テキスト テンプレートでコードを記述するときには、常に使用できるメソッドがいくつかあります。 これらのメソッドは <xref:Microsoft.VisualStudio.TextTemplating.TextTransformation> で定義されています。

> [!TIP]
> また、通常の (前処理されていない) テキスト テンプレートで、ホスト環境によって提供されるその他のメソッドやサービスを使用することもできます。 たとえば、ファイル パスを解決したり、エラーをログに記録したり、Visual Studio や読み込まれたパッケージによって提供されるサービスを取得したりすることができます。 詳細については、[テキスト テンプレートから Visual Studio へのアクセス](/previous-versions/visualstudio/visual-studio-2010/gg604090\(v\=vs.100\))に関するページを参照してください。

## <a name="write-methods"></a>書き込みメソッド

式コード ブロックを使用する代わりに、`Write()` メソッドと `WriteLine()` メソッドを使用して、標準コード ブロック内にテキストを追加できます。 次の 2 つのコード ブロックは機能的に同等です。

### <a name="code-block-with-an-expression-block"></a>式ブロックのあるコード ブロック

```
<#
int i = 10;
while (i-- > 0)
    { #>
        <#= i #>
    <# }
#>
```

### <a name="code-block-using-writeline"></a>WriteLine() を使用したコード ブロック

```
<#
    int i = 10;
    while (i-- > 0)
    {
        WriteLine((i.ToString()));
    }
#>
```

入れ子になった制御構造を持つ長いコード ブロック内の式ブロックの代わりに、これらのユーティリティ メソッドのいずれかを使用すると役に立つ場合があります。

`Write()` メソッドと `WriteLine()` メソッドには 2 つのオーバーロードがあります。1 つは単一の文字列パラメーターを受け取り、もう 1 つは複合書式指定文字列とその文字列に含めるオブジェクトの配列を受け取ります (`Console.WriteLine()` メソッドなど)。 次の 2 つの `WriteLine()` の使用方法は機能的に等しくなります。

```
<#
    string msg = "Say: {0}, {1}, {2}";
    string s1 = "hello";
    string s2 = "goodbye";
    string s3 = "farewell";

    WriteLine(msg, s1, s2, s3);
    WriteLine("Say: hello, goodbye, farewell");
#>
```

## <a name="indentation-methods"></a>インデント メソッド

インデント メソッドを使用して、テキスト テンプレートの出力を書式設定できます。 <xref:Microsoft.VisualStudio.TextTemplating.TextTransformation> クラスには、テキスト テンプレートの現在のインデントを示す `CurrentIndent` 文字列プロパティと、追加されたインデントのリストである `indentLengths` フィールドがあります。 `PushIndent()` メソッドを使用してインデントを追加することも、`PopIndent()` メソッドを使用してインデントを減らすこともできます。 すべてのインデントを解除する場合は、`ClearIndent()` メソッドを使用します。 次のコード ブロックでは、これらのメソッドの使用方法を示します。

```
<#
    WriteLine(CurrentIndent + "Hello");
    PushIndent("    ");
    WriteLine(CurrentIndent + "Hello");
    PushIndent("    ");
    WriteLine(CurrentIndent + "Hello");
    ClearIndent();
    WriteLine(CurrentIndent + "Hello");
    PushIndent("    ");
    WriteLine(CurrentIndent + "Hello");
#>
```

このコード ブロックを実行すると、次の出力が生成されます。

```
Hello
        Hello
                Hello
Hello
        Hello
```

## <a name="error-and-warning-methods"></a>エラーと警告のメソッド

エラーと警告のユーティリティ メソッドを使用すると、Visual Studio のエラー一覧にメッセージを追加できます。 たとえば、次のコードでは、エラー一覧にエラー メッセージを追加します。

```
<#
  try
  {
    string str = null;
    Write(str.Length.ToString());
  }
  catch (Exception e)
  {
    Error(e.Message);
  }
#>
```

## <a name="access-to-host-and-service-provider"></a>ホストとサービス プロバイダーへのアクセス

`this.Host` プロパティでは、テンプレートを実行しているホストによって公開されているプロパティへのアクセスを提供できます。 `this.Host` を使用するには、`<@template#>` ディレクティブに `hostspecific` 属性を設定する必要があります。

`<#@template ... hostspecific="true" #>`

`this.Host` の型は、テンプレートが実行されているホストの種類によって異なります。 Visual Studio で実行されているテンプレートでは、`this.Host` を `IServiceProvider` にキャストして、IDE などのサービスにアクセスできます。 次に例を示します。

```
EnvDTE.DTE dte = (EnvDTE.DTE) ((IServiceProvider) this.Host)
                       .GetService(typeof(EnvDTE.DTE));
```

## <a name="using-a-different-set-of-utility-methods"></a>別のユーティリティ メソッドのセットの使用

テキスト生成プロセスの一環として、テンプレート ファイルはクラスに変換されます。このクラスは常に `GeneratedTextTransformation` という名前で、<xref:Microsoft.VisualStudio.TextTemplating.TextTransformation> から継承されます。 代わりに別のメソッドのセットを使用する場合は、独自のクラスを記述し、テンプレート ディレクティブで指定できます。 クラスは、<xref:Microsoft.VisualStudio.TextTemplating.TextTransformation> から継承する必要があります。

```
<#@ template inherits="MyUtilityClass" #>
```

`assembly` ディレクティブを使用して、コンパイル済みクラスが見つかるアセンブリを参照します。
