---
title: ポート サプライヤー | Microsoft Docs
description: この記事では、Visual Studio のデバッガー アーキテクチャにおけるポート サプライヤーの定義と役割について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- port suppliers
- debugging [Debugging SDK], port suppliers
ms.assetid: a8f3db96-1a13-4e93-9ef6-0861880369e0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 7ace9a7072287fa26aee3fa2abd083cc9f7f1314
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105067804"
---
# <a name="port-suppliers"></a>ポート サプライヤー
デバッガー アーキテクチャにおいて、"*ポート サプライヤー*" は次のようなものです。

- サーバーに含まれており、要求に応じてそのサーバーにポートが提供されます。

- 含まれているサーバーからポートの追加と削除を行うことができます。

- サーバーに提供されたすべてのポートを列挙できます。

- レジストリを介して Visual Studio に登録されている [IDebugPortSupplier2](../../extensibility/debugger/reference/idebugportsupplier2.md) インターフェイスで表されます。 このインターフェイスは、[GetPortSupplier](../../extensibility/debugger/reference/idebugcoreserver2-getportsupplier.md) を呼び出して取得できます。

  [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] により、既定のポート サプライヤーと既定のポートが提供されます。 カスタム ポートを実装する必要がある場合は、カスタム ポート サプライヤーも実装し、それらのカスタム ポートを提供する必要があります。

## <a name="see-also"></a>こちらもご覧ください
- [サーバー](../../extensibility/debugger/servers-visual-studio-sdk.md)
- [ポート](../../extensibility/debugger/ports.md)
- [デバッガーの概念](../../extensibility/debugger/debugger-concepts.md)
- [IDebugPortSupplier2](../../extensibility/debugger/reference/idebugportsupplier2.md)
- [GetPortSupplier](../../extensibility/debugger/reference/idebugcoreserver2-getportsupplier.md)
