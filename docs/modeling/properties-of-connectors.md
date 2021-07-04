---
title: コネクタのプロパティ
description: 生成されたデザイナーのドメインリレーションシップがコネクタによって表されること、およびこれらのプロパティを使用してドメイン固有言語をカスタマイズおよび拡張することについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Domain-Specific Language, connectors
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 43f55aecf134bf8e4d043a4fc7f6ffa2201f8e95
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112390816"
---
# <a name="properties-of-connectors"></a>コネクタのプロパティ
コネクタは、生成されたデザイナーでのドメインのリレーションシップを表します。

 詳細については、「[方法: ドメイン固有言語を定義する](../modeling/how-to-define-a-domain-specific-language.md)」を参照してください。 これらのプロパティの使用方法の詳細については、「[ドメイン固有言語のカスタマイズと拡張](../modeling/customizing-and-extending-a-domain-specific-language.md)」を参照してください。

 コネクタには、次の表に示すプロパティがあります。

|プロパティ|説明|Default|
|-|-|-|
|Color|このコネクタの色。|Black|
|Dash Style|このコネクタの線の破線スタイル (Solid、Dash、Dot、DashDot、DashDotDot、Custom)。|[実線]|
|Source End Style|このコネクタのソース端のスタイル (HollowArrow、EmptyArrow、FilledArrow、EmptyDiamond、FilledDiamond、None)。|なし|
|Target End Style|このコネクタのターゲット端のスタイル (HollowArrow、EmptyArrow、FilledArrow、EmptyDiamond、FilledDiamond、None)。|なし|
|Text Color|このコネクタに関連付けられているテキスト デコレーターに使用される色。|Black|
|太さ|このコネクタの線の太さ (インチ単位で測定)。|0.03125|
|アクセス修飾子|クラスのアクセスのレベル (`public` または `internal`)。|パブリック|
|カスタム属性|このコネクタから生成されるソース コード クラスに属性を追加するために使用されます。|\<none>|
|Generates Double Derived|`True` の場合、(オーバーライドによるカスタマイズをサポートするために) 基底クラスと部分クラスの両方が生成されます。 詳細については、「[生成されたクラスをオーバーライドして拡張する](../modeling/overriding-and-extending-the-generated-classes.md)」を参照してください。|False|
|カスタム コンストラクターがある|`True` の場合、ソース コードにカスタム コンストラクターが用意されます。 詳細については、「[生成されたクラスをオーバーライドして拡張する](../modeling/overriding-and-extending-the-generated-classes.md)」を参照してください。|False|
|Inheritance Modifier|コネクタから生成されるソース コード クラスの継承の種類を記述します (`none`、`abstract`、`sealed`)。|なし|
|Base Connector|このコネクタの基底クラス。|(なし)|
|名前|このコネクタの名前。|現在の名前|
|名前空間|このコネクタに関係する名前空間。|現在の名前空間|
|Tooltip Type|ツールヒントがどのように定義されるか (固定、変数、またはなし)。 固定の場合は、`Fixed Tooltip Text` プロパティの値がツールヒントとして使用されます。変数の場合、ツールヒントはカスタム コードで定義されます。|\<none>|
|メモ|このコネクタに関連付けられる私的な覚書。|\<none>|
|Routing Style|コネクタのルーティングに使用されるスタイル。 `Rectilinear` コネクタは、必要に応じて直角に曲がります。`Straight` コネクタは曲がりません。|Rectilinear|
|Exposed Color As Property<br /><br /> Exposed Dash Style As Property<br /><br /> Exposed Thickness As Property<br /><br /> Exposes Text Color|`True` の場合、ユーザーは指定された図形のプロパティを設定できます。 これを設定するには、図形の定義を右クリックし、 **[公開済みの項目を追加]** をクリックします。|False|
|説明|生成されたデザイナーを文書化するために使用します。|\<none>|
|表示名|生成されたデザイナーに表示されるこのコネクタの名前。|\<none>|
|Fixed Tooltip Text|固定のツールヒントに使用されるテキスト。|\<none>|
|ヘルプ キーワード|この要素に対する F1 ヘルプのインデックスを作成するために使用されるキーワード。|\<none>|

## <a name="see-also"></a>こちらもご覧ください

- [ドメイン固有言語ツールの用語集](/previous-versions/bb126564(v=vs.100))