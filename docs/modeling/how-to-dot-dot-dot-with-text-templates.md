---
title: '方法: テキスト テンプレートを使用する'
description: テキスト テンプレートを使用してテキストを生成する際によく寄せられる質問への回答について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: c5b5e1f4e7488253112eb33905fe534be3591782
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99934898"
---
# <a name="how-to--with-text-templates"></a>方法: テキスト テンプレートを使用する
Visual Studio のテキスト テンプレートは、任意の種類のテキストを生成する便利な方法を提供します。 テキスト テンプレートを使用して、アプリケーションの一部として実行時にテキストを生成したり、デザイン時にプロジェクト コードを生成したりすることができます。 このトピックでは、最もよく寄せられる操作方法に関する質問を まとめました。

 このトピックでは、箇条書きにした複数ある回答のそれぞれが代替候補です。

 テキスト テンプレートの概要については、「[コード生成と T4 テキスト テンプレート](../modeling/code-generation-and-t4-text-templates.md)」を参照してください。

## <a name="how-to-"></a>方法:

### <a name="generate-part-of-my-application-code"></a>アプリケーション コードの一部を生成する
 ファイルまたはデータベースに構成または "*モデル*" があります。 コードの 1 つ以上の部分が、そのモデルに依存しています。

- テキスト テンプレートからいくつかのコード ファイルを生成します。 詳細については、「[T4 テキスト テンプレートを使用したデザイン時コード生成](../modeling/design-time-code-generation-by-using-t4-text-templates.md)」と、[テンプレートの作成を開始するための最適な方法](#starting)に関する説明を参照してください。

### <a name="generate-files-at-run-time-passing-data-into-the-template"></a>実行時にファイルを生成し、テンプレートにデータを渡す
 アプリケーションでは、実行時に、標準テキストとデータの組み合わせが含まれる、レポートなどのテキスト ファイルが生成されます。 何百もの `write` ステートメントの記述を避ける必要があり ます。

- 実行時テキスト テンプレートをプロジェクトに追加します。 このテンプレートでは、コード内にクラスを作成します。このクラスをインスタンス化して、テキストを生成するために使用できます。 コンストラクター パラメーターでデータを渡すことができます。 詳細については、「[T4 テキスト テンプレートを使用した実行時テキスト生成](../modeling/run-time-text-generation-with-t4-text-templates.md)」を参照してください。

- 実行時にのみ使用できるテンプレートから生成する場合は、標準のテキスト テンプレートを使用できます。 Visual Studio 拡張機能を作成する場合は、テキスト テンプレート サービスを呼び出すことができます。 詳細については、「[VS 拡張機能でのテキスト変換の呼び出し](../modeling/invoking-text-transformation-in-a-vs-extension.md)」を参照してください。 他のコンテキストでは、テキスト テンプレート エンジンを使用できます。 詳細については、「<xref:Microsoft.VisualStudio.TextTemplating.Engine?displayProperty=fullName>」を参照してください。

     これらのテンプレートにパラメーターを渡すには、\<#@parameter#> ディレクティブを使用します。 詳細については、「[T4 パラメーター ディレクティブ](../modeling/t4-parameter-directive.md)」を参照してください。

### <a name="read-another-project-file-from-a-template"></a>テンプレートから別のプロジェクト ファイルを読み取る
 同じ Visual Studio プロジェクトからテンプレートとしてファイルを読み取るには:

- `hostSpecific="true"` ディレクティブに `<#@template#>` を挿入します。

     コードで、`this.Host.ResolvePath(filename)` を使用してファイルの完全なパスを取得します。

### <a name="invoke-methods-from-a-template"></a>テンプレートからメソッドを呼び出す

メソッドが既に存在している場合 (たとえば、.NET クラス):

- \<#@assembly#> ディレクティブを使用してアセンブリを読み込み、\<#@import#> を使用して名前空間コンテキストを設定します。 詳細については、「[T4 インポート ディレクティブ](../modeling/t4-import-directive.md)」を参照してください。

   アセンブリとインポート ディレクティブの同じセットを頻繁に使用する場合は、ディレクティブ プロセッサの記述を検討します。 各テンプレートでは、ディレクティブ プロセッサを呼び出すことができます。このプロセッサは、アセンブリとモデル ファイルを読み込み、名前空間コンテキストを設定できます。 詳細については、[カスタム T4 テキスト テンプレート ディレクティブ プロセッサの作成](../modeling/creating-custom-t4-text-template-directive-processors.md)に関するページを参照してください。

メソッドを自分で作成する場合:

- 実行時テキスト テンプレートを記述する場合は、実行時テキスト テンプレートと同じ名前を持つ部分クラス定義を記述します。 このクラスに追加メソッドを追加します。

- メソッド、プロパティ、プライベート クラスを宣言できるクラス機能コントロール ブロック `<#+ ... #>` を記述します。 テキスト テンプレートがコンパイルされると、クラスに変換されます。 標準のコントロール ブロック `<#...#>` とテキストは 1 つのメソッドに変換され、クラス機能ブロックは個別のメンバーとして挿入されます。 詳細については、「[テキスト テンプレートのコントロール ブロック](../modeling/text-template-control-blocks.md)」を参照してください。

   クラス機能として定義されたメソッドには、埋め込みテキスト ブロックを含めることもできます。

   クラス機能を別のファイルに配置することを検討します。このファイルは、1 つまたは複数のテンプレート ファイルに `<#@include#>` することができます。

- メソッドを別のアセンブリ (クラス ライブラリ) に記述し、テンプレートから呼び出します。 `<#@assembly#>` ディレクティブを使用してアセンブリを読み込み、`<#@import#>` を使用して名前空間コンテキストを設定します。 デバッグ中にアセンブリをリビルドするには、Visual Studio を停止して再起動する必要があることに注意してください。 詳細については、「[T4 テキスト テンプレートのディレクティブ](../modeling/t4-text-template-directives.md)」を参照してください。

### <a name="generate-many-files-from-one-model-schema"></a>1 つのモデル スキーマから多数のファイルを生成する
 同じ XML またはデータベース スキーマを持つモデルからファイルを生成することが多い場合:

- ディレクティブ プロセッサの記述を検討します。 これにより、各テンプレートの複数のアセンブリ ステートメントとインポート ステートメントを 1 つのカスタム ディレクティブで置き換えることができます。 ディレクティブ プロセッサでは、モデル ファイルを読み込んで解析することもできます。 詳細については、[カスタム T4 テキスト テンプレート ディレクティブ プロセッサの作成](../modeling/creating-custom-t4-text-template-directive-processors.md)に関するページを参照してください。

### <a name="generate-files-from-a-complex-model"></a>複雑なモデルからファイルを生成する

- モデルを表現するために、ドメイン固有言語 (DSL) の作成を検討します。 モデル内の要素の名前を反映する型とプロパティを使用するため、テンプレートの記述が非常に簡単になります。 ファイルを解析したり、XML ノードを移動したりする必要はありません。 次に例を示します。

     `foreach (Book book in this.Library) { ... }`

     詳細については、「[ドメイン固有言語の概要](../modeling/getting-started-with-domain-specific-languages.md)」および「[ドメイン固有言語からのコード生成](../modeling/generating-code-from-a-domain-specific-language.md)」を参照してください。

### <a name="get-data-from-visual-studio"></a>Visual Studio からデータを取得する
 Visual Studio で提供されるサービスを使用するには、`hostSpecific` 属性を設定し、`EnvDTE` アセンブリを読み込みます。 次に例を示します。

```csharp
<#@ template hostspecific="true" language="C#" #>
<#@ output extension=".txt" #>
<#@ assembly name="EnvDTE" #>
<#
  IServiceProvider serviceProvider = (IServiceProvider)this.Host;
  EnvDTE.DTE dte = (EnvDTE.DTE) serviceProvider.GetService(typeof(EnvDTE.DTE));
#>

Number of projects in this VS solution:  <#= dte.Solution.Projects.Count #>
```

### <a name="execute-text-templates-in-the-build-process"></a>ビルド プロセスでテキスト テンプレートを実行する

- 詳細については、「[ビルド処理でのコード生成](../modeling/code-generation-in-a-build-process.md)」を参照してください。

## <a name="more-general-questions"></a>その他の一般的な質問

### <a name="what-is-the-best-way-to-start-writing-a-text-template"></a><a name="starting"></a>テキスト テンプレートの記述を開始する最適な方法は何ですか?

1. 生成されるファイルの具体的な例を記述します。

2. それをテキスト テンプレートに変換するため、`<#@template #>` ディレクティブと、入力ファイルまたはモデルを読み込むために必要なディレクティブとコードを挿入します。

3. ファイルの一部を式およびコード ブロックで段階的に置換します。

### <a name="what-is-a-model"></a>"モデル" とは何ですか?

- テンプレートによって読み取られた入力です。 ファイルまたはデータベースに存在する可能性があります。 XML、Visio 図面、ドメイン固有言語 (DSL)、UML モデルの場合もあれば、プレーン テキストである場合もあります。 複数のファイルにわたって分散できます。 通常、複数のテンプレートで 1 つのモデルを読み取ります。

     "モデル" という用語の意味は、生成されたプログラム コードや他のファイルよりも、ビジネスの一部をより直接的に表現するということです。 たとえば、生成されたソフトウェアが監視する通信ネットワークの計画を表現することがあります。

### <a name="what-is-the-benefit-of-using-text-templates"></a>テキスト テンプレートを使用する利点は何ですか?
 通常は、1 つのモデルから複数のコードまたは他のファイルを生成します。 このモデルは、生成されたコードと比べて、要求をより直接的に表現します。 実装の詳細が省略され、コードではなく要件の観点で記述されます。 要件が変更された場合 (通常は変更されるものです)、プログラム コードのさまざまな部分よりも簡単かつ確実にモデルを更新できます。

 このため、コード生成はアジャイル開発手法の観点から重要なツールです。

### <a name="what-best-practices-are-there-for-text-templates"></a>テキスト テンプレートには、どのような "ベスト プラクティス" がありますか?

- 詳細については、「[T4 テキスト テンプレートの記述に関するガイドライン](../modeling/guidelines-for-writing-t4-text-templates.md)」を参照してください。

### <a name="what-is-t4"></a>"T4" とは何ですか?

- ここで説明されている Visual Studio テキストテンプレート機能の別名です。 公開されていなかった以前のバージョンでは、"Text Template Transformation" (テキスト テンプレート変換) の省略形でした。
