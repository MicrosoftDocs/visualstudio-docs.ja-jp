---
title: '方法: カスタム プロパティを追加する | Microsoft Docs'
description: Visual Studio の BDC エクスプローラーでプロパティ エディターを使用して SharePoint の Business Data Connectivity (BDC) モデルにカスタム プロパティを追加する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- VS.SharePointTools.BDC.Property_Editor
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- BDC [SharePoint development in Visual Studio], properties
- Business Data Connectivity service [SharePoint development in Visual Studio], properties
- Business Data Connectivity service [SharePoint development in Visual Studio], custom properties
- BDC [SharePoint development in Visual Studio], custom properties
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: d335cc809a8415a2b41f3de63138c113c2a78706
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99876603"
---
# <a name="how-to-add-a-custom-property"></a>方法: カスタム プロパティを追加する
  **プロパティ エディター** を使用して、モデルにカスタム プロパティを追加できます。 コードでこれらのプロパティにアクセスして、実行時に接続文字列やその他のデータなどの情報を取得できます。

### <a name="to-add-a-custom-property"></a>カスタム プロパティを追加するには

1. **BDC エクスプローラー** で、カスタム プロパティを適用するモデル要素を表すノードを選択します。

2. メニュー バーで、 **[表示]**  >  **[プロパティ ウィンドウ]** の順に選択します。

3. **[プロパティ]** ウィンドウで、 **[カスタム プロパティ]** プロパティを選択してから、省略記号ボタン (![ASP.NET モバイル デザイナーの省略記号](../sharepoint/media/mwellipsis.gif "ASP.NET モバイル デザイナー楕円")) をクリックします。

     **[プロパティ エディター]** ダイアログ ボックスが表示されます。

4. **[名前]** 列のテキスト ボックスで、プロパティの名前を指定します。

5. カスタム プロパティの **[型]** フィールドで、適切なデータ型を選択します。

6. カスタム プロパティの **[値]** フィールドに値を指定してから、 **[OK]** ボタンを選択します。

## <a name="see-also"></a>関連項目
- [ビジネス データ接続モデルを設計する](../sharepoint/designing-a-business-data-connectivity-model.md)
- [ビジネス データ接続モデルを設計する](../sharepoint/designing-a-business-data-connectivity-model.md)
- [ビジネス データ接続モデルを作成する](../sharepoint/creating-a-business-data-connectivity-model.md)
- [SharePoint へのビジネス データの統合](../sharepoint/integrating-business-data-into-sharepoint.md)
