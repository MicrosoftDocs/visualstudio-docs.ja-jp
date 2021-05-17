---
description: このインターフェイスは、ポートのサーバーおよび通知機能にアクセスするための複数のメソッドを提供します。
title: IDebugDefaultPort2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDefaultPort2
helpviewer_keywords:
- IDebugDefaultPort2 interface
ms.assetid: 7b3452af-9a96-4c4c-9946-4339b72d3d7b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 03eb9f8c1bae74f15d295a72b27821d41b8282a1
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105067115"
---
# <a name="idebugdefaultport2"></a>IDebugDefaultPort2
このインターフェイスは、ポートのサーバーおよび通知機能にアクセスするための複数のメソッドを提供します。

## <a name="syntax"></a>構文

```
IDebugDefaultPort2 : IDebugPort2
```

## <a name="notes-for-implementers"></a>実装側の注意
 Visual Studio では、プログラムにアクセスするためのデバッグ ポートを表すために、このインターフェイスを実装します。 カスタム ポート サプライヤーは、リモート デバッグを処理する場合、このインターフェイスを実装することもできます。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 [IDebugProgramProvider2](../../../extensibility/debugger/reference/idebugprogramprovider2.md) インターフェイスのメソッドの引数で、このインターフェイスを指定します。 このインターフェイスは、[IDebugPort2](/cpp/atl/queryinterface) インターフェイスの [QueryInterface](../../../extensibility/debugger/reference/idebugport2.md) を呼び出して取得することもできます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md) で定義されているメソッドに加えて、このインターフェイスは次のメソッドを実装します。

|メソッド|説明|
|------------|-----------------|
|[GetPortNotify](../../../extensibility/debugger/reference/idebugdefaultport2-getportnotify.md)|このポートからのポート通知インターフェイスを取得します。|
|[GetServer](../../../extensibility/debugger/reference/idebugdefaultport2-getserver.md)|このポートをホストしているサーバーへのインターフェイスを取得します。|
|[QueryIsLocal](../../../extensibility/debugger/reference/idebugdefaultport2-queryislocal.md)|このポートがローカル コンピューター上で実行されているかどうかを判断します。|

## <a name="remarks"></a>解説
 既定のポートを表すわけではないため、"`IDebugDefaultPort2`" という名前はやや誤解を招きます。 "IDebugPort3" のような名前にすることができます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)
- [IDebugProgramProvider2](../../../extensibility/debugger/reference/idebugprogramprovider2.md)
