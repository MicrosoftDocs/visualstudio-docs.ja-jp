---
title: 変更内容への対応および変更内容の反映
description: 要素を作成、削除、または更新するときに、その変更をモデルの他の部分または外部リソースに反映するコードを記述できることについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, events
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: d6fc8345ca90414f410dde9a089d9529ed19536b
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112387581"
---
# <a name="respond-to-and-propagate-changes"></a>変更に対応し、変更を反映する

要素を作成、削除、または更新するときに、その変更をモデルの他の部分または外部リソース (ファイル、データベース、その他のコンポーネントなど) に反映するコードを記述できます。

## <a name="reference"></a>関連項目

ガイドラインとして、これらの手法を次の順序で検討します。

|手法|シナリオ|詳細情報|
|-|-|-|
|計算されるドメイン プロパティを定義します。|モデル内の他のプロパティから計算された値を持つドメイン プロパティ。 たとえば、関連する要素の価格の合計である価格です。|[計算プロパティおよびカスタム格納プロパティ](../modeling/calculated-and-custom-storage-properties.md)|
|カスタム格納ドメイン プロパティを定義します。|モデルの他の部分または外部に格納されるドメイン プロパティ。 たとえば、式文字列をモデル内のツリーに解析することができます。|[計算プロパティおよびカスタム格納プロパティ](../modeling/calculated-and-custom-storage-properties.md)|
|OnValueChanging や OnDeleting などの変更ハンドラーをオーバーライドします。|異なる要素を同期し、外部の値をモデルと同期させます。<br /><br /> 定義された範囲に値を制限します。<br /><br /> プロパティ値およびその他の変更の直前と直後に呼び出されます。 例外をスローすることによって、変更を終了できます。|[ドメイン プロパティ値変更ハンドラー](../modeling/domain-property-value-change-handlers.md)|
|ルール|変更が発生したトランザクションの終了直前に実行されるようキューに登録されるルールを定義できます。 [元に戻す] または [やり直す] では実行されません。 それらを使用して、ストアの一部分を別の部分と同期させます。|[規則によって変更内容がモデル内に反映される](../modeling/rules-propagate-changes-within-the-model.md)|
|ストア イベント|モデリング ストアでは、要素またはリンクの追加や削除、プロパティ値の変更などのイベントの通知を提供します。 イベントは、[元に戻す] または [やり直す] でも実行されます。 ストア イベントを使用して、ストア内にない値を更新します。|[イベント ハンドラーによって変更内容がモデル外に反映される](../modeling/event-handlers-propagate-changes-outside-the-model.md)|
|.NET イベント|シェイプには、マウス クリックやその他のジェスチャに応答するイベント ハンドラーがあります。 オブジェクトごとに、これらのイベントに登録する必要があります。 通常、登録は InitializeInstanceResources のオーバーライドで実行され、各要素に対して実行される必要があります。<br /><br /> これらのイベントは、通常、トランザクションの外部で発生します。|[方法: シェイプまたはデコレーターに対するクリック操作を受け取る](../modeling/how-to-intercept-a-click-on-a-shape-or-decorator.md)|
|境界ルール|境界ルールは、特にシェイプの境界を制限するために使用されます。|[BoundsRules によってシェイプの位置とサイズが制限される](/previous-versions/visualstudio/visual-studio-2015/modeling/boundsrules-constrain-shape-location-and-size?preserve-view=true&view=vs-2015)|
|選択ルール|選択ルールでは、特にユーザーが選択できる内容を制限します。|[方法: 現在の選択項目を表示および制限する](../modeling/how-to-access-and-constrain-the-current-selection.md)|
|OnAssocatedPropertyChanged|シェイプやコネクタの特徴 (影、矢印、色、線幅、スタイルなど) を使用して、モデル要素の状態を示します。|[シェイプおよびコネクタの更新とモデルへの反映](../modeling/updating-shapes-and-connectors-to-reflect-the-model.md)|

## <a name="compare-rules-and-store-events"></a>ルールとストア イベントの比較

変更通知、ルール、およびイベントは、モデルで変更が発生したときに実行されます。

通常、ルールは変更が発生した最後のトランザクションで適用され、イベントはトランザクションの変更がコミットされた後に適用されます。

ストア イベントを使用してモデルをストアの外部にあるオブジェクトと同期し、ルールを使用してストア内の一貫性を維持します。

- **カスタム ルールの作成**: 派生クラスとして、抽象ルールからカスタム ルールを作成します。 また、カスタム ルールについてフレームワークに通知する必要があります。 詳細については、「[ルールによってモデル内の変更が反映される](../modeling/rules-propagate-changes-within-the-model.md)」を参照してください。

- **イベントのサブスクライブ**: イベントをサブスクライブする前に、イベント ハンドラーとデリゲートを作成します。 次に、<xref:Microsoft.VisualStudio.Modeling.Store.EventManagerDirectory%2A> プロパティを使用してイベントをサブスクライブします。 詳細については、「[イベント ハンドラーによって変更がモデル外に反映される](../modeling/event-handlers-propagate-changes-outside-the-model.md)」を参照してください。

- **変更を元に戻す**: トランザクションを元に戻すと、イベントが発生しますが、ルールは適用されません。 ルールによって値が変更され、その変更を元に戻すと、元に戻す操作中に値が元の値にリセットされます。 イベントが発生した場合は、値を元の値に手動で変更する必要があります。 トランザクションと元に戻すの詳細については、「[方法: トランザクションを使用してモデルを更新する](../modeling/how-to-use-transactions-to-update-the-model.md)」を参照してください。

- **ルールとイベントへのイベント引数の引き渡し**: イベントとルールの両方に、モデルがどのように変更されたかに関する情報を含む `EventArgs` パラメーターが渡されます。

## <a name="see-also"></a>関連項目

- [方法: シェイプまたはデコレーターに対するクリック操作を受け取る](../modeling/how-to-intercept-a-click-on-a-shape-or-decorator.md)
- [ドメイン固有言語をカスタマイズするコードの記述](../modeling/writing-code-to-customise-a-domain-specific-language.md)