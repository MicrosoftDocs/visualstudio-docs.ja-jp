---
title: コード生成と T4 テキスト テンプレート
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-modeling
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.TextTemplating.TextTemplating
helpviewer_keywords:
- generating text
- .tt files
- code generation
- text templates
- generating code
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: fa6195a531c74aebbcb7884cc8e3158df6b9ca96
ms.sourcegitcommit: e9d1018a01af62c3dc5aeb6b325faba7e20bd496
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/28/2018
ms.locfileid: "37089400"
---
# <a name="code-generation-and-t4-text-templates"></a>コード生成と T4 テキスト テンプレート

Visual Studio で、 *T4 テキスト テンプレート*テキスト ブロックとテキスト ファイルを生成できる制御ロジックの組み合わせです。 制御ロジックは、 [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] または [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]のプログラム コードのフラグメントとして記述します。 Visual Studio 2015 Update 2 以降では、T4 テンプレート ディレクティブで C# バージョン 6.0 の機能を使用できます。 Web ページ、リソース ファイル、任意の言語のプログラム ソース コードなど、あらゆる種類のテキスト ファイルを生成できます。

T4 テキスト テンプレートの 2 種類があります: 時およびデザイン時に実行します。

## <a name="run-time-t4-text-templates"></a>実行時 T4 テキスト テンプレート

呼ばれます '前処理された' テンプレート、実行時テンプレートは、通常は、出力の一部として、テキスト文字列を生成するために、アプリケーションで実行されます。 たとえば、次のように HTML ページを定義するテンプレートを作成できます。

```
<html><body>
 The date and time now is: <#= DateTime.Now #>
</body></html>
```

このテンプレートは、生成される出力に似ている点にご注目ください。 このように、テンプレートは結果の出力に似ているため、テンプレートを変更する場合に誤りを防ぐことができます。

また、テンプレートにはプログラム コードのフラグメントも含まれます。 これらのフラグメントを使用して、テキストのセクションの繰り返し、条件付きセクションの作成、アプリケーションのデータの表示を行うことができます。

出力を生成するには、テンプレートによって生成される関数をアプリケーションで呼び出します。 例えば:

```csharp
string webResponseText = new MyTemplate().TransformText();
```

アプリケーションは、Visual Studio をインストールしていないコンピューターで実行できます。

実行時テンプレートを作成するには、 **前処理されたテキスト テンプレート** ファイルをプロジェクトに追加します。 または、プレーンテキスト ファイルを追加し、 **[カスタム ツール]** プロパティを **TextTemplatingFilePreprocessor**に設定することもできます。

詳細については、次を参照してください。 [T4 テキスト テンプレートを使用した実行時テキスト生成](../modeling/run-time-text-generation-with-t4-text-templates.md)します。 テンプレートの構文の詳細については、次を参照してください。 [T4 テキスト テンプレートの作成](../modeling/writing-a-t4-text-template.md)です。

## <a name="design-time-t4-text-templates"></a>デザイン時 T4 テキスト テンプレート

デザイン時テンプレートは、ソース コードの一部と、アプリケーションの他のリソースを定義します。 通常、1 つの入力ファイルまたはデータベースのデータを読み取るいくつかのテンプレートを使用しの一部を生成、 *.cs*、 *.vb*、または他のソース ファイル。 テンプレートごとに 1 つのファイルが生成されます。 Visual Studio または MSBuild 内で実行されます。

たとえば、入力データが構成データの XML ファイルであるとします。 開発中に XML ファイルを編集するたびに、テキスト テンプレートには、アプリケーション コードの一部が再生成します。 テンプレートの例を次に示します。

```
<#@ output extension=".cs" #>
<#@ assembly name="System.Xml" #>
<#
 System.Xml.XmlDocument configurationData = ...; // Read a data file here.
#>
namespace Fabrikam.<#= configurationData.SelectSingleNode("jobName").Value #>
{
  ... // More code here.
}
```

生成された XML ファイル内の値に応じて *.cs*ファイルは、次のようになります。

```
namespace Fabrikam.FirstJob
{
  ... // More code here.
}
```

別の例として、入力がビジネス アクティビティのワークフローの図であるとします。 ユーザーがビジネス ワークフローを変更した場合や、別のワークフローを使用する新しいユーザーとの作業を開始する場合は、新しいモデルに合わせてコードを簡単に再生成できます。

デザイン時テンプレートを使用すると、要件が変わったときに構成をすばやく変更できるようになり、変更の信頼性も高まります。 ワークフローの例のように、ビジネス要件の観点で入力を定義するのが一般的です。 このように定義すると、変更点についてユーザーと共に検討しやすくなります。 そのため、デザイン時テンプレートは、アジャイル開発プロセスにおける有用なツールとなります。

デザイン時テンプレートを作成するには、 **テキスト テンプレート** ファイルをプロジェクトに追加します。 または、プレーンテキスト ファイルを追加し、 **[カスタム ツール]** プロパティを **TextTemplatingFileGenerator**に設定することもできます。

詳細については、次を参照してください。 [T4 テキスト テンプレートを使用したデザイン時コード生成](../modeling/design-time-code-generation-by-using-t4-text-templates.md)します。 テンプレートの構文の詳細については、次を参照してください。 [T4 テキスト テンプレートの作成](../modeling/writing-a-t4-text-template.md)です。

> [!NOTE]
> 1 つ以上のテンプレートで読み込まれるデータを示す際に、 *モデル* という用語を使用する場合があります。 モデルはどのような形式でもかまいません。あらゆる種類のファイルまたはデータベースを使用できます。 必ずしも UML モデルやドメイン固有言語モデルである必要はありません。 'モデル' は、コードのようなものではなく、ビジネス概念の観点でデータを定義できることを示します。

テキスト テンプレート変換機能は、 *T4*と名付けられています。

## <a name="see-also"></a>関連項目

- [ドメイン固有言語からコードを生成する](../modeling/generating-code-from-a-domain-specific-language.md)
