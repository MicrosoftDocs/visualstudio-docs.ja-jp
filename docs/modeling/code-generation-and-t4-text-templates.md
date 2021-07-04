---
title: コード生成と T4 テキスト テンプレート
description: テキスト ブロックと制御ロジックが混在する T4 テキスト テンプレートを使用してテキスト ファイルを生成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: overview
f1_keywords:
- VS.ToolsOptionsPages.TextTemplating.TextTemplating
helpviewer_keywords:
- generating text
- .tt files
- code generation
- text templates
- generating code
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 76714be09c38f6426626e94ee7734873c823f704
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112389775"
---
# <a name="code-generation-and-t4-text-templates"></a>コード生成と T4 テキスト テンプレート

Visual Studio の "*T4 テキスト テンプレート*" は、テキスト ファイルを生成できる、テキスト ブロックと制御ロジックが混在するファイルです。 制御ロジックは、 [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] または [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]のプログラム コードのフラグメントとして記述します。 Visual Studio 2015 Update 2 以降では、T4 テンプレート ディレクティブで C# バージョン 6.0 の機能を使用できます。 Web ページ、リソース ファイル、任意の言語のプログラム ソース コードなど、あらゆる種類のテキスト ファイルを生成できます。

T4 テキスト テンプレートには、実行時とデザイン時の 2 種類があります。

## <a name="run-time-t4-text-templates"></a>実行時 T4 テキスト テンプレート

実行時テンプレートは '前処理された' テンプレートとも呼ばれ、通常、出力の一部としてテキスト文字列を生成するために、アプリケーションで実行されます。 たとえば、次のように HTML ページを定義するテンプレートを作成できます。

```
<html><body>
 The date and time now is: <#= DateTime.Now #>
</body></html>
```

このテンプレートは、生成される出力に似ている点にご注目ください。 このように、テンプレートは結果の出力に似ているため、テンプレートを変更する場合に誤りを防ぐことができます。

また、テンプレートにはプログラム コードのフラグメントも含まれます。 これらのフラグメントを使用して、テキストのセクションの繰り返し、条件付きセクションの作成、アプリケーションのデータの表示を行うことができます。

出力を生成するには、テンプレートによって生成される関数をアプリケーションで呼び出します。 次に例を示します。

```csharp
string webResponseText = new MyTemplate().TransformText();
```

アプリケーションは、Visual Studio がインストールされていないコンピューターでも実行できます。

実行時テンプレートを作成するには、 **前処理されたテキスト テンプレート** ファイルをプロジェクトに追加します。 または、プレーンテキスト ファイルを追加し、 **[カスタム ツール]** プロパティを **TextTemplatingFilePreprocessor** に設定することもできます。

詳細については、「[T4 テキスト テンプレートを使用した実行時テキスト生成](../modeling/run-time-text-generation-with-t4-text-templates.md)」を参照してください。 テンプレートの構文の詳細については、「[T4 テキスト テンプレートの作成](../modeling/writing-a-t4-text-template.md)」を参照してください。

## <a name="design-time-t4-text-templates"></a>デザイン時 T4 テキスト テンプレート

デザイン時テンプレートは、アプリケーションのソース コードや他のリソースの一部を定義します。 通常は、複数のテンプレートを使用して 1 つの入力ファイルまたはデータベースのデータを読み込み、一部の *.cs*、 *.vb* などのソース ファイルを生成します。 テンプレートごとに 1 つのファイルが生成されます。 これらは、Visual Studio または MSBuild 内で実行されます。

たとえば、入力データが構成データの XML ファイルであるとします。 開発中に XML ファイルを編集するたびに、テキスト テンプレートによって、アプリケーション コードの一部が再生成されます。 テンプレートの例を次に示します。

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

XML ファイルの値に応じて、次のような *.cs* ファイルが生成されます。

```
namespace Fabrikam.FirstJob
{
  ... // More code here.
}
```

別の例として、入力がビジネス アクティビティのワークフローの図であるとします。 ユーザーがビジネス ワークフローを変更した場合や、別のワークフローを使用する新しいユーザーとの作業を開始する場合は、新しいモデルに合わせてコードを簡単に再生成できます。

デザイン時テンプレートを使用すると、要件が変わったときに構成をすばやく変更できるようになり、変更の信頼性も高まります。 ワークフローの例のように、ビジネス要件の観点で入力を定義するのが一般的です。 このように定義すると、変更点についてユーザーと共に検討しやすくなります。 そのため、デザイン時テンプレートは、アジャイル開発プロセスにおける有用なツールとなります。

デザイン時テンプレートを作成するには、 **テキスト テンプレート** ファイルをプロジェクトに追加します。 または、プレーンテキスト ファイルを追加し、 **[カスタム ツール]** プロパティを **TextTemplatingFileGenerator** に設定することもできます。

詳細については、「[T4 テキスト テンプレートを使用したデザイン時コード生成](../modeling/design-time-code-generation-by-using-t4-text-templates.md)」を参照してください。 テンプレートの構文の詳細については、「[T4 テキスト テンプレートの作成](../modeling/writing-a-t4-text-template.md)」を参照してください。

> [!NOTE]
> 1 つ以上のテンプレートで読み込まれるデータを示す際に、 *モデル* という用語を使用する場合があります。 モデルはどのような形式でもかまいません。あらゆる種類のファイルまたはデータベースを使用できます。 必ずしも UML モデルやドメイン固有言語モデルである必要はありません。 'モデル' は、コードのようなものではなく、ビジネス概念の観点でデータを定義できることを示します。

テキスト テンプレート変換機能は、 *T4* と名付けられています。

## <a name="see-also"></a>関連項目

- [ドメイン固有言語からコードを生成する](../modeling/generating-code-from-a-domain-specific-language.md)
