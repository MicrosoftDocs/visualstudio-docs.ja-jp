---
title: データセットと TableAdapters を別々 のプロジェクトに分割します |。Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- TableAdapters, n-tier applications
- n-tier applications, separating Datasets and TableAdapters
ms.assetid: f66a3940-6227-46af-a930-9177f425f4fd
caps.latest.revision: 21
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 9228eaec55dc936d44eeccd55e6a05559aea27e4
ms.sourcegitcommit: 53aa5a413717a1b62ca56a5983b6a50f7f0663b3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59647465"
---
# <a name="separate-datasets-and-tableadapters-into-different-projects"></a>データセットと TableAdapters を別々のプロジェクトに分離する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

型指定されたデータセットが強化されているように、 [Tableadapter](http://msdn.microsoft.com/library/09416de9-134c-4dc7-8262-6c8d81e3f364)および個別のプロジェクトにデータセット クラスを生成することができます。 これにより、アプリケーション層を分離して、n 層データ アプリケーションをすばやく生成できるようになります。  
  
 次の手順をデータセット デザイナーを使用して、プロジェクトには、生成されたプロジェクトとは別にデータセット コードを生成するプロセスを説明する`TableAdapter`コード。  
  
## <a name="separatedatasets-and-tableadapters"></a>Separatedatasets と tableadapters の分離  
 コードからデータセット コードを分離する場合`TableAdapter`データセット コードを含むプロジェクトのコードは、現在のソリューションである必要があります。 このプロジェクトが現在のソリューションにない場合で使用できない、 **DataSet プロジェクト**の一覧で、**プロパティ**ウィンドウ。  
  
 [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]  
  
#### <a name="to-separate-the-dataset-into-a-different-project"></a>データセットを別のプロジェクトに分離するには  
  
1. データセット (.xsd ファイル) を含むソリューションを開きます。  
  
   > [!NOTE]
   >  ソリューションに、データセット コードを分離するプロジェクトが含まれていない場合は、プロジェクトを作成または既存のプロジェクトをソリューションに追加します。  
  
2. 型指定されたデータセット ファイル (.xsd ファイル) をダブルクリックして**ソリューション エクスプ ローラー**でデータセットを開きます、**データセット デザイナー**します。  
  
3. 空の領域を選択して、**データセット デザイナー**します。  
  
4. **プロパティ**ウィンドウで、検索、 **DataSet プロジェクト**ノード。  
  
5. **DataSet プロジェクト**一覧で、データセット コードを生成するプロジェクトの名前を選択します。  
  
    データセット コードを生成するプロジェクトを選択した後、**データセット ファイル**プロパティには、既定のファイル名が設定されます。 必要な場合は、この名前を変更できます。 さらに、データセット コードを特定のディレクトリに生成する場合は、**[プロジェクト フォルダー]** プロパティをフォルダーの名前に設定できます。  
  
   > [!NOTE]
   >  データセットと Tableadapter を分離する場合 (設定して、 **DataSet プロジェクト**プロパティ)、プロジェクト内の既存のデータセット部分クラスが自動的に移動しません。 既存のデータセット部分クラスは、データセット プロジェクトに手動で移動する必要があります。  
  
6. データセットを保存します。  
  
    選択したプロジェクトにデータセット コードが生成された、 **DataSet プロジェクト**プロパティ、および**TableAdapter**現在のプロジェクトにコードが生成されます。  
  
   既定では、データセットと `TableAdapter` コードを分離すると、結果としてプロジェクトごとに別個のクラス ファイルが生成されます。 元のプロジェクトにという名前のファイルを含む DatasetName.Designer.vb (または DatasetName.Designer.cs)、`TableAdapter`コード。 指定されているプロジェクト、 **Dataset プロジェクト**プロパティ ファイルは、データセット コードを含む DatasetName.DataSet.Designer.vb (または DatasetName.DataSet.Designer.cs) という名前です。  
  
> [!NOTE]
>  生成されたクラス ファイルを表示するには、データセットを選択します。 または`TableAdapter`プロジェクト。 次に、**ソリューション エクスプ ローラー**、 **すべてのファイル**します。  
  
## <a name="see-also"></a>関連項目  
 [N 層データ アプリケーションの概要](../data-tools/n-tier-data-applications-overview.md)   
 [チュートリアル: N 層データ アプリケーションの作成](../data-tools/walkthrough-creating-an-n-tier-data-application.md)   
 [階層更新](../data-tools/hierarchical-update.md)   
 [Visual Studio でのデータへのアクセス](../data-tools/accessing-data-in-visual-studio.md)   
 [ADO.NET](http://msdn.microsoft.com/library/5b96ed06-9759-4966-a797-a1d5f6ee50ca)
