---
title: '[アクティビティ&#39;のプロパティへのバインド] ダイアログボックス (レガシ) |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Workflow.ComponentModel.Design.ActivityBindForm.UI
helpviewer_keywords:
- Bind to an Activity's Property dialog box
ms.assetid: 19ebb207-e0a9-4642-8f5f-a5e31395c683
caps.latest.revision: 5
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: b93f6787ef24a191385c0fd86672aa23ff72e3e5
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72659218"
---
# <a name="bind-to-an-activity39s-property-dialog-box-legacy"></a>[アクティビティ&#39;のプロパティへのバインド] ダイアログボックス (レガシ)
このトピックでは、従来の [!INCLUDE[wfd1](../includes/wfd1-md.md)] の **[アクティビティのプロパティへのバインド]** ダイアログボックスの使用方法について説明します。 [!INCLUDE[wfd2](../includes/wfd2-md.md)] または [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] を対象とする必要がある場合は、従来の[!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)]を使用します。

 依存関係プロパティのインスタンス型は、別のアクティビティのパブリック プロパティまたはイベントにバインドすることができます。 アクティビティバインディングの詳細については、「[依存関係プロパティの使用](http://go.microsoft.com/fwlink?LinkID=65007)」を参照してください。

 バインドするプロパティを選択するには、 **[アクティビティのプロパティへのバインド]** ダイアログボックスを使用します。 このダイアログボックスを開くには、 **[プロパティ]** ウィンドウで選択したプロパティのテキストボックスの最後にある省略記号 **[...]** をクリックするか、プロパティブラウザーでプロパティ名の横に表示される青い感嘆符アイコンをクリックします。

 次の表では、 **[アクティビティのプロパティへのバインド]** ダイアログボックスのユーザーインターフェイス (UI) 要素について説明します。

|UI 要素|説明|
|----------------|-----------------|
|**既存のメンバーにバインドする**|ツリー表示ペインで、バインド先となるメンバーを選択します。 ツリー表示の下にあるペインには、そのメンバーがバインド先として有効な型であるかどうかを示すメッセージが表示されます。 **[OK]** をクリックして、選択した有効なメンバーにバインドします。|
|**新しいメンバーにバインドする**|バインド先となる新しいメンバー フィールドまたはプロパティを作成します。 **新しいメンバー名**を入力してください。 [フィールドの作成 **]** または **[プロパティの作成]** を選択して、依存関係プロパティとパブリックフィールドのどちらを作成するかを選択します。 **[OK]** をクリックして、新しいメンバーを作成します。|

## <a name="see-also"></a>参照
 [依存関係プロパティ](http://go.microsoft.com/fwlink?LinkID=65007)を使用した[アクティビティプロパティの使用](http://go.microsoft.com/fwlink?LinkID=65013) [Windows Workflow Foundation UI ヘルプのレガシデザイナー](../workflow-designer/legacy-designer-for-windows-workflow-foundation-ui-help.md)