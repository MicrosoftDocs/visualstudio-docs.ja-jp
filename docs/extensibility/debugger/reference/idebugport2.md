---
description: このインターフェイスは、マシン上のデバッグ ポートを表します。
title: IDebugPort2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPort2
helpviewer_keywords:
- IDebugPort2 interface
ms.assetid: 8fd87f05-a950-4d14-b925-98be29d4facc
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 4d0b173f362418171def93ee92e3883b2910ad18
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105087341"
---
# <a name="idebugport2"></a>IDebugPort2
このインターフェイスは、マシン上のデバッグ ポートを表します。

## <a name="syntax"></a>構文

```
IDebugPort2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 カスタム ポート サプライヤーでは、このインターフェイスを実装してマシン上のデバッグ ポートを表します。

 ポートで送信ポート イベントがサポートされる場合は、<xref:System.Runtime.InteropServices.ComTypes.IConnectionPoint> インターフェイス (このインターフェイスによって [IDebugPortEvents2](../../../extensibility/debugger/reference/idebugportevents2.md) インターフェイスが提供されます) をサポートするために <xref:System.Runtime.InteropServices.ComTypes.IConnectionPointContainer> インターフェイスも実装する必要があります。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 [GetPort](../../../extensibility/debugger/reference/idebugportsupplier2-getport.md) または [AddPort](../../../extensibility/debugger/reference/idebugportsupplier2-addport.md) を呼び出すと、要求されたポートを表すこのインターフェイスが返されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、`IDebugPort2` のメソッドを示します。

|メソッド|説明|
|------------|-----------------|
|[GetPortName](../../../extensibility/debugger/reference/idebugport2-getportname.md)|ポートの名前を返します。|
|[GetPortId](../../../extensibility/debugger/reference/idebugport2-getportid.md)|ポートの ID を返します。|
|[GetPortRequest](../../../extensibility/debugger/reference/idebugport2-getportrequest.md)|ポートの作成に使用された要求を返します (存在する場合)。|
|[GetPortSupplier](../../../extensibility/debugger/reference/idebugport2-getportsupplier.md)|このポートのポート サプライヤーを返します。|
|[GetProcess](../../../extensibility/debugger/reference/idebugport2-getprocess.md)|プロセスの ID を指定して、プロセスへのインターフェイスを返します。|
|[EnumProcesses](../../../extensibility/debugger/reference/idebugport2-enumprocesses.md)|ポートで実行されているすべてのプロセスを列挙します。|

## <a name="remarks"></a>解説
 ローカル ポートでは、ローカル マシン上で実行されているすべてのプロセスとプログラムへのアクセスが提供されます。 その他のポートは、Windows CE ベースのデバイスへのシリアル ケーブル接続、または非 DCOM コンピューターへのネットワーク接続を表す場合があります。 `IDebugPort2` インターフェイスは、ポートの名前と ID を検索し、ポートで実行されているすべてのプロセスを列挙するために使用されます。 ポートでプロセスを起動および終了するための機能は、`IDebugPortEx2` インターフェイスに実装されます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md)
- [IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md)
