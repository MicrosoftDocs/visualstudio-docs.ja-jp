---
title: BDC モデルのデザイン ツールの概要 | Microsoft Docs
description: ビジネス データ接続 (BDC) モデルで使用するデザイン ツールの概要を説明します。 BDC デザイナー、[BDC メソッドの詳細] ウィンドウ、BDC エクスプローラーについて説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VS.SharePointTools.BDC.Method_Details
- VS.SharePointTools.BDC.Explorer
- VS.SharePointTools.BDC.Diagram
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- BDC [SharePoint development in Visual Studio], visual tools
- Business Data Connectivity service [SharePoint development in Visual Studio], visual tools
- Business Data Connectivity service [SharePoint development in Visual Studio], BDC Explorer
- BDC [SharePoint development in Visual Studio], method details
- Business Data Connectivity service [SharePoint development in Visual Studio], designer
- Business Data Connectivity service [SharePoint development in Visual Studio], method details
- BDC [SharePoint development in Visual Studio], BDC Explorer
- BDC [SharePoint development in Visual Studio], designer
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: b398d9c00caf3a4fa2ca58bafa3273673a305859
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99851687"
---
# <a name="bdc-model-design-tools-overview"></a>BDC モデルのデザイン ツールの概要
  BDC デザイナー、 **[BDC メソッドの詳細]** ウィンドウ、**BDC エクスプローラー** を使用して、ビジネス データ接続 (BDC) モデルを設計できます。

 **BDC エクスプローラー** を使用すると、モデルを参照したり、モデルを検索したり、型記述子を定義したりすることができます。

## <a name="bdc-designer"></a>BDC デザイナー
 BDC デザイナーを使用すると、モデル内でエンティティを定義したり、それらの相互の関係を視覚的に配置したりできます。 BDC デザイナーを使用して、次のタスクを実行します。

- モデルにエンティティを追加する。

- モデルからエンティティを削除する。

- エンティティ間のリレーションシップを定義する。

  BDC デザイナーを開くには、プロジェクトでモデル ファイルをダブルクリックするか、モデル ファイルのショートカット メニューを開き、 **[開く]** を選択します。 **ツールボックス** からデザイナーに **エンティティ** をドラッグまたはコピーして、エンティティをモデルに追加します。 2 つのエンティティ間の関連付けを作成するには、**ツールボックス** で **関連付け** コントロールを選択し、最初のエンティティを選択して、2 番目のエンティティを選択します。

## <a name="bdc-method-details-window"></a>[BDC メソッドの詳細] ウィンドウ
 **[BDC メソッドの詳細]** ウィンドウを使用して、メソッドのパラメーター、インスタンス、およびフィルター記述子を定義します。

 **[BDC メソッドの詳細]** ウィンドウで、Finder、Specific Finder、Creator、Updater、および Deleter メソッドをすばやく生成できます。 これらのメソッドの生成時に、Visual Studio によって、パラメーター、インスタンス、型記述子などのメタデータがメソッドに追加されます。 このメタデータは、特定のシナリオを満たすように変更できます。

 **[BDC メソッドの詳細]** ウィンドウを開くには、メニュー バーで、 **[表示]**  >  **[その他のウィンドウ]**  >  **[BDC メソッドの詳細]** の順に選択します。

 **[BDC メソッドの詳細]** ウィンドウでメソッドを表示するには、BDC デザイナーでエンティティを選択します。 選択したエンティティのメソッドが、 **[BDC メソッドの詳細]** ウィンドウに表示されます。 BDC デザイナーでエンティティを選択しなかった場合、 **[BDC メソッドの詳細]** ウィンドウに情報は表示されません。

 **[BDC メソッドの詳細]** ウィンドウでノードを展開または折りたたんで、パラメーター、インスタンス、およびフィルター記述子を定義します。 **BDC エクスプローラー** を使用して、型記述子を定義します。

## <a name="bdc-explorer"></a>BDC エクスプローラー
 **BDC エクスプローラー** には、モデルを構成する要素が表示されます。 **BDC エクスプローラー** を開くには、メニュー バーで、 **[表示]**  >  **[その他のウィンドウ]**  >  **[BDC エクスプローラー]** を選択します。 モデルを参照するには、**BDC エクスプローラー** でノードを展開します。 各ノードは、モデル ファイルの XML 内の要素を表します。

 **BDC エクスプローラー** でノードを選択すると、選択した各ノードのプロパティが **プロパティ** ウィンドウに表示されます。 これらのプロパティの多くは、モデル ファイルの属性に対応しています。 **BDC エクスプローラー** の上部にある検索ボックスを使用して、モデルを検索できます。

> [!NOTE]
> **BDC エクスプローラー** には、識別子、カスタム プロパティ、ローカライズされた文字列、関連付けグループ、アクション、フィルター記述子、アクション制御リスト、および既定のパラメーター値は表示されません。

### <a name="define-type-descriptors"></a>型記述子の定義
 **BDC エクスプローラー** を使用して、型記述子を定義します。 BDC エクスプローラーでは、型記述子を 1 回定義するだけで、モデル内の他の場所でその型記述子を再利用できます。 これを実現するには、型記述子をコピーし、他のパラメーターまたは型記述子に貼り付けます。

> [!NOTE]
> 元の型記述子を変更しても、その型記述子のコピーには影響しません。

 詳細については、「[方法: パラメーターの型記述子を定義する](../sharepoint/how-to-define-the-type-descriptor-of-a-parameter.md)」を参照してください。

## <a name="see-also"></a>こちらもご覧ください
- [方法: BDC モデルを作成する](../sharepoint/how-to-create-a-bdc-model.md)
- [方法: モデルにエンティティを追加する](../sharepoint/how-to-add-an-entity-to-a-model.md)
- [方法: Finder メソッドを追加する](../sharepoint/how-to-add-a-finder-method.md)
- [方法: 特定の Finder メソッドを追加する](../sharepoint/how-to-add-a-specific-finder-method.md)
- [方法: Creator メソッドを追加する](../sharepoint/how-to-add-a-creator-method.md)
- [方法: Deleter メソッドを追加する](../sharepoint/how-to-add-a-deleter-method.md)
- [方法: Updater メソッドを追加する](../sharepoint/how-to-add-an-updater-method.md)
- [エンティティ間に関連付けを作成する](../sharepoint/creating-an-association-between-entities.md)
- [チュートリアル: ビジネス データを使用した SharePoint での外部リストの作成](../sharepoint/walkthrough-creating-an-external-list-in-sharepoint-by-using-business-data.md)
- [SharePoint へのビジネス データの統合](../sharepoint/integrating-business-data-into-sharepoint.md)
- [ビジネス データ接続モデルの作成](../sharepoint/creating-a-business-data-connectivity-model.md)
- [ビジネス データ接続モデルの設計](../sharepoint/designing-a-business-data-connectivity-model.md)
