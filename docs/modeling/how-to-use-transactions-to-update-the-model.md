---
title: '方法: トランザクションを使用してモデルを更新する'
description: トランザクションではストアに加えられた変更がグループとして扱われること、およびトランザクションを使用してモデルを更新する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: e91e569573076d1614a9fa946b67f3bda01e6fba
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112390543"
---
# <a name="how-to-use-transactions-to-update-the-model"></a>方法: トランザクションを使用してモデルを更新する
トランザクションでは、ストアに加えられた変更がグループとして扱われます。 グループ化された変更は、単一のユニットとしてコミットまたはロールバックできます。

 プログラム コードで Visual Studio の視覚化およびモデリング SDK のストアの要素を変更、追加、または削除するときは、常にトランザクション内で実行する必要があります。 変更が発生するときに、ストアに関連付けられている <xref:Microsoft.VisualStudio.Modeling.Transaction> のアクティブなインスタンスが存在している必要があります。 これは、すべてのモデル要素、リレーションシップ、図形、図、およびそれらのプロパティに適用されます。

 トランザクション メカニズムは、一貫性のない状態を回避するのに役立ちます。 トランザクションの実行中にエラーが発生した場合は、すべての変更がロールバックされます。 ユーザーが元に戻すコマンドを実行した場合は、最近のトランザクションがそれぞれ単一の手順として処理されます。 最近の変更が別個のトランザクションに明示的に配置されていない限り、ユーザーは変更の一部を元に戻すことはできません。

## <a name="opening-a-transaction"></a>トランザクションを開く
 トランザクションを管理する最も便利な方法は、`try...catch` ステートメントの中で `using` ステートメントを使用することです。

```csharp
Store store; ...
try
{
  using (Transaction transaction =
    store.TransactionManager.BeginTransaction("update model"))
    // Outermost transaction must always have a name.
  {
    // Make several changes in Store:
    Person p = new Person(store);
    p.FamilyTreeModel = familyTree;
    p.Name = "Edward VI";
    // end of changes to Store

    transaction.Commit(); // Don't forget this!
  } // transaction disposed here
}
catch (Exception ex)
{
  // If an exception occurs, the Store will be
  // rolled back to its previous state.
}
```

 変更中に最後の `Commit()` を妨げる例外が発生した場合、ストアは前の状態にリセットされます。 これにより、エラーによってモデルが不整合な状態にならないようにすることができます。

 1 つのトランザクション内で任意の数の変更を行うことができます。 アクティブなトランザクション内で新しいトランザクションを開くことができます。 入れ子になったトランザクションは、親トランザクションが終了する前にコミットまたはロールバックする必要があります。 詳細については、<xref:Microsoft.VisualStudio.Modeling.Transaction.TransactionDepth%2A> プロパティの例を参照してください。

 変更を永続的なものにするには、トランザクションが破棄される前にトランザクションの `Commit` を実行する必要があります。 トランザクション内でキャッチされない例外が発生した場合、ストアは変更前の状態にリセットされます。

## <a name="rolling-back-a-transaction"></a>トランザクションのロールバック
 ストアをトランザクション実行前の状態のままにするか、その状態に戻すには、次のいずれかの方法を使用できます。

1. トランザクションのスコープ内でキャッチされない例外を発生させます。

2. トランザクションを明示的にロールバックします。

    ```csharp
    this.Store.TransactionManager.CurrentTransaction.Rollback();
    ```

## <a name="transactions-do-not-affect-non-store-objects"></a>トランザクションはストア以外のオブジェクトには影響しない
 トランザクションでは、ストアの状態のみが制御されます。 ファイル、データベース、または DSL 定義の外部で通常の型で宣言したオブジェクトなど、外部項目に対して行われた部分的な変更を元に戻すことはできません。

 例外によってストアとの一貫性を欠く変更が残る可能性がある場合は、その可能性を例外ハンドラーで処理する必要があります。 外部リソースとストア オブジェクトが確実に同期されるようにする方法の 1 つは、イベント ハンドラーを使用して、各外部オブジェクトをストア内の要素に結合することです。 詳細については、「[イベント ハンドラーによって変更がモデル外に反映される](../modeling/event-handlers-propagate-changes-outside-the-model.md)」を参照してください。

## <a name="rules-fire-at-the-end-of-a-transaction"></a>ルールはトランザクションの終了時に起動される
 トランザクションの最後、トランザクションが破棄される前に、ストア内の要素に関連付けられているルールが起動されます。 各ルールは、変更されたモデル要素に適用されるメソッドです。 たとえば、モデル要素が変更されたときに図形の状態を更新し、モデル要素が作成されたときに図形を作成する "修正" ルールがあります。 起動順序は指定されていません。 ルールによって行われた変更によって、別のルールを起動できます。

 独自のルールを定義できます。 ルールの詳細については、「[変更に対する応答と反映](../modeling/responding-to-and-propagating-changes.md)」を参照してください。

 元に戻す、やり直す、またはロールバックするためのコマンドを実行しても、ルールは起動されません。

## <a name="transaction-context"></a>トランザクション コンテキスト
 各トランザクションには、必要なすべての情報を格納できるディクショナリがあります。

 `store.TransactionManager`

 `.CurrentTransaction.TopLevelTransaction`

 `.Context.Add(aKey, aValue);`

 これは、ルール間で情報を転送する場合に特に便利です。

## <a name="transaction-state"></a>トランザクションの状態
 場合によっては、トランザクションを元に戻す操作またはやり直す操作によって変更が発生した場合に、変更が反映されないようにする必要があります。 これは、たとえば、ストア内の別の値を更新できるプロパティ値ハンドラーを記述した場合に発生する可能性があります。 元に戻す操作では、ストア内のすべての値が以前の状態にリセットされるので、更新された値を計算する必要はありません。 次のコードを使用します。

```csharp
if (!this.Store.InUndoRedoOrRollback) {...}
```

 ストアが最初にファイルから読み込まれたときにルールが起動される可能性があります。 これらの変更に対する応答を回避するには、以下を使用します。

```csharp
if (!this.Store.InSerializationTransaction) {...}
```
