---
title: IDebugSessionProviderEx インターフェイス |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 26c5da2d-8c93-4d2b-94d2-97aaa377dcfe
caps.latest.revision: 6
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: c9bf341adeaeb17c8986b1b30b12f58113aef562
ms.sourcegitcommit: d3a485d47c6ba01b0fc9878cbbb7fe88755b29af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2019
ms.locfileid: "58146774"
---
# <a name="idebugsessionproviderex-interface"></a>IDebugSessionProviderEx インターフェイス
デバッガーのデバッグ ホスト側言語開始を有効にする IDE によって提供される主インターフェイスです。 実行中のアプリケーションのデバッグ セッションを確立します。 このインターフェイスは、マシン デバッグ マネージャーによって実装されます。  
  
 継承されたメソッドだけでなく`IUnknown`、`IDebugSessionProviderEx`インターフェイスは、次のメソッドを公開します。  
  
## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[IDebugSessionProviderEx:CanJITDebug](../../winscript/reference/idebugsessionproviderex-canjitdebug.md)|Just-in-time デバッグが、指定されたアプリケーションで実行できるかどうかを判断します。|  
|[IDebugSessionProviderEx:StartDebugSession](../../winscript/reference/idebugsessionproviderex-startdebugsession.md)|指定したアプリケーションのデバッグ セッションを開始します。|