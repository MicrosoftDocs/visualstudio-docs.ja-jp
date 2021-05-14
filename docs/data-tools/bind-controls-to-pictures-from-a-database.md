---
title: データベースの画像にコントロールをバインドする
description: '[データ ソース] ウィンドウを使用し、データベースのイメージを Visual Studio アプリケーションのコントロールにバインドします。'
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- images [Visual Basic], displaying on Windows Forms
- data binding [Windows Forms], pictures
- images [Visual Basic], data binding
- pictures, data binding
- pictures, dragging from Data Sources window
- Data Sources Window, setting controls to display images
- PictureBox control [Windows Forms], data binding
- images [Visual Basic], dragging from Data Sources window
ms.assetid: 9748815e-3556-49e8-86b1-c6aa593c6163
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: 2ce969ddab5e48ac495754369e980747332f9b0a
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99867374"
---
# <a name="bind-controls-to-pictures-from-a-database"></a>データベースの画像にコントロールをバインドする

**[データ ソース]** ウィンドウを使用して、データベースのイメージをアプリケーションのコントロールにバインドできます。 たとえば、WPF アプリケーションの <xref:System.Windows.Controls.Image> コントロールまたは Windows フォーム アプリケーションの <xref:System.Windows.Forms.PictureBox> コントロールにイメージをバインドできます。

データベースの画像は、通常はバイト配列として格納されます。 **[データ ソース]** ウィンドウ内のバイト配列として格納されている項目は、既定ではコントロール型が **[なし]** に設定されています。これは、バイト配列には、シンプルなバイトの配列から大規模なアプリケーションの実行可能ファイルまで、どのようなものでも含めることができるためです。 **[データ ソース]** ウィンドウ内のイメージを表すバイト配列項目のデータ バインド コントロールを作成するには、作成するコントロールを選択する必要があります。

次の手順では、イメージにバインドされている項目が既に **[データ ソース]** ウィンドウに作成されていると仮定します。

## <a name="to-bind-a-picture-in-a-database-to-a-control"></a>データベースの画像をコントロールにバインドするには

1. コントロールを追加するデザイン サーフェイスが WPF デザイナーまたは Windows フォーム デザイナーで開いていることを確認します。

2. **[データ ソース]** ウィンドウで、目的のテーブルまたはオブジェクトを展開して、その列またはプロパティを表示します。

   > [!TIP]
   > **[データ ソース]** ウィンドウが開いていない場合、 **[表示]** 、 **[その他のウィンドウ]** 、 **[データ ソース]** の順に選択して開きます。

3. イメージ データを含む列またはプロパティを選択し、ドロップダウン コントロール リストから次のいずれかのコントロールを選択します。

    - WPF デザイナーが開いている場合は、**[Image]** を選択します。

    - Windows フォーム デザイナーが開いている場合は、**[PictureBox]** を選択します。

    - または、データ バインディングをサポートし、かつイメージを表示できる、別のコントロールを選択することもできます。 使用するコントロールが利用できるコントロールのリストに含まれていない場合は、そのコントロールをリストに追加してから選択できます。 詳細については、「[[データ ソース] ウィンドウにカスタム コントロールを追加する](../data-tools/add-custom-controls-to-the-data-sources-window.md)」をご覧ください。

## <a name="see-also"></a>関連項目

- [Visual Studio でデータに WPF コントロールをバインドする](../data-tools/bind-wpf-controls-to-data-in-visual-studio.md)
