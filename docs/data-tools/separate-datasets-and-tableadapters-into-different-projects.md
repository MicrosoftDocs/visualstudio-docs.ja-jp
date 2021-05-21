---
title: 個別のプロジェクトの使用エラー
description: データセットと TableAdapter を別々のプロジェクトに分離する方法について説明します。これにより、アプリケーション層を分離して、n 層データ アプリケーションをすばやく生成できます。
ms.date: 11/04/2016
ms.topic: how-to
ms.custom: SEO-VS-2020
helpviewer_keywords:
- TableAdapters, n-tier applications
- n-tier applications, separating Datasets and TableAdapters
ms.assetid: f66a3940-6227-46af-a930-9177f425f4fd
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: 9463fe0371ee3184fd78684e7fe0565820ab3bf0
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99866542"
---
# <a name="separate-datasets-and-tableadapters-into-different-projects"></a>データセットと TableAdapters を別々のプロジェクトに分離する
[TableAdapter](create-and-configure-tableadapters.md) とデータセット クラスを別々のプロジェクトに生成できるように、型指定されたデータセットが強化されました。 これにより、アプリケーション層を分離して、n 層データ アプリケーションをすばやく生成できるようになります。

次の手順では、**データセット デザイナー** を使用して、生成された TableAdapter コードを含むプロジェクトとは別のプロジェクトにデータセット コードを生成するプロセスについて説明します。

## <a name="separate-datasets-and-tableadapters"></a>データセットと TableAdapter を分離する
TableAdapter コードからデータセット コードを分離する場合、データセット コードを含めるプロジェクトを現在のソリューションに配置する必要があります。 このプロジェクトが現在のソリューションに配置されていない場合、 **[プロパティ]** ウィンドウの **[DataSet プロジェクト]** の一覧で使用することはできません。

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

#### <a name="to-separate-the-dataset-into-a-different-project"></a>データセットを別のプロジェクトに分離するには

1. データセット ( *.xsd* ファイル) を含むソリューションを開きます。

    > [!NOTE]
    > データセット コードの分離先のプロジェクトがソリューションに含まれていない場合は、プロジェクトを作成するか、既存のプロジェクトをソリューションに追加します。

2. **ソリューション エクスプローラー** で型指定されたデータセット ファイル (*.xsd* ファイル) をダブルクリックして、**データセット デザイナー** でデータセットを開きます。

3. **データセット デザイナー** の空の領域を選択します。

4. **[プロパティ]** ウィンドウで **[DataSet プロジェクト]** ノードを見つけます。

5. **[DataSet プロジェクト]** の一覧で、データセット コードの生成先のプロジェクトの名前を選択します。

     データセット コードの生成先のプロジェクトを選択すると、 **[DataSet ファイル]** プロパティに既定のファイル名が設定されます。 必要に応じて、この名前を変更できます。 さらに、データセット コードを特定のディレクトリに生成する場合は、**[プロジェクト フォルダー]** プロパティをフォルダーの名前に設定できます。

    > [!NOTE]
    > ( **[DataSet プロジェクト]** プロパティを設定して) データセットと TableAdapter を分離するときに、プロジェクト内の既存のデータセット部分クラスは自動的には移動されません。 既存のデータセット部分クラスは、データセット プロジェクトに手動で移動する必要があります。

6. データセットを保存します。

     データセット コードが、 **[DataSet プロジェクト]** プロパティで選択したプロジェクトに生成され、**TableAdapter** コードが現在のプロジェクトに生成されます。

既定では、データセット コードと TableAdapter コードを分離すると、プロジェクトごとに別個のクラス ファイルが生成されます。 元のプロジェクトには、TableAdapter コードを含む *DatasetName.Designer.vb* (または *DatasetName.Designer.cs*) という名前のファイルが存在します。 **[DataSet プロジェクト]** プロパティで指定したプロジェクトには、データセット コードを含む *DatasetName.DataSet.Designer.vb* (または *DatasetName.DataSet.Designer.cs*) という名前のファイルが存在します。

> [!NOTE]
> 生成されたクラス ファイルを表示するには、データセット プロジェクトまたは TableAdapter プロジェクトを選択します。 次に、**ソリューション エクスプローラー** で、 **[すべてのファイルを表示]** を選択します。

## <a name="see-also"></a>関連項目

- [n 層データ アプリケーションの概要](../data-tools/n-tier-data-applications-overview.md)
- [チュートリアル: n 層データ アプリケーションの作成](../data-tools/walkthrough-creating-an-n-tier-data-application.md)
- [階層更新](../data-tools/hierarchical-update.md)
- [Visual Studio でのデータへのアクセス](../data-tools/accessing-data-in-visual-studio.md)
- [ADO.NET](/dotnet/framework/data/adonet/index)
