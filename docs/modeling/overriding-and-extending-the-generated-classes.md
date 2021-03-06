---
title: 生成済みクラスのオーバーライドおよび拡張
description: DSL 定義が、ドメイン固有言語に基づいた強力なツールセットを構築するためのプラットフォームであることについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, providing overridable classes
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 07c44e7ff7a603f339ec268b06bd78cc84cd6be2
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112390946"
---
# <a name="override-and-extend-the-generated-classes"></a>生成済みクラスのオーバーライドおよび拡張

DSL 定義は、ドメイン固有言語に基づいた強力なツールセットを構築するためのプラットフォームです。 多くの拡張機能と適応は、DSL 定義から生成されたクラスをオーバーライドして拡張することによって作成できます。 これらのクラスには、DSL 定義図で明示的に定義したドメイン クラスだけでなく、ツールボックス、エクスプローラー、シリアル化などを定義するその他のクラスも含まれています。

## <a name="extensibility-mechanisms"></a>拡張機能のメカニズム

生成されたコードを拡張できるように、いくつかのメカニズムが用意されています。

### <a name="override-methods-in-a-partial-class"></a>部分クラスのメソッドをオーバーライドする

部分クラス定義を使用すると、クラスを複数の場所で定義できます。 これにより、自分で記述したコードから生成されたコードを分離することができます。 手動で記述したコードでは、生成されたコードによって継承されたクラスをオーバーライドできます。

たとえば、DSL 定義で `Book` という名前のドメイン クラスを定義する場合、次のようにオーバーライド メソッドを追加するカスタム コードを記述できます。

```csharp
public partial class Book
{
   protected override void OnDeleting()
   {
      MessageBox.Show("Deleting book " + this.Title);
      base.OnDeleting();
   }
}
```

> [!NOTE]
> 生成されたクラスのメソッドをオーバーライドするには、生成されたファイルから分離されたファイルに必ずコードを記述します。 通常、このファイルは、CustomCode という名前のフォルダーに格納されています。 生成されたコードに変更を加えた場合、DSL 定義からコードを再生成すると、そのコードは失われます。

オーバーライドできるメソッドを検出するには、クラスで「**override**」と入力し、その後にスペースを入力します。 IntelliSense ツールヒントには、オーバーライドできるメソッドが示されます。

### <a name="double-derived-classes"></a>二重派生クラス

生成されたクラスのメソッドのほとんどは、モデリング名前空間の固定されたクラスのセットから継承されます。 ただし、生成されるコードにはいくつかのメソッドが定義されています。 通常、これはオーバーライドできないことを意味します。1 つの部分クラスで、同じクラスの別の部分定義で定義されているメソッドをオーバーライドすることはできません。

それでも、これらのメソッドをオーバーライドするには、ドメイン クラス向けに **Generates Double Derived** フラグを設定します。 これにより、2 つのクラスが生成されます。1 つはもう一方の抽象基底クラスです。 すべてのメソッドとプロパティの定義は基底クラスにあり、コンストラクターだけが派生クラスに含まれます。

たとえば、サンプルの Library.dsl では、`CirculationBook` ドメイン クラスの `Generates``Double Derived` プロパティが `true` に設定されています。 このドメイン クラス向けに生成されたコードには、次の 2 つのクラスが含まれています。

- `CirculationBookBase` は抽象で、すべてのメソッドとプロパティが含まれています。

- `CirculationBook` は、`CirculationBookBase` から派生しています。 そのコンストラクターを除き、空です。

任意のメソッドをオーバーライドするには、`CirculationBook` などの派生クラスの部分定義を作成します。 生成されたメソッドと、モデリング フレームワークから継承されたメソッドの両方をオーバーライドできます。

このメソッドは、モデル要素、リレーションシップ、シェイプ、図、コネクタなど、すべての種類の要素で使用できます。 また、その他の生成されたクラスのメソッドをオーバーライドすることもできます。 ToolboxHelper などの生成されたクラスの中には、常に二重に派生するものがあります。

### <a name="custom-constructors"></a>カスタム コンストラクター

コンストラクターをオーバーライドすることはできません。 二重派生クラスであっても、コンストラクターは派生クラスに存在する必要があります。

独自のコンストラクターを指定する場合は、DSL 定義のドメイン クラスに `Has Custom Constructor` を設定します。 **[すべてのテンプレートを変換する]** をクリックすると、生成されたコードにはそのクラスのコンストラクターが含まれません。 見つからないコンストラクターの呼び出しが含まれます。 これにより、ソリューションのビルド時にエラー レポートが生成されます。 エラー レポートをダブルクリックし、指定する必要があるものを説明している生成されたコードのコメントを確認します。

生成されたファイルとは別のファイルに部分クラス定義を記述し、コンストラクターを指定します。

### <a name="flagged-extension-points"></a>フラグ付き拡張ポイント

フラグ付き拡張ポイントは DSL 定義内の場所であり、プロパティまたはチェックボックスを設定してカスタム メソッドを指定することを示すことができます。 カスタム コンストラクターが一例です。 その他の例としては、計算済みまたはカスタムのストレージへのドメインプロパティの `Kind` の設定、または接続ビルダーでの **Is Custom** フラグの設定などがあります。

どちらの場合も、フラグを設定してコードを再生成すると、ビルド エラーが発生します。 エラーをダブルクリックし、指定する必要があるものを説明しているコメントを確認します。

### <a name="rules"></a>ルール

トランザクション マネージャーでは、プロパティの変更など、指定されたイベントが発生した場合、トランザクションの終了前に実行される規則を定義できます。 通常、規則は、ストア内の異なる要素間で同期を維持するために使用されます。 たとえば、規則を使用して、モデルの現在の状態がダイアグラムに表示されるようにします。

規則はクラス単位で定義されるため、各オブジェクトに規則を登録するコードを用意する必要はありません。 詳細については、「[ルールによってモデル内の変更が反映される](../modeling/rules-propagate-changes-within-the-model.md)」を参照してください。

### <a name="store-events"></a>ストア イベント

モデリング ストアには、要素の追加と削除、プロパティ値の変更など、ストア内の特定の種類の変更をリッスンするために使用できるイベント メカニズムが用意されています。 イベント ハンドラーは、変更が加えられたトランザクションの終了後に呼び出されます。 通常、これらのイベントは、ストアの外部のリソースを更新するために使用されます。

### <a name="net-events"></a>.NET イベント

シェイプに対するいくつかのイベントに登録できます。 たとえば、シェイプに対するマウスクリックをリッスンできます。 各オブジェクトのイベントにサブスクライブするコードを記述する必要があります。 このコードは、InitializeInstanceResources() のオーバーライドで記述できます。

一部のイベントは、シェイプでデコレーターを描画するために使用される、ShapeFields に対して生成されます。 例については、「[方法: シェイプまたはデコレーターに対するクリック操作を受け取る](../modeling/how-to-intercept-a-click-on-a-shape-or-decorator.md)」を参照してください。

これらのイベントは、通常、トランザクション内では発生しません。 ストアに変更を加える場合は、トランザクションを作成する必要があります。
