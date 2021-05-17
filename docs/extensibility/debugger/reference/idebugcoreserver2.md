---
description: このインターフェイスは、ネットワーク上のコンピューター上のサーバーから情報を表示および取得するために使用されます。
title: IDebugCoreServer2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCoreServer2
helpviewer_keywords:
- IDebugCoreServer2 interface
ms.assetid: 9c47d0a6-9eb1-464e-bd44-fa2b552d4d36
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 318644353ff3643e92b2a7186359661b403db486
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105077721"
---
# <a name="idebugcoreserver2"></a>IDebugCoreServer2
このインターフェイスは、ネットワーク上のコンピューター上のサーバーから情報を表示および取得するために使用されます。

## <a name="syntax"></a>構文

```
IDebugCoreServer2 : IUknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 Visual Studio では、サーバーを表すためにこのインターフェイスを実装します。 Visual Studio の各インスタンスでは、このインターフェイスのインスタンスを作成します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 カスタム ポート サプライヤーでは、[Event](../../../extensibility/debugger/reference/idebugportevents2-event.md) の呼び出しでこのインターフェイスを受け取ります。

 デバッグ エンジンでは、(`IDebugCoreServer2` から派生したインターフェイスである [IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md) を返す) [GetServer](../../../extensibility/debugger/reference/idebugdefaultport2-getserver.md) を呼び出すことによって、このインターフェイスを間接的に取得できます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、`IDebugCoreServer2` のメソッドを示します。

|メソッド|説明|
|------------|-----------------|
|[GetMachineInfo](../../../extensibility/debugger/reference/idebugcoreserver2-getmachineinfo.md)|コンピューターの名前と属性を取得します。|
|[GetMachineName](../../../extensibility/debugger/reference/idebugcoreserver2-getmachinename.md)|コンピューターの名前を取得します。|
|[GetPortSupplier](../../../extensibility/debugger/reference/idebugcoreserver2-getportsupplier.md)|コンピューター上に存在するポート サプライヤーを取得します。|
|[GetPort](../../../extensibility/debugger/reference/idebugcoreserver2-getport.md)|コンピューター上に既に存在するポートを取得します。|
|[EnumPorts](../../../extensibility/debugger/reference/idebugcoreserver2-enumports.md)|コンピューター上のすべてのポートの列挙子を作成します。|
|[EnumPortSuppliers](../../../extensibility/debugger/reference/idebugcoreserver2-enumportsuppliers.md)|コンピューター上のすべてのポート サプライヤーの列挙子を作成します。|
|[GetMachineUtilities_V7](../../../extensibility/debugger/reference/idebugcoreserver2-getmachineutilities-v7.md)|コンピューターのコンピューター ユーティリティを取得します。|

## <a name="remarks"></a>解説
 このインターフェイスは、Visual Studio でネットワーク上のコンピューターで実行されているプロセスを参照するためにも使用されます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)
- [Event](../../../extensibility/debugger/reference/idebugportevents2-event.md)
- [GetServer](../../../extensibility/debugger/reference/idebugdefaultport2-getserver.md)
- [IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md)
