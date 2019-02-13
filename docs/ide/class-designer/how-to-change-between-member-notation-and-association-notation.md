---
title: '方法: メンバー表記と関連付け表記の間で変更する (クラス デザイナー)'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- notation, member
- association notation
- member notation
- notation, association
ms.assetid: 65881c5a-d251-4a36-ad0d-73d088436092
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0138ec1e2a36ce20b80982103ec408077502993a
ms.sourcegitcommit: 21d667104199c2493accec20c2388cf674b195c3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2019
ms.locfileid: "55913825"
---
# <a name="how-to-change-between-member-notation-and-association-notation-in-class-designer"></a>方法: クラス デザイナーでメンバー表記と関連付け表記の間で変更する

**クラス デザイナー**では、クラス ダイアグラムで 2 つの型の間の関連付けの関係が表される方法を、メンバー表記から関連付け表記に、またはその逆に、変更できます。 関連行として表示されるメンバーは、多くの場合、型の関連をわかりやすく視覚化します。

> [!NOTE]
> 関連付けの関係は、メンバー プロパティまたはフィールドとして表すことができます。 メンバー表記を関連付け表記に変更するには、一方の型に別の型のメンバーが含まれている必要があります。 関連付け表記をメンバー表記に変更するには、2 つの型が関連行によって接続されている必要があります。 詳細については、「[方法 :型の間の関連付けを作成する方法](how-to-create-associations-between-types.md)に関する記事をご覧ください。 プロジェクトに複数のクラス ダイアグラムが含まれている場合、ダイアグラムでの関連付けの関係の表示方法に対する変更は、そのダイアグラムだけに適用されます。 別のダイアグラムでの関連付けの関係の表示方法を変更するには、そのダイアグラムを開くか表示して、次の手順を実行します。

## <a name="to-change-member-notation-to-association-notation"></a>メンバー表記を関連付け表記に変更するには

1.  ソリューション エクスプローラーのプロジェクト ノードから、クラス ダイアグラム (.cd) ファイルを開きます。

2.  クラス ダイアグラムの型の図形で、メンバー プロパティまたは関連付けを表すフィールドを右クリックして、**[関連として表示]** を選びます。

    > [!TIP]
    > 型の図形にプロパティまたはフィールドが表示されていない場合は、図形のコンパートメントが折りたたまれている可能性があります。 型の図形を展開するには、コンパートメントの名前をダブルクリックするか、または型の図形を右クリックして **[展開]** を選びます。

    型の図形のコンパートメントにメンバーが表示されなくなり、2 つの型を接続する関連行が表示されます。 関連行のラベルには、プロパティまたはフィールドの名前が表示されます。

## <a name="to-change-association-notation-to-member-notation"></a>関連付け表記をメンバー表記に変更するには

クラス ダイアグラムで関連行を右クリックし、**[プロパティとして表示]** または **[フィールドとして表示]** を選びます。 関連行が表示されなくなり、ダイアグラムの型の図形内の適切なコンパートメントにプロパティが表示されます。

## <a name="see-also"></a>関連項目

- [方法: 型の間の継承を作成する](how-to-create-inheritance-between-types.md)
- [方法: 型の間の継承を表示する](how-to-view-inheritance-between-types.md)
- [型およびリレーションシップの表示](designing-and-viewing-classes-and-types.md)
- [方法: コレクションの関連付けを視覚化する](how-to-visualize-a-collection-association.md)