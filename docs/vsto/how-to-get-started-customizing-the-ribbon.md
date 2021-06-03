---
title: '方法: リボンのカスタマイズの概要'
description: Microsoft Office アプリケーションのリボンをカスタマイズし、リボン (ビジュアル デザイナー) またはリボン (XML) 項目を Office プロジェクトに追加する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- custom Ribbon, adding Ribbon to project
- Ribbon [Office development in Visual Studio], adding
- Ribbon [Office development in Visual Studio], customizing
- customizing the Ribbon, adding Ribbon to project
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: d82d059166b9efbb80ed6ce4cffcbb973235b01b
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99953917"
---
# <a name="how-to-get-started-customizing-the-ribbon"></a>方法: リボンのカスタマイズの概要
  Microsoft Office アプリケーションのリボンをカスタマイズし、**リボン (ビジュアル デザイナー)** または **リボン (XML)** 項目を Office プロジェクトに追加するには。

 [!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]

### <a name="to-add-a-ribbon-to-a-project"></a>リボンをプロジェクトに追加するには

1. **[プロジェクト]** メニューの **[新しい項目の追加]** をクリックします。

2. **[新しい項目の追加]** ダイアログ ボックスで、 **[リボン (ビジュアル デザイナー)]** または **[リボン (XML)]** を選択します。 これらのテンプレートの詳細については、[リボンの概要](../vsto/ribbon-overview.md)に関するページを参照してください。

3. **[名前]** ボックスに、リボン項目の名前を入力します。

    次の文字は名前に使用できません。

   - シャープ記号 (#)

   - パーセント (%)

   - アンパサンド (&)

   - アスタリスク (*)

   - 縦棒 (|)

   - 円記号 (\\)

   - コロン (:)

   - 二重引用符 (")

   - より小さい (\<)

   - より大きい (>)

   - 疑問符 (?)

   - スラッシュ (/)

   - 先頭または末尾の空白 (' ')

   - Windows または DOS の予約語 ("nul"、"aux"、"con"、"com1"、"lpt1" など)

4. **[OK]** をクリックします。

   **ソリューション エクスプローラー** にリボン項目が表示されます。 次の手順の詳細については、[リボンの概要](../vsto/ribbon-overview.md)に関するページを参照してください。

## <a name="see-also"></a>関連項目
- [実行時のリボンへのアクセス](../vsto/accessing-the-ribbon-at-run-time.md)
- [リボン デザイナー](../vsto/ribbon-designer.md)
- [Ribbon XML](../vsto/ribbon-xml.md)
- [チュートリアル: リボン デザイナーを使用したカスタム タブの作成](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)
- [チュートリアル : リボン XML を使用してカスタム タブを作成する](../vsto/walkthrough-creating-a-custom-tab-by-using-ribbon-xml.md)
