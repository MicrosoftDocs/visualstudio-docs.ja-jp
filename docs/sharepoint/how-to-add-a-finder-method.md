---
title: '方法: Finder メソッドを追加する | Microsoft Docs'
description: Visual Studio で Finder メソッドを追加します。これにより、ビジネス データ接続 (BDC) サービスで SharePoint Web パーツまたはリスト内のエンティティの一覧を表示できるようになります。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- BDC [SharePoint development in Visual Studio], get entities
- Business Data Connectivity service [SharePoint development in Visual Studio], return entities
- BDC [SharePoint development in Visual Studio], return entities
- Business Data Connectivity service [SharePoint development in Visual Studio], Finder method
- Business Data Connectivity service [SharePoint development in Visual Studio], get entities
- BDC [SharePoint development in Visual Studio], Finder method
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 6bd75c94e2f0f557b85d945d141f952950abb2eb
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106216346"
---
# <a name="how-to-add-a-finder-method"></a>方法: Finder メソッドを追加する
  ビジネス データ接続 (BDC) サービスで Web パーツまたはリスト内のエンティティの一覧を表示できるようにするには、*Finder* メソッドを作成する必要があります。 Finder メソッドは、エンティティ インスタンスのコレクションを返す特殊なメソッドです。 詳細については、[ビジネス データ接続モデルの設計](../sharepoint/designing-a-business-data-connectivity-model.md)に関するページを参照してください。

### <a name="to-create-a-finder-method"></a>Finder メソッドを作成するには

1. **BDC デザイナー** で、エンティティを選択します。

    詳細については、「[方法: モデルにエンティティを追加する](../sharepoint/how-to-add-an-entity-to-a-model.md)」を参照してください。

2. メニュー バーで、 **[表示]**  >  **[その他のウィンドウ]**  >  **[BDC メソッドの詳細]** の順に選択します。

    **[BDC メソッドの詳細]** ウィンドウが開きます。 **[BDC メソッドの詳細]** ウィンドウの詳細については、「[BDC モデルのデザイン ツールの概要](../sharepoint/bdc-model-design-tools-overview.md)」を参照してください。

3. **[メソッドの追加]** 一覧で、 **[Finder メソッドの作成]** を選択します。

    Visual Studio によって、メソッド、戻り値パラメーター、型記述子が追加されます。

4. 型記述子をエンティティ コレクション型記述子として構成します。 エンティティ コレクション型記述子を作成する方法の詳細については、「[方法: パラメーターの型記述子を定義する](../sharepoint/how-to-define-the-type-descriptor-of-a-parameter.md)」を参照してください。

   > [!NOTE]
   > このエンティティに Specific Finder メソッドを追加している場合、この手順を実行する必要はありません。 Visual Studio では、その Specific Finder メソッドで定義されている型記述子を使用します。

5. **ソリューション エクスプローラー** で、エンティティに対して生成されたサービス コード ファイルのショートカット メニューを開き、 **[コードの表示]** を選択します。 サービス コード ファイルの詳細については、「[ビジネス データ接続モデルを作成する](../sharepoint/creating-a-business-data-connectivity-model.md)」を参照してください。

6. Finder メソッドにコードを追加します。 このコードは、以下のタスクを実行します。

   - データ ソースからデータを取得します。

   - BDC サービスにエンティティの一覧を返します。

     次の例では、SQL Server 用の AdventureWorks サンプル データベースからのデータを使用して、`Contact` エンティティのコレクションを返します。

   > [!NOTE]
   > `ServerName` フィールドの値をサーバーの名前に置き換えてください。

    :::code language="csharp" source="../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/contactservice.cs" id="Snippet2":::
    :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/contactservice.vb" id="Snippet2":::

## <a name="see-also"></a>関連項目
- [BDC モデルのデザイン ツールの概要](../sharepoint/bdc-model-design-tools-overview.md)
- [ビジネス データ接続モデルを設計する](../sharepoint/designing-a-business-data-connectivity-model.md)
- [方法: Specific Finder メソッドを追加する](../sharepoint/how-to-add-a-specific-finder-method.md)
- [方法: Creator メソッドを追加する](../sharepoint/how-to-add-a-creator-method.md)
- [方法: Deleter メソッドを追加する](../sharepoint/how-to-add-a-deleter-method.md)
- [方法: Updater メソッドを追加する](../sharepoint/how-to-add-an-updater-method.md)
- [方法: メソッドにパラメーターを追加する](../sharepoint/how-to-add-a-parameter-to-a-method.md)
- [方法: メソッド インスタンスを定義する](../sharepoint/how-to-define-a-method-instance.md)
