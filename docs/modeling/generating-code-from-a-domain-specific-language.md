---
title: ドメイン固有言語からのコード生成
description: ドメイン固有言語ツールが、モデルで表されるデータからコード、ドキュメント、およびその他の成果物を生成するための強力な方法を提供するしくみについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 6eee4fe2400bac1534bdc9c208fa60d9af8d3cfd
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112388842"
---
# <a name="generating-code-from-a-domain-specific-language"></a>ドメイン固有言語からのコード生成

Microsoft [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] では、モデルで表されるデータからコード、ドキュメント、構成ファイル、およびその他の成果物を生成するための強力な方法を提供しています。 [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] を使用すると、データを表すクラスのセットを作成できます。また、名前とプロパティにそのデータが反映されたクラスにテキスト テンプレートを記述することもできます。

たとえば、Fabrikam には、顧客名と電子メールアドレスの XML ファイルがあります。 開発者は、Customer をクラスとし、プロパティとして名と電子メールを含むモデルを作成します。 データを処理するために複数のテキスト テンプレートを記述します。このフラグメントを使用すると、すべての顧客のテーブルが HTML ページの一部として生成されます。

```
<table>
<# foreach (Customer c in ContactList) {  #>
  <tr><td> <#= c.FullName #> </td>
      <td> <#= c.EmailAddress #> </td> </tr>
<# } #>  </table>
```

顧客データベースが処理されると、XML ファイルがモデル ストアに読み込まれます。 [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] を使用して作成された *ディレクティブ プロセッサ* を使用すると、テキスト テンプレート内のコードで Customer クラスを使用できるようになります。 多くのテキスト テンプレートは、同じストアに対して実行できます。

テキストテンプレートは、[!INCLUDE[dsl](../modeling/includes/dsl_md.md)] に不可欠です。 これらは、ツールを Visual Studio と統合するために使用される VSPackage およびコントロールに加えて、ドメイン モデルの要素のソース コードを生成するために使用されます。

このセクションでは、[!INCLUDE[dsl](../modeling/includes/dsl_md.md)] で使用されるテキスト テンプレートを作成、変更、およびデバッグするためのいくつかの方法について説明します。

## <a name="in-this-section"></a>このセクションの内容

[テキスト テンプレートからモデルへのアクセス](../modeling/accessing-models-from-text-templates.md)\
テキスト テンプレートでドメイン固有言語を参照する方法についての基本的な情報を提供します。

[チュートリアル: モデルにアクセスするテキスト テンプレートのデバッグ](../modeling/walkthrough-debugging-a-text-template-that-accesses-a-model.md)\
ドメイン固有言語を参照するテキスト テンプレートでトラブルシューティングとデバッグを行う方法について説明します。

[チュートリアル: 生成済みディレクティブ プロセッサへのホストの接続](../modeling/walkthrough-connecting-a-host-to-a-generated-directive-processor.md)\
生成されたディレクティブ プロセッサにカスタム ホストを接続する方法について説明します。

[DslTextTransform コマンド](../modeling/the-dsltexttransform-command.md)\
ドメイン固有言語を参照するテキスト テンプレートのコマンド ラインで TextTransform 実行可能ファイルを実行するコマンド ファイルについて説明します。

## <a name="reference"></a>関連項目

[T4 テキスト テンプレートの作成](../modeling/writing-a-t4-text-template.md)\
テキスト テンプレートのディレクティブとコントロール ブロックの構文を示します。

## <a name="related-sections"></a>関連項目

[T4 テキスト テンプレートを使用したデザイン時コード生成](../modeling/design-time-code-generation-by-using-t4-text-templates.md)\
テキスト テンプレート変換プロセスを説明します。

[ビルド処理でのコード生成](../modeling/code-generation-in-a-build-process.md)\
ビルド サーバーで DSL からファイルを生成する場合は、このトピックをお読みください。
