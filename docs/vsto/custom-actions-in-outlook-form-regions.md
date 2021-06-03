---
title: Outlook フォーム領域のカスタム アクション
description: アクションの表示ボタン ([返信] や [全員に返信] など) を使用して、ユーザーが Microsoft Office Outlook アイテムに応答できるようにする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- form regions [Office development in Visual Studio], custom actions
- custom actions [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 1f95c5bfcd0dda73b3cd3392c5a8b0bb7384bd9f
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99947881"
---
# <a name="custom-actions-in-outlook-form-regions"></a>Outlook フォーム領域のカスタム アクション
  アクションには、ユーザーが Microsoft Office Outlook アイテムに応答できるようにするボタンが表示されます。 たとえば、メール アイテムに応答するには、 **[返信]** 、 **[全員に返信]** 、または **[転送]** 操作ボタンをクリックします。 これらの各アクションは、新しいメール アイテムを作成し、元のアイテムの情報を使用してアイテムのフィールドを設定します。

 任意の種類の Outlook アイテムを開くカスタム アクションを作成できます。 たとえば、新しい予定またはタスク アイテムを開くカスタム アクションを追加できます。 カスタム アクションのプロパティを設定するか、カスタム コードを使用して新しいアイテムのフィールドを設定します。 カスタム アクションは、Outlook インスペクター ウィンドウで開いているアイテムの **[カスタム アクション]** ドロップダウンに表示されます。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="add-custom-actions-to-a-form-region"></a>フォーム領域にカスタム アクションを追加する
 カスタム アクションをフォーム領域に追加するには、 **[カスタム アクション]** ダイアログ ボックスを使用します。 **[カスタム アクション]** ダイアログ ボックスを開くには、**ソリューション エクスプローラー** でフォーム領域を選択し、**プロパティ ウィンドウ** で **[マニフェスト]** ノードを展開します。次に、 **[CustomActions]** プロパティを選択し、省略記号ボタン (![ASP.NET モバイル デザイナーの省略記号](../sharepoint/media/mwellipsis.gif "ASP.NET モバイル デザイナー楕円")) をクリックします。

 **[カスタム アクション]** ダイアログ ボックスを使用すると、"*ターゲット フォーム*" を指定できます。 ターゲット フォームは、ユーザーがカスタム アクションを実行したときに表示されるフォームです。

 また、 **[カスタム アクション]** ダイアログ ボックスを使用して、元のアイテムの情報をターゲット フォームに表示する方法を指定することもできます。

 次の表では、 **[カスタム アクション]** ダイアログ ボックスで使用できるプロパティについて説明します。

|プロパティ|説明|
|--------------|-----------------|
|**AddressLike**|ターゲット フォームのアドレス指定方法を指定します。|
|**本文**|元のアイテムの本文がターゲット フォームにどのように追加されるかを指定します。|
|**Enabled**|カスタム アクションが有効かどうかを示します。 このプロパティが **false** に設定されている場合、カスタム アクションは無効です。|
|**方法**|カスタム アクションの実行時に使用可能な応答の種類を指定します。 カスタム アクションでは、フォームを送信したり、フォームを開いたり、フォームを送信するか開くかをユーザーに確認したりできます。|
|**名前**|コード内でこのカスタム アクションを参照するために使用できる内部名を指定します。|
|**ShowOnRibbon**|元のアイテムのリボンにカスタム アクションを表示するかどうかを示します。|
|**SubjectPrefix**|ターゲット フォームの件名行の先頭に挿入されるテキストを指定します。|
|**TargetForm**|ターゲット フォームのメッセージ クラス名を指定します。 たとえば、タスク フォームを開くには、「**IPM.Task**」と入力します。|
|**Title**|カスタム アクションのボタンのラベルを指定します。|

## <a name="customize-a-custom-action-at-run-time"></a>実行時にカスタム アクションをカスタマイズする
 コードを使用して、カスタム アクションに動作を追加することもできます。 たとえば、電子メールの受信者の名前を取得し、それらの名前を出席者として新しい予定アイテムに追加するコードを追加できます。 これを行うには、[MailItem オブジェクト](/office/vba/api/Outlook.MailItem)の [CustomAction](/office/vba/api/Outlook.MailItem.CustomAction) イベントを処理します。

## <a name="see-also"></a>関連項目
- [Outlook フォーム領域の作成](../vsto/creating-outlook-form-regions.md)
- [チュートリアル: Outlook フォーム領域のデザイン](../vsto/walkthrough-designing-an-outlook-form-region.md)
- [フォーム領域を Outlook メッセージ クラスに関連付ける](../vsto/associating-a-form-region-with-an-outlook-message-class.md)
