---
title: データセットと TableAdapters を別々のプロジェクトに分離する
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- TableAdapters, n-tier applications
- n-tier applications, separating Datasets and TableAdapters
ms.assetid: f66a3940-6227-46af-a930-9177f425f4fd
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 9198378c5acf492216e2bebaceb210073766ea23
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72648183"
---
# <a name="separate-datasets-and-tableadapters-into-different-projects"></a>データセットと TableAdapters を別々のプロジェクトに分離する
型指定されたデータセットが拡張され、 [tableadapter](create-and-configure-tableadapters.md)とデータセットクラスを別々のプロジェクトに生成できるようになりました。 これにより、アプリケーション層を分離して、n 層データ アプリケーションをすばやく生成できるようになります。

次の手順では、**データセットデザイナー**を使用して、生成された TableAdapter コードを含むプロジェクトとは別のプロジェクトにデータセットコードを生成するプロセスについて説明します。

## <a name="separate-datasets-and-tableadapters"></a>データセットと Tableadapter を分離する
データセットコードを TableAdapter コードから分離する場合は、データセットコードを含むプロジェクトを現在のソリューションに配置する必要があります。 このプロジェクトが現在のソリューションに配置されていない場合、 **[プロパティ]** ウィンドウの **[データセットプロジェクト]** の一覧では使用できません。

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

#### <a name="to-separate-the-dataset-into-a-different-project"></a>データセットを別のプロジェクトに分離するには

1. データセット ( *.xsd* ファイル) を含むソリューションを開きます。

    > [!NOTE]
    > データセットコードを分離するプロジェクトがソリューションに含まれていない場合は、プロジェクトを作成するか、既存のプロジェクトをソリューションに追加します。

2. **ソリューション エクスプローラー**で型指定されたデータセット ファイル ( *.xsd* ファイル) をダブルクリックして、**データセット デザイナー**でデータセットを開きます。

3. **データセットデザイナー**の空の領域を選択します。

4. **[プロパティ]** ウィンドウで、 **[データセットプロジェクト]** ノードを見つけます。

5. **[データセットプロジェクト]** ボックスの一覧で、データセットコードを生成するプロジェクトの名前を選択します。

     データセットコードを生成するプロジェクトを選択すると、既定のファイル名が**データセットファイル**のプロパティに設定されます。 必要に応じて、この名前を変更できます。 さらに、データセット コードを特定のディレクトリに生成する場合は、 **[プロジェクト フォルダー]** プロパティをフォルダーの名前に設定できます。

    > [!NOTE]
    > データセットと Tableadapter を分離すると ( **DataSet プロジェクト**プロパティを設定することによって)、プロジェクト内の既存の部分データセットクラスは自動的には移動されません。 既存の部分データセットクラスは、データセットプロジェクトに手動で移動する必要があります。

6. データセットを保存します。

     データセットコードは、**データセットプロジェクト**のプロパティで選択されたプロジェクトに生成され、 **TableAdapter**コードは現在のプロジェクトに生成されます。

既定では、データセットと TableAdapter コードを分離した後、結果は各プロジェクトの不連続クラスファイルになります。 元のプロジェクトには、TableAdapter コードを含む*DatasetName* (または*DatasetName.Designer.cs*) という名前のファイルがあります。 " **Dataset プロジェクト**" プロパティで指定されているプロジェクトには、データセットコードを含む*DatasetName* (または*DatasetName.DataSet.Designer.cs*) という名前のファイルがあります。

> [!NOTE]
> 生成されたクラスファイルを表示するには、データセットまたは TableAdapter プロジェクトを選択します。 次に、**ソリューションエクスプローラー**で **[すべてのファイルを表示]** を選択します。

## <a name="see-also"></a>関連項目

- [n 層データ アプリケーションの概要](../data-tools/n-tier-data-applications-overview.md)
- [チュートリアル: n 層データ アプリケーションの作成](../data-tools/walkthrough-creating-an-n-tier-data-application.md)
- [階層更新](../data-tools/hierarchical-update.md)
- [Visual Studio でのデータへのアクセス](../data-tools/accessing-data-in-visual-studio.md)
- [ADO.NET](/dotnet/framework/data/adonet/index)