---
title: SharePoint プロジェクトでリソース ファイルを使用する方法 | Microsoft Docs
titleSuffix: ''
description: リソース ファイルを SharePoint プロジェクトで使用すると、ローカライズされた名前の指定、プロパティの定義のほか、BDC モデルで定義されているオブジェクトにアクセス許可を適用できます。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
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
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 49546d11dbf4f19bb2fd826ace2850468f780d13
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99851557"
---
# <a name="how-to-use-a-resource-file-in-a-sharepoint-project"></a>SharePoint プロジェクトでリソース ファイルを使用する方法

  リソース ファイルを使用すると、ローカライズされた名前の指定、プロパティの定義、ビジネス データ接続 (BDC) モデルで定義されているオブジェクトにアクセス許可を適用できます。 この情報を指定するには、**ビジネス データ接続リソース** 項目を、**ビジネス データ接続モデル** 項目を含むプロジェクトに追加します。 次に、リソース ファイルの XML を編集して、名前、プロパティ、およびアクセス許可を指定します。

### <a name="to-add-a-bdc-resource-file-to-a-sharepoint-project"></a>BDC リソース ファイルを SharePoint プロジェクトに追加するには

1. **ソリューション エクスプローラー** で、SharePoint プロジェクトのフォルダーを展開し、BDC モデルが含まれているフォルダーを選択します。

2. メニュー バーで **[プロジェクト]**  >  **[新しい項目の追加]** の順に選択します。

3. **[SharePoint]** ノードを展開し、 **[2010]** ノードを選択します。

4. **[新しい項目の追加]** ダイアログ ボックスで、 **[ビジネス データ接続リソース項目]** を選択します。

5. **[名前]** ボックスにリソース ファイルの名前を指定し、 **[追加]** ボタンを選択します。

     拡張子が .bdcr のリソース ファイルがプロジェクトに追加され、編集用に開かれます。

6. XML を追加して、BDC モデルを適用するローカライズされた名前、プロパティ、およびアクセス許可を定義します。

     これらの要素を定義する方法の詳細については、「[Model ファイルと Resource ファイル](/previous-versions/office/developer/sharepoint-2010/aa674515(v=office.14))」を参照してください。

## <a name="see-also"></a>こちらもご覧ください
- [方法: 既存の BDC モデル ファイルを SharePoint プロジェクトに追加する](../sharepoint/how-to-add-an-existing-bdc-model-file-to-a-sharepoint-project.md)
- [ビジネス データ接続モデルを作成する](../sharepoint/creating-a-business-data-connectivity-model.md)
- [方法: BDC モデルを作成する](../sharepoint/how-to-create-a-bdc-model.md)
- [方法: BDC 機能にカスタム アセンブリを含める](../sharepoint/how-to-include-a-custom-assembly-in-a-bdc-feature.md)
- [SharePoint へのビジネス データの統合](../sharepoint/integrating-business-data-into-sharepoint.md)
