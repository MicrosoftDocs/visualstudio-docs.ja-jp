---
title: Activity Views (Legacy) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
helpviewer_keywords:
- activities, activity views
- views, activity
- activity views
ms.assetid: 83dc68cd-2cb2-45c2-9a6e-10d82053171a
caps.latest.revision: 5
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 9b65a46d5d0061eeaf3ad707affea1423e5fca5d
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74297540"
---
# <a name="activity-views-legacy"></a>アクティビティ ビュー (レガシ)
[!INCLUDE[wf](../includes/wf-md.md)] が提供するアクティビティの多くには、従来の [!INCLUDE[wfd1](../includes/wfd1-md.md)]で使用できるデザイン ビューが複数あります。ワークフローは、これらのアクティビティを使用して作成されます。 When you drag an activity designer from the **Toolbox** onto the design surface, and thereafter whenever you select the activity, you can switch between the different design views by using either the **Workflow** menu or by right-clicking the selected activity. さらに、選択したアクティビティの名前の上にポインタを移動すると、ドロップダウン タブのセットが表示され、これを使ってさまざまなビューに切り替えることができます。

 Every activity has at least one view; this is the default view shown when you drag an activity designer from the **Toolbox** onto the design surface. This activity default view is available as the **View [activity type]** option on the menus and tab, for example, **View Parallel**. ほとんどのアクティビティには他にもビューがあり、ビューの種類はアクティビティによってさまざまに異なります。 For example, the [TransactionScopeActivity](https://go.microsoft.com/fwlink?LinkID=65093) activity has the compensation view and the [EventHandlingScopeActivity](https://go.microsoft.com/fwlink?LinkID=65030) activity has an events view. Many of the activities that come with Windows Workflow Foundation have **View Cancel Handler** and **View Faults** design views to view the [CancellationHandlerActivity](https://go.microsoft.com/fwlink?LinkID=65050) and a [FaultHandlersActivity](https://go.microsoft.com/fwlink?LinkID=65055) associated with them.

 各ビューの名前と説明の一覧を次の表に示します。

|メニュー/タブ オプション|説明|
|----------------------|-----------------|
|**View [activity type]**|このメニュー オプションまたはタブ オプションをクリックすると、選択したアクティビティの既定のビューがグラフィック表示されます。|
|**View Cancel Handler**|Select this menu or tab option view to view the [CancellationHandlerActivity](https://go.microsoft.com/fwlink?LinkID=65050) associated with the selected activity.|
|**View Fault Handler**|Select this menu or tab option view to view the [FaultHandlersActivity](https://go.microsoft.com/fwlink?LinkID=65055) associated with the selected activity.|
|**View Compensation Handler**|Select this menu or tab option view to view the [CompensationHandlerActivity](https://go.microsoft.com/fwlink?LinkID=65053) associated with the selected [TransactionScopeActivity](https://go.microsoft.com/fwlink?LinkID=65093).|
|**View Events Handler**|Select this menu or tab option view to view the [EventHandlersActivity](https://go.microsoft.com/fwlink?LinkID=65018) associated with the selected the [EventHandlingScopeActivity](https://go.microsoft.com/fwlink?LinkID=65030).|

 For information about similar views, see [Sequential Workflow Views (Legacy)](../workflow-designer/sequential-workflow-views-legacy.md).

## <a name="see-also"></a>参照
 [Legacy Workflow Activities](../workflow-designer/legacy-workflow-activities.md) [Sequential Workflow Views (Legacy)](../workflow-designer/sequential-workflow-views-legacy.md)