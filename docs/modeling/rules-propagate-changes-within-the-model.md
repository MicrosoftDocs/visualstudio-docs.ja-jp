---
title: 規則によって変更内容がモデル内に反映される
description: 視覚化およびモデリング SDK (VMSDK) で、ある要素から別の要素に変更を反映するためのストア ルールを作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, programming domain models
- Domain-Specific Language, rules
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: bde67bd8375e3752370b3b815f8ed155d3123741
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112387594"
---
# <a name="rules-propagate-changes-within-the-model"></a>規則によって変更内容がモデル内に反映される
視覚化およびモデリング SDK (VMSDK) で、ある要素から別の要素に変更を反映するためのストア ルールを作成することができます。 ストア内のいずれかの要素に変更が加えられると、通常、最も外側のトランザクションがコミットされるときに、規則が実行されるようにスケジュールされます。 要素の追加や削除など、さまざまな種類のイベントに対して異なる種類のルールがあります。 ルールは、特定の種類の要素、シェイプ、または図に適用できます。 多くの組み込み機能がルールによって定義されています。たとえば、ルールによって、モデルが変更されたときに図が更新されます。 独自の規則を追加することで、ドメイン固有言語をカスタマイズできます。

 ストア ルールは、ストア内の変更 (モデル要素、リレーションシップ、シェイプ、コネクタ、およびそれらのドメイン プロパティの変更) を反映する場合に特に便利です。 ユーザーが [元に戻す] または [再実行] コマンドを呼び出しても、ルールは実行されません。 代わりに、トランザクション マネージャーによって、ストアの内容が正しい状態に復元されます。 ストアの外部のリソースに変更を反映する場合は、ストア イベントを使用します。 詳細については、「[イベント ハンドラーによって変更がモデル外に反映される](../modeling/event-handlers-propagate-changes-outside-the-model.md)」を参照してください。

 たとえば、ユーザー (またはコード) が型 ExampleDomainClass の新しい要素を作成するたびに、別の型の他の要素がモデルの別の部分に作成されるように指定したいとします。 AddRule を記述して、それを ExampleDomainClass に関連付けることができます。 ルールにコードを記述して、追加の要素を作成します。

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using Microsoft.VisualStudio.Modeling;

namespace ExampleNamespace
{
 // Attribute associates the rule with a domain class:
 [RuleOn(typeof(ExampleDomainClass), FireTime=TimeToFire.TopLevelCommit)]
 // The rule is a class derived from one of the abstract rules:
 class MyAddRule : AddRule
 {
  // Override the abstract method:
  public override void ElementAdded(ElementAddedEventArgs e)
  {
    base.ElementAdded(e);
    ExampleDomainClass element = e.ModelElement;
    Store store = element.Store;
    // Ignore this call if we're currently loading a model:
    if (store.TransactionManager.CurrentTransaction.IsSerializing)
       return;

    // Code here propagates change as required - for example:
      AnotherDomainClass echo = new AnotherDomainClass(element.Partition);
      echo.Name = element.Name;
      echo.Parent = element.Parent;
    }
  }
 // The rule must be registered:
 public partial class ExampleDomainModel
 {
   protected override Type[] GetCustomDomainModelTypes()
   {
     List<Type> types = new List<Type>(base.GetCustomDomainModelTypes());
     types.Add(typeof(MyAddRule));
     // If you add more rules, list them here.
     return types.ToArray();
   }
 }
}
```

> [!NOTE]
> ルールのコードは、ストア内の要素の状態のみを変更する必要があります。つまり、ルールでは、モデル要素、リレーションシップ、シェイプ、コネクタ、図、またはそれらのプロパティのみを変更する必要があります。 ストアの外部のリソースに変更を反映する場合は、ストア イベントを定義します。 詳細については、「[イベント ハンドラーによって変更がモデル外に反映される](../modeling/event-handlers-propagate-changes-outside-the-model.md)」を参照してください。

### <a name="to-define-a-rule"></a>ルールを定義するには

1. `RuleOn` 属性をプレフィックスとして付けるクラスとしてルールを定義します。 属性により、ルールがドメイン クラス、リレーションシップ、または図要素の 1 つに関連付けられます。 ルールは、抽象型を含むこのクラスのすべてのインスタンスに適用されます。

2. ドメイン モデル クラスの `GetCustomDomainModelTypes()` によって返されるセットに追加して、ルールを登録します。

3. いずれかの抽象ルール クラスからルール クラスを派生させ、実行メソッドのコードを記述します。

   以降のセクションで、これらの手順について詳しく説明します。

### <a name="to-define-a-rule-on-a-domain-class"></a>ドメイン クラスでルールを定義するには

- 次のようにカスタム コード ファイルで、クラスを定義し、<xref:Microsoft.VisualStudio.Modeling.RuleOnAttribute> 属性でプレフィックスを付けます。

    ```csharp
    [RuleOn(typeof(ExampleElement),
         // Usual value - but required, because it is not the default:
         FireTime = TimeToFire.TopLevelCommit)]
    class MyRule ...

    ```

- 最初のパラメーターのサブジェクトの種類には、ドメイン クラス、ドメイン リレーションシップ、シェイプ、コネクタ、または図を使用できます。 通常は、ドメイン クラスとリレーションシップにルールを適用します。

     通常、`FireTime` は `TopLevelCommit` です。 これにより、トランザクションのすべての主要な変更が行われた後にのみ、ルールが実行されるようになります。 代替手段は Inline であり、変更後すぐにルールが実行されます。また LocalCommit では、現在のトランザクションの最後 (最も外側ではない可能性があります) にルールを実行します。 ルールの優先度を設定して、キュー内での順序に影響を与えることもできますが、これは必要な結果を実現する信頼性の低い方法です。

- サブジェクトの種類として抽象クラスを指定できます。

- このルールは、サブジェクト クラスのすべてのインスタンスに適用されます。

- `FireTime` の規定値は TimeToFire.TopLevelCommit です。 これにより、最も外側のトランザクションがコミットされるときにルールが実行されます。 別の方法として、TimeToFire.Inline があります。 これにより、トリガー イベントの直後にルールが実行されます。

### <a name="to-register-the-rule"></a>ルールを登録するには

- ドメイン モデルで `GetCustomDomainModelTypes` によって返される型の一覧に、ルール クラスを追加します。

    ```csharp
    public partial class ExampleDomainModel
     {
       protected override Type[] GetCustomDomainModelTypes()
       {
         List<Type> types = new List<Type>(base.GetCustomDomainModelTypes());
         types.Add(typeof(MyAddRule));
         // If you add more rules, list them here.
         return types.ToArray();
       }
     }

    ```

- ドメイン モデル クラスの名前がわからない場合は、ファイル **Dsl\GeneratedCode\DomainModel.cs** を検索してください

- DLS プロジェクト内のカスタム コード ファイルに次のコードを記述します。

### <a name="to-write-the-code-of-the-rule"></a>ルールのコードを記述するには

- 次のいずれかの基底クラスからルール クラスを派生させます。

  | 基本クラス | トリガー |
  |-|-|
  | <xref:Microsoft.VisualStudio.Modeling.AddRule> | 要素、リンク、またはシェイプが追加されます。<br /><br /> 新しい要素に加えて新しいリレーションシップを検出する場合に使用します。 |
  | <xref:Microsoft.VisualStudio.Modeling.ChangeRule> | ドメイン プロパティの値が変更されます。 メソッド引数により古い値と新しい値が返されます。<br /><br /> シェイプの場合、このルールは、シェイプが移動された場合に組み込み `AbsoluteBounds` プロパティが変更されたときにトリガーされます。<br /><br /> 多くの場合、プロパティ ハンドラーで `OnValueChanged` または `OnValueChanging` をオーバーライドする方が便利です。 これらのメソッドは、変更の直前と直後に呼び出されます。 これに対し、ルールは通常、トランザクションの最後に実行されます。 詳細については、「[ドメイン プロパティ値変更ハンドラー](../modeling/domain-property-value-change-handlers.md)」を参照してください。 **注:** このルールは、リンクが作成または削除されたときにはトリガーされません。 代わりに、ドメイン リレーションシップに対して `AddRule` と `DeleteRule` を記述します。 |
  | <xref:Microsoft.VisualStudio.Modeling.DeletingRule> | 要素またはリンクが削除されようとしているときにトリガーされます。 ModelElement.IsDeleting プロパティは、トランザクションが終了するまで true になります。 |
  | <xref:Microsoft.VisualStudio.Modeling.DeleteRule> | 要素またはリンクが削除されたときに実行されます。 このルールは、他のすべてのルールが実行された後 (DeletingRules を含む) に実行されます。 ModelElement.IsDeleting が false で、ModelElement.IsDeleted が true になっています。 後続の元に戻す操作を可能にするために、要素は実際にはメモリから削除されませんが、Store.ElementDirectory からは削除されます。 |
  | <xref:Microsoft.VisualStudio.Modeling.MoveRule> | あるストア パーティションから別のものに要素が移動されます。<br /><br /> (これは、シェイプのグラフィカルな位置には関係していないことに注意してください)。 |
  | <xref:Microsoft.VisualStudio.Modeling.RolePlayerChangeRule> | このルールはドメイン リレーションシップにのみ適用されます。 モデル要素をリンクのどちらかの末尾に明示的に割り当てると、トリガーされます。 |
  | <xref:Microsoft.VisualStudio.Modeling.RolePlayerPositionChangeRule> | リンクの MoveBefore または MoveToIndex メソッドを使用して、要素との間のリンクの順序が変更されたときにトリガーされます。 |
  | <xref:Microsoft.VisualStudio.Modeling.TransactionBeginningRule> | トランザクションが作成されるときに実行されます。 |
  | <xref:Microsoft.VisualStudio.Modeling.TransactionCommittingRule> | トランザクションがコミットされようとしているときに実行されます。 |
  | <xref:Microsoft.VisualStudio.Modeling.TransactionRollingBackRule> | トランザクションがロールバックされようとしているときに実行されます。 |

- 各クラスには、オーバーライドするメソッドがあります。 クラスに `override` を入力して検出します。 このメソッドのパラメーターは、変更されている要素を識別します。

  ルールについては次の点に注意してください。

1. トランザクション内の一連の変更によって、多くのルールがトリガーされることがあります。 通常、最も外側のトランザクションがコミットされるときにルールが実行されます。 これらは、指定されていない順序で実行されます。

2. ルールは、常にトランザクション内で実行されます。 したがって、変更を行うために新しいトランザクションを作成する必要はありません。

3. ルールは、トランザクションがロールバックされるとき、または元に戻す操作または再実行操作が実行されるときには実行されません。 これらの操作では、ストアのすべてのコンテンツが以前の状態にリセットされます。 そのため、ルールによってストアの外部にあるすべての状態が変更された場合、ストアのコンテンツとの同期が保持されない可能性があります。 ストアの外部で状態を更新するには、イベントを使用することをお勧めします。 詳細については、「[イベント ハンドラーによって変更がモデル外に反映される](../modeling/event-handlers-propagate-changes-outside-the-model.md)」を参照してください。

4. 一部のルールは、モデルがファイルから読み込まれたときに実行されます。 読み込みまたは保存が進行中かどうかを判断するには、`store.TransactionManager.CurrentTransaction.IsSerializing` を使用します。

5. ルールのコードによってさらに多くのルール トリガーが作成された場合は、トリガーが起動リストの末尾に追加され、トランザクションが完了する前に実行されます。 DeletedRules は、他のすべてのルールの後に実行されます。 1 つのルールを 1 回のトランザクションで何度も実行できます。変更ごとに 1 回です。

6. ルールとの間で情報をやり取りするには、`TransactionContext` に情報を格納します。 これは、トランザクション中に保持されるディクショナリにすぎません。 トランザクションの終了時に破棄されます。 各ルールのイベント引数を使用して、それにアクセスできます。 ルールは、予測可能な順序で実行されないことに注意してください。

7. 他の代替手段を検討した後、ルールを使用します。 たとえば、値が変更されたときにプロパティを更新する場合は、計算されたプロパティの使用を検討してください。 シェイプのサイズまたは位置を制限する場合は、`BoundsRule` を使用します。 プロパティ値の変更に応答する場合は、プロパティに `OnValueChanged` ハンドラーを追加します。 詳細については、[変更内容への対応および変更内容の反映](../modeling/responding-to-and-propagating-changes.md)に関するページを参照してください。

## <a name="example"></a>例
 次の例では、2 つの要素をリンクするためにドメイン リレーションシップがインスタンス化されるときに、プロパティを更新します。 このルールは、ユーザーが図にリンクを作成したときだけでなく、プログラム コードによりリンクが作成された場合にもトリガーされます。

 この例をテストするには、タスク フロー ソリューション テンプレートを使用して DSL を作成し、Dsl プロジェクト内のファイルに次のコードを挿入します。 ソリューションをビルドして実行し、デバッグ プロジェクトでサンプル ファイルを開きます。 コメント シェイプとフロー要素の間にコメント リンクを描画します。 コメント内のテキストは、最後に接続した要素に関するレポートに変更されます。

 実際には、各 AddRule に対して DeleteRule を記述します。

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Microsoft.VisualStudio.Modeling;

namespace Company.TaskRuleExample
{

  [RuleOn(typeof(CommentReferencesSubjects))]
  public class RoleRule : AddRule
  {

    public override void ElementAdded(ElementAddedEventArgs e)
    {
      base.ElementAdded(e);
      CommentReferencesSubjects link = e.ModelElement as CommentReferencesSubjects;
      Comment comment = link.Comment;
      FlowElement subject = link.Subject;
      Transaction current = link.Store.TransactionManager.CurrentTransaction;
      // Don't want to run when we're just loading from file:
      if (current.IsSerializing) return;
      comment.Text = "Flow has " + subject.FlowTo.Count + " outgoing connections";
    }

  }

  public partial class TaskRuleExampleDomainModel
  {
    protected override Type[] GetCustomDomainModelTypes()
    {
      List<Type> types = new List<Type>(base.GetCustomDomainModelTypes());
      types.Add(typeof(RoleRule));
      return types.ToArray();
    }
  }

}
```

## <a name="see-also"></a>関連項目

- [イベント ハンドラーによって変更内容がモデル外に反映される](../modeling/event-handlers-propagate-changes-outside-the-model.md)