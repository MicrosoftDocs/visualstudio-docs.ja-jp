---
title: スイムレーンのプロパティ
description: スイムレーンを使用してダイアグラムを縦または横の領域に分割し、スイムレーンの内部に表示する他の図形を定義する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.dsltools.dsldesigner.swimlane
helpviewer_keywords:
- Domain-Specific Language, swimlane
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 9c171bda2670b698297dd876a8a4403a91cd4af7
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112386489"
---
# <a name="properties-of-swimlanes"></a>スイムレーンのプロパティ
スイムレーンを図に追加できます。 図はスイムレーンによって縦または横に並んだ領域に分割されます。 スイムレーンの内部に表示される他の図形を定義できます。 詳細については、「[方法: ドメイン固有言語を定義する](../modeling/how-to-define-a-domain-specific-language.md)」を参照してください。 これらのプロパティの使用方法の詳細については、「[ドメイン固有言語のカスタマイズと拡張](../modeling/customizing-and-extending-a-domain-specific-language.md)」を参照してください。

 スイムレーンには、次の表に示すプロパティがあります。

|プロパティ|説明|Default|
|-|-|-|
|Body Fill Color|スイムレーンの本体の塗りつぶしの色。|白|
|Header Fill Color|スイムレーンのヘッダーの塗りつぶしの色。|濃い灰色|
|Separator Color|区切り線の色。|LightGray|
|Separator Line Style|区切り線のスタイル (`Solid`、`Dash`、`Dot`、`DashDot`、`DashDotDot`、`Custom`)。|`Dash`|
|Separator Thickness|区切り線の太さ (インチ単位)。|0.03125|
|Text Color|このスイムレーンに関連付けられているテキスト デコレーターに使用される色。|Black|
|アクセス修飾子|クラスのアクセスのレベル (`public` または `internal`)。|パブリック|
|カスタム属性|このスイムレーンから生成されるコード クラスに属性を追加するために使用されます。|\<none>|
|Generates Double Derived|`True` の場合、(オーバーライドによるカスタマイズをサポートするために) 基底クラスと部分クラスの両方が生成されます。 詳細については、「[生成されたクラスをオーバーライドして拡張する](../modeling/overriding-and-extending-the-generated-classes.md)」を参照してください。|False|
|カスタム コンストラクターがある|`True` の場合、ソース コードにカスタム コンストラクターが用意されます。 詳細については、「[生成されたクラスをオーバーライドして拡張する](../modeling/overriding-and-extending-the-generated-classes.md)」を参照してください。|False|
|Inheritance Modifier|スイムレーンから生成されるソース コード クラスの継承の種類を記述します(`none`、`abstract`、`sealed`)。|なし|
|Base Swimlane|このスイムレーンの基底クラス。|(なし)|
|名前|このスイムレーンの名前。|現在の名前|
|名前空間|このスイムレーンに関係する名前空間。|現在の名前空間|
|Tooltip Type|ツールヒントの定義方法 (`fixed`、`variable`、`none`)。 `fixed` の場合は、`Fixed Tooltip Text` プロパティの値が使用されます。`variable` の場合は、ツールヒントはカスタム コードで定義されます。|\<none>|
|メモ|このスイムレーンに関連付けられる私的な覚書。|\<none>|
|アラインメント|横または縦の配置。|Vertical|
|Initial Height|このスイムレーンの初期の高さ (インチ単位)。 横方向スイムレーンにのみ適用されます。|0|
|Initial Width|このスイムレーンの初期の幅 (インチ単位)。 縦方向のスイムレーンにのみ適用されます。|0|
|Exposes Text Color|`True` の場合、ユーザーは生成されたデザイナーでスイムレーンの色を設定できます。 これを設定するには、スイムレーンの図形を右クリックして、 **[公開済みの項目を追加]** をクリックします。|False|
|説明|生成されたデザイナーを文書化するために使用します。|\<none>|
|表示名|生成されたデザイナーで、このスイムレーン クラスを示すために表示される名前。|\<none>|
|Fixed Tooltip Text|固定のツールヒントに使用されるテキスト。|\<none>|
|ヘルプ キーワード|このスイムレーンに対する F1 ヘルプのインデックスを作成するために使用されるキーワード。|\<none>|

## <a name="see-also"></a>こちらもご覧ください

- [ドメイン固有言語ツールの用語集](/previous-versions/bb126564(v=vs.100))