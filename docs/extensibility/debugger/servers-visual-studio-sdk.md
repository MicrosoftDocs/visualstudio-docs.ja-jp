---
title: サーバー (Visual Studio SDK) | Microsoft Docs
description: この記事では、Visual Studio のデバッガー アーキテクチャにおけるサーバーの定義と役割について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- servers, debugging
- debugging [Debugging SDK], servers
ms.assetid: 62236d64-7956-448c-9ac3-5528f3edac1d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: b7bb19262d4ce5fd1b3139f05cd9bbc57131db1c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105070363"
---
# <a name="servers-visual-studio-sdk"></a>サーバー (Visual Studio SDK)
デバッガー アーキテクチャでは、"*サーバー*" は次の役割を果たします。

- ポートとポート サプライヤーのコンテナーであり、ポートとポート サプライヤーをセッション デバッグ マネージャー (SDM) およびデバッグ エンジンに伝えます。

- 名前によって自身を識別し、そのポートとポート サプライヤーを列挙することができます。

- [IDebugCoreServer2](../../extensibility/debugger/reference/idebugcoreserver2.md) インターフェイスによって表されます。これは、Visual Studio によってのみ実装されます (実行されている Visual Studio のインスタンスごとに 1 つのサーバー インスタンス)。

## <a name="see-also"></a>関連項目
- [ポート](../../extensibility/debugger/ports.md)
- [ポート サプライヤー](../../extensibility/debugger/port-suppliers.md)
- [デバッガーの概念](../../extensibility/debugger/debugger-concepts.md)
- [IDebugCoreServer2](../../extensibility/debugger/reference/idebugcoreserver2.md)
