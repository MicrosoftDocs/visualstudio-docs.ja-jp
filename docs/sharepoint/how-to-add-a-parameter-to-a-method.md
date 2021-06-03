---
title: '方法: メソッドにパラメーターを追加する | Microsoft Docs'
description: ビジネス データ接続 (BDC) メソッドにパラメーターを追加する方法を理解します。これにより、メソッドに情報を渡したり、メソッドから情報を返したりできます。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Business Data Connectivity service [SharePoint development in Visual Studio], adding a method to a parameter
- Business Data Connectivity service [SharePoint development in Visual Studio], parameter
- BDC [SharePoint development in Visual Studio], adding a method to a parameter
- BDC [SharePoint development in Visual Studio], parameter
- Business Data Connectivity service [SharePoint development in Visual Studio], method parameters
- BDC [SharePoint development in Visual Studio], method parameters
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: d568d5ca2025f1467fa96387493b1e8b4ed1ec6e
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99931696"
---
# <a name="how-to-add-a-parameter-to-a-method"></a>方法: メソッドにパラメーターを追加する
  パラメーターを使用して、メソッドに情報を渡したり、メソッドから情報を返したりします。 すべてのメソッドには、少なくとも 1 つのパラメーターが必要です。 作成するメソッドの種類をサポートするパラメーターをデザインする方法の詳細については、「[ビジネス データ接続モデルの設計](../sharepoint/designing-a-business-data-connectivity-model.md)」を参照してください。

 メソッドにパラメーターを追加すると、Visual Studio によって、Parameter 要素がプロジェクトのモデル ファイルの XML に追加されます。 Parameter 要素の属性の詳細については、[Parameter](/previous-versions/office/developer/sharepoint-2010/ee557705(v=office.14)) に関するページを参照してください。

### <a name="to-add-a-parameter-to-a-method"></a>メソッドにパラメーターを追加するには

1. メソッドをエンティティに追加します。

2. メニュー バーで、 **[表示]**  >  **[その他のウィンドウ]**  >  **[BDC メソッドの詳細]** の順に選択します。

     **[BDC メソッドの詳細]** ウィンドウが開きます。 詳細については、「[BDC モデルのデザイン ツールの概要](../sharepoint/bdc-model-design-tools-overview.md)」を参照してください。

3. **[BDC メソッドの詳細]** ウィンドウで、メソッドのノードを展開し、 **[パラメーター]** ノードを展開します。

4. **[パラメーターの追加]** 一覧で、 **[パラメーターの作成]** を選択します。

     **[パラメーター]** ノードの下に新しいパラメーターが表示されます。

5. メニュー バーで、 **[表示]**  >  **[プロパティ ウィンドウ]** の順に選択します。

6. **[プロパティ]** ウィンドウで、 **[名前]** プロパティを意味のある任意の名前に設定します。 たとえば、メソッドが顧客を返す場合は、メソッドに **GetCustomers** という名前を指定できます。

7. **[BDC メソッドの詳細]** ウィンドウで、パラメーターの方向として表示される一覧を開き、 **[In]** 、 **[InOut]** 、 **[Out]** 、または **[Return]** を選択します。

     作成する type メソッドに対して選択する方向の詳細については、「[ビジネス データ接続モデルを設計する](../sharepoint/designing-a-business-data-connectivity-model.md)」を参照してください。

8. パラメーターの型記述子を変更します。 詳細については、「[方法: パラメーターの型記述子を定義する](../sharepoint/how-to-define-the-type-descriptor-of-a-parameter.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [BDC モデルのデザイン ツールの概要](../sharepoint/bdc-model-design-tools-overview.md)
- [方法: モデルにエンティティを追加する](../sharepoint/how-to-add-an-entity-to-a-model.md)
- [方法: パラメーターの型記述子を定義する](../sharepoint/how-to-define-the-type-descriptor-of-a-parameter.md)
- [方法: メソッド インスタンスを定義する](../sharepoint/how-to-define-a-method-instance.md)
- [ビジネス データ接続モデルを設計する](../sharepoint/designing-a-business-data-connectivity-model.md)
