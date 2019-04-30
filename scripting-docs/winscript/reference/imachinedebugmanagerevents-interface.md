---
title: IMachineDebugManagerEvents インターフェイス |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IMachineDebugManagerEvents interface
ms.assetid: 468de2f4-49e0-4f6f-ba0c-0f5f6832c092
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: fcfcc2aed0fedefdc149b83e911d33cd3b54cdef
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62977631"
---
# <a name="imachinedebugmanagerevents-interface"></a>IMachineDebugManagerEvents インターフェイス
マシン デバッグ マネージャーによって管理されている実行中アプリケーションのリストの変更を通知します。 このインターフェイスは、アプリケーションの動的な一覧を表示するデバッガー IDE で使用できます。  
  
 継承されたメソッドだけでなく`IUnknown`、`IMachineDebugManagerEvents`インターフェイスは、次のメソッドを公開します。  
  
## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[IMachineDebugManagerEvents::onAddApplication](../../winscript/reference/imachinedebugmanagerevents-onaddapplication.md)|アプリケーションが、実行中に追加されたときにイベントを処理するアプリケーションの一覧。|  
|[IMachineDebugManagerEvents::onRemoveApplication](../../winscript/reference/imachinedebugmanagerevents-onremoveapplication.md)|アプリケーションが実行から削除されたときにイベントを処理するアプリケーションの一覧。|