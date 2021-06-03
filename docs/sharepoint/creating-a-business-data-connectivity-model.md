---
title: ビジネス データ接続モデルの作成 | Microsoft Docs
description: ビジネス データ接続 (BDC) モデルを作成したり、Visual Studio を使用して既存の BDC モデルをカスタマイズしたりします。 各 SharePoint プロジェクトに含めることができるモデルは 1 つだけです。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Business Data Connectivity service [SharePoint development in Visual Studio], model
- BDC [SharePoint development in Visual Studio], creating a model
- Business Data Connectivity service [SharePoint development in Visual Studio], creating a model
- SharePoint development in Visual Studio, Business Data Connectivity service
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 8232847ce336ca559134aa1211a70057a1306faa
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99949260"
---
# <a name="create-a-business-data-connectivity-model"></a>ビジネス データ接続モデルを作成する
  ビジネス データ接続 (BDC) モデルを作成するか、Visual Studio を使用して既存の BDC モデルをカスタマイズすることができます。 各 SharePoint プロジェクトに含めることができるモデルは 1 つだけです。 詳細については、「[SharePoint へのビジネス データの統合](../sharepoint/integrating-business-data-into-sharepoint.md)」を参照してください。

## <a name="create-a-new-model"></a>新しいモデルを作成する
 新しいモデルを作成するには、"**ビジネス データ接続モデル**" プロジェクトを作成するか、"**空の SharePoint プロジェクト**" に **[ビジネス データ接続モデル]** 項目を追加します。

> [!NOTE]
> コンピューターに [!INCLUDE[moss_14_long](../sharepoint/includes/moss-14-long-md.md)] がインストールされている必要があります。

 Visual Studio によってプロジェクトにフォルダーが追加されます。 このフォルダーには、 **[新しい項目の追加]** ダイアログ ボックスで **[ビジネス データ接続モデル]** 項目に指定した名前が付けられます。 新しい "**ビジネス データ接続モデル**" プロジェクトを作成すると、Visual Studio によってフォルダーに **BdcModel1** という名前が付けられます。

 Visual Studio によって新しいフォルダーに次のファイルが追加されます。

|ファイル|説明|
|----------|-----------------|
|モデル定義ファイル|エンティティ、メソッド、基幹業務 (LOB) システム オブジェクト、およびモデルを記述するその他のメタデータを定義する XML が含まれています。<br /><br /> このファイル内のメタデータは、BDC デザイナー、"**BDC エクスプローラー**"、 **[BDC メソッドの詳細]** ウィンドウ、および **[プロパティ]** ウィンドウを使用して変更します。|
|エンティティ サービスのコード ファイル|既定のエンティティのインスタンスを取得、更新、および削除するメソッドが含まれています。|

 エンティティのプロパティを定義するには、エンティティ コード ファイルを編集します。 詳細については、「[方法: モデルにエンティティを追加する](../sharepoint/how-to-add-an-entity-to-a-model.md)」を参照してください。

 エンティティのインスタンスを取得、更新、および削除するには、エンティティ サービスのコード ファイルにコードを追加します。 詳細については、[ビジネス データ接続モデルの設計](../sharepoint/designing-a-business-data-connectivity-model.md)に関するページを参照してください。

 プロジェクトをコンパイルすると、Visual Studio によってアセンブリが作成されます。 プロジェクト アセンブリにコードを追加する他の項目 ("**シーケンシャル ワークフロー**" 項目や "**Web パーツ**" 項目など) をプロジェクトに追加しないようにしてください。 ソリューション パッケージではアセンブリがグローバル アセンブリ キャッシュにコピーされないため、ソリューションを配置するときにその項目のコードは実行されません。  ソリューション パッケージでは、アセンブリは SharePoint の BDC データベースにのみ配置されます。

> [!NOTE]
> Visual Studio では、プロジェクトをデバッグするときに、ローカル コンピューター上の両方の場所にアセンブリがコピーされます。

## <a name="add-an-existing-model"></a>既存のモデルを追加する
 SharePoint Designer などの他のツールを使用して作成されたモデルをインポートできます。 次の状況では、既存のモデルをプロジェクトにインポートすることを選択できます。

- SharePoint サーバー ファームに既に配置されているモデルをカスタマイズする場合。

- 既存のモデルをパッケージ化して複数の SharePoint サーバー ファームに配置する場合。

  どちらの場合も、インポートするモデルで定義されている LOB システムは影響を受けず、期待どおりに機能し続けます。 既存のモデルを SharePoint プロジェクトに追加するには、Visual Studio の **[既存項目の追加]** ダイアログ ボックスを使用します。 詳細については、「[方法: 既存の BDC モデル ファイルを SharePoint プロジェクトに追加する](../sharepoint/how-to-add-an-existing-bdc-model-file-to-a-sharepoint-project.md)」を参照してください。

  **[.Net アセンブリ LobSystem の追加]** のオプションを選択すると、インポートしたモデルに .NET Framework 型のアセンブリの LOB システムを追加できます。 これにより、カスタム コードを記述し、デザイナーを使用してインポートされたモデルのメタデータを定義できます。

## <a name="related-topics"></a>関連トピック

|Title|説明|
|-----------|-----------------|
|[方法: BDC モデルを作成する](../sharepoint/how-to-create-a-bdc-model.md)|新しい BDC モデルを作成する方法を示します。|
|[方法: 既存の BDC モデル ファイルを SharePoint プロジェクトに追加する](../sharepoint/how-to-add-an-existing-bdc-model-file-to-a-sharepoint-project.md)|既存のモデルを SharePoint プロジェクトにインポートする方法を示します。|
|[方法: リソース ファイルを使用して、ローカライズした名前、プロパティ、およびアクセス許可を指定する](../sharepoint/how-to-use-a-resource-file-to-specify-localized-names-properties-and-permissions.md)|モデルが Web パーツまたは Web ページによって使用される場合に、モデル メタデータとマージされる文字列を指定する方法について説明します。|
|[方法: BDC 機能にカスタム アセンブリを含める](../sharepoint/how-to-include-a-custom-assembly-in-a-bdc-feature.md)|機能にカスタム アセンブリを含める方法を示します。|
