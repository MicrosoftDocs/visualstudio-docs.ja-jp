---
title: '方法: Deleter メソッドを追加する | Microsoft Docs'
description: エンド ユーザーが SharePoint サイト上の外部リストからデータ レコードを削除できるように、Visual Studio の BDC デザイナーで Deleter メソッドを追加する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- BDC [SharePoint development in Visual Studio], deleting data
- Business Data Connectivity service [SharePoint development in Visual Studio], Deleter
- BDC [SharePoint development in Visual Studio], Deleter
- BDC [SharePoint development in Visual Studio], removing data
- BDC [SharePoint development in Visual Studio], deleting entity instances
- Business Data Connectivity service [SharePoint development in Visual Studio], deleting entity instances
- Business Data Connectivity service [SharePoint development in Visual Studio], deleting data
- Business Data Connectivity service [SharePoint development in Visual Studio], removing data
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: f5c9dc0a5ca6b7651b4ddc1f4b58a8b72305a1a5
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106217997"
---
# <a name="how-to-add-a-deleter-method"></a>方法: Deleter メソッドを追加する
  モデルに Deleter メソッドを追加することによって、エンド ユーザーが SharePoint サイト上の外部リストからデータ レコードを削除できるようにすることができます。 詳細については、[ビジネス データ接続モデルの設計](../sharepoint/designing-a-business-data-connectivity-model.md)に関するページを参照してください。

### <a name="to-create-a-deleter-method"></a>Deleter メソッドを作成するには

1. **BDC デザイナー** で、エンティティを選択します。

2. メニュー バーで、 **[表示]**  >  **[その他のウィンドウ]**  >  **[BDC メソッドの詳細]** の順に選択します。

    **[BDC メソッドの詳細]** ウィンドウが開きます。 このウィンドウの詳細については、「[BDC モデルのデザイン ツールの概要](../sharepoint/bdc-model-design-tools-overview.md)」を参照してください。

3. **[メソッドの追加]** 一覧で、 **[Deleter メソッドの作成]** を選択します。

    Visual Studio により、次の要素がモデルに追加されます。 これらの要素は、 **[BDC メソッドの詳細]** ウィンドウに表示されます。

   - **Delete** という名前のメソッド。

   - メソッドの入力パラメーター。

   - パラメーターの型記述子。

   - メソッドのメソッド インスタンス。

     詳細については、[ビジネス データ接続モデルの設計](../sharepoint/designing-a-business-data-connectivity-model.md)に関するページを参照してください。

4. **ソリューション エクスプローラー** で、エンティティに対して生成されたサービス コード ファイルのショートカット メニューを開き、 **[コードの表示]** を選択します。

    エンティティ サービス コード ファイルがコード エディターで開きます。 エンティティ サービス コード ファイルの詳細については、「[ビジネス データ接続モデルを作成する](../sharepoint/creating-a-business-data-connectivity-model.md)」を参照してください。

5. Deleter メソッドに、レコードを削除するコードを追加します。 次の例では、SQL Server 用の AdventureWorks サンプル データベースを使用して、販売注文から行項目を削除します。

   > [!NOTE]
   > この例のメソッドでは、2 つの入力パラメーターを使用します。

   > [!NOTE]
   > `ServerName` フィールドの値をサーバーの名前に置き換えてください。

    :::code language="csharp" source="../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/salesorderdetailservice.cs" id="Snippet6":::
    :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/salesorderdetailservice.vb" id="Snippet6":::

## <a name="see-also"></a>関連項目
- [ビジネス データ接続モデルを設計する](../sharepoint/designing-a-business-data-connectivity-model.md)
- [方法: Finder メソッドを追加する](../sharepoint/how-to-add-a-finder-method.md)
- [方法: Specific Finder メソッドを追加する](../sharepoint/how-to-add-a-specific-finder-method.md)
- [方法: Creator メソッドを追加する](../sharepoint/how-to-add-a-creator-method.md)
- [方法: Updater メソッドを追加する](../sharepoint/how-to-add-an-updater-method.md)
- [BDC モデルのデザイン ツールの概要](../sharepoint/bdc-model-design-tools-overview.md)
- [方法: メソッドにパラメーターを追加する](../sharepoint/how-to-add-a-parameter-to-a-method.md)
- [方法: メソッド インスタンスを定義する](../sharepoint/how-to-define-a-method-instance.md)
