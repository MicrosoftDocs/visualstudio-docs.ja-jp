---
title: ドメイン固有言語をカスタマイズする
description: カスタム コードを使用して、ドメイン固有言語 (DSL) でモデルへのアクセス、変更、または作成を行う方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, programming
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 2231ef94bee01558e2c26899a5d9a0c855489e94
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112388049"
---
# <a name="write-code-to-customize-a-domain-specific-language"></a>ドメイン固有言語をカスタマイズするコードを記述する

このセクションでは、カスタム コードを使用して、ドメイン固有言語でモデルへのアクセス、変更、または作成を行う方法について説明します。

DSL で動作するコードを記述できるコンテキストがいくつかあります。

- **カスタム コマンド。** ダイアグラムを右クリックして、ユーザーが呼び出すことができるコマンドを作成できます。このコマンドでは、モデルを変更できます。 詳細については、「[方法: ショートカット メニューにコマンドを追加する](../modeling/how-to-add-a-command-to-the-shortcut-menu.md)」を参照してください。

- **検証。** モデルが正しい状態であることを確認するコードを記述できます。 詳細については、「[ドメイン固有言語における検証](../modeling/validation-in-a-domain-specific-language.md)」を参照してください。

- **既定の動作のオーバーライド。** DslDefinition.dsl から生成されるコードの多くの側面を変更できます。 詳細については、「[生成されたクラスをオーバーライドして拡張する](../modeling/overriding-and-extending-the-generated-classes.md)」を参照してください。

- **テキスト変換。** モデルにアクセスするコードを含むテキスト テンプレートを作成し、テキスト ファイルを生成することができます。たとえば、プログラム コードを生成します。 詳細については、「[ドメイン固有言語からのコード生成](../modeling/generating-code-from-a-domain-specific-language.md)」を参照してください。

- **その他の Visual Studio 拡張機能。** モデルの読み取りと変更を行う個別の VSIX 拡張機能を作成できます。 詳細については、「[方法: プログラム コード内のファイルからモデルを開く](../modeling/how-to-open-a-model-from-file-in-program-code.md)」を参照してください。

DslDefinition.dsl で定義したクラスのインスタンスは、"*メモリ内ストア*" (IMS) または "*ストア*" と呼ばれるデータ構造に保持されます。 DSL で定義するクラスでは、常にコンストラクターの引数としてストアを受け取ります。 たとえば、DSL で次のように Example というクラスを定義しているとします。

`Example element = new Example (theStore);`

(通常のオブジェクトとしてではなく) ストアにオブジェクトを保持すると、いくつかの利点があります。

- **Transactions**。 一連の関連する変更を 1 つのトランザクションにグループ化できます。

     `using (Transaction t = store.TransactionManager.BeginTransaction("updates"))`

     `{`

     `// make several changes to Store elements here`

     `t.Commit();`

     `}`

     変更中に例外が発生し、最終的な Commit() が実行されない場合、ストアは以前の状態にリセットされます。 これにより、エラーによってモデルが不整合な状態にならないようにすることができます。 詳細については、[プログラム コードにおけるモデル内の移動およびモデルの更新](../modeling/navigating-and-updating-a-model-in-program-code.md)に関するページを参照してください。

- **2 項リレーションシップ**。 2 つのクラス間のリレーションシップを定義する場合、両端のインスタンスには、もう一方の端を指すプロパティがあります。 2 つの端は常に同期されます。 たとえば、Parents と Children という名前のロールを持つ親リレーションシップを定義する場合、次のように記述できます。

     `John.Children.Add(Mary)`

     次の式はどちらも true になります。

     `John.Children.Contains(Mary)`

     `Mary.Parents.Contains(John)`

     次のように記述して同じ効果を得ることもできます。

     `Mary.Parents.Add(John)`

     詳細については、[プログラム コードにおけるモデル内の移動およびモデルの更新](../modeling/navigating-and-updating-a-model-in-program-code.md)に関するページを参照してください。

- **ルールとイベント**。 指定された変更が行われるたびに起動するルールを定義できます。 たとえば、モデル要素を使用して、ダイアグラムの図形を最新の状態に保つために、ルールが使用されます。 詳細については、[変更内容への対応および変更内容の反映](../modeling/responding-to-and-propagating-changes.md)に関するページを参照してください。

- **シリアル化**。 ストアには、ファイルに格納されているオブジェクトをシリアル化するための標準的な方法が用意されています。 シリアル化および逆シリアル化のルールをカスタマイズできます。 詳細については、「[ファイル格納処理および XML シリアル化処理をカスタマイズする](../modeling/customizing-file-storage-and-xml-serialization.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [ドメイン固有言語のカスタマイズおよび拡張](../modeling/customizing-and-extending-a-domain-specific-language.md)