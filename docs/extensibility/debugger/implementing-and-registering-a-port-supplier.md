---
title: ポート サプライヤーの実装および登録 | Microsoft Docs
description: ポートの追跡と提供を行い、プロセスを管理するポート サプライヤーを実装および登録する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], registering port suppliers
- port suppliers, registering
ms.assetid: fb057052-ee16-4272-8e16-a4da5dda0ad4
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 16c1738d4059468384df7ee2e882c20c8b5a0537
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105059835"
---
# <a name="implement-and-register-a-port-supplier"></a>ポート サプライヤーを実装して登録する
ポート サプライヤーの役割は、ポートを追跡して提供することで、プロセスを管理します。 ポートを作成する必要がある場合は、ポート サプライヤーの GUID と共に CoCreate を使用してポート サプライヤーがインスタンス化されます (セッション デバッグ マネージャー [SDM] では、ユーザーが選択したポート サプライヤー、またはプロジェクト システムによって指定されたポート サプライヤーが使用されます)。 次に、SDM から [CanAddPort](../../extensibility/debugger/reference/idebugportsupplier2-canaddport.md) が呼び出され、ポートを追加できるかどうかを確認します。 ポートを追加できる場合、[AddPort](../../extensibility/debugger/reference/idebugportsupplier2-addport.md) を呼び出し、ポートを説明する [IDebugPortRequest2](../../extensibility/debugger/reference/idebugportrequest2.md) を渡すことによって、新しいポートが要求されます。 `AddPort` から [IDebugPort2](../../extensibility/debugger/reference/idebugport2.md) インターフェイスによって表される新しいポートが返されます。

## <a name="discussion"></a>ディスカッション
 ポートは、マシンまたはデバッグ サーバーに関連付けられているポート サプライヤーによって作成されます。 サーバーでは、[EnumPortSuppliers](../../extensibility/debugger/reference/idebugcoreserver2-enumportsuppliers.md) メソッドを使用してポート サプライヤーが列挙され、ポート サプライヤーでは [EnumPorts](../../extensibility/debugger/reference/idebugportsupplier2-enumports.md) メソッドを使用してポートが列挙されます。

 一般的な COM の登録に加えて、CLSID と名前を特定のレジストリの場所に配置することによって、ポート サプライヤー自体による Visual Studio への登録が必要です。 `SetMetric` というデバッグ SDK ヘルパー関数により、このような作業が処理されます。これは、登録される項目ごとに 1 回呼び出されます。

```cpp
SetMetric(metrictypePortSupplier,
          <GUID of your port supplier>,
          metricCLSID,
          <CLSID of your port supplier>,
          false,
          NULL)
SetMetric(metrictypePortSupplier,
          <GUID of your port supplier>,
          metricName,
          <name of your port supplier>,
          false,
          NULL);
```

 ポート サプライヤーから登録された項目ごとに 1 回 `RemoveMetric` (別のデバッグ SDK ヘルパー関数) が呼び出され、それ自身の登録が解除されます。

```cpp
RemoveMetric(metrictypePortSupplier,
             <GUID of your port supplier>,
             metricCLSID,
             NULL);
RemoveMetric(metrictypePortSupplier,
             <GUID of your port supplier>,
             metricName,
             NULL);
```

> [!NOTE]
> [デバッグ用の SDK ヘルパー](../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)`SetMetric`と `RemoveMetric` は、*dbgmetric.h* で定義され、*ad2de.lib* にコンパイルされた静的関数です。 `metrictypePortSupplier`、`metricCLSID`、`metricName`の各ヘルパーは、*dbgmetric.h* でも定義されています。

 ポート サプライヤーにより、メソッド [GetPortSupplierName](../../extensibility/debugger/reference/idebugportsupplier2-getportsuppliername.md) と [GetPortSupplierId](../../extensibility/debugger/reference/idebugportsupplier2-getportsupplierid.md) がそれぞれ使用されることで、名前と GUID の指定ができます。

## <a name="see-also"></a>関連項目
- [ポート サプライヤーを実装する](../../extensibility/debugger/implementing-a-port-supplier.md)
- [デバッグ用 SDK ヘルパー](../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)
- [ポート サプライヤー](../../extensibility/debugger/port-suppliers.md)
