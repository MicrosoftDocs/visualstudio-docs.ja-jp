---
title: サーバー (Visual Studio SDK) |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- servers, debugging
- debugging [Debugging SDK], servers
ms.assetid: 62236d64-7956-448c-9ac3-5528f3edac1d
caps.latest.revision: 18
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 7ed2ce924b22827a82a67664e3e473f0930a87e3
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "68199396"
---
# <a name="servers-visual-studio-sdk"></a>サーバー (Visual Studio SDK)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

デバッガーのアーキテクチャの観点から、 **server**:  
  
- ポートおよびポート サプライヤーのコンテナーは、セッション デバッグ マネージャー (SDM) のポートとポート サプライヤーの通信し、エンジンのデバッグに使用されます。  
  
- 名前で識別し、そのポートとポート サプライヤーを列挙できます。  
  
- によって表される、 [IDebugCoreServer2](../../extensibility/debugger/reference/idebugcoreserver2.md)インターフェイスで、Visual Studio (Visual Studio の実行の各インスタンスのサーバーの 1 つのインスタンス) によってのみ実装されます。  
  
## <a name="see-also"></a>関連項目  
 [ポート](../../extensibility/debugger/ports.md)   
 [ポート サプライヤー](../../extensibility/debugger/port-suppliers.md)   
 [デバッガーの概念](../../extensibility/debugger/debugger-concepts.md)   
 [IDebugCoreServer2](../../extensibility/debugger/reference/idebugcoreserver2.md)
