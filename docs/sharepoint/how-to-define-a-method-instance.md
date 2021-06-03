---
title: '方法: メソッド インスタンスを定義する | Microsoft Docs'
description: ビジネス データ接続 (BDC) モデルのメソッドのメソッド インスタンスを定義する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Business Data Connectivity service [SharePoint development in Visual Studio], method instance
- BDC [SharePoint development in Visual Studio], method instance
- BDC [SharePoint development in Visual Studio], method
- Business Data Connectivity service [SharePoint development in Visual Studio], method
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 055193123f99825027238166d762ce54b288d716
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99885665"
---
# <a name="how-to-define-a-method-instance"></a>方法: メソッド インスタンスを定義する
  モデル内の各メソッドに対して、少なくとも 1 つのメソッド インスタンスを定義する必要があります。

 メソッド インスタンスを追加するには、 **[BDC メソッドの詳細]** ウィンドウを使用します。 メソッド インスタンスを追加すると、Visual Studio によってプロジェクトのモデル ファイルの XML に `<MethodInstance>` 要素が追加されます。 `<MethodInstance>` 要素の属性の詳細については、[MethodInstance](/previous-versions/office/developer/sharepoint-2010/ee556838(v=office.14)) に関する記事をご覧ください。

### <a name="to-define-a-method-instance"></a>メソッド インスタンスを定義するには

1. **[BDC メソッドの詳細]** ウィンドウで、メソッドのノードを展開してから **[インスタンス]** ノードを展開します。

2. **[メソッド インスタンスの追加]** ボックスの一覧で、 **[Finder インスタンスの作成]** を選択します。

     **[インスタンス]** ノードの下に新しいメソッド インスタンスが表示されます。

3. メニュー バーで、 **[表示]**  >  **[プロパティ ウィンドウ]** の順に選択します。

4. **[プロパティ]** ウィンドウで、メソッド インスタンスのプロパティを設定します。 各プロパティの詳細については、[MethodInstance](/previous-versions/office/developer/sharepoint-2010/ee556838(v=office.14)) に関する記事をご覧ください。

## <a name="see-also"></a>関連項目
- [BDC モデルのデザイン ツールの概要](../sharepoint/bdc-model-design-tools-overview.md)
- [方法: モデルにエンティティを追加する](../sharepoint/how-to-add-an-entity-to-a-model.md)
- [方法: メソッドにパラメーターを追加する](../sharepoint/how-to-add-a-parameter-to-a-method.md)
- [方法: パラメーターの型記述子を定義する](../sharepoint/how-to-define-the-type-descriptor-of-a-parameter.md)
- [ビジネス データ接続モデルを設計する](../sharepoint/designing-a-business-data-connectivity-model.md)
