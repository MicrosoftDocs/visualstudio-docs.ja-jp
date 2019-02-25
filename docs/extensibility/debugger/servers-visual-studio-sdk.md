---
title: サーバー (Visual Studio SDK) |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- servers, debugging
- debugging [Debugging SDK], servers
ms.assetid: 62236d64-7956-448c-9ac3-5528f3edac1d
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f2e5b50a3f2969f8f22ce938522526a6010c640a
ms.sourcegitcommit: b0d8e61745f67bd1f7ecf7fe080a0fe73ac6a181
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/22/2019
ms.locfileid: "56691385"
---
# <a name="servers-visual-studio-sdk"></a>サーバー (Visual Studio SDK)
デバッガーのアーキテクチャで、 *server*:

-   ポートおよびポート サプライヤーのコンテナーと、セッション デバッグ マネージャー (SDM) とデバッグ エンジンにポートとポート サプライヤーを通信します。

-   名前で識別し、そのポートとポート サプライヤーを列挙できます。

-   によって表される、 [IDebugCoreServer2](../../extensibility/debugger/reference/idebugcoreserver2.md)インターフェイスで、Visual Studio (Visual Studio の実行の各インスタンスのサーバーの 1 つのインスタンス) によってのみ実装されます。

## <a name="see-also"></a>関連項目
- [ポート](../../extensibility/debugger/ports.md)
- [ポート サプライヤー](../../extensibility/debugger/port-suppliers.md)
- [デバッガーの概念](../../extensibility/debugger/debugger-concepts.md)
- [IDebugCoreServer2](../../extensibility/debugger/reference/idebugcoreserver2.md)