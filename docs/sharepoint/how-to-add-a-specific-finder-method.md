---
title: '方法: Specific Finder メソッドを追加する | Microsoft Docs'
description: Finder メソッドを追加することによってエンティティ インスタンスを取得します。 BDC サービスでは、ユーザーがビジネス データ Web パーツまたは外部リスト内のエンティティを選択したときにこのメソッドを呼び出します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
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
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 87f5b0cf86178b88b1611f4b0ce8a4bbacde780e
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106216801"
---
# <a name="how-to-add-a-specific-finder-method"></a>方法: Specific Finder メソッドを追加する
  *Specific Finder* メソッドを作成することによって、1 つのエンティティ インスタンスを返すことができます。 ビジネス データ接続 (BDC) サービスでは、ユーザーがビジネス データ Web パーツまたは外部リスト内のエンティティを選択したときに Specific Finder メソッドを実行します。 詳細については、[ビジネス データ接続モデルの設計](../sharepoint/designing-a-business-data-connectivity-model.md)に関するページを参照してください。

### <a name="to-create-a-specific-finder-method"></a>Specific Finder メソッドを作成するには

1. **BDC デザイナー** で、エンティティを選択します。

    Visual Studio の **BDC デザイナー** にエンティティを追加する方法については、「[方法: モデルにエンティティを追加する](../sharepoint/how-to-add-an-entity-to-a-model.md)」を参照してください。

2. メニュー バーで、 **[表示]**  >  **[その他のウィンドウ]** 、 **[BDC メソッドの詳細]** の順に選択します。

    **[BDC メソッドの詳細]** ウィンドウが開きます。 そのウィンドウの詳細については、「[BDC モデルのデザイン ツールの概要](../sharepoint/bdc-model-design-tools-overview.md)」を参照してください。

3. **[メソッドの追加]** 一覧で、 **[Specific Finder メソッドの作成]** を選択します。

    Visual Studio により、次の要素がモデルに追加されます。 これらの要素は、 **[BDC メソッドの詳細]** ウィンドウに表示されます。

   - メソッド。

   - メソッドの入力パラメーター。

   - メソッドの戻り値パラメーター。

   - 各パラメーターの型記述子。

   - メソッドのメソッド インスタンス。

     詳細については、[ビジネス データ接続モデルの設計](../sharepoint/designing-a-business-data-connectivity-model.md)に関するページを参照してください。

4. Visual Studio の **[プロパティ]** ウィンドウを開きます。

5. 戻り値パラメーターの型記述子をエンティティ型記述子として構成します。 エンティティ型記述子を作成する方法については、「[方法: パラメーターの型記述子を定義する](../sharepoint/how-to-define-the-type-descriptor-of-a-parameter.md)」を参照してください。

   > [!NOTE]
   > このエンティティに Finder メソッドを追加している場合、この手順を実行する必要はありません。 Visual Studio では、その Finder メソッドで定義されている型記述子を使用します。

   > [!NOTE]
   > エンティティ型の識別子フィールドが、自動的に生成されたデータベース テーブル内のフィールドを表している場合は、その識別子フィールドの **Read-only** プロパティを **True** に設定します。

6. **[メソッドの詳細]** ウィンドウで、そのメソッドのメソッド インスタンスを選択します。

7. **[プロパティ ウィンドウ]** で、 **[戻り値パラメーター名]** プロパティをそのメソッドの戻り値パラメーターの名前に設定します。 メソッド インスタンスのプロパティの詳細については、[MethodInstance](/previous-versions/office/developer/sharepoint-2010/ee556838(v=office.14)) に関するページを参照してください。

8. **ソリューション エクスプローラー** で、エンティティに対して生成されたサービス コード ファイルのショートカット メニューを開き、 **[コードの表示]** を選択します。

    エンティティ サービス コード ファイルがコード エディターで開きます。 エンティティ サービス コード ファイルの詳細については、「[ビジネス データ接続モデルを作成する](../sharepoint/creating-a-business-data-connectivity-model.md)」を参照してください。

9. Specific Finder メソッドにコードを追加します。 このコードは、以下のタスクを実行します。

   - データ ソースからレコードを取得します。

   - BDC サービスにエンティティを返します。

     次の例では、SQL Server 用の AdventureWorks サンプル データベースから連絡先を返します。

     > [!NOTE]
     > `ServerName` フィールドの値をサーバーの名前に置き換えてください。

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/contactservice.cs" id="Snippet3":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/contactservice.vb" id="Snippet3":::

## <a name="see-also"></a>関連項目
- [ビジネス データ接続モデルを設計する](../sharepoint/designing-a-business-data-connectivity-model.md)
- [方法: Finder メソッドを追加する](../sharepoint/how-to-add-a-finder-method.md)
- [方法: Creator メソッドを追加する](../sharepoint/how-to-add-a-creator-method.md)
- [方法: Deleter メソッドを追加する](../sharepoint/how-to-add-a-deleter-method.md)
- [方法: Updater メソッドを追加する](../sharepoint/how-to-add-an-updater-method.md)
- [BDC モデルのデザイン ツールの概要](../sharepoint/bdc-model-design-tools-overview.md)
- [方法: メソッドにパラメーターを追加する](../sharepoint/how-to-add-a-parameter-to-a-method.md)
- [方法: メソッド インスタンスを定義する](../sharepoint/how-to-define-a-method-instance.md)
