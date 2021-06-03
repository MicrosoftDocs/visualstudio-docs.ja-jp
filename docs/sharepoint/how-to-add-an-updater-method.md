---
title: '方法: Updater メソッドを追加する | Microsoft Docs'
description: Updater メソッドを追加することによって、ユーザーが SharePoint 外部リスト内のビジネス データを更新できるようにする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- BDC [SharePoint development in Visual Studio], updating data
- BDC [SharePoint development in Visual Studio], Updater
- Business Data Connectivity service [SharePoint development in Visual Studio], updating data
- Business Data Connectivity service [SharePoint development in Visual Studio], Updater
- Business Data Connectivity service [SharePoint development in Visual Studio], updating entity instances
- BDC [SharePoint development in Visual Studio], updating entity instances
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: d6337ac237c2a030593b90b29af5e8474052de99
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106216736"
---
# <a name="how-to-add-an-updater-method"></a>方法: Updater メソッドを追加する
  *Updater* メソッドを作成することによって、ユーザーが SharePoint 外部リスト内のビジネス データを更新できるようにすることができます。 詳細については、[ビジネス データ接続モデルの設計](../sharepoint/designing-a-business-data-connectivity-model.md)に関するページを参照してください。

### <a name="to-create-an-updater-method"></a>Updater メソッドを作成するには

1. BDC デザイナーで、エンティティを選択します。

2. メニュー バーで、 **[表示]**  >  **[その他のウィンドウ]**  >  **[BDC メソッドの詳細]** の順に選択します。

    [BDC メソッドの詳細] ウィンドウが開きます。 このウィンドウの詳細については、「[BDC モデルのデザイン ツールの概要](../sharepoint/bdc-model-design-tools-overview.md)」を参照してください。

3. **[メソッドの追加]** 一覧で、 **[Updater メソッドの作成]** を選択します。

    Visual Studio により、次の要素がモデルに追加されます。 これらの要素は、[BDC メソッドの詳細] ウィンドウに表示されます。

   - **Update** という名前のメソッド。

   - メソッドの入力パラメーター。

   - パラメーターの型記述子。 既定では、Visual Studio では、Finder メソッドに対して定義されたエンティティ型記述子 (Contact など) を使用します。

   - メソッドのメソッド インスタンス。

     詳細については、[ビジネス データ接続モデルの設計](../sharepoint/designing-a-business-data-connectivity-model.md)に関するページを参照してください。

   > [!NOTE]
   > エンティティ型の識別子が、自動的に生成されていないデータベース テーブル内のフィールドを表している場合は、**Pre-Updater Field** プロパティを **True** に設定します。

4. **ソリューション エクスプローラー** で、エンティティに対して生成されたサービス コード ファイルのショートカット メニューを開き、 **[コードの表示]** を選択します。

    エンティティ サービス コード ファイルが **コード エディター** で開きます。 そのファイルの詳細については、「[ビジネス データ接続モデルを作成する](../sharepoint/creating-a-business-data-connectivity-model.md)」を参照してください。

5. Update メソッドに、データを更新するコードを追加します。 次の例では、SQL Server 用の AdventureWorks サンプル データベース内の連絡先に関する情報を更新します。

   > [!NOTE]
   > `ServerName` フィールドの値をサーバーの名前に置き換えてください。

    :::code language="csharp" source="../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/contactservice.cs" id="Snippet5":::
    :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/contactservice.vb" id="Snippet5":::

## <a name="see-also"></a>関連項目
- [ビジネス データ接続モデルを設計する](../sharepoint/designing-a-business-data-connectivity-model.md)
- [方法: Finder メソッドを追加する](../sharepoint/how-to-add-a-finder-method.md)
- [方法: Specific Finder メソッドを追加する](../sharepoint/how-to-add-a-specific-finder-method.md)
- [方法: Creator メソッドを追加する](../sharepoint/how-to-add-a-creator-method.md)
- [方法: Updater メソッドを追加する](../sharepoint/how-to-add-an-updater-method.md)
- [方法: Deleter メソッドを追加する](../sharepoint/how-to-add-a-deleter-method.md)
- [BDC モデルのデザイン ツールの概要](../sharepoint/bdc-model-design-tools-overview.md)
- [方法: メソッドにパラメーターを追加する](../sharepoint/how-to-add-a-parameter-to-a-method.md)
- [方法: メソッド インスタンスを定義する](../sharepoint/how-to-define-a-method-instance.md)
