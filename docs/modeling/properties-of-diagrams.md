---
title: 図のプロパティ
description: 図について、および生成されたデザイナーでの図の表示方法を指定するプロパティを設定する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 10/31/2018
ms.topic: reference
f1_keywords:
- vs.dsltools.dsldesigner.dsldiagram
helpviewer_keywords:
- Domain-Specific Language, diagram
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 943b634114c28f6f914926c74861a902c663523e
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99956166"
---
# <a name="properties-of-diagrams"></a>図のプロパティ
生成されたデザイナーでの図の表示方法を指定するプロパティを設定できます。 たとえば、図のテキストの既定の色を指定できます。

 詳細については、「[方法: ドメイン固有言語を定義する](../modeling/how-to-define-a-domain-specific-language.md)」を参照してください。 これらのプロパティの使用方法の詳細については、「[ドメイン固有言語のカスタマイズと拡張](../modeling/customizing-and-extending-a-domain-specific-language.md)」を参照してください。

 図のプロパティを次の表に示します。

|プロパティ|説明|Default|
|-|-|-|
|[塗りつぶしの色]|図の塗りつぶしの色。|白|
|テキストの色|図に表示されるテキストの色。|Black|
|アクセス修飾子|クラスのアクセス修飾子 (public または internal)。|パブリック|
|カスタム属性|生成されたコード クラスに属性を追加するために使用されます。|\<none>|
|2 つの派生を生成する|`True` の場合、(オーバーライドによるカスタマイズをサポートするために) 基底クラスと部分クラスの両方が生成されます。 詳細については、「[オーバーライドして生成されたクラスを拡張する](../modeling/overriding-and-extending-the-generated-classes.md)」を参照してください。|False|
|カスタム コンストラクターがある|`True` の場合、ソース コードにカスタム コンストラクターが用意されます。 詳細については、「[生成されたクラスをオーバーライドして拡張する](../modeling/overriding-and-extending-the-generated-classes.md)」を参照してください。|False|
|継承修飾子|図から生成されるソース コード クラスの継承の種類 (`none`、`abstract`、または `sealed`) を記述します。|なし|
|基本の図|この図の基底クラス。|(なし)|
|名前|この図の名前。|現在の名前|
|名前空間|この図に関係する名前空間。|現在の名前空間|
|Class Represented\(表現されるクラス\)|この図が表現するルート ドメイン クラス。|現在のルート クラス (該当する場合)|
|メモ|この要素に関連付けられる私的な覚書。|\<none>|
|塗りつぶしの色をプロパティとして公開する|`True` の場合、ユーザーは、生成されたデザイナーの図の塗りつぶしの色を設定できます。 このプロパティを設定するには、図形を右クリックし、 **[公開済みの項目を追加]** をクリックします。|False|
|テキストの色をプロパティとして公開する|`True` の場合、ユーザーは、生成されたデザイナーの図のテキストの色を設定できます。 このプロパティを設定するには、図形を右クリックし、 **[公開済みの項目を追加]** をクリックします。|False|
|説明|生成されたデザイナーを文書化するために使用される説明。|\<none>|
|表示名|生成されたデザイナーに表示されるこの図の名前。|\<none>|
|ヘルプ キーワード|この図に対する F1 ヘルプのインデックスを作成するために使用されるキーワード。|\<none>|

## <a name="see-also"></a>こちらもご覧ください

[ドメイン固有言語ツールの用語集](/previous-versions/bb126564(v=vs.100))