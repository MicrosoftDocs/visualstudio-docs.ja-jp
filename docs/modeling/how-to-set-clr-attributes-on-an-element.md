---
title: '方法: 要素の CLR 属性を設定する'
description: System.Attribute クラスから継承する属性を追加する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.dsltools.EditAttributesDialog
helpviewer_keywords:
- Domain-Specific Language, custom attrributes
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: b11a6bd4a04bdb469cdf5c2fe2d7b78e0c0fe29a
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112387334"
---
# <a name="how-to-set-clr-attributes-on-an-element"></a>方法: 要素の CLR 属性を設定する
カスタム属性は、ドメイン要素、シェイプ、コネクタ、および図に追加できる特殊な属性です。 `System.Attribute` クラスから継承する任意の属性を追加できます。

### <a name="to-add-a-custom-attribute"></a>カスタム属性を追加するには

1. **DSL エクスプローラー** で、カスタム属性を追加する要素を選択します。

2. **プロパティ]** [ ウィンドウで、] **[カスタム属性** プロパティの横にある参照 ( **[...]** ) アイコンをクリックします。

     **[属性の編集]** ダイアログ ボックスが開きます。

3. **[名前]** 列で、 **\<add attribute>** をクリックし、属性の名前を入力します。 ENTER キーを押します。

4. 属性名の下の行には、かっこが表示されます。 この行で、属性のパラメーターの型 (たとえば `string`) を入力し、ENTER キーを押します。

5. **[名前のプロパティ]** 列に、適切な名前 (たとえば `MyString`) を入力します。

6. **[OK]** をクリックします。

     **[カスタム属性]** プロパティの属性が次の形式で表示されるようになりました。

     `[` *AttributeName* `(` *ParameterName* `=` *Type* `)]`

## <a name="see-also"></a>関連項目

- [ドメイン固有言語ツールの用語集](/previous-versions/bb126564(v=vs.100))