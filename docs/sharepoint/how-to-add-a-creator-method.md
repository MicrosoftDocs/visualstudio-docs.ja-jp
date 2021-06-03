---
title: '方法: Creator メソッドを追加する | Microsoft Docs'
description: Creator メソッドを追加する方法について説明します。これは、SharePoint のビジネス データ接続 (BDC) サービスでエンティティのデータ ソースに新しいデータを追加します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- BDC [SharePoint development in Visual Studio], Creator
- BDC [SharePoint development in Visual Studio], adding entity instances
- Business Data Connectivity service [SharePoint development in Visual Studio], adding entities
- Business Data Connectivity service [SharePoint development in Visual Studio], adding entity instances
- BDC [SharePoint development in Visual Studio], adding entities
- Business Data Connectivity service [SharePoint development in Visual Studio], Creator
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 950745a533fbea8d360c8bea6d839a304dd6e0d7
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106216411"
---
# <a name="how-to-add-a-creator-method"></a>方法: Creator メソッドを追加する
  Creator メソッドでは、エンティティのデータ ソースに新しいデータを追加します。 ビジネス データ接続 (BDC) サービスでは、ユーザーがモデルに基づいたリストの **[リボン]** で **[新しい項目]** ボタンを選択したときにこのメソッドを呼び出します。 詳細については、[ビジネス データ接続モデルの設計](../sharepoint/designing-a-business-data-connectivity-model.md)に関するページを参照してください。

### <a name="to-add-a-creator-method"></a>Creator メソッドを追加するには

1. **BDC デザイナー** で、エンティティを選択します。

2. メニュー バーで、 **[表示]**  >  **[その他のウィンドウ]**  > **[BDC メソッドの詳細]** の順に選択します。

    **[BDC メソッドの詳細]** ウィンドウが開きます。 そのウィンドウの詳細については、「[BDC モデルのデザイン ツールの概要](../sharepoint/bdc-model-design-tools-overview.md)」を参照してください。

3. **[メソッドの追加]** 一覧で、 **[Creator メソッドの作成]** を選択します。

    Visual Studio がモデルに次の要素を追加すると、これらの要素が **[BDC メソッドの詳細]** ウィンドウに表示されます。

   - **Create** という名前のメソッド。

   - メソッドの入力パラメーター。

   - メソッドの戻り値パラメーター。

   - パラメーターの型記述子。

   - メソッドのメソッド インスタンス。

     詳細については、[ビジネス データ接続モデルの設計](../sharepoint/designing-a-business-data-connectivity-model.md)に関するページを参照してください。

4. **ソリューション エクスプローラー** で、エンティティに対して生成されたサービス コード ファイルのショートカット メニューを開き、 **[コードの表示]** を選択します。

    エンティティ サービス コード ファイルがコード エディターで開きます。 エンティティ サービス コード ファイルの詳細については、「[ビジネス データ接続モデルを作成する](../sharepoint/creating-a-business-data-connectivity-model.md)」を参照してください。

5. Creator メソッドに、データ ソースにデータを追加するコードを追加します。 次の例では、SQL Server 用の AdventureWorks サンプル データベースに連絡先を追加します。

   > [!NOTE]
   > `ServerName` フィールドの値をサーバーの名前に置き換えてください。

    :::code language="csharp" source="../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/contactservice.cs" id="Snippet4":::
    :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/contactservice.vb" id="Snippet4":::

## <a name="see-also"></a>関連項目
- [ビジネス データ接続モデルを設計する](../sharepoint/designing-a-business-data-connectivity-model.md)
- [方法: Finder メソッドを追加する](../sharepoint/how-to-add-a-finder-method.md)
- [方法: Specific Finder メソッドを追加する](../sharepoint/how-to-add-a-specific-finder-method.md)
- [方法: Deleter メソッドを追加する](../sharepoint/how-to-add-a-deleter-method.md)
- [方法: Updater メソッドを追加する](../sharepoint/how-to-add-an-updater-method.md)
- [BDC モデルのデザイン ツールの概要](../sharepoint/bdc-model-design-tools-overview.md)
- [方法: メソッドにパラメーターを追加する](../sharepoint/how-to-add-a-parameter-to-a-method.md)
- [方法: メソッド インスタンスを定義する](../sharepoint/how-to-define-a-method-instance.md)
