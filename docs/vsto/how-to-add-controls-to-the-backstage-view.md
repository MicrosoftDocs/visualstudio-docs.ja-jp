---
title: '方法: Backstage ビューにコントロールを追加する '
description: リボン デザイナーを使用して、[ファイル] タブをクリックしたときに表示されるメニューにコントロールを追加する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- customizing the Ribbon, menus
- controls, Ribbon
- menus, customizing
- Microsoft Office Button
- custom Ribbon, menus
- Ribbon, customizing
- Office button
- Ribbon, menus
- Microsoft Office Menu
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 830ecea036ee972321d98994ab36924e0c61a09b
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99954268"
---
# <a name="how-to-add-controls-to-the-backstage-view"></a>方法: Backstage ビューにコントロールを追加する
  リボン デザイナーを使用すると、 **[ファイル]** タブをクリックしたときに表示されるメニューにコントロールを追加できます。アプリケーションを実行すると、 **[ファイル]** タブに追加したコントロールに、"**アドイン**" という名前のグループが表示されます。

 Visual Studio でリボン デザイナーを使用して、ビルトイン コントロールの前または後ろにコントロールを配置することはできません。 ビルトイン コントロールは、Backstage ビューで既に表示されているコントロールです。 ビルトイン コントロールの前または後ろにコントロールを配置するには、リボン XML を使用する必要があります。 **リボン (XML)** の詳細については、[リボン XML](../vsto/ribbon-xml.md) に関するページを参照してください。 Backstage ビューのカスタマイズの詳細については、[開発者向け Office 2010 Backstage ビューの概要](/previous-versions/office/developer/office-2010/ee691833(v=office.14))および[開発者向け Office 2010 Backstage ビューのカスタマイズ](/previous-versions/office/developer/office-2010/ee815851(v=office.14))に関するそれぞれのページを参照してください。

 [!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]

### <a name="to-add-controls-to-backstage-view"></a>Backstage ビューにコントロールを追加するには

1. デザイン ビューでリボン項目を開きます。

     "**リボン (ビジュアル デザイナー)** " 項目をプロジェクトに追加する方法については、「[方法: リボンのカスタマイズの概要](../vsto/how-to-get-started-customizing-the-ribbon.md)」を参照してください。

2. リボン デザイナーで、 **[ファイル]** タブをクリックします。

     メニュー デザイナーが表示されます。 このデザイン サーフェイスには、コントロールは含まれていません。

3. **ツールボックス** の **[Office リボン コントロール]** タブから、次のコントロールのいずれかをメニュー デザイナーにドラッグします。

    - ボタン

    - CheckBox

    - [ギャラリー]

    - メニュー

    - 区切り記号

    - SplitButton

    - ToggleButton

4. コントロールをドラッグして、メニューの新しい位置に移動します。

## <a name="see-also"></a>関連項目
- [リボンの概要](../vsto/ribbon-overview.md)
- [リボン デザイナー](../vsto/ribbon-designer.md)
- [Ribbon XML](../vsto/ribbon-xml.md)
- [方法: リボンのカスタマイズの概要](../vsto/how-to-get-started-customizing-the-ribbon.md)
- [チュートリアル: リボン デザイナーを使用したカスタム タブの作成](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)
