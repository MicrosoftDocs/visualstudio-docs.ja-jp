---
title: LINQ to SQL でストアド プロシージャを使用してデータを更新する
description: データの更新、挿入、および削除を行うには、LINQ to SQL オブジェクト リレーショナル デザイナー (O/R デザイナー) でストアド プロシージャを使用します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: e88224ab-ff61-4a3a-b6b8-6f3694546cac
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: f0b7ab161a252e1d3a89ef856325963bddffdc56
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99866854"
---
# <a name="how-to-assign-stored-procedures-to-perform-updates-inserts-and-deletes-or-designer"></a>方法: 更新、挿入、および削除を実行するストアド プロシージャを割り当てる (O/R デザイナー)

ストアド プロシージャは **O/R デザイナー** に追加でき、通常の <xref:System.Data.Linq.DataContext> メソッドとして実行できます。 これを使用して、エンティティ クラスからデータベースに変更が保存されたときに挿入、更新、および削除を実行する既定の LINQ to SQL ランタイムの動作をオーバーライドすることもできます (たとえば、<xref:System.Data.Linq.DataContext.SubmitChanges%2A> メソッドを呼び出すときなど)。

> [!NOTE]
> ストアド プロシージャが、クライアントに送信する必要のある値 (たとえば、ストアド プロシージャで計算された値) を返す場合は、ストアド プロシージャに出力パラメーターを作成します。 出力パラメーターを使用できない場合は、O/R デザイナーによって生成されたオーバーライドを利用するのではなく、部分メソッドを実装します。 データベースによって生成される値にマップされるメンバーは、INSERT 操作または UPDATE 操作が正常に完了した後で、適切な値に設定する必要があります。 詳細については、「[既定の動作をオーバーライドするときの開発者の責任](/dotnet/framework/data/adonet/sql/linq/responsibilities-of-the-developer-in-overriding-default-behavior)」を参照してください。

> [!NOTE]
> LINQ to SQL は、ID 列 (自動インクリメント)、rowguidcol 列 (データベースが生成した GUID)、およびタイムスタンプ列であれば、データベースによって生成された値を自動的に処理します。 その他の列型のデータベースが生成した値は、予想に反して null 値になります。 データベースが生成した値を返すには、手動で <xref:System.Data.Linq.Mapping.ColumnAttribute.IsDbGenerated%2A> を **true** に設定し、<xref:System.Data.Linq.Mapping.ColumnAttribute.AutoSync%2A> を [AutoSync.Always](<xref:System.Data.Linq.Mapping.AutoSync.Always>)、[AutoSync.OnInsert](<xref:System.Data.Linq.Mapping.AutoSync.OnInsert>)、または [AutoSync.OnUpdate](<xref:System.Data.Linq.Mapping.AutoSync.OnUpdate>) のいずれかに設定する必要があります。

## <a name="configure-the-update-behavior-of-an-entity-class"></a>エンティティ クラスの更新動作の構成

既定では、LINQ to SQL エンティティ クラスのデータに対して行われた変更でデータベースを更新 (挿入、更新、および削除) するロジックは、LINQ to SQL ランタイムによって提供されます。 ランタイムは、テーブルのスキーマ (列および主キー情報) に基づいて、既定の INSERT、UPDATE、および DELETE の各コマンドを作成します。 既定の動作が適切でない場合は、更新動作を構成し、テーブルのデータの操作に必要な挿入、更新、および削除を実行する特定のストアド プロシージャを割り当てることができます。 この方法は、既定の動作が生成されていない場合、たとえばエンティティ クラスがビューにマップされている場合にも実行できます。 最後に、データベースのテーブルへのアクセスには常にストアド プロシージャを通すようにすると、既定の更新動作をオーバーライドできます。

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

### <a name="to-assign-stored-procedures-to-override-the-default-behavior-of-an-entity-class"></a>ストアド プロシージャを割り当てて、エンティティ クラスの既定の動作をオーバーライドするには

1. デザイナーで **LINQ to SQL** ファイルを開きます。 (**ソリューション エクスプローラー** で **.dbml** ファイルをダブルクリックします。)

2. **サーバー エクスプローラー** または **データベース エクスプローラー** で、**[ストアド プロシージャ]** を展開し、エンティティ クラスの Insert、Update、Delete の各コマンドで使用するストアド プロシージャを探します。

3. ストアド プロシージャを **O/R デザイナー** にドラッグします。

     ストアド プロシージャが <xref:System.Data.Linq.DataContext> メソッドとしてメソッド ペインに追加されます。 詳しくは、「[DataContext メソッド (O/R デザイナー)](../data-tools/datacontext-methods-o-r-designer.md)」をご覧ください。

4. 更新の実行にストアド プロシージャを使用するエンティティ クラスを選択します。

5. **[プロパティ]** ウィンドウで、オーバーライドするコマンド (**[Insert]**、**[Update]**、または **[Delete]**) を選択します。

6. **[ランタイムを使用]** の横にある省略記号 ([...]) をクリックして、**[動作の構成]** ダイアログ ボックスを開きます。

7. **[カスタマイズ]** を選択します。

8. **[カスタマイズ]** リストで、目的のストアド プロシージャを選択します。

9. **[メソッドの引数]** および **[クラスのプロパティ]** のリストを調べて、**[メソッドの引数]** が適切な **[クラスのプロパティ]** にマップされていることを確認します。 `Update` コマンドと `Delete` コマンドについて、元のメソッド引数 (`Original_<ArgumentName>`) を元のプロパティ (`<PropertyName> (Original)`) にマップします。

    > [!NOTE]
    > 既定では、メソッド引数は名前が一致した場合にクラス プロパティにマップされます。 変更されたプロパティ名がテーブルとエンティティ クラス間で一致しなくなり、デザイナーが正しいマッピングを判断できないときは、マップ先となる同等のクラス プロパティを選択することが必要になる場合があります。

10. **[OK]** または **[適用]** をクリックします。

    > [!NOTE]
    > 変更を行うたびに **[適用]** をクリックすると、各クラスと動作の組み合わせに対して動作の構成を続けることができます。 **[適用]** をクリックする前にクラスまたは動作を変更した場合は、警告ダイアログ ボックスが表示され、ここで変更を適用できます。

更新時に既定のランタイム ロジックを使用するように戻すには、**[プロパティ]** ウィンドウで、**[Insert]**、**[Update]**、または **[Delete]** の各コマンドの横にある省略記号をクリックし、**[動作の構成]** ダイアログ ボックスで **[ランタイムを使用]** を選択します。

## <a name="see-also"></a>関連項目

- [Visual Studio の LINQ to SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
- [DataContext メソッド](../data-tools/datacontext-methods-o-r-designer.md)
- [LINQ to SQL (.NET Framework)](/dotnet/framework/data/adonet/sql/linq/index)
- [挿入、更新、および削除の各操作 (.NET Framework)](/dotnet/framework/data/adonet/sql/linq/insert-update-and-delete-operations)
