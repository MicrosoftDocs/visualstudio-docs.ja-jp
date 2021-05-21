---
title: データセット間にリレーションシップを作成する
description: Visual Studio でデータセット間にリレーションシップを作成します。 DataRelation オブジェクトと制約について説明します。 データセット マネージャーでデータのリレーションシップを手動で作成します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vbData.Microsoft.VSDesigner.DataSource.DesignRelation
- vbdata.Microsoft.VSDesigner.DataSource.DesignRelation
helpviewer_keywords:
- relationships, about relationships
- datasets [Visual Basic], relationships
- relationships, datasets
ms.assetid: cfe274f0-71fe-40f6-994e-7c7f6273c9ba
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: 92e1a03a9a72b550c77aa734c4a9ff2d0b184839
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99866607"
---
# <a name="create-relationships-between-datasets"></a>データセット間にリレーションシップを作成する
関連するデータ テーブルが含まれるデータセットでは、テーブル間の親子関係を表し、相互に関連するレコードを返すために、<xref:System.Data.DataRelation> オブジェクトが使用されます。 **データ ソース構成ウィザード** または **データセット デザイナー** を使用して、関連するテーブルをデータセットに追加すると、<xref:System.Data.DataRelation> オブジェクトが自動的に作成および構成されます。

<xref:System.Data.DataRelation> オブジェクトにより、次の 2 つの機能が実行されます。

- ユーザーが作業しているレコードに関連するレコードを利用できるようにします。 ユーザーが親レコードを使用している場合は子レコードが提供され (<xref:System.Data.DataRow.GetChildRows%2A>)、子レコードを使用している場合は親レコードが提供されます (<xref:System.Data.DataRow.GetParentRow%2A>)。

- 参照整合性の制約を適用できます (たとえば、親レコードを削除すると、関連する子レコードが削除されます)。

真の結合と、<xref:System.Data.DataRelation> オブジェクトの関数の違いを理解しておくことが重要です。 真の結合では、親テーブルと子テーブルからレコードが取得され、1 つのフラット レコードセットに格納されます。 <xref:System.Data.DataRelation> オブジェクトを使用すると、新しいレコードセットは作成されません。 代わりに、DataRelation によってテーブル間のリレーションシップが追跡され、親レコードと子レコードの同期が維持されます。

## <a name="datarelation-objects-and-constraints"></a>DataRelation のオブジェクトと制約
<xref:System.Data.DataRelation> オブジェクトは、次の制約を作成して適用するためにも使用されます。

- 一意制約。テーブル内の列に重複が含まれていないことが保証されます。

- 外部キー制約。データセット内の親テーブルと子テーブルの間の参照整合性を維持するために使用できます。

<xref:System.Data.DataRelation> オブジェクトで指定する制約は、自動的に適切なオブジェクトを作成するか、プロパティを設定することによって実装されます。 <xref:System.Data.DataRelation> オブジェクトを使用して外部キー制約を作成すると、<xref:System.Data.ForeignKeyConstraint> クラスのインスタンスが <xref:System.Data.DataRelation> オブジェクトの <xref:System.Data.DataRelation.ChildKeyConstraint%2A> プロパティに追加されます。

一意制約は、単にデータ列の <xref:System.Data.DataColumn.Unique%2A> プロパティを `true` に設定することによって、または <xref:System.Data.UniqueConstraint> クラスのインスタンスを <xref:System.Data.DataRelation> オブジェクトの <xref:System.Data.DataRelation.ParentKeyConstraint%2A> プロパティに追加することによって、実装されます。 データセットの制約を中断する方法の詳細については、「[データセットの読み込み中に制約をオフにする](../data-tools/turn-off-constraints-while-filling-a-dataset.md)」を参照してください。

### <a name="referential-integrity-rules"></a>参照整合性の規則
外部キー制約の一部として、次の 3 つのタイミングで適用される参照整合性規則を指定できます。

- 親レコードが更新されたとき

- 親レコードが削除されたとき

- 変更が受け入れられるか拒否されたとき

作成できる規則は、<xref:System.Data.Rule> 列挙型で指定されています。次の表にそれを示します。

|外部キー制約の規則|アクション|
| - |------------|
|<xref:System.Data.Rule.Cascade>|親レコードに対して行われた変更 (更新または削除) が、子テーブルの関連レコードでも行われます。|
|<xref:System.Data.Rule.SetNull>|子レコードは削除されませんが、子レコードの外部キーは <xref:System.DBNull> に設定されます。 この設定では、子レコードを "孤立" として残すことができます。つまり、それらは親レコードとのリレーションシップがありません。 **注:** この規則を使用すると、子テーブルに無効なデータが発生する可能性があります。|
|<xref:System.Data.Rule.SetDefault>|関連する子レコードの外部キーは、(列の <xref:System.Data.DataColumn.DefaultValue%2A> プロパティによって設定される) 既定値に設定されます。|
|<xref:System.Data.Rule.None>|関連する子レコードは変更されません。 この設定では、子レコードに無効な親レコードへの参照を含めることができます。|

データセットのテーブルの更新について詳しくは、「[データをデータベースに保存する](../data-tools/save-data-back-to-the-database.md)」を参照してください。

### <a name="constraint-only-relations"></a>制約のみのリレーションシップ
<xref:System.Data.DataRelation> オブジェクトを作成するときに、制約を適用するためにのみリレーションシップを使用することを指定できます。つまり、関連するレコードへのアクセスには使用されません。 このオプションを使用すると、関連レコード機能を持つものより、少しだけ効率的で、含まれるメソッドが少ないデータセットを生成できます。 ただし、関連するレコードにアクセスすることはできません。 たとえば、制約のみのリレーションシップを使用すると、まだ子レコードがある親レコードを削除することはできず、親を介して子レコードにアクセスすることもできません。

## <a name="manually-creating-a-data-relation-in-the-dataset-designer"></a>データセット デザイナーでのデータのリレーションシップの手動作成
Visual Studio のデータ デザイン ツールを使用してデータ テーブルを作成するとき、データのソースから情報を収集できる場合は、リレーションシップが自動的に作成されます。 **ツールボックス** の **[データセット]** タブから手動でデータ テーブルを追加する場合は、リレーションシップの手動作成が必要になる場合があります。 プログラムによる <xref:System.Data.DataRelation> オブジェクトの作成については、「[DataRelation の追加](/dotnet/framework/data/adonet/dataset-datatable-dataview/adding-datarelations)」を参照してください。

データ テーブル間のリレーションシップは、**データセット デザイナー** では線として表示され、キーと無限大のグリフによってリレーションシップの一対多の側面が示されます。 既定では、リレーションシップの名前はデザイン サーフェイスに表示されません。

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

#### <a name="to-create-a-relationship-between-two-data-tables"></a>2 つのデータ テーブル間にリレーションシップを作成するには

1. **データセット デザイナー** でご自分のデータセットを開きます。 詳細については、「[チュートリアル: データセット デザイナーを使用したデータセットの作成](walkthrough-creating-a-dataset-with-the-dataset-designer.md)」を参照してください。

2. **[データセット]** ツールボックスから **Relation** オブジェクトをリレーションシップの子データ テーブルにドラッグします。

     **[リレーションシップ]** ダイアログ ボックスが開き、 **[子テーブル]** ボックスに **Relation** オブジェクトをドラッグしたテーブルが設定されます。

3. **[親テーブル]** ボックスから親テーブルを選択します。 親テーブルには、一対多リレーションシップの "一" 側のレコードが含まれます。

4. **[子テーブル]** ボックスに正しい子テーブルが表示されていることを確認します。 子テーブルには、一対多リレーションシップの "多" 側のレコードが含まれます。

5. **[名前]** ボックスにリレーションシップの名前を入力するか、選択したテーブルに基づく既定の名前をそのまま使用します。 これは、コード内の実際の <xref:System.Data.DataRelation> オブジェクトの名前です。

6. **[キー列]** と **[外部キー列]** の一覧で、テーブルを結合する列を選択します。

7. リレーションシップと制約のどちらか一方または両方を作成するかどうかを選択します。

8. **[入れ子になった関係]** ボックスをオンまたはオフにします。 このオプションを音にすると、<xref:System.Data.DataRelation.Nested%2A> プロパティが `true` に設定され、それらの行が XML データとして書き込まれるとき、または <xref:System.Xml.XmlDataDocument> と同期されるときに、リレーションシップの子の行が親の列に入れ子にされます。 詳しくは、「[DataRelation の入れ子化](/dotnet/framework/data/adonet/dataset-datatable-dataview/nesting-datarelations)」をご覧ください。

9. これらのテーブルのレコードを変更するときに適用される規則を設定します。 詳細については、「<xref:System.Data.Rule>」を参照してください。

10. **[OK]** をクリックしてリレーションシップを作成します。 デザイナーで 2 つのテーブルの間にリレーションシップの線が表示されます。

#### <a name="to-display-a-relation-name-in-the-dataset-designer"></a>データセット デザイナーでリレーションシップの名前を表示するには

1. **データセット デザイナー** でご自分のデータセットを開きます。 詳細については、「[チュートリアル: データセット デザイナーを使用したデータセットの作成](walkthrough-creating-a-dataset-with-the-dataset-designer.md)」を参照してください。

2. **[データ]** メニューの **[リレーションシップ ラベルの表示]** を選択して、リレーションシップ名を表示します。 リレーションシップ名を非表示にするには、そのコマンドをオフにします。

## <a name="see-also"></a>こちらもご覧ください

- [Visual Studio でデータセットを作成および構成する](../data-tools/create-and-configure-datasets-in-visual-studio.md)
