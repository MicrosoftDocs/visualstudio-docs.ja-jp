---
title: データセット デザイナーで DataTable を作成する
description: このチュートリアルでは、データセット デザイナーを使用して、(TableAdapter のない) DataTable を作成します。 新しい Windows フォーム アプリケーションを作成して、新しいデータセットを追加します。
ms.custom: SEO-VS-2020
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- DataTable objects, creating
- Dataset Designer, creating data tables
- tables [Visual Studio], creating
- data [Visual Studio], Dataset Designer
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: feec31fa0a9e34ad63e0b849d09084081e5710e5
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99858177"
---
# <a name="walkthrough-create-a-datatable-in-the-dataset-designer"></a>チュートリアル: データセット デザイナーで DataTable を作成する

このチュートリアルでは、**データセット デザイナー** を使用して、(TableAdapter のない) <xref:System.Data.DataTable> を作成する方法を説明します。 TableAdapter を含むデータ テーブルの作成方法については、「[TableAdapter の作成および構成](../data-tools/create-and-configure-tableadapters.md)」を参照してください。

## <a name="create-a-new-windows-forms-application"></a>新しい Windows フォーム アプリケーションを作成する

1. Visual Studio の **[ファイル]** メニューで､ **[新規作成]**  >  **[プロジェクト]** を選択します。

2. 左側のペインで **[Visual C#]** または **[Visual Basic]** を展開し、 **[Windows デスクトップ]** を選択します。

3. 中央のペインで、 **[Windows フォーム アプリ]** プロジェクト タイプを選択します。

4. プロジェクトに **DataTableWalkthrough** という名前を付け、 **[OK]** を選択します。

     **DataTableWalkthrough** プロジェクトが作成され、**ソリューション エクスプローラー** に追加されます。

## <a name="add-a-new-dataset-to-the-application"></a>新しいデータセットをアプリケーションに追加する

1. **[プロジェクト]** メニューで、 **[新しい項目の追加]** を選択します。

     **[新しい項目の追加]** ダイアログ ボックスが表示されます。

2. 左側のペインで、 **[データ]** を選択し、中央のペインで **[データセット]** を選択します。

3. **[追加]** を選びます。

     Visual Studio によってプロジェクトに **DataSet1.xsd** という名前のファイルが追加され、**データセット デザイナー** でこれが開かれます。

## <a name="add-a-new-datatable-to-the-dataset"></a>新しい DataTable をデータセットに追加する

1. **DataTable** を **[ツールボックス]** の **[データセット]** タブから **データセット デザイナー** にドラッグします。

     **DataTable1** という名前のテーブルが、データセットに追加されます。

2. **DataTable1** のタイトル バーをクリックし、名前を `Music` に変更します。

## <a name="add-columns-to-the-datatable"></a>DataTable に列を追加する

1. **[Music]** テーブルを右クリックします。 **[追加]** をポイントして、**[列]** をクリックします。

2. 列に `SongID` という名前を付けます。

3. **[プロパティ]** ウィンドウで、 <xref:System.Data.DataColumn.DataType%2A> プロパティを <xref:System.Int16?displayProperty=fullName>に設定します。

4. このプロセスを繰り返し、次の列を追加します。

     `SongTitle`: <xref:System.String?displayProperty=fullName>

     `Artist`: <xref:System.String?displayProperty=fullName>

     `Genre`: <xref:System.String?displayProperty=fullName>

## <a name="set-the-primary-key-for-the-table"></a>テーブルに主キーを設定する

すべてのデータ テーブルには主キーが必要です。 主キーは、データ テーブル内の特定のレコードを一意に識別します。

主キーを設定するには、 **[SongID]** 列を右クリックし、 **[主キーの設定]** をクリックします。 キー アイコンが **[SongID]** 列の横に表示されます。

## <a name="save-your-project"></a>プロジェクトを保存する

**DataTableWalkthrough** プロジェクトを保存するには、 **[ファイル]** メニューの **[すべて保存]** を選択します。

## <a name="see-also"></a>こちらもご覧ください

- [Visual Studio でデータセットを作成および構成する](../data-tools/create-and-configure-datasets-in-visual-studio.md)
- [Visual Studio でのデータへのコントロールのバインド](../data-tools/bind-controls-to-data-in-visual-studio.md)
- [データの検証](../data-tools/validate-data-in-datasets.md)
