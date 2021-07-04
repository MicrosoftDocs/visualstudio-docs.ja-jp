---
title: ドメイン固有言語のカスタマイズおよび拡張
description: Visual Studio Modeling and Visualization SDK (VMSDK) で、モデリング ツールを定義できるいくつかレベルがどのように提供されるかについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language Tools, creating solutions
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 04180b1fc8930b58c2d78635c794c8a614db5ed5
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112389385"
---
# <a name="customize-and-extend-a-domain-specific-language"></a>ドメイン固有言語のカスタマイズおよび拡張

Visual Studio Modeling and Visualization SDK (VMSDK) には、モデリング ツールを定義できるいくつかのレベルがあります。

1. DSL 定義図を使用して、ドメイン固有言語 (DSL) を定義します。 図の表記法、読み取り可能な XML フォーム、およびコードやその他の成果物の生成に必要な基本ツールを使用して、DSL を迅速に作成できます。 詳細については、「[方法: ドメイン固有言語を定義する](../modeling/how-to-define-a-domain-specific-language.md)」を参照してください。

2. DSL 定義のさまざまな高度な機能を使用して DSL を細かく調整します。 たとえば、ユーザーが要素を作成するときに追加のリンクが表示されるようにできます。 ほとんどの場合この手法は DSL 定義で実現しますが、場合によってはプログラム コードを数行記述する必要があります。

3. プログラム コードを使用して、モデリング ツールを拡張します。 VMSDK は特に、DSL 定義から生成されるコードにより、拡張機能を容易に統合できるようにすることを目的としています。 詳細については、[ドメイン固有言語をカスタマイズするコードの記述](../modeling/writing-code-to-customise-a-domain-specific-language.md)に関するページを参照してください。

> [!NOTE]
> DSL 定義ファイルの更新を完了したら、ソリューションをリビルドする前に、必ず **ソリューション エクスプローラー** のツールバーにある **[すべてのテンプレートの変換]** をクリックしてください。

## <a name="article-reference"></a>記事リファレンス

|達成する効果|参照するトピック|
|-|-|
|シェイプの色とスタイルのプロパティをユーザーが設定できるようにします。|シェイプまたはコネクタ クラスを右クリックし、 **[公開対象の追加]** をポイントして、項目をクリックします。|
|モデル要素のさまざまなクラスが、ダイアグラム上で同じように表示され、初期の高さと幅、色、ヒントなどのプロパティを共有します。|シェイプまたはコネクタ クラス間の継承を使用します。 派生シェイプと派生ドメイン クラス間のマッピングにより、親のマッピングの詳細が継承されます。<br /><br /> または、異なるドメイン クラスを同じシェイプ クラスにマップします。|
|モデル要素のクラスが、さまざまなシェイプのコンテキストによって表示されます。|複数のシェイプ クラスを同じドメイン クラスにマップします。 ソリューションをビルドするときに、エラー報告に従って、要求されたコードを指定して、使用するシェイプを決定します。|
|シェイプの色またはその他の機能 (フォントなど) が現在の状態を示します。|[シェイプおよびコネクタの更新とモデルへの反映](../modeling/updating-shapes-and-connectors-to-reflect-the-model.md)に関するページを参照してください。<br /><br /> 公開されているプロパティを更新する規則を作成します。 「[規則によって変更内容がモデル内に反映される](../modeling/rules-propagate-changes-within-the-model.md)」を参照してください。<br /><br /> または、OnAssociatedPropertyChanged() を使用して、リンク矢印やフォントなどの公開されていない機能を更新します。|
|シェイプ上のアイコンが状態を示すように変化します。|[DSL の詳細] ウィンドウで、デコレーター マッピングの可視性を設定します。 同じ位置に複数のイメージ デコレーターを配置します。 [シェイプおよびコネクタの更新とモデルへの反映](../modeling/updating-shapes-and-connectors-to-reflect-the-model.md)に関するページを参照してください。<br /><br /> または、`ImageField.GetDisplayImage()` をオーバーライドします。 <xref:Microsoft.VisualStudio.Modeling.Diagrams.ImageField> の例を参照してください。|
|任意のシェイプ上に背景イメージを設定します|InitializeInstanceResources() をオーバーライドして、固定された ImageField を追加します。|
|シェイプを任意の深さの入れ子にします|再帰的な埋め込みツリーを設定します。 それらのシェイプを含めるように BoundsRules を定義します。|
|要素の境界上の固定ポイントでコネクタをアタッチします。|ダイアグラム上の小さなポートで表される埋め込みのターミナル要素を定義します。 BoundsRules を使用して、それらのポートを所定の位置に取り付けます。 サーキット ダイアグラムのサンプルについては、[Visualization and Modeling SDK](https://code.msdn.microsoft.com/Visualization-and-Modeling-313535db) に関するページを参照してください。|
|他の値から派生した値がテキスト フィールドに表示されます。|テキスト デコレーターを [計算] または [カスタム格納] ドメイン プロパティにマップします。 詳細については、「[計算プロパティおよびカスタム格納プロパティ](../modeling/calculated-and-custom-storage-properties.md)」を参照してください。|
|モデル要素間またはシェイプ間で変更を反映させます|「[ドメイン固有言語における検証](../modeling/validation-in-a-domain-specific-language.md)」を参照してください。|
|ストアの外部にあるリソース (他の Visual Studio 拡張機能など) に変更を反映させます。|「[イベント ハンドラーによって変更内容がモデル外に反映される](../modeling/event-handlers-propagate-changes-outside-the-model.md)」を参照してください。|
|プロパティ ウィンドウに関連要素のプロパティが表示されます。|プロパティ転送を設定します。 [プロパティ ウィンドウのカスタマイズ](../modeling/customizing-the-properties-window.md)に関するページを参照してください。|
|プロパティのカテゴリ|プロパティ ウィンドウは、カテゴリと呼ばれるセクションに分けられています。 ドメイン プロパティの **[カテゴリ]** を設定します。 同じカテゴリ名を持つプロパティは同じセクションに表示されます。 また、リレーションシップ ロールの **[カテゴリ]** を設定することもできます。|
|ドメイン プロパティへのユーザー アクセスを制御します|**[参照可能]** を [false] に設定すると、実行時にドメイン プロパティがプロパティ ウィンドウに表示されなくなります。 それをテキスト デコレーターにマップすることもできます。<br /><br /> **[読み取り専用]** を設定すると、ユーザーはドメイン プロパティを変更できなくなります。<br /><br /> ドメイン プロパティへのプログラム アクセスは影響を受けません。|
|DSL のモデル エクスプローラーで、ノードの名前、アイコン、可視性を変更します。|「[モデル エクスプローラーのカスタマイズ](../modeling/customizing-the-model-explorer.md)」を参照してください。|
|コピー、切り取り、貼り付けを有効にする|DSL エクスプローラーで、 **[エディター]** ノードの **[コピー貼り付けの有効化]** プロパティを設定します。|
|要素がコピーされるたびに参照リンクとそのターゲットをコピーします。 たとえば、項目に添付されたコメントをコピーします。|ソース ロールの **[コピーを反映する]** プロパティを設定します (DSL 定義図では、ドメイン リレーションシップの一方の行で表されます)。<br /><br /> より複雑な効果を達成するには、ProcessOnCopy をオーバーライドします。<br /><br /> 「[コピー動作のカスタマイズ](../modeling/customizing-copy-behavior.md)」を参照してください。|
|要素が削除されたときに関連要素の削除、親の再指定、または再リンクを行います。|リレーションシップ ロールの **[削除を反映する]** 値を設定します。 より複雑な効果を達成するには、**DomainModel.cs** で定義されている、`MyDslDeleteClosure` クラス内の `ShouldVisitRelationship` および `ShouldVisitRolePlayer` メソッドをオーバーライドします。|
|コピーおよびドラッグ アンド ドロップ時にシェイプのレイアウトと外観を保持します。|シェイプおよびコネクタを、コピーした `ElementGroupPrototype` に追加します。 オーバーライドする最も便利なメソッドは `ElementOperations.CreateElementGroupPrototype()` です<br /><br /> 「[コピー動作のカスタマイズ](../modeling/customizing-copy-behavior.md)」を参照してください。|
|現在のカーソル位置など、選択した場所に図形を貼り付けます。|`ClipboardCommandSet.ProcessOnCopy()` をオーバーライドし、`ElementOperations.Merge().` の場所固有のバージョンを使用します。「[コピー動作のカスタマイズ](../modeling/customizing-copy-behavior.md)」を参照してください。|
|貼り付け時に追加のリンクを作成します|ClipboardCommandSet.ProcessOnPasteCommand() をオーバーライドします|
|このダイアグラムからの、他の DSL および Windows 要素のドラッグ アンド ドロップを有効にします|「[方法: ドラッグ アンド ドロップ ハンドラーを追加する](../modeling/how-to-add-a-drag-and-drop-handler.md)」を参照してください|
|シェイプまたはツールを、あたかも親にドラッグしたかように、ポートなどの子シェイプにドラッグできるようにします。|ドロップされたオブジェクトを親に転送するために、ターゲット オブジェクト クラスで要素マージ ディレクティブを定義します。 「[要素作成処理および要素移動処理のカスタマイズ](../modeling/customizing-element-creation-and-movement.md)」を参照してください。|
|シェイプまたはツールをあるシェイプ上にドラッグし、追加のリンクまたはオブジェクトを作成できるようにします。 たとえば、リンク先の項目にコメントをドロップできるようにします。|ターゲット ドメイン クラスで要素マージ ディレクティブを定義し、生成されるリンクを定義します。 複雑なケースでは、カスタム コードを追加できます。 「[要素作成処理および要素移動処理のカスタマイズ](../modeling/customizing-element-creation-and-movement.md)」を参照してください。|
|1 つのツールで要素のグループを作成します。 例: 一定のポートを含むコンポーネント。|ToolboxHelper.cs 内のツールボックス初期化メソッドをオーバーライドします。 要素とそのリレーションシップ リンクを含む要素グループ プロトタイプ (EGP) を作成します。 「[ツールおよびツールボックスのカスタマイズ](../modeling/customizing-tools-and-the-toolbox.md)」を参照してください。<br /><br /> EGP にプリンシパルとポートのシェイプを含めるか、EGP がインスタンス化されるときにポート シェイプを配置するように BoundsRules を定義します。|
|1 つの接続ツールを使用して、複数の種類のリレーションシップをインスタンス化します。|そのツールによって呼び出される接続ビルダーにリンク接続ディレクティブ (LCD) を追加します。 LCD では、2 つの要素の型からリレーションシップの種類を決定します。 これを要素の状態に応じて行うようにする場合は、カスタム コードを追加できます。 「[ツールおよびツールボックスのカスタマイズ](../modeling/customizing-tools-and-the-toolbox.md)」を参照してください。|
|固定のツール - ユーザーは任意のツールをダブルクリックして、多数のシェイプやコネクタを連続して作成できます。|DSL エクスプローラーで、`Editor` ノードを選択します。 プロパティ ウィンドウで、 **[固定のツールボックス項目を使用する]** を設定します。|
|メニュー コマンドを定義します|[標準のメニュー コマンドを修正する方法](../modeling/how-to-modify-a-standard-menu-command-in-a-domain-specific-language.md)に関するページを参照してください|
|検証規則を使用してモデルを制約します|「[ドメイン固有言語における検証](../modeling/validation-in-a-domain-specific-language.md)」を参照してください|
|DSL からコード、構成ファイル、またはドキュメントを生成します。|[ドメイン固有言語からのコード生成](../modeling/generating-code-from-a-domain-specific-language.md)|
|モデルがファイルに保存される方法をカスタマイズします。|「[ファイル格納処理および XML シリアル化処理のカスタマイズ](../modeling/customizing-file-storage-and-xml-serialization.md)」を参照してください|
|モデルをデータベースまたはその他のメディアに保存します。|*YourLanguage* DocData をオーバーライドします<br /><br /> 「[ファイル格納処理および XML シリアル化処理のカスタマイズ](../modeling/customizing-file-storage-and-xml-serialization.md)」を参照してください|
|複数の DSL を統合して、1 つのアプリケーションの一部として動作するようにします。|[Visual Studio Modelbus によるモデルの統合](../modeling/integrating-models-by-using-visual-studio-modelbus.md)に関するページを参照してください。|
|サードパーティが DSL を拡張できるようにし、拡張機能を制御します。|[MEF による DSL の拡張](../modeling/extend-your-dsl-by-using-mef.md)<br /><br /> [DSL ライブラリによる DSL 間でのクラスの共有](../modeling/sharing-classes-between-dsls-by-using-a-dsl-library.md)<br /><br /> [ロック ポリシーの定義と読み取り専用セグメントの作成](../modeling/defining-a-locking-policy-to-create-read-only-segments.md)|

## <a name="see-also"></a>関連項目

- [方法: ドメイン固有言語を定義する](../modeling/how-to-define-a-domain-specific-language.md)
- [ドメイン固有言語をカスタマイズするコードの記述](../modeling/writing-code-to-customise-a-domain-specific-language.md)
- [Modeling SDK for Visual Studio - ドメイン固有言語](../modeling/modeling-sdk-for-visual-studio-domain-specific-languages.md)

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]
