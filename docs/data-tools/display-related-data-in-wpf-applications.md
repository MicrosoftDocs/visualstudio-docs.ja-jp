---
title: WPF アプリケーションで関連データを表示する
description: WPF アプリケーションで関連データを表示します。 親子関係で相互に関連する複数のテーブルまたはエンティティからのデータを操作します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- data [WPF], displaying
- WPF, data binding in Visual Studio
- WPF data binding [Visual Studio]
- displaying data, WPF
- WPF [WPF], data
- WPF Designer, data binding
- data binding, WPF
ms.assetid: 3aa80194-0191-474d-9d28-5ec05654b426
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: 3467b2a3c4f49b22ab36b44ff0d3ea47d143e971
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99866958"
---
# <a name="display-related-data-in-wpf-applications"></a>WPF アプリケーションで関連データを表示する

アプリケーションによっては、親子関係で相互に関連する複数のテーブルまたはエンティティからのデータを操作することが必要な場合があります。 たとえば、`Customers` テーブルの顧客を表示するグリッドを表示したい場合があります。 ユーザーが特定の顧客を選択すると、関連する `Orders` テーブルにあるその顧客の注文が別のグリッドに表示されます。

**[データ ソース]** ウィンドウから WPF デザイナーに項目をドラッグすることで、関連データを表示するデータバインド コントロールを作成できます。

## <a name="to-create-controls-that-display-related-records"></a>関連するレコードを表示するコントロールを作成するには

1. **[データ]** メニューの **[データ ソースの表示]** をクリックして **[データ ソース]** ウィンドウを開きます。

2. **[新しいデータ ソースの追加]** をクリックして、**データ ソース構成ウィザード** の操作を完了します。

3. WPF デザイナーを開き、 **[データ ソース]** ウィンドウ内の項目の有効なドロップ ターゲットであるコンテナーがデザイナーに含まれていることを確認します。

     有効なドロップ ターゲットの詳細については、「[Visual Studio でデータに WPF コントロールをバインドする](../data-tools/bind-wpf-controls-to-data-in-visual-studio.md)」を参照してください。

4. **[データ ソース]** ウィンドウで、リレーションシップの親テーブルまたはオブジェクトを表すノードを展開します。 親テーブルまたはオブジェクトは、一対多リレーションシップの "一" 側になります。

5. 親ノード (または親ノード内の個々の項目) を、 **[データ ソース]** ウィンドウからデザイナーの有効なドロップ ターゲットにドラッグします。

     Visual Studio により、ドラッグした項目ごとに新しいデータバインド コントロールを作成する XAML が生成されます。 この XAML では、親テーブルまたはオブジェクトの新しい <xref:System.Windows.Data.CollectionViewSource> もドロップ ターゲットのリソースに追加します。 一部のデータ ソースでは、Visual Studio によって、親テーブルまたはオブジェクトにデータを読み込むコードも生成されます。 詳細については、「[Visual Studio でデータに WPF コントロールをバインドする](../data-tools/bind-wpf-controls-to-data-in-visual-studio.md)」を参照してください。

6. **[データ ソース]** ウィンドウで、関連する子テーブルまたはオブジェクトを見つけます。 関連する子テーブルおよびオブジェクトは、親ノードのデータ リストの下部に展開可能なノードとして表示されます。

7. 子ノード (または子ノード内の個々の項目) を、 **[データ ソース]** ウィンドウからデザイナーの有効なドロップ ターゲットにドラッグします。

     Visual Studio により、ドラッグした項目ごとに新しいデータバインド コントロールを作成する XAML が生成されます。 この XAML では、子テーブルまたはオブジェクトの新しい <xref:System.Windows.Data.CollectionViewSource> もドロップ ターゲットのリソースに追加します。 この新しい <xref:System.Windows.Data.CollectionViewSource> は、先ほどデザイナーにドラッグした親テーブルまたはオブジェクトのプロパティにバインドされます。 一部のデータ ソースでは、Visual Studio によって、子テーブルまたはオブジェクトにデータを読み込むコードも生成されます。

     次の図は、 **[データ ソース]** ウィンドウのデータセットにある **Customers** テーブルの関連する **Orders** テーブルを示しています。

     ![関係を示すデータ ソース ウィンドウ](../data-tools/media/datasources2.gif)

## <a name="see-also"></a>関連項目

- [Visual Studio でデータに WPF コントロールをバインドする](../data-tools/bind-wpf-controls-to-data-in-visual-studio.md)
- [WPF アプリケーションでルックアップ テーブルを作成する](../data-tools/create-lookup-tables-in-wpf-applications.md)
