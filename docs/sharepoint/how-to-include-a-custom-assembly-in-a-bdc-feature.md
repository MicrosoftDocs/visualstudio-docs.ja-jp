---
title: '方法: BDC 機能にカスタム アセンブリを含める | Microsoft Docs'
description: ビジネス データ接続 (BDC) 機能にカスタム アセンブリを含めて、プロジェクトで同じソリューション内の他のプロジェクトからアセンブリを参照できるようにします。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- VS.SharePointTools.BDC.Add_Assemblies_Dialog
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Business Data Connectivity service [SharePoint development in Visual Studio], add reference
- Business Data Connectivity service [SharePoint development in Visual Studio], custom assembly
- BDC [SharePoint development in Visual Studio], custom assembly
- BDC [SharePoint development in Visual Studio], add reference
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 7a5bce649a0bd9411c064c463defa0946b47e81f
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99913612"
---
# <a name="how-to-include-a-custom-assembly-in-a-bdc-feature"></a>方法: BDC 機能にカスタム アセンブリを含める
  プロジェクトは、同じソリューション内の他のプロジェクトのアセンブリを参照できます。 ただし、 **[参照されたアセンブリの LobSystem への割り当て]** ダイアログ ボックスを使用して、プロジェクトの機能ファイルにこれらのアセンブリを追加する必要があります。

### <a name="to-include-a-custom-assembly-in-a-business-data-connectivity-bdc-feature"></a>ビジネス データ接続 (BDC) 機能にカスタム アセンブリを含めるには

1. **ソリューション エクスプローラー** で、BDC モデルが含まれているフォルダーを選択します。

2. **[表示]** メニューの **[プロパティ ウィンドウ]** をクリックします。

3. **[プロパティ]** ウィンドウで、 **[アセンブリ]** プロパティ、そのあと省略記号ボタン (![ASP.NET モバイル デザイナーの省略記号](../sharepoint/media/mwellipsis.gif "ASP.NET モバイル デザイナー楕円")) を選択します。

     **[参照アセンブリの LobSystem への割り当て]** ダイアログ ボックスが表示されます。

4. **[アセンブリの選択]** 一覧で、カスタム アセンブリを選択します。

    > [!NOTE]
    > アセンブリを含むプロジェクトへの参照を追加した場合、アセンブリは **[参照されたアセンブリの LobSystem への割り当て]** ダイアログ ボックスにのみ表示されます。 詳しくは、「[方法: [参照の追加] ダイアログ ボックスを使用して参照を追加または削除する](/previous-versions/wkze6zky(v=vs.140))」を参照してください。

5. **[参照プロパティ]** グループで、 **[LobSystem スコープ]** プロパティに対して表示される一覧を開き、カスタム アセンブリを使用するメソッドの LOB システムを選択してから、 **[OK]** を選択します。

    > [!NOTE]
    > カスタム アセンブリのコードをデバッグするには、ソリューション パッケージにアセンブリを追加する必要があります。 詳細については、「[方法: アセンブリを追加および削除する](../sharepoint/how-to-add-and-remove-additional-assemblies.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [方法: リソース ファイルを使用して、ローカライズした名前、プロパティ、およびアクセス許可を指定する](../sharepoint/how-to-use-a-resource-file-to-specify-localized-names-properties-and-permissions.md)
- [方法: 既存の BDC モデル ファイルを SharePoint プロジェクトに追加する](../sharepoint/how-to-add-an-existing-bdc-model-file-to-a-sharepoint-project.md)
- [ビジネス データ接続モデルを作成する](../sharepoint/creating-a-business-data-connectivity-model.md)
- [方法: BDC モデルを作成する](../sharepoint/how-to-create-a-bdc-model.md)
- [SharePoint へのビジネス データの統合](../sharepoint/integrating-business-data-into-sharepoint.md)