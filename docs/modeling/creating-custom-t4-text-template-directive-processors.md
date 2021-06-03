---
title: カスタム T4 テキスト テンプレート ディレクティブ プロセッサの作成
description: テキスト テンプレート変換プロセスと、カスタム T4 テキスト テンプレート ディレクティブ プロセッサを作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- text templates, custom directive processors
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: bf17d2a7e3b38e267f0353f71c7cd83826b141bf
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99945332"
---
# <a name="create-custom-t4-text-template-directive-processors"></a>カスタム T4 テキスト テンプレート ディレクティブ プロセッサを作成する

"*テキスト テンプレート変換*" プロセスでは、"*テキスト テンプレート*" ファイル を入力として受け取り、テキスト ファイルを出力として生成します。 このプロセスは "*テキスト テンプレート変換エンジン*" によって制御され、このエンジンではテキスト テンプレート変換ホストおよび 1 つ以上のテキスト テンプレート "*ディレクティブ プロセッサ*" との相互作用によってプロセスを完了します。 詳細については、「[テキスト テンプレート変換プロセス](../modeling/the-text-template-transformation-process.md)」を参照してください。

カスタム ディレクティブ プロセッサを作成するには、<xref:Microsoft.VisualStudio.TextTemplating.DirectiveProcessor> または <xref:Microsoft.VisualStudio.TextTemplating.RequiresProvidesDirectiveProcessor> を継承するクラスを作成します。

これら 2 つの違いは、<xref:Microsoft.VisualStudio.TextTemplating.DirectiveProcessor> では、ユーザーからパラメーターを受け取り、テンプレート出力ファイルを作成するコードを生成するために必要な最小限のインターフェイスを実装することです。 <xref:Microsoft.VisualStudio.TextTemplating.RequiresProvidesDirectiveProcessor> では requires/provides 設計パターンを実装します。 <xref:Microsoft.VisualStudio.TextTemplating.RequiresProvidesDirectiveProcessor> では、`requires` と `provides` の 2 つの特殊なパラメーターを処理します。  たとえば、カスタム ディレクティブ プロセッサでは、ユーザーからファイル名を受け取り、そのファイルを開いて読み取った後、`fileText` という名前の変数にファイルのテキストを格納できます。 <xref:Microsoft.VisualStudio.TextTemplating.RequiresProvidesDirectiveProcessor> クラスのサブクラスでは、`requires` パラメーターの値としてユーザーからファイル名を受け取り、`provides` パラメーターの値としてテキストを格納する変数の名前を受け取ることができます。 このプロセッサは、ファイルを開いて読み取った後、指定された変数にファイルのテキストを格納します。

Visual Studio でテキスト テンプレートからカスタム ディレクティブ プロセッサを呼び出す前に、それを登録する必要があります。

レジストリ キーを追加する方法の詳細については、「[カスタム ディレクティブ プロセッサの配置](../modeling/deploying-a-custom-directive-processor.md)」を参照してください。

## <a name="custom-directives"></a>カスタム ディレクティブ

カスタム ディレクティブは次のようになります。

`<#@ MyDirective Processor="MyDirectiveProcessor" parameter1="value1" ... #>`

テキスト テンプレートから外部データまたはリソースにアクセスする場合は、カスタム ディレクティブ プロセッサを使用できます。

1 つのディレクティブ プロセッサによって提供される機能をさまざまなテキスト テンプレートで共有できるため、ディレクティブ プロセッサを使用すると、再利用するコードを組み込むことができます。 組み込みの `include` ディレクティブも同様です。これを使用すると、コードを除外したり、さまざまなテキスト テンプレート間で共有したりできるためです。 違いは、`include` ディレクティブで提供されるすべての機能が固定されていて、パラメーターを受け入れないことです。 共通の機能をテキスト テンプレートに提供し、そのテンプレートでパラメーターを渡すことができるようにする場合は、カスタム ディレクティブ プロセッサを作成する必要があります。

カスタム ディレクティブ プロセッサの例として、以下が考えられます。

- パラメーターとしてユーザー名とパスワードを受け取る、データベースからデータを返すディレクティブ プロセッサ。

- パラメーターとしてファイル名を受け取る、ファイルを開いて読み取るディレクティブ プロセッサ。

### <a name="principal-parts-of-a-custom-directive-processor"></a>カスタム ディレクティブ プロセッサの主要部分

ディレクティブ プロセッサを開発するには、<xref:Microsoft.VisualStudio.TextTemplating.DirectiveProcessor> または <xref:Microsoft.VisualStudio.TextTemplating.RequiresProvidesDirectiveProcessor> を継承するクラスを作成する必要があります。

実装する必要がある最も重要な `DirectiveProcessor` メソッドは次のとおりです。

- `bool IsDirectiveSupported(string directiveName)` - ディレクティブ プロセッサが名前付きディレクティブを処理できる場合に `true` を返します。

- `void ProcessDirective (string directiveName, IDictionary<string, string> arguments)` - テンプレート内でディレクティブが出現するたびに、テンプレート エンジンによってこのメソッドが呼び出されます。 プロセッサによって結果が保存されます。

ProcessDirective() へのすべての呼び出しの後、テンプレート エンジンによって以下のメソッドが呼び出されます。

- `string[] GetReferencesForProcessingRun()` - テンプレート コードで必要とされるアセンブリの名前を返します。

- `string[] GetImportsForProcessingRun()` - テンプレート コードで使用できる名前空間を返します。

- `string GetClassCodeForProcessingRun()` - テンプレート コードで使用できるメソッド、プロパティ、およびその他の宣言のコードを返します。 そのための最も簡単な方法は、C# または Visual Basic コードを含む文字列を作成することです。 任意の CLR 言語を使用するテンプレートからディレクティブ プロセッサを呼び出すことができるようにする場合は、ステートメントを CodeDom ツリーとして構築した後、テンプレートで使用されている言語でそのツリーをシリアル化した結果を返すことができます。

- 詳細については、[カスタム ディレクティブ プロセッサの作成のチュートリアル](../modeling/walkthrough-creating-a-custom-directive-processor.md)に関するページを参照してください。

## <a name="see-also"></a>関連項目

- 「[カスタム ディレクティブ プロセッサの配置](../modeling/deploying-a-custom-directive-processor.md)」では、カスタム ディレクティブ プロセッサを登録する方法について説明します。
- 「[チュートリアル: カスタム ディレクティブ プロセッサを作成する](../modeling/walkthrough-creating-a-custom-directive-processor.md)」では、カスタム ディレクティブ プロセッサを作成する方法、ディレクティブ プロセッサを登録およびテストする方法、出力ファイルを HTML 形式で書式設定する方法について説明します。
