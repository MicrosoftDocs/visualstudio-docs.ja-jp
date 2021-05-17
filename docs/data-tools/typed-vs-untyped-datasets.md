---
title: 型指定されたデータセットと型指定されていないデータセットの比較
description: 型指定されたデータセットと型指定されていないデータセットの違いについて説明します。 型指定されたデータセットと型指定されていないデータセットのデータ アクセスを比較します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
ms.assetid: c83ba0bb-5425-4d47-8891-6b4dbf937701
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: daf4f722eb51a08e7a6ddb287e5b54956ecdfe73
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106216021"
---
# <a name="typed-vs-untyped-datasets"></a>型指定されたデータセットと型指定されていないデータセットの比較
型指定されたデータセットは、最初に基底の <xref:System.Data.DataSet> クラスから派生したデータセットであり、.xsd ファイルに格納された **データセット デザイナー** の情報を使用して、新しい厳密に型指定されたデータセット クラスを生成します。 スキーマ (テーブル、列など) からの情報が生成され、ファーストクラスのオブジェクトとプロパティのセットとして、この新しいデータセット クラスにコンパイルされます。 型指定されたデータセットは基底の <xref:System.Data.DataSet> クラスから継承しているため、型指定されたクラスは <xref:System.Data.DataSet> クラスのすべての機能を持ち、<xref:System.Data.DataSet> クラスのインスタンスをパラメーターとして受け取るメソッドで使用できます。

これに対し、型指定されていないデータセットには、対応する組み込みスキーマがありません。 型指定されたデータセットと同様に、型指定されていないデータセットにはテーブルや列などが含まれますが、これらはコレクションとしてのみ公開されます (ただし、型指定されていないデータセットのテーブルおよびその他のデータ要素を手動で作成した後は、データセットの <xref:System.Data.DataSet.WriteXmlSchema%2A> メソッドを使用して、データセットの構造をスキーマとしてエクスポートできます)。

## <a name="contrast-data-access-in-typed-and-untyped-datasets"></a>型指定されたデータセットと型指定されていないデータセットのデータ アクセスを比較する
型指定されたデータセットのクラスには、そのプロパティがテーブルと列の実際の名前を持つオブジェクト モデルがあります。 たとえば、型指定されたデータセットを操作する場合は、次のようなコードを使用して列を参照できます。

:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataDatasets/CS/Form1.cs" id="Snippet4":::
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataDatasets/VB/Form1.vb" id="Snippet4":::

これに対し、型指定されていないデータセットを操作する場合、同等のコードは次のようになります。

:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataDatasets/CS/Form1.cs" id="Snippet5":::
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataDatasets/VB/Form1.vb" id="Snippet5":::

型指定されたアクセスは、読みやすくなるだけでなく、Visual Studio **コード エディター** の IntelliSense でも完全にサポートされています。 型指定されたデータセットの構文では、操作が簡単になるだけでなく、コンパイル時に型チェックが行われるため、データセットのメンバーに値を代入する際にエラーが発生する可能性が大幅に減少します。 <xref:System.Data.DataSet> クラスの列の名前を変更してからアプリケーションをコンパイルすると、ビルド エラーが発生します。 **[タスク一覧]** でビルド エラーをダブルクリックすると、以前の列名を参照する行またはコード行に直接移動できます。 型指定されたデータセット内のテーブルと列へのアクセスも、実行時に多少高速になります。これは、実行時にコレクションを使用するのではなく、コンパイル時にアクセスが決定されるためです。

型指定されたデータセットには多くの利点がありますが、型指定されていないデータセットはさまざまな状況で役立ちます。 最も明白なシナリオは、データセットで使用できるスキーマがない場合です。 このような状況は、データセットを返すコンポーネントをアプリケーションで操作していても、その構造を事前に把握していない場合などに発生する可能性があります。 同様に、静的で予測可能な構造を持たないデータを操作する場合もあります。 この場合、型指定されたデータセットを使用するのは現実的ではありません。データ構造の変更を行うたびに、型指定されたデータセット クラスを再生成する必要があるためです。

一般に、スキーマが使用できなくてもデータセットを動的に作成する場合は多くあります。 その場合、データをリレーショナルな方法で表現できる限り、データセットは情報を保持できる便利な構造に過ぎません。 同時に、データセットの機能を利用して、別のプロセスに渡す情報をシリアル化したり、XML ファイルを書き出したりすることができます。

## <a name="see-also"></a>関連項目

- [データセットのツール](../data-tools/dataset-tools-in-visual-studio.md)
