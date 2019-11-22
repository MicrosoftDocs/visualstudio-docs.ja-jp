---
title: Bind to an Activity&#39;s Property Dialog Box (Legacy) | Microsoft Docs
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
ms.openlocfilehash: 451544a84237bc6fa4e069df9dd1e17feccf86f7
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74301023"
---
# <a name="bind-to-an-activity39s-property-dialog-box-legacy"></a>Bind to an Activity&#39;s Property Dialog Box (Legacy)
This topic describes how use the **Bind to an Activity's Property** dialog box in the legacy [!INCLUDE[wfd1](../includes/wfd1-md.md)]. [!INCLUDE[wfd2](../includes/wfd2-md.md)] または [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] を対象とする必要がある場合は、従来の[!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)]を使用します。

 依存関係プロパティのインスタンス型は、別のアクティビティのパブリック プロパティまたはイベントにバインドすることができます。 For more information about activity binding, see [Using Dependency Properties](https://go.microsoft.com/fwlink?LinkID=65007).

 You select a property to bind to using the **Bind to an Activity's Property** dialog box. You open this dialog box by clicking the ellipses **[…]** at the end of the selected property's text box in the **Properties** window, or by clicking the blue exclamation mark icon that appears next to the property name in the property browser.

 The following table describes the user interface (UI) elements of the **Bind to an Activity's Property** dialog box.

|UI 要素|説明|
|----------------|-----------------|
|**Bind to an existing member**|ツリー表示ペインで、バインド先となるメンバーを選択します。 ツリー表示の下にあるペインには、そのメンバーがバインド先として有効な型であるかどうかを示すメッセージが表示されます。 Click **OK** to bind to the selected valid member.|
|**Bind to a new member**|バインド先となる新しいメンバー フィールドまたはプロパティを作成します。 Enter a **New Member Name**. Choose whether you want to create a dependency property or a public field by selecting **Create Field** or **Create Property**. Click **OK** to create the new member.|

## <a name="see-also"></a>参照
 [Using Activity Properties](https://go.microsoft.com/fwlink?LinkID=65013) [Using Dependency Properties](https://go.microsoft.com/fwlink?LinkID=65007) [Legacy Designer for Windows Workflow Foundation UI Help](../workflow-designer/legacy-designer-for-windows-workflow-foundation-ui-help.md)