---
title: '方法: Office プロジェクトでのイベント ハンドラーを作成します。'
ms.date: 02/02/2017
ms.topic: conceptual
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
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 537bae766b71744a61e5158b1a859cade4cdcda7
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63419652"
---
# <a name="how-to-create-event-handlers-in-office-projects"></a>方法: Office プロジェクトでのイベント ハンドラーを作成します。
  Visual Basic および c# でイベント ハンドラーを作成するいくつかの方法はあります。 デザイン ビューでコントロールをダブルクリックして既定のコントロールのイベント ハンドラーを作成またはの [イベント] ペインを使用して、**プロパティ**ウィンドウ コントロールのすべてのイベント ハンドラーを作成します。 ただし、コード ビューでは、可能性がありますいないする場合、イベント ハンドラーを作成、デザイン ビューに切り替えます。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

 [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

### <a name="to-create-an-event-handler-in-visual-basic"></a>Visual Basic でイベント ハンドラーを作成するには

1. **クラス名**コード エディターの上部にあるドロップダウン リストを選択するオブジェクトがのイベント ハンドラーを作成します。

    > [!NOTE]
    > イベント ハンドラーを作成する場合`ThisDocument`または`ThisWorkbook`、選択する必要があります **(ThisDocument イベント)** または **(ThisWorkbook イベント)** で、**クラス名**ドロップダウン リスト

2. **メソッド名**ドロップダウン リストで、コード エディターの上部にあるイベントを選択します。

     Visual Studio では、イベント ハンドラーを作成して、新しく作成されたイベント ハンドラーにカーソルを移動します。 イベント ハンドラーが既に存在する場合は、既存のイベント ハンドラーにカーソルが移動します。

### <a name="to-create-an-event-handler-in-c"></a>C でイベント ハンドラーを作成するには\#

1. 内のイベントのデリゲートを作成、**スタートアップ**修飾イベント名の後にスペースを入力し、入力してクラスのイベント**+=** 後にスペースをします。 例:

     `this.<object name>.<event name> +=`

2. コードの行の終わりには、TAB キーを 2 回押します。

     Visual Studio が自動的のコード行が完了すると、イベント ハンドラーを作成および、新しく作成されたイベント ハンドラーにカーソルを移動します。

## <a name="see-also"></a>関連項目
- [Office ソリューションにおけるコードの記述](../vsto/writing-code-in-office-solutions.md)
- [チュートリアル: NamedRange コントロールのイベントのプログラム](../vsto/walkthrough-programming-against-events-of-a-namedrange-control.md)
- [Office ソリューションの構築](../vsto/building-office-solutions.md)
