---
description: このインターフェイスは、プロセスが実行されているサーバーに関する情報にアクセスできるようにします。
title: IDebugCoreServer3 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCoreServer3
helpviewer_keywords:
- IDebugCoreServer3 interface
ms.assetid: 51f5f41b-a5a4-4df0-a703-41f3d1811d7f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ab605db6a49b8b7cc9893692ff1bb9e6da15171f
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105088147"
---
# <a name="idebugcoreserver3"></a>IDebugCoreServer3
このインターフェイスは、プロセスが実行されているサーバーに関する情報にアクセスできるようにします。

## <a name="syntax"></a>構文

```
IDebugCoreServer3 : IDebugCoreServer2
```

## <a name="notes-for-implementers"></a>実装側の注意
 Visual Studio により、このインターフェイスが実装されます。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 [IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md) インターフェイスからこのインターフェイスを取得するには、[QueryInterface](/cpp/atl/queryinterface) を使用します。 [GetServer](../../../extensibility/debugger/reference/idebugdefaultport2-getserver.md) の呼び出しで、このインターフェイスを返すこともできます。 このインターフェイスは、多くの場合、カスタム ポート供給業者がサーバー (ローカルまたはリモート) でプログラムを起動するために使用されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 このインターフェイスは、[IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md) インターフェイスのメソッドに加えて、次のメソッドを実装します。

|メソッド|説明|
|------------|-----------------|
|[GetServerName](../../../extensibility/debugger/reference/idebugcoreserver3-getservername.md)|サーバーの名前を取得します。|
|[GetServerFriendlyName](../../../extensibility/debugger/reference/idebugcoreserver3-getserverfriendlyname.md)|サーバー名のフレンドリ バージョンを取得します|
|[EnableAutoAttach](../../../extensibility/debugger/reference/idebugcoreserver3-enableautoattach.md)|プロセスが開始されたときに自動的にプロセスにアタッチするように、特定のデバッグ エンジンに指示します。|
|[DiagnoseWebDebuggingError](../../../extensibility/debugger/reference/idebugcoreserver3-diagnosewebdebuggingerror.md)|自動アタッチに失敗した場合に、特定のエラー コードを取得します。|
|[CreateInstanceInServer](../../../extensibility/debugger/reference/idebugcoreserver3-createinstanceinserver.md)|サーバー上にデバッグ エンジンのインスタンスを作成します。|
|[QueryIsLocal](../../../extensibility/debugger/reference/idebugcoreserver3-queryislocal.md)|サーバーが呼び出し元と同じマシン上にあるかどうかを示すフラグを取得します。|
|[GetConnectionProtocol](../../../extensibility/debugger/reference/idebugcoreserver3-getconnectionprotocol.md)|サーバーとの通信に使用されているプロトコルを示す値を取得します。|
|[DisableAutoAttach](../../../extensibility/debugger/reference/idebugcoreserver3-disableautoattach.md)|このサーバーが認識しているすべてのデバッグ エンジンのすべての自動アタッチ設定を無効にします。|

## <a name="remarks"></a>解説
 カスタム ポート供給業者は、[Event](../../../extensibility/debugger/reference/idebugportevents2-event.md) の呼び出しで [IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md) インターフェイスを受け取ります。 `IDebugCoreServer3` インターフェイスは、そのインターフェイスから取得できます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md)
- [GetServer](../../../extensibility/debugger/reference/idebugdefaultport2-getserver.md)
