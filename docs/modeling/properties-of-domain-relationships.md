---
title: ドメイン リレーションシップのプロパティ
description: ドメイン リレーションシップに関連付けられているプロパティ ([アクセス修飾子]、[カスタム属性]、[2 つの派生を生成する] など) について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Domain-Specific Language, domain relationships
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 6fb50018dccbe03512c8ab6e5f07c17dbcee307d
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99941334"
---
# <a name="properties-of-domain-relationships"></a>ドメイン リレーションシップのプロパティ
次の表に示すプロパティは、ドメイン リレーションシップに関連付けられています。 ドメイン リレーションシップについては、「[モデル、クラス、およびリレーションシップについて」](../modeling/understanding-models-classes-and-relationships.md)を参照してください。 これらのプロパティの使用方法の詳細については、「[ドメイン固有言語のカスタマイズおよび拡張](../modeling/customizing-and-extending-a-domain-specific-language.md)」を参照してください。

|プロパティ|説明|Default|
|-|-|-|
|アクセス修飾子|ドメイン リレーションシップのアクセスのレベル (`public` または `internal`)。|`public`|
|カスタム属性|ドメイン リレーションシップから生成されるソース コード クラスに属性を追加するために使用されます。|\<none>|
|二重派生を生成する|`True` の場合、(オーバーライドによるカスタマイズをサポートするために) 基底クラスと部分クラスの両方が生成されます。 詳細については、「[生成されたクラスをオーバーライドして拡張する](../modeling/overriding-and-extending-the-generated-classes.md)」を参照してください。|`False`|
|カスタム コンストラクターを含む|`True` の場合、ソース コード内にカスタム コンストラクターが指定されていることを示します。 詳細については、「[生成されたクラスをオーバーライドして拡張する](../modeling/overriding-and-extending-the-generated-classes.md)」を参照してください。|`False`|
|継承修飾子|ドメイン リレーションシップから生成されるソース コード クラスの継承の種類 (`none`、`abstract`、または `sealed`) を記述します。|\<none>|
|重複を許可する|`True` の場合、同じ 2 つの要素間にドメイン リレーションシップの重複リンクを作成できます。|`False`|
|ベース リレーションシップ|ドメイン リレーションシップが派生している場合は、そのドメイン リレーションシップのベース リレーションシップ。|\<none>|
|埋め込み|`True` の場合、そのドメイン リレーションシップは埋め込みリレーションシップです。 `False` の場合、そのドメイン リレーションシップは参照リレーションシップです。|\<both>|
|名前|ドメイン リレーションシップの名前。|現在の名前|
|名前空間|ドメイン リレーションシップに関係する名前空間。|現在の名前空間|
|Notes|ドメイン リレーションシップに関連付けられる非公式のメモ。|\<none>|
|説明|コードを文書化するために使用され、生成されたデザイナーの UI 内で使用される説明。|\<none>|
|表示名|生成されたデザイナーに表示される、ドメイン リレーションシップの名前。|\<none>|
|ヘルプ キーワード|ドメイン リレーションシップ用の F1 ヘルプのインデックスを作成するために使用されるオプションのキーワード。|\<none>|

## <a name="see-also"></a>関連項目

- [ドメイン固有言語ツールの用語集](/previous-versions/bb126564(v=vs.100))