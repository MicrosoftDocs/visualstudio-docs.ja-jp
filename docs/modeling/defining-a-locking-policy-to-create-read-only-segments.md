---
title: ロック ポリシーの定義と読み取り専用セグメントの作成
description: ドメイン固有言語 (DSL) モデルの一部または全部をロックするプログラム用のポリシーを定義して、読み取りはできるが変更はできないようにする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 6bb8e05ffc030716f32ab7e79233ca9e02ef2e11
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112385787"
---
# <a name="defining-a-locking-policy-to-create-read-only-segments"></a>ロック ポリシーの定義と読み取り専用セグメントの作成
Visual Studio の視覚化およびモデリング SDK の不変 API を使用すると、ドメイン固有言語 (DSL) モデルの一部または全部をプログラムでロックして、読み取りはできるが変更はできないようにすることができます。 この読み取り専用オプションを使用して、たとえばユーザーが同僚に DSL モデルに注釈付けとレビューを行うように依頼できますが、同僚はオリジナルを変更することはできないようにすることができます。

 さらに、DSL の作成者として、"*ロック ポリシー*" を定義でき ます。 ロック ポリシーには、許可されるロック、許可されないロック、または必須のロックを定義します。 たとえば、DSL を発行するときに、サードパーティの開発者が新しいコマンドでそれを拡張することを奨励できます。 ただし、ロック ポリシーを使用して、モデルの特定部分の読み取り専用状態を変更できないようにすることもできます。

> [!NOTE]
> ロック ポリシーは、リフレクションを使用することによって迂回できます。 サードパーティの開発者に対して明確な境界が用意されますが、強力なセキュリティは提供されません。

 詳細とサンプルについては、Visual Studio の[視覚化およびモデリング SDK](https://code.msdn.microsoft.com/Visualization-and-Modeling-313535db) の Web サイトを参照してください。

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]

## <a name="setting-and-getting-locks"></a>ロックの設定と取得
 ストア、パーティション、または個々の要素に対してロックを設定できます。 たとえば、次のステートメントを実行すると、モデル要素が削除されるのを防ぐことができ、プロパティが変更されるのも防ぐことができます。

```csharp
using Microsoft.VisualStudio.Modeling.Immutability; ...
element.SetLocks(Locks.Delete | Locks.Property);
```

 他のロック値を使用して、リレーションシップ、要素の作成、パーティション間の移動、およびロール内のリンクの順序変更を防止できます。

 ロックは、ユーザー操作とプログラム コードの両方に適用されます。 プログラム コードによって変更が試行されると、`InvalidOperationException` がスローされます。 [元に戻す] 操作または [やり直す] 操作では、ロックは無視されます。

 `IsLocked(Locks)` を使用して、特定のセット内の要素にロックがあるかどうかを検出でき、`GetLocks()` を使用して、要素の現在のロック セットを取得できます。

 トランザクションを使用せずにロックを設定できます。 ロック データベースはストアの一部ではありません。 ストア内の値の変更に応答するロック (OnValueChanged など) を設定する場合は、[元に戻す] 操作の一部である変更を許可する必要があります。

 これらのメソッドは、<xref:Microsoft.VisualStudio.Modeling.Immutability> 名前空間に定義される拡張メソッドです。

### <a name="locks-on-partitions-and-stores"></a>パーティションとストアのロック
 ロックは、パーティションとストアにも適用できます。 パーティションに設定されたロックは、パーティション内のすべての要素に適用されます。 したがって、たとえば、次のステートメントを使用すると、そのロックの状態に関係なく、パーティション内のすべての要素が削除されるのを防ぐことができます。 ただし、`Locks.Property` などの他のロックを個々の要素に設定できます。

```csharp
partition.SetLocks(Locks.Delete);
```

 ストアに設定されたロックは、パーティションと要素に対するロックの設定に関係なく、すべての要素に適用されます。

### <a name="using-locks"></a>ロックの使用
 ロックを使用して、次の例のようなスキームを実装できます。

- コメントを表すものを除くすべての要素とリレーションシップへの変更を禁止します。 これにより、ユーザーはモデルを変更せずに注釈を付けることができます。

- 既定のパーティションの変更を禁止しますが、ダイアグラム パーティションの変更は許可します。 ユーザーはダイアグラムを再配置できますが、基になるモデルを変更することはできません。

- 別のデータベースに登録されているユーザーのグループ以外のストアへの変更を禁止します。 他のユーザーにとって、ダイアグラムとモデルは読み取り専用になります。

- ダイアグラムのブール型プロパティが true に設定されている場合は、モデルへの変更を許可しません。 そのプロパティを変更するメニュー コマンドを用意します。 これにより、ユーザーが誤って変更することがないようにできます。

- 特定のクラスの要素とリレーションシップの追加と削除を禁止しますが、プロパティの変更は許可します。 これにより、ユーザーがプロパティを入力できる固定フォームが用意されます。

## <a name="lock-values"></a>値のロック
 ロックは、ストア、パーティション、または個々の ModelElement に設定できます。 ロックは `Flags` 列挙体です。'&#124;' を使用して値を組み合わせることができます。

- ModelElement のロックには、常にそのパーティションのロックが含まれます。

- パーティションのロックには、常にストアのロックが含まれます。

  パーティションまたはストアにロックを設定するのと同時に、個々の要素のロックを無効にすることはできません。

|値|`IsLocked(Value)` が true の場合の意味|
|-|-|
|なし|制限はありません。|
|プロパティ|要素のドメイン プロパティは変更できません。 これは、リレーションシップのドメイン クラスのロールによって生成されるプロパティには適用されません。|
|追加|パーティションまたはストアに新しい要素とリンクを作成することはできません。<br /><br /> `ModelElement` には適用されません。|
|詳細ビュー|`element.IsLocked(Move)` が true の場合、または `targetPartition.IsLocked(Move)` が true の場合、パーティション間で要素を移動することはできません。|
|削除|要素自体、または削除が反映される要素 (埋め込まれている要素や図形など) に対してこのロックが設定されている場合、要素を削除することはできません。<br /><br /> `element.CanDelete()` を使用して、要素を削除できるかどうかを検出できます。|
|Reorder|Roleplayer でのリンクの順序を変更することはできません。|
|RolePlayer|この要素をソースとするリンクのセットを変更することはできません。 たとえば、新しい要素をこの要素の下に埋め込むことはできません。 これは、この要素がターゲットであるリンクには影響しません。<br /><br /> この要素がリンクの場合、ソースとターゲットは影響を受けません。|
|All|他の値のビットごとの OR。|

## <a name="locking-policies"></a>ロック ポリシー
 DSL の作成者として、"*ロック ポリシー*" を定義できます。 ロック ポリシーは SetLocks () の操作を抑制して、特定のロックが設定されないようにしたり、特定のロックの設定を必須にしたりすることができます。 通常、ロック ポリシーを使用して、変数 `private` を宣言するのと同じように、ユーザーまたは開発者が意図せずに DSL の使用目的に違反することを防止できます。

 また、ロック ポリシーを使用して、要素の型に依存するすべての要素にロックを設定することもできます。 これは、`SetLocks(Locks.None)` は、要素が最初に作成されたとき、またはファイルから逆シリアル化されたときに常に呼び出されるためです。

 ただし、ポリシーを使用して、要素の有効期間中にロックを変更することはできません。 この効果を実現するには、`SetLocks()` への呼び出しを使用する必要があります。

 ロック ポリシーを定義するには、次のことを行う必要があります。

- <xref:Microsoft.VisualStudio.Modeling.Immutability.ILockingPolicy> を実装するクラスを作成します。

- このクラスを、DSL の DocData で利用できるサービスに追加します。

### <a name="to-define-a-locking-policy"></a>ロック ポリシーを定義するには
 <xref:Microsoft.VisualStudio.Modeling.Immutability.ILockingPolicy> には次の定義が含まれています。

```csharp
public interface ILockingPolicy
{
  Locks RefineLocks(ModelElement element, Locks proposedLocks);
  Locks RefineLocks(Partition partition, Locks proposedLocks);
  Locks RefineLocks(Store store, Locks proposedLocks);
}
```

 これらのメソッドは、ストア、パーティション、または ModelElement に対する `SetLocks()` の呼び出しが行われたときに呼び出されます。 各メソッドには、推奨されるロックのセットが用意されています。 推奨されるセットを返すことも、ロックを追加および削除することもできます。

 次に例を示します。

```csharp
using Microsoft.VisualStudio.Modeling;
using Microsoft.VisualStudio.Modeling.Immutability;
namespace Company.YourDsl.DslPackage // Change
{
  public class MyLockingPolicy : ILockingPolicy
  {
    /// <summary>
    /// Moderate SetLocks(this ModelElement target, Locks locks)
    /// </summary>
    /// <param name="element">target</param>
    /// <param name="proposedLocks">locks</param>
    /// <returns></returns>
    public Locks RefineLocks(ModelElement element, Locks proposedLocks)
    {
      // In my policy, users can never delete an element,
      // and other developers cannot easily change that:
      return proposedLocks | Locks.Delete);
    }
    public Locks RefineLocks(Store store, Locks proposedLocks)
    {
      // Only one user can change this model:
      return Environment.UserName == "aUser"
           ? proposedLocks : Locks.All;
    }
```

 他のコードで `SetLocks(Lock.Delete):` が呼び出される場合でも、ユーザーが常に要素を削除できるようにするには:

 `return proposedLocks & (Locks.All ^ Locks.Delete);`

 MyClass のすべての要素のすべてのプロパティの変更を禁止するには:

 `return element is MyClass ? (proposedLocks | Locks.Property) : proposedLocks;`

### <a name="to-make-your-policy-available-as-a-service"></a>ポリシーをサービスとして使用できるようにするには
 `DslPackage` プロジェクトに、次の例のようなコードを含む新しいファイルを追加します。

```csharp
using Microsoft.VisualStudio.Modeling;
using Microsoft.VisualStudio.Modeling.Immutability;
namespace Company.YourDsl.DslPackage // Change
{
  // Override the DocData GetService() for this DSL.
  internal partial class YourDslDocData // Change
  {
    /// <summary>
    /// Custom locking policy cache.
    /// </summary>
    private ILockingPolicy myLockingPolicy = null;

    /// <summary>
    /// Called when a service is requested.
    /// </summary>
    /// <param name="serviceType">Service requested</param>
    /// <returns>Service implementation</returns>
    public override object GetService(System.Type serviceType)
    {
      if (serviceType == typeof(SLockingPolicy)
       || serviceType == typeof(ILockingPolicy))
      {
        if (myLockingPolicy == null)
        {
          myLockingPolicy = new MyLockingPolicy();
        }
        return myLockingPolicy;
      }
      // Request is for some other service.
      return base.GetService(serviceType);
    }
}
```
