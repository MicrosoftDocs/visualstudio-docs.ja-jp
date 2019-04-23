---
title: '方法: リボンのカスタマイズの概要します。'
ms.date: 02/02/2017
ms.topic: conceptual
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
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: f164a8f1d1c84725530e7a3afab5e63472ae257e
ms.sourcegitcommit: 1fc6ee928733e61a1f42782f832ead9f7946d00c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "60081568"
---
# <a name="how-to-get-started-customizing-the-ribbon"></a>方法: リボンのカスタマイズの概要します。
  Microsoft Office アプリケーションのリボンをカスタマイズするには追加、**リボン (ビジュアル デザイナー)** または**リボン (XML)** を Office プロジェクトの項目。

 [!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]

### <a name="to-add-a-ribbon-to-a-project"></a>プロジェクトにリボンを追加するには

1. **プロジェクト** メニューのをクリックして**新しい項目の追加**します。

2. **新しい項目の追加**ダイアログ ボックスで、**リボン (ビジュアル デザイナー)** または**リボン (XML)** します。 これらのテンプレートの詳細については、次を参照してください。[リボンの概要](../vsto/ribbon-overview.md)します。

3. **名前**ボックスに、リボン項目の名前を入力します。

    名前は、次の文字を含めることはできません。

   - ポンド (#)

   - パーセント (%)

   - アンパサンド (&)

   - アスタリスク (*)

   - 縦棒 (|)

   - 円記号 (\\)

   - コロン (:)

   - 二重引用符 (")

   - より小さい (\<)

   - 大なり (>)

   - 疑問符 (?)

   - フォワード スラッシュ (/)

   - 先頭または末尾の空白 (' ')

   - ("Nul"、"aux"、"con"、"com1"、"lpt1"など) など、Windows または DOS の予約されている名前

4. **[OK]** をクリックします。

   リボンのアイテムを表示**ソリューション エクスプ ローラー**します。 次の手順については、次を参照してください。[リボンの概要](../vsto/ribbon-overview.md)します。

## <a name="see-also"></a>関連項目
- [実行時にリボンへのアクセスします。](../vsto/accessing-the-ribbon-at-run-time.md)
- [リボン デザイナー](../vsto/ribbon-designer.md)
- [Ribbon XML](../vsto/ribbon-xml.md)
- [チュートリアル: リボン デザイナーを使用してカスタム タブを作成します。](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)
- [チュートリアル: リボン XML を使用してカスタム タブを作成します。](../vsto/walkthrough-creating-a-custom-tab-by-using-ribbon-xml.md)
