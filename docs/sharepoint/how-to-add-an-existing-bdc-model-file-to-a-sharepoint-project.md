---
title: '方法: 既存の BDC モデル ファイルを SharePoint プロジェクトに追加する | Microsoft Docs'
titleSuffix: ''
description: 既存のビジネス データ接続 (BDC) モデル ファイルを Visual Studio の SharePoint プロジェクトに追加して、BDC モデルをカスタマイズ、パッケージ化、再配置できるようにします。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- VS.SharePointTools.BDC.ImportDialog
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Business Data Connectivity service [SharePoint development in Visual Studio], import a model
- Business Data Connectivity service [SharePoint development in Visual Studio], reuse a model
- BDC [SharePoint development in Visual Studio], import a model
- BDC [SharePoint development in Visual Studio], remove a model
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: af0768b4834eb1cad3654b6d74ee8f02cf464245
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99882675"
---
# <a name="how-to-add-an-existing-bdc-model-file-to-a-sharepoint-project"></a>方法: 既存の BDC モデル ファイルを SharePoint プロジェクトに追加する
  Visual Studio を使用してモデル ファイル ( *.bdcm*) を任意の SharePoint ファーム プロジェクトに追加すると、ビジネス データ接続 (BDC) モデルをカスタマイズ、パッケージ化、再配置できます。 詳細については、「[ビジネス データ接続モデルを作成する](../sharepoint/creating-a-business-data-connectivity-model.md)」を参照してください。

### <a name="to-add-a-bdc-model-file-to-a-sharepoint-project"></a>BDC モデル ファイルを SharePoint プロジェクトに追加するには

1. **ソリューション エクスプローラー** で、SharePoint プロジェクトのフォルダーを選択します。

2. メニュー バーで **[プロジェクト]**  >  **[既存項目の追加]** の順に選択します。

3. **[既存項目の追加]** ダイアログ ボックスで、プロジェクトに追加するモデル定義ファイルの場所を参照し、ファイルを選択してから **[追加]** ボタンを選択します。

    モデルで " *.NET アセンブリ型の基幹業務 (LOB) システム*" が定義されていない場合は、 **[.NET アセンブリの LobSystem を追加]** ダイアログ ボックスが開きます。

4. ダイアログ ボックスが表示されたら、次のいずれかの手順を実行します。

   - カスタム コードを記述し、デザイナーを使用してインポートされたモデルのメタデータを定義する場合は、 **[はい]** ボタンを選択し、システムの名前を指定してから **[OK]** ボタンを選択します。

   - それ以外の場合は、 **[いいえ]** ボタンを選択してから **[OK]** ボタンを選択します。

     **ビジネス データ接続モデル** 項目がプロジェクトに追加されます。

## <a name="see-also"></a>関連項目
- [ビジネス データ接続モデルを作成する](../sharepoint/creating-a-business-data-connectivity-model.md)
- [方法: BDC モデルを作成する](../sharepoint/how-to-create-a-bdc-model.md)
- [方法: リソース ファイルを使用して、ローカライズした名前、プロパティ、およびアクセス許可を指定する](../sharepoint/how-to-use-a-resource-file-to-specify-localized-names-properties-and-permissions.md)
- [方法: BDC 機能にカスタム アセンブリを含める](../sharepoint/how-to-include-a-custom-assembly-in-a-bdc-feature.md)
- [SharePoint へのビジネス データの統合](../sharepoint/integrating-business-data-into-sharepoint.md)
