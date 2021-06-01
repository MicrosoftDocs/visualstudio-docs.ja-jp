---
title: '方法: Office プロジェクトでイベント ハンドラーを作成する'
description: Visual Basic と C# でコントロール用の既定のイベント ハンドラーを作成するいくつかの方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Visual Basic [Office development in Visual Studio], event handlers
- event handlers [Office development in Visual Studio]
- Visual C# [Office development in Visual Studio], event handlers
- events [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: b2aed6102b6aed5938ecfab826363e62dcfac48a
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99889422"
---
# <a name="how-to-create-event-handlers-in-office-projects"></a>方法: Office プロジェクトでイベント ハンドラーを作成する
  Visual Basic と C# では、いくつかの方法でイベント ハンドラーを作成できます。 デザイン ビューでは、コントロールをダブルクリックすることでコントロール用の既定のイベント ハンドラーを作成したり、 **[プロパティ]** ウィンドウのイベント ペインを使用して、コントロールでの任意のイベント用のハンドラーを作成することができます。 ただし、コード ビューで作業している場合、イベント ハンドラーを作成するためにデザイン ビューに切り替えたくないことがあります。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

 [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

### <a name="to-create-an-event-handler-in-visual-basic"></a>Visual Basic でイベント ハンドラーを作成するには

1. コード エディターの上部にある **[クラス名]** ドロップダウン リストから、イベント ハンドラーを作成するオブジェクトを選択します。

    > [!NOTE]
    > `ThisDocument` または `ThisWorkbook` のイベント ハンドラーを作成する場合は、 **[クラス名]** ボックスの一覧で **[(ThisDocument Events)]\((ThisDocument イベント)\)** または **[(ThisWorkbook Events)]\((ThisWorkbook イベント)\)** を選択する必要があります

2. コード エディターの上部にある **[メソッド名]** ドロップダウン リストから、イベントを選択します。

     Visual Studio によってイベント ハンドラーが作成され、挿入ポイントが新しく作成されたイベント ハンドラーに移動されます。 イベント ハンドラーが既に存在する場合、挿入ポイントは既存のイベント ハンドラーに移動します。

### <a name="to-create-an-event-handler-in-c"></a>C\# でイベント ハンドラーを作成するには

1. 修飾されたイベント名の後にスペースを入力し、続いてスペースを入力せずに **+=** と入力することで、クラスの **Startup** イベントにイベント デリゲートを作成します。 次に例を示します。

     `this.<object name>.<event name> +=`

2. コード行の最後で、Tab キーを 2 回押します。

     Visual Studio により自動的にコード行が補完され、イベント ハンドラーが作成されて、新しく作成されたイベント ハンドラーに挿入ポイントが移動されます。

## <a name="see-also"></a>関連項目
- [Office ソリューションでコードを書く](../vsto/writing-code-in-office-solutions.md)
- [チュートリアル: NamedRange コントロールのイベントに対するプログラミング](../vsto/walkthrough-programming-against-events-of-a-namedrange-control.md)
- [Office ソリューションをビルドする](../vsto/building-office-solutions.md)
