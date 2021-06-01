---
title: エンティティ間の関連付けの作成 | Microsoft Docs
description: ビジネス データ接続 (BDC) モデル内のエンティティ間の関連付けを作成します。 関連付けメソッドと関連付けの種類について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VS.SharePointTools.BDC.Association_Dialog
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- BDC [SharePoint development in Visual Studio], create an assocation
- Business Data Connectivity service [SharePoint development in Visual Studio], associations between entities
- BDC [SharePoint development in Visual Studio], associations between entities
- Business Data Connectivity service [SharePoint development in Visual Studio], create an assocation
- Business Data Connectivity service [SharePoint development in Visual Studio], associate external content types
- Business Data Connectivity service [SharePoint development in Visual Studio], relate entities
- BDC [SharePoint development in Visual Studio], relate entities
- BDC [SharePoint development in Visual Studio], associate external content types
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: d40c4e5c5d61b9da3cdbdd3fe96f45c4a0cff929
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106213967"
---
# <a name="create-an-association-between-entities"></a>エンティティ間に関連付けを作成する
  関連付けを作成することによって、ビジネス データ接続 (BDC) モデルのエンティティ間のリレーションシップを定義できます。 Visual Studio では、モデルのコンシューマーに各関連付けに関する情報を提供するメソッドが生成されます。 これらのメソッドは、SharePoint Web パーツ、リスト、またはカスタム アプリケーションで、ユーザー インターフェイス (UI) にデータ リレーションシップを表示するために使用できます。

## <a name="create-an-association"></a>関連付けを作成する
 関連付けを作成するには、Visual Studio の **[ツールボックス]** で **[関連付け]** コントロールを選択し、1 つ目のエンティティ (ソース エンティティと呼ばれます) を選択した後、2 つ目のエンティティ (ターゲット エンティティと呼ばれます) を選択します。 関連付けの詳細は、**関連付けエディター** で定義できます。 詳しくは、「[方法: エンティティ間に関連付けを作成する](../sharepoint/how-to-create-an-association-between-entities.md)」をご覧ください。

## <a name="association-methods"></a>関連付けメソッド
 SharePoint ビジネス データ Web パーツなどのアプリケーションは、エンティティのサービス クラスでメソッドを呼び出すことによって、関連付けを使用します。 エンティティのサービス クラスにメソッドを追加するには、**関連付けエディター** でそれらを選択します。

 既定では、**関連付けエディター** によって、ソース エンティティとターゲット エンティティに関連付けナビゲーション メソッドが追加されます。 ソース エンティティの関連付けナビゲーション メソッドを使用すると、コンシューマーはターゲット エンティティの一覧を取得できます。 ターゲット エンティティの関連付けナビゲーション メソッドを使用すると、コンシューマーは、ターゲット エンティティに関連付けられているソース エンティティを取得できます。

 適切な情報を返すには、これらの各メソッドにコードを追加する必要があります。 さらに高度なシナリオをサポートするために、他の種類のメソッドを追加することもできます。 これらの各方法について詳しくは、[サポートされる操作](/previous-versions/office/developer/sharepoint-2010/ee557363(v=office.14))に関する記事をご覧ください。

## <a name="types-of-associations"></a>関連付けの種類
 BDC デザイナーでは、2 種類の関連付けを作成できます。外部キー ベースの関連付けと、外部キーなしの関連付けです。

### <a name="foreign-key-based-association"></a>外部キー ベースの関連付け
 外部キー ベースの関連付けを作成するには、ソース エンティティの識別子を、ターゲット エンティティで定義されている型記述子に関連付けます。 このリレーションシップを使用することで、モデルのコンシューマーは、ユーザーに対して高度な UI を提供できます。 たとえば、Outlook のフォームでユーザーが販売注文を作成し、ドロップダウン リストに顧客を表示できるようにしたり、SharePoint の販売注文一覧でユーザーが顧客のプロファイル ページを開けるようにしたりすることができます。

 外部キー ベースの関連付けを作成するには、同じ名前と型を共有する、識別子と型記述子を関連付けます。 たとえば、`Contact` エンティティと `SalesOrder` エンティティの間に外部キー ベースの関連付けを作成できます。 `SalesOrder` エンティティは、Finder または Specific Finder メソッドの戻りパラメーターの一部として、`ContactID` 型記述子を返します。 **関連付けエディター** には、両方の型記述子が表示されます。 `Contact` エンティティと `SalesOrder` エンティティの間に外部キー ベースのリレーションシップを作成するには、これらの各フィールドの横にある `ContactID` 識別子を選択します。

 ソース エンティティの関連付けナビゲーター メソッドには、ターゲット エンティティのコレクションを返すコードを追加します。 次の例では、連絡先の販売注文が返されます。

 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/contactservice.cs" id="Snippet7":::
 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/contactservice.vb" id="Snippet7":::

 ターゲット エンティティの関連付けナビゲーター メソッドには、ソース エンティティを返すコードを追加します。 次の例では、販売注文に関連付けられている連絡先が返されます。

 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/salesorderservice.cs" id="Snippet8":::
 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/salesorderservice.vb" id="Snippet8":::

### <a name="foreign-keyless-association"></a>外部キーなしの関連付け
 関連付けは、識別子をフィールド型記述子にマップせずに作成することもできます。 ソース エンティティにターゲット エンティティとの直接的なリレーションシップがない場合は、この種類の関連付けを作成します。 たとえば、`SalesOrderDetail` テーブルには、`Contact` テーブル内の主キーにマップされる外部キーがありません。

 `Contact` に関連する情報を `SalesOrderDetail` テーブルに表示したい場合は、`Contact` エンティティと `SalesOrderDetail` エンティティの間に外部キーなし関連付けを作成します。

 `Contact` エンティティの関連付けナビゲーション メソッドでは、テーブルを結合するか、ストアド プロシージャを呼び出すことで、`SalesOrderDetail` エンティティを返します。

 次の例では、テーブルを結合することで、すべての販売注文の詳細が返されます。

 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/contactservice.cs" id="Snippet9":::
 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/contactservice.vb" id="Snippet9":::

 `SalesOrderDetail` エンティティの関連付けナビゲーション メソッドでは、関連する `Contact` を返します。 次に例を示します。
                                                                            
 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/salesorderdetailservice.cs" id="Snippet10":::
 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/salesorderdetailservice.vb" id="Snippet10":::

## <a name="see-also"></a>関連項目
- [ビジネス データ接続モデルを設計する](../sharepoint/designing-a-business-data-connectivity-model.md)
- [方法: エンティティ間に関連付けを作成する](../sharepoint/how-to-create-an-association-between-entities.md)
