---
title: "ツールおよびツールボックスのカスタマイズ |Microsoft ドキュメント"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- vs.dsltools.dsldesigner.selectiondialog
- vs.dsltools.dsldesigner.selecticondialog
- vs.dsltools.dsldesigner.selectcursordialog
helpviewer_keywords:
- Domain-Specific Language, toolbox
ms.assetid: 2a0d03d7-ebc6-4458-b9f4-d2cb8418a62d
caps.latest.revision: 26
author: alancameronwills
ms.author: awills
manager: douge
translationtype: Machine Translation
ms.sourcegitcommit: 5db97d19b1b823388a465bba15d057b30ff0b3ce
ms.openlocfilehash: c4edbf4ca922134924d171c8f6368740e6921a2c
ms.lasthandoff: 02/22/2017

---
# <a name="customizing-tools-and-the-toolbox"></a>ツールおよびツールボックスのカスタマイズ
ユーザーがモデルに追加可能な要素についてツールボックス項目を定義する必要があります。 ツールには要素ツールと接続ツールの&2; 種類があります。 生成されたデザイナーで、ユーザーは要素ツールを選択して図形を図へドラッグすることができ、接続ツールを選択して図形間のリンクを描画できます。 一般にユーザーは、要素ツールを使用するとドメイン クラスのインスタンスをモデルに追加することができ、接続ツールを使用するとドメイン リレーションシップのインスタンスを追加できます。  
  
 このトピックの内容  
  
-   [ツールボックスの定義方法](#ToolboxDef)  
  
-   [要素ツールのカスタマイズ](#customizing)  
  
-   [ツールからの要素のグループを作成します。](#groups)  
  
-   [接続ツールのカスタマイズ](#connections)  
  
##  <a name="a-nametoolboxdefa-how-the-toolbox-is-defined"></a><a name="ToolboxDef"></a>ツールボックスの定義方法  
 DSL エクスプローラーで、エディター ノードとその下のノードを展開します。 一般に、次のような階層が表示されます。  
  
```  
  
Editor  
     Toobox Tabs  
        MyDsl          //a tab  
           Tools  
               ExampleElement      // an element tool  
               ExampleRelationship // a connection tool  
  
```  
  
 DSL エクスプローラーのこの部分で、次の操作を実行できます。  
  
-   新しいタブを作成します。 タブはツールボックス内のセクション見出しを定義します。  
  
-   新しいツールを作成します。  
  
-   ツールをコピーして貼り付けます。  
  
-   一覧内のツールを上下に移動します。  
  
-   タブとツールを削除します。  
  
> [!IMPORTANT]
>  DSL エクスプローラー内の項目を追加または貼り付けるには、新しいノードの親の親を右クリックします。 たとえば、ツールを追加する、タブを右クリックと not、**ツール**ノードです。 タブを追加するには、右クリックし、**エディター**ノードです。  
  
 **ツールボックス アイコン**すべてのツールのプロパティは、16 x 16 ビットマップ ファイルを参照します。 通常、これらのファイルは保持、 **dsl \resources**フォルダーです。  
  
 **クラス**要素ツールのプロパティは具象ドメイン クラスを参照します。 既定では、ツールはこのクラスのインスタンスを作成します。 ただし、コードを作成して、ツールに要素のグループまたはさまざまな種類の要素を作成させることができます。  
  
 **接続ビルダー**接続ツールのプロパティは、ツールで接続可能な要素の種類、およびそれらの間でどのようなリレーションシップが作成を定義する接続ビルダーを参照します。 DSL エクスプローラーで、接続ビルダーはノードとして定義されます。 接続ビルダーは、ドメイン リレーションシップを定義すると自動的に作成されますが、コードを作成してカスタマイズできます。  
  
#### <a name="to-add-a-tool-to-the-toolbox"></a>ツールボックスにツールを追加するには  
  
1.  通常、図形クラスを作成し、それをドメイン クラスにマップした後で、要素ツールを作成します。  
  
     通常、コネクタ クラスを作成し、それを参照リレーションシップにマップした後で、コネクタ ツールを作成します。  
  
2.  DSL エクスプ ローラーで、**エディター**ノードおよび**ツールボックス タブ**ノードです。  
  
     ツールボックス タブ ノードを右クリックし、をクリックし、**新しい要素ツールの追加**または**新しい接続ツール**します。  
  
3.  設定、**ツールボックス アイコン**プロパティを 16 x 16 ビットマップを参照してください。  
  
     新しいアイコンを定義する場合は、ソリューション エクスプ ローラーでビットマップ ファイルを作成、 **dsl \resources**フォルダーです。 ファイルは、次のプロパティ値を持つ必要があります:**ビルド アクション** = **コンテンツ**です。**出力ディレクトリにコピー** = **コピーしない**します。  
  
4.  **要素ツール:**設定、**クラス**図形にマップされる具象ドメイン クラスを参照するツールのプロパティです。  
  
     **コネクタ ツール:**設定、**接続ビルダー**ドロップダウン リストで提供されている項目のいずれかのツールのプロパティです。 接続ビルダーは、コネクタをドメイン リレーションシップにマップすると、自動的に作成されます。 最近、コネクタを作成した場合、通常、関連する接続ビルダーを選択しています。  
  
5.  DSL をテストするには、F5 キーまたは CTRL+F5 キーを押し、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] の実験用インスタンスでサンプル モデル ファイルを開きます。 ツールボックスに新しいツールが表示されます。 それを図の上にドラッグし、新しい要素が作成されることを確認します。  
  
     ツールが表示されない場合、実験用の [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] を停止します。 Windows**開始**] メニューの [実行**、Microsoft Visual Studio 2010 実験用インスタンスをリセット**します。 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]**ビルド** メニューのをクリックして**ソリューションのリビルド**します。 再度 DSL をテストします。  
  
##  <a name="a-namecustomizinga-customizing-element-tools"></a><a name="customizing"></a>要素ツールのカスタマイズ  
 既定では、ツールは指定されたクラスの単一インスタンスを作成しますが、次の&2; つの方法で変更できます。  
  
-   他のクラスで要素マージ ディレクティブを定義し、このクラスの新しいインスタンスが受け入れられ、新しい要素が作成されるときに追加のリンクが作成されるようにします。 たとえば、ユーザーが別の要素にコメントをドロップし、両者の間に参照リンクを作成可能にすることができます。  
  
     これらのカスタマイズは、ユーザーが要素を貼り付けたりドラッグ アンド ドロップしたりするときに発生することにも影響します。  
  
     詳細については、次を参照してください。[をカスタマイズする要素の作成と移動](../modeling/customizing-element-creation-and-movement.md)します。  
  
-   コードを作成して、ツールをカスタマイズし、要素のグループを作成可能にします。 ツールはオーバーライド可能な ToolboxHelper.cs 内のメソッドにより初期化されます。 詳細については、次を参照してください。[グループの要素の作成ツールから](#groups)します。  
  
##  <a name="a-namegroupsa-creating-groups-of-elements-from-a-tool"></a><a name="groups"></a>ツールからの要素のグループを作成します。  
 各要素ツールは作成する要素のプロトタイプを含みます。 既定では、各要素ツールは単一の要素を作成しますが、1 つのツールで関連するオブジェクトのグループを作成することも可能です。 これを行うには、使用して、ツールを初期化する、<xref:Microsoft.VisualStudio.Modeling.ElementGroupPrototype>に関連する項目を格納している</xref:Microsoft.VisualStudio.Modeling.ElementGroupPrototype>。  
  
 次の例は、型 Transistor がある DSL から取得しています。 各 Transistor には名前の付いた Terminal が&3; つあります。 Transistor の要素ツールは、4 つのモデル要素と&3; つのリレーションシップ リンクを含むプロトタイプを格納します。 ユーザーがツールを図の上にドラッグすると、プロトタイプはインスタンス化され、モデル ルートにリンクされます。  
  
 このコードで定義されているメソッドをオーバーライドして**Dsl\GeneratedCode\ToolboxHelper.cs**します。  
  
 プログラム コードを使用して、モデルのカスタマイズに関する詳細については、次を参照してください。[ナビゲートおよびプログラム コードでモデルを更新](../modeling/navigating-and-updating-a-model-in-program-code.md)します。  
  
```  
using Microsoft.VisualStudio.Modeling;  
using Microsoft.VisualStudio.Modeling.Diagrams;  
  
  public partial class CircuitsToolboxHelper  
  {  
    /// <summary>  
    /// Toolbox initialization, called for each element tool on the toolbox.  
    /// This version deals with each Component subtype separately.  
    /// </summary>  
    /// <param name="store"></param>  
    /// <param name="domainClassId">Identifies the domain class this tool should instantiate.</param>  
    /// <returns>prototype of the object or group of objects to be created by tool</returns>  
    protected override ElementGroupPrototype CreateElementToolPrototype(Store store, Guid domainClassId)  
    {  
        if (domainClassId == Transistor.DomainClassId)  
        {  
            Transistor transistor = new Transistor(store);  
  
            transistor.Base = new ComponentTerminal(store);  
            transistor.Collector = new ComponentTerminal(store);  
            transistor.Emitter = new ComponentTerminal(store);  
  
            transistor.Base.Name = "base";  
            transistor.Collector.Name = "collector";  
            transistor.Emitter.Name = "emitter";  
  
            // Create an ElementGroup for the Toolbox.  
            ElementGroup elementGroup = new ElementGroup(store.DefaultPartition);  
            elementGroup.AddGraph(transistor, true);  
            // AddGraph includes the embedded parts  
  
            return elementGroup.CreatePrototype();  
        }  
        else  
        {  
            return base.CreateElementToolPrototype(store, domainClassId);  
}  }    }  
  
```  
  
##  <a name="a-nameconnectionsa-customizing-connection-tools"></a><a name="connections"></a>接続ツールのカスタマイズ  
 通常、新しいコネクタ クラスを作成するときに要素ツールを作成します。 または、両端の種類でリレーションシップの種類を確認可能にすることで、1 つのツールをオーバーロードできます。 たとえば、Person-Person リレーションシップと Person-Town リレーションシップの両方を作成可能な&1; つの接続ツールを定義できます。  
  
 接続ツールは接続ビルダーを呼び出します。 接続ビルダーを使用して、ユーザーが生成されたデザイナー内で要素をリンク可能な方法を指定します。 接続ビルダーは、リンク可能な要素と要素間に作成されるリンクの種類を指定します。  
  
 ドメイン クラス間に参照リレーションシップを作成すると、接続ビルダーは自動的に作成されます。 接続ツールをマップするときにこの接続ビルダーを使用します。 接続ツールを作成する方法の詳細については、次を参照してください。[ツールボックスの構成](../modeling/customizing-tools-and-the-toolbox.md)します。  
  
 既定の接続ビルダーを変更して、異なる範囲のソース型とターゲット型を扱い、異なる種類のリレーションシップを作成できます。  
  
 接続ビルダー用にカスタム コードを作成し、接続用のソース クラスとターゲット クラスの指定、作成される接続の種類の定義、および接続の作成に関連するその他の処理を実行できます。  
  
### <a name="the-structure-of-connection-builders"></a>接続ビルダーの構造  
 接続ビルダーには&1; つ以上のリンク接続ディレクティブが含まれ、それによってドメイン リレーションシップとソース要素およびターゲット要素が指定されます。 たとえば、Task Flow ソリューション テンプレートで確認できます、 **CommentReferencesSubjectsBuilder**で、 **DSL エクスプ ローラー**します。 この接続ビルダーには、1 つのリンクが含まれています。 接続ディレクティブ**CommentReferencesSubjects**、ドメイン リレーションシップに割り当て先となる**CommentReferencesSubjects**します。 このリンク接続ディレクティブには、`Comment` ドメイン クラスを指し示すソース ロール ディレクティブと `FlowElement` ドメイン クラスを指し示すターゲット ロール ディレクティブが含まれます。  
  
### <a name="using-connection-builders-to-restrict-source-and-target-roles"></a>接続ビルダーを使用したソース ロールとターゲット ロールの制限  
 接続ビルダーを使用して、指定されたドメイン リレーションシップのソース ロールまたはターゲット ロールのどちらかで、特定のクラスの出現を制限できます。 たとえば、別のドメイン クラスへのドメイン リレーションシップを伴う基底ドメイン クラスがあるが、そのリレーションシップにおいて、その基底クラスのすべての派生クラスのロールが同じロールになるのは望ましくないという場合があるかもしれません。 Task Flow ソリューションでは、4 つの具象ドメイン クラス (**StartPoint**、**エンドポイント**、 **MergeBranch**と**同期**) 抽象ドメイン クラスから直接継承した**FlowElement**、2 つの具象ドメイン クラスと (**タスク**と**ObjectInState**) を間接的に継承しています。 **フロー**参照を受け取るリレーションシップ**FlowElement**ソース ロールとターゲット ロールの両方のドメイン クラスです。 ただしのインスタンス、**エンドポイント**ドメイン クラスのインスタンスのソースがすることはできません、**フロー**リレーションシップのインスタンスには、 **StartPoint**クラスのインスタンスの対象にする、**フロー**リレーションシップです。 **FlowBuilder**接続ビルダーには、接続ディレクティブという名前のリンクが用意されて**フロー**を指定するドメイン クラスには、ソース役割を果たします (**タスク**、 **MergeBranch**、 **StartPoint**、および**同期**) およびターゲット ロールを再生することができます (**MergeBranch**、**エンドポイント**、および**同期**)。  
  
### <a name="connection-builders-with-multiple-link-connect-directives"></a>複数のリンク接続ディレクティブを持つ接続ビルダー  
 接続ビルダーには複数のリンク接続ディレクティブを追加できます。 これはユーザーから、ドメイン モデルの複雑さの一部を非表示にして役立つ保持、**ツールボックス**が煩雑です。 単一の接続ビルダーにいくつかの異なるドメイン リレーションシップのリンク接続ディレクティブを追加できます。 ただし、ほぼ同一の関数を実行するときはドメイン リレーションシップを結合する必要があります。  
  
 Task Flow ソリューションで、**フロー**接続ツールを使用して、両方のインスタンスを描画、**フロー**と**ObjectFlow**ドメイン間の関係。 **FlowBuilder**接続ビルダーは、さらに、**フロー**リンク接続ディレクティブの前に説明した、2 つのリンク接続ディレクティブを名前付き**ObjectFlow**します。 これらのディレクティブを指定するのインスタンス、 **ObjectFlow**のインスタンス間で関係を描画することがあります、 **ObjectInState**ドメイン クラスのインスタンスから、または、 **ObjectInState**のインスタンスに、**タスク**、2 つのインスタンス間ではなく、**タスク**、またはのインスタンスから、**タスク**のインスタンスに、 **ObjectInState**します。 ただしのインスタンス、**フロー**の&2; つのインスタンス間にリレーションシップを作成することがあります、**タスク**します。 コンパイルして、Task Flow ソリューションを実行する場合は、その描画を表示できます、**フロー**のインスタンスから、 **ObjectInState**のインスタンスに、**タスク**のインスタンスを作成、 **ObjectFlow**が、描画、**フロー**の&2; つのインスタンス間で、**タスク**のインスタンスを作成、**フロー**します。  
  
### <a name="custom-code-for-connection-builders"></a>接続ビルダーのカスタム コード  
 ユーザー インターフェイスには接続ビルダーの異なる種類のカスタマイズを定義する&4; つのチェック ボックスがあります。  
  
-   **カスタム受け入れ**ソースまたはターゲット ロール ディレクティブ上のチェック ボックス  
  
-   **カスタム接続**ソースまたはターゲット ロール ディレクティブ上のチェック ボックス  
  
-   **カスタム接続を使用**接続ディレクティブ上のチェック ボックス  
  
-   **はカスタム**接続ビルダーのプロパティ  
  
 これらのカスタマイズを実施するためにプログラム コードを準備する必要があります。 どのようなコードを準備する必要があるのかを知るためには、これらのボックスのいずれかをチェックし、[すべてのテンプレートの変換] をクリックして、ソリューションをビルドします。 エラー レポートが生成されます。 エラー レポートをダブルクリックし、追加する必要があるコードを説明しているコメントを確認します。  
  
> [!NOTE]
>  カスタム コードを追加するには、GeneratedCode フォルダー内のコード ファイルとは別のコード ファイルに部分クラス定義を作成します。 作業内容を失わないために、生成されたコード ファイルを編集しないでください。 詳細については、次を参照してください。[をオーバーライドすると、生成されたクラスを拡張する](../modeling/overriding-and-extending-the-generated-classes.md)です。  
  
#### <a name="creating-custom-connection-code"></a>カスタム接続コードの作成  
 各リンク接続ディレクティブを**ソース ロール ディレクティブ** タブの定義からな型をドラッグできます。 同様に、**ターゲット ロール ディレクティブ** タブの定義にどのようなデータ型をドラッグできます。 種類ごとに、さらを指定できます (そのリンク接続ディレクティブ) の接続を許可する設定するかどうか、**カスタム受け入れ**フラグを設定し、余分なコードを指定します。  
  
 接続が確立されたときに発生することをカスタマイズすることもできます。 たとえば、特定のクラスに対してドラッグが発生するただ&1; つのケース、あるリンク接続ディレクティブが規定するすべてのケース、または FlowBuilder 接続ビルダー全体をカスタマイズできます。 これらの各オプションについて、適切なレベルでカスタム フラグを設定できます。 すべてのテンプレートを変換し、ソリューションのビルドを試みると、エラー メッセージから生成されたコード内のコメントに誘導されます。 これらのコメントにより、提供する必要のあるものが特定されます。  
  
 コンポーネント図のサンプルで、Connection ドメイン リレーションシップの接続ビルダーはポート間に作成可能な接続を制限するようにカスタマイズされています。 次の図は、`OutPort` 要素から `InPort` 要素への接続のみ可能であること、しかし互いの内部でコンポーネントを入れ子にすることが可能であることを示しています。  
  
 **入れ子になったコンポーネントから OutPort へ取り込む接続**  
  
 ![接続ビルダー](~/modeling/media/connectionbuilder_3.png "ConnectionBuilder_3")  
  
 したがって、入れ子になったコンポーネントから OutPort への接続が可能であることを指定するのが適切です。 設定するこのような接続を指定する**カスタム受け入れを使用**上、 **InPort**ソース ロールと型、および**OutPort**ターゲット ロールとしての型、 **DSL 詳細**ウィンドウの次の図に示すように。  
  
 **DSL エクスプ ローラーにおけるリンク接続ディレクティブ**  
  
 ![接続ビルダー イメージ](~/modeling/media/connectionbuilder_4a.png "ConnectionBuilder_4a")  
  
 **DSL 詳細ウィンドウにおけるリンク接続ディレクティブ**  
  
 ![](~/modeling/media/connectionbuilder_4b.png "ConnectionBuilder_4b")  
  
 次に、ConnectionBuilder クラスにメソッドを入力する必要があります。  
  
```  
  public partial class ConnectionBuilder  
  {  
    /// <summary>  
    /// OK if this component has children  
    /// </summary>  
    private static bool CanAcceptInPortAsSource(InPort candidate)  
    {  
       return candidate.Component.Children.Count > 0;  
    }  
  
    /// <summary>  
    /// Only if source is on parent of target.  
    /// </summary>  
    private static bool CanAcceptInPortAndInPortAsSourceAndTarget                (InPort sourceInPort, InPort targetInPort)  
    {  
      return sourceInPort.Component == targetInPort.Component.Parent;  
    }  
// And similar for OutPorts…  
```  
  
 プログラム コードを使用して、モデルのカスタマイズに関する詳細については、次を参照してください。[ナビゲートおよびプログラム コードでモデルを更新](../modeling/navigating-and-updating-a-model-in-program-code.md)します。  
  
 たとえば、同様のコードを使用して、ユーザーによる親子リンクを含むループの作成を防ぐことができます。 これらの制限は、どんな場合でもユーザーが違反することができないため、「ハード」な制約と見なされます。 ユーザーが保存できない無効な構成を作成することにより、一時的に迂回可能な「ソフト」な検証チェックを作成することもできます。  
  
### <a name="good-practice-in-defining-connection-builders"></a>接続ビルダーを定義する際の適切なプラクティス  
 異なる種類のリレーションシップを作成するために、それらが概念的に関連する場合にのみ、1 つの接続ビルダーを定義する必要があります。 タスク フローのサンプルでは、同じビルダーを使用して、タスク間のフローのほか、タスクとオブジェクト間のフローも作成します。 ただし、コメントとタスク間のリレーションシップを作成するために同じビルダーを使用することは混乱を招くことがあります。  
  
 複数の種類のリレーションシップに対して接続ビルダーを定義する場合、ソース オブジェクトとターゲット オブジェクトの同じペアから複数の型が一致しないことを確認する必要があります。 そうでない場合、結果は予測不可能になります。  
  
 カスタム コードを使用して「ハード」な制約を適用できますが、ユーザーが一時的に無効な接続を確立できる必要があるかどうかを考慮してください。 その必要がある場合、制約を変更して、ユーザーが変更内容を保存しようとするまで、接続が検証されないようにすることができます。  
  
## <a name="see-also"></a>関連項目  
 [要素の作成と移動をカスタマイズします。](../modeling/customizing-element-creation-and-movement.md)   
 [コピー動作のカスタマイズ](../modeling/customizing-copy-behavior.md)   
 [方法: ドラッグ アンド ドロップ ハンドラーを追加します。](../modeling/how-to-add-a-drag-and-drop-handler.md)   
 [移動して、プログラム コードでモデルを更新します。](../modeling/navigating-and-updating-a-model-in-program-code.md)   
 [回路図のサンプル DSL](http://code.msdn.microsoft.com/Visualization-Modeling-SDK-763778e8)
