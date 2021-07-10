---
title: '方法: BDC モデルを作成する | Microsoft Docs'
description: 'アイテムの種類に対応する Visual Studio テンプレートを使用し、モデルを任意の SharePoint プロジェクトに追加して、ビジネス データ接続 (BDC: Business Data Connectivity) モデルを作成します。'
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- BDC [SharePoint development in Visual Studio], creating a model
- Business Data Connectivity service [SharePoint development in Visual Studio], creating a model
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: fd5184f87cf3895e1519a91e6f7e6661702f1181
ms.sourcegitcommit: 1f27f33852112702ee35fbc0c02fba37899e4cf5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2021
ms.locfileid: "112112408"
---
# <a name="how-to-create-a-bdc-model"></a>方法: BDC モデルを作成する

  ビジネス データ接続 (BDC: Business Data Connectivity) モデルを作成するには、アイテムの種類に対応するテンプレートを使用し、モデルを任意の SharePoint プロジェクトに追加します。 詳細については、「[ビジネス データ接続モデルを作成する](../sharepoint/creating-a-business-data-connectivity-model.md)」を参照してください。 モデルのデザイン方法の詳細については、「[ビジネスデータ接続モデルを設計する](../sharepoint/designing-a-business-data-connectivity-model.md)」を参照してください。

## <a name="to-create-a-bdc-project"></a>BDC プロジェクトを作成するには

1. メニュー バーで、 **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** を選択します。
::: moniker range="=vs-2017"
   > [!NOTE]
   > IDE で Visual Basic 開発設定を使用するように設定されている場合は、 **[ファイル]**  >  **[新しいプロジェクト]** の順にクリックします。

  **[新しいプロジェクト]** ダイアログ ボックスが表示されます。

2. **[Visual Basic]** または **[Visual C#]** で、 **[Office/SharePoint]** 、 **[SharePoint ソリューション]** の順にクリックします。

3. **[テンプレート]** ペインで、 **[SharePoint 2013 - 空のプロジェクト]** 項目をクリックし、 **[OK]** をクリックします。

     **SharePoint カスタマイズ ウィザード** が開きます。
::: moniker-end
::: moniker range=">=vs-2019"
2. **[新しいプロジェクトの作成]** ダイアログで、インストールした SharePoint の特定のバージョンに対応する *SharePoint の空のプロジェクト** を選択します。 たとえば、SharePoint 2019 がインストールされている場合は、 **[SharePoint 2019 - 空のプロジェクト]** テンプレートを選択します。
    [!INCLUDE[new-project-dialog-search](../sharepoint/includes/new-project-dialog-search-md.md)]

3. 必要であればプロジェクトの名前を変更し、 **[作成]** ボタンを選択します。

::: moniker-end
4. **[デバッグのサイトとセキュリティ レベルの指定]** ページで、ローカル コンピューター上の SharePoint サイトの URL を指定して、 **[ファーム ソリューションとして配置する]** をクリックし、 **[完了]** をクリックします。

     指定した SharePoint サイトでモデルをテストします。

    > [!IMPORTANT]
    > BDC モデルはファーム ソリューションのみサポートするため、プロジェクトはファーム ソリューションとして配置する必要があります。

     空の SharePoint プロジェクトが作成されます。

5. メニュー バーで **[プロジェクト]**  >  **[新しい項目の追加]** の順に選択します。

6. **[新しい項目の追加]** ダイアログ ボックスで、 **[Office/SharePoint]** ノードを選択します。

7. SharePoint テンプレートの一覧で、 **[ビジネス データ接続モデル (ファーム ソリューションのみ)]** を選択します。

8. **[名前]** ボックスに BDC モデルの名前を入力し、 **[追加]** ボタンを選択します。

     **ビジネス データ接続モデル** 項目がプロジェクトに追加されます。 既定で、BDC デザイナーにモデルが表示されます。 詳細については、「[ビジネス データ接続モデルを作成する](../sharepoint/creating-a-business-data-connectivity-model.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [ビジネス データ接続モデルを作成する](../sharepoint/creating-a-business-data-connectivity-model.md)
- [方法: 既存の BDC モデル ファイルを SharePoint プロジェクトに追加する](../sharepoint/how-to-add-an-existing-bdc-model-file-to-a-sharepoint-project.md)
- [方法: リソース ファイルを使用して、ローカライズした名前、プロパティ、およびアクセス許可を指定する](../sharepoint/how-to-use-a-resource-file-to-specify-localized-names-properties-and-permissions.md)
- [方法: BDC 機能にカスタム アセンブリを含める](../sharepoint/how-to-include-a-custom-assembly-in-a-bdc-feature.md)
- [SharePoint へのビジネス データの統合](../sharepoint/integrating-business-data-into-sharepoint.md)
