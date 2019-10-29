---
title: '方法: リソースファイルを使用してローカライズされた名前、プロパティ、およびアクセス許可を指定するMicrosoft Docs'
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Business Data Connectivity service [SharePoint development in Visual Studio], localize strings
- BDC [SharePoint development in Visual Studio], localize strings
- BDC [SharePoint development in Visual Studio], resource file
- Business Data Connectivity service [SharePoint development in Visual Studio], resource strings
- BDC [SharePoint development in Visual Studio], properties
- Business Data Connectivity service [SharePoint development in Visual Studio], properties
- Business Data Connectivity service [SharePoint development in Visual Studio], resource file
- BDC [SharePoint development in Visual Studio], resource strings
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: fa2fec260921d66328b2c16075d44b38686c08de
ms.sourcegitcommit: dcbb876a5dd598f2538e62e1eabd4dc98595b53a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/28/2019
ms.locfileid: "72982552"
---
# <a name="how-to-use-a-resource-file-to-specify-localized-names-properties-and-permissions"></a>方法: リソースファイルを使用してローカライズされた名前、プロパティ、およびアクセス許可を指定する
  リソースファイルを使用すると、ローカライズされた名前の指定、プロパティの定義、ビジネスデータ接続 (BDC) モデルで定義されているアクセス許可 tor オブジェクトの適用を行うことができます。 この情報を指定するには、ビジネスデータ接続**モデル**アイテムを含むプロジェクトに**ビジネスデータ接続リソース**アイテムを追加します。 次に、リソースファイルの XML を編集して、名前、プロパティ、およびアクセス許可を指定します。

### <a name="to-add-a-bdc-resource-file-to-a-sharepoint-project"></a>BDC リソースファイルを SharePoint プロジェクトに追加するには

1. **ソリューションエクスプローラー**で、SharePoint プロジェクトのフォルダーを展開し、BDC モデルが含まれているフォルダーを選択します。

2. メニュー バーで **[プロジェクト]**  >  **[新しい項目の追加]** の順に選択します。

3. **[SharePoint]** ノードを展開し、 **[2010]** ノードを選択します。

4. **[新しい項目の追加]** ダイアログボックスで、 **[ビジネスデータ接続リソース項目]** を選択します。

5. **[名前]** ボックスにリソースファイルの名前を指定し、 **[追加]** をクリックします。

     拡張子が bdcr のリソースファイルがプロジェクトに追加され、編集用に開かれます。

6. XML を追加して、BDC モデルを適用するローカライズされた名前、プロパティ、およびアクセス許可を定義します。

     これらの要素を定義する方法の詳細については、「[モデルファイルとリソースファイル](/previous-versions/office/developer/sharepoint-2010/aa674515(v=office.14))」を参照してください。

## <a name="see-also"></a>関連項目
- [方法: 既存の BDC モデルファイルを SharePoint プロジェクトに追加する](../sharepoint/how-to-add-an-existing-bdc-model-file-to-a-sharepoint-project.md)
- [ビジネスデータ接続モデルを作成する](../sharepoint/creating-a-business-data-connectivity-model.md)
- [方法: BDC モデルを作成する](../sharepoint/how-to-create-a-bdc-model.md)
- [方法: BDC 機能にカスタムアセンブリを含める](../sharepoint/how-to-include-a-custom-assembly-in-a-bdc-feature.md)
- [SharePoint へのビジネスデータの統合](../sharepoint/integrating-business-data-into-sharepoint.md)
