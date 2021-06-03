---
title: '方法: リボンをリボン デザイナーからリボン XML にエクスポートする'
description: リボンをカスタマイズするために、デザイナーからリボン XML にリボンをエクスポートし、XML を直接編集できることについて説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- custom Ribbon, XML
- customizing the Ribbon, XML
- Ribbon [Office development in Visual Studio], XML
- Ribbon [Office development in Visual Studio], exporting
- XML [Office development in Visual Studio], Ribbon
- Ribbon Designer [Office development in Visual Studio]
- exporting Ribbon
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 1514410094deaf9c77e088c3b69e2d39d29175c2
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107825590"
---
# <a name="how-to-export-a-ribbon-from-the-ribbon-designer-to-ribbon-xml"></a>方法: リボンをリボン デザイナーからリボン XML にエクスポートする
  **リボン (ビジュアル デザイナー)** 項目では、すべての種類のリボンのカスタマイズがサポートされているわけではありません。 高度な方法でリボンをカスタマイズするために、デザイナーからリボン XML にリボンをエクスポートし、XML を直接編集することができます。

> [!NOTE]
> リボン XML ファイルには、すべてのプロパティ値が表示されるわけではありません。 詳細については、「[リボンの概要](../vsto/ribbon-overview.md)」を参照してください。

 [!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]

### <a name="to-export-a-ribbon-from-the-ribbon-designer-to-ribbon-xml"></a>リボンをリボン デザイナーからリボン XML にエクスポートするには

1. **ソリューション エクスプローラー** で、リボンのコード ファイルを右クリックし、 **[デザイナーの表示]** をクリックします。

2. リボン デザイナーを右クリックしてから、 **[リボンを XML にエクスポート]** をクリックします。

     Visual Studio によって、リボン XML ファイルとリボン XML コード ファイルがプロジェクトに追加されます。

3. リボンのコード クラスで、`TODO:` で始まるコメントを見つけます。

4. 開発しているソリューションの種類に応じて、これらのコメントのコード ブロックを **ThisAddin**、**ThisWorkbook**、**ThisDocument** のいずれかのクラスにコピーします。

     このコードにより、Microsoft Office アプリケーションでカスタム リボンを検出して読み込むことができます。 詳細については、「 [Ribbon XML](../vsto/ribbon-xml.md)」を参照してください。

5. **ThisAddin**、**ThisWorkbook**、または **ThisDocument** クラスで、コード ブロックのコメントを解除します。

     コードのコメントを解除すると、次の例のようになります。 この例では、リボン クラスの名前として `MyRibbon` を使用しています。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_Ribbon_Custom_Tab_XML_O12/ThisAddIn.cs" id="Snippet1":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_Ribbon_Custom_Tab_XML_O12/ThisAddIn.vb" id="Snippet1":::

6. リボン XML コード ファイルに切り替えて、`Ribbon Callbacks` 領域を見つけます。

     ここには、ボタンのクリックなど、ユーザーの操作を処理するコールバック メソッドを記述します。

7. リボン デザイナー コードで記述した各イベント ハンドラーのコールバック メソッドを作成します。

8. イベント ハンドラーからこれらのコールバック メソッドにすべてのイベント ハンドラー コードを移動し、リボン機能拡張 (RibbonX) プログラミング モデルで動作するようにコードを変更します。

     コールバック メソッドの記述と、RibbonX プログラミング モデルの使用の詳細については、「[リボン XML](../vsto/ribbon-xml.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [リボンの概要](../vsto/ribbon-overview.md)
- [リボン デザイナー](../vsto/ribbon-designer.md)
- [Ribbon XML](../vsto/ribbon-xml.md)
- [チュートリアル: リボン デザイナーを使用したカスタム タブの作成](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)
- [チュートリアル: リボン XML を使用してカスタム タブを作成する](../vsto/walkthrough-creating-a-custom-tab-by-using-ribbon-xml.md)
