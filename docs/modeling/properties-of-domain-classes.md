---
title: ドメイン クラスのプロパティ
description: アクセス修飾子、カスタム属性、2 つの派生を生成するなど、ドメイン クラスのさまざまなプロパティについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Domain-Specific Language, domain class
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: cc86f04841a819423bc45c9220d6de80a5340b2d
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99915997"
---
# <a name="properties-of-domain-classes"></a>ドメイン クラスのプロパティ
ドメイン クラスには、次の表に示したプロパティがあります。 ドメイン クラスについては、「[モデル、クラス、およびリレーションシップについて」](../modeling/understanding-models-classes-and-relationships.md)を参照してください。 これらのプロパティの使用方法の詳細については、「[ドメイン固有言語のカスタマイズおよび拡張](../modeling/customizing-and-extending-a-domain-specific-language.md)」を参照してください。

|プロパティ|説明|Default|
|-|-|-|
|アクセス修飾子|ドメイン クラスのアクセスのレベル (`public` または `internal`)。|`public`|
|カスタム属性|このドメイン クラスから生成されるソース コード クラスに属性を追加するために使用されます。|\<none>|
|2 つの派生を生成する|`True` の場合、(オーバーライドによるカスタマイズをサポートするために) 基底クラスと部分クラスの両方が生成されます。 詳細については、「[生成されたクラスをオーバーライドして拡張する](../modeling/overriding-and-extending-the-generated-classes.md)」を参照してください。|`False`|
|カスタム コンストラクターがある|`True` の場合、ソース コードにカスタム コンストラクターが用意されます。 詳細については、「[生成されたクラスをオーバーライドして拡張する](../modeling/overriding-and-extending-the-generated-classes.md)」を参照してください。|`False`|
|継承修飾子|ドメイン クラスから生成されるソース コード クラスの継承の種類 (`none`、`abstract`、または `sealed`) を記述します。|`none`|
|基底クラス|このドメイン クラスが派生している場合は、基底クラスの名前。|\<none>|
|名前|このドメイン クラスの名前。|現在の名前|
|名前空間|このドメイン クラスの名前空間。|現在の名前空間|
|Notes|このドメイン クラスに関連付けられる非公式な注釈。|\<none>|
|説明|生成されたデザイナーの UI を文書化するために使用される説明。|\<none>|
|表示名|生成されたデザイナーで、このドメイン クラス向けに表示される名前。|\<none>|
|ヘルプ キーワード|このドメイン クラスに対して、F1 ヘルプのインデックスを作成するために使用される、オプションのキーワード。|\<none>|

## <a name="see-also"></a>関連項目

- [ドメイン固有言語ツールの用語集](/previous-versions/bb126564(v=vs.100))