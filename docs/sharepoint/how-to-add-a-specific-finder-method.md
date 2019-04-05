---
title: '方法: Specificfinder メソッドの追加 |Microsoft Docs'
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Business Data Connectivity service [SharePoint development in Visual Studio], Specific Finder
- BDC [SharePoint development in Visual Studio], return an entity
- BDC [SharePoint development in Visual Studio], get an entity
- Business Data Connectivity service [SharePoint development in Visual Studio], return an entity
- BDC [SharePoint development in Visual Studio], Specific Finder
- Business Data Connectivity service [SharePoint development in Visual Studio], get an entity
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: e6f52caf33820b230eb00b1be2999fe7f972176f
ms.sourcegitcommit: d0425b6b7d4b99e17ca6ac0671282bc718f80910
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/21/2019
ms.locfileid: "56615287"
---
# <a name="how-to-add-a-specific-finder-method"></a>方法: 特定の Finder メソッドを追加します。
  作成して、1 つのエンティティ インスタンスを返すことができます、 *Specificfinder*メソッド。 ビジネス データ接続 (BDC) サービスは、ユーザーがビジネス データ web パーツまたは外部の一覧でエンティティを選択すると Specificfinder メソッドを実行します。 詳細については、[ビジネス データ接続モデルを設計する](../sharepoint/designing-a-business-data-connectivity-model.md)を参照してください。

### <a name="to-create-a-specific-finder-method"></a>特定の Finder メソッドを作成するには

1. **BDC デザイナー**エンティティを選択します。

    エンティティを追加する方法については、 **BDC デザイナー** Visual Studio で、次を参照してください。[方法。エンティティ モデルを追加する](../sharepoint/how-to-add-an-entity-to-a-model.md)します。

2. メニュー バーで、**ビュー** > **その他の Windows**、 **BDC メソッドの詳細**します。

    **BDC メソッドの詳細**ウィンドウが開きます。 そのウィンドウの詳細については、[BDC モデルのデザイン ツールの概要](../sharepoint/bdc-model-design-tools-overview.md)を参照してください。

3. **メソッドを追加する**一覧で、選択**特定 Finder メソッドの作成**です。

    Visual Studio では、モデルに、次の要素を追加します。 これらの要素、 **BDC メソッドの詳細**ウィンドウ。

   - メソッド。

   - メソッドの入力パラメーター。

   - メソッドの戻り値のパラメーター。

   - 各パラメーターの型記述子。

   - メソッドのメソッドのインスタンス。

     詳細については、[ビジネス データ接続モデルを設計する](../sharepoint/designing-a-business-data-connectivity-model.md)を参照してください。

4. Visual Studio を開き**プロパティ**ウィンドウ。

5. エンティティ型記述子として戻り値パラメーターの型記述子を構成します。 エンティティ型記述子を作成する方法については、次を参照してください。[方法。パラメーターの型記述子を定義](../sharepoint/how-to-define-the-type-descriptor-of-a-parameter.md)します。

   > [!NOTE]
   >  Finder メソッドをエンティティに追加した場合、この手順を実行する必要はありません。 Visual Studio では、Finder メソッドで定義した型記述子を使用します。

   > [!NOTE]
   >  エンティティ型の識別子のフィールドが自動的に生成されるデータベース テーブル内のフィールドを表している場合は、設定、**読み取り専用**プロパティ識別子フィールドの**True**します。

6. **メソッドの詳細**ウィンドウで、メソッドのメソッドのインスタンスを選択します。

7. **プロパティ ウィンドウ**、設定、**パラメーター名を返す**プロパティ、メソッドの戻り値パラメーターの名前をします。 メソッド インスタンスのプロパティの詳細については、[MethodInstance](http://go.microsoft.com/fwlink/?LinkID=169282)を参照してください。

8. **ソリューション エクスプ ローラー**エンティティの場合に生成されたサービスのコード ファイルのショートカット メニューを開き、選択し、**コードの表示**します。

    エンティティ サービス コード ファイルがコード エディターで開きます。 詳細については、エンティティ サービス コード ファイルは、[business data connectivity モデルの作成](../sharepoint/creating-a-business-data-connectivity-model.md)を参照してください。

9. Specific Finder メソッドにコードを追加します。 このコードは次のタスクを実行します。

   - データ ソースからレコードを取得します。

   - BDC サービスにエンティティを返します。

     次の例では、SQL Server の AdventureWorks サンプル データベースから連絡先を返します。

     > [!NOTE]
     >  値を置き換える、`ServerName`フィールドに、サーバーの名前。

     [!code-csharp[SP_BDC#3](../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/contactservice.cs#3)]
     [!code-vb[SP_BDC#3](../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/contactservice.vb#3)]

## <a name="see-also"></a>関連項目
- [ビジネス データ接続モデルを設計します。](../sharepoint/designing-a-business-data-connectivity-model.md)
- [方法: Finder メソッドを追加します。](../sharepoint/how-to-add-a-finder-method.md)
- [方法: Creator メソッドを追加します。](../sharepoint/how-to-add-a-creator-method.md)
- [方法: Deleter メソッドを追加します。](../sharepoint/how-to-add-a-deleter-method.md)
- [方法: Updater メソッドを追加します。](../sharepoint/how-to-add-an-updater-method.md)
- [BDC モデルのデザイン ツールの概要](../sharepoint/bdc-model-design-tools-overview.md)
- [方法: メソッドにパラメーターを追加します。](../sharepoint/how-to-add-a-parameter-to-a-method.md)
- [方法: メソッド インスタンスを定義します。](../sharepoint/how-to-define-a-method-instance.md)
