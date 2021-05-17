---
description: このインターフェイスにより、アドレスがこのインターフェイスによって表されるオブジェクトを所有するプロセスの ID へのアクセスが提供されます。
title: IDebugAddress2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugAddress2
helpviewer_keywords:
- IDebugAddress2 interface
ms.assetid: b150e0ed-4ac0-4f8c-9732-4b3e54b9d243
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 7e74833768ed1a287c0dcf3b641b858261c2d661
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105059184"
---
# <a name="idebugaddress2"></a>IDebugAddress2
このインターフェイスにより、アドレスがこのインターフェイスによって表されるオブジェクトを所有するプロセスの ID へのアクセスが提供されます。

## <a name="syntax"></a>構文

```
IDebugAddress2 : IDebugAddress
```

## <a name="notes-for-implementers"></a>実装側の注意
 シンボル プロバイダーでは、[IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) インターフェイスを実装するのと同じオブジェクトにこのインターフェイスを実装します。 このインターフェイスにより、このアドレスに関連するオブジェクトを所有するプロセスの ID へのアクセスが提供されます。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 [QueryInterface](/cpp/atl/queryinterface) を使用して、[IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) インターフェイスからこのインターフェイスを取得します。

## <a name="methods-in-vtable-order"></a>vtable 順序のメソッド
 このインターフェイスには、[IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) インターフェイスから継承されたメソッドに加えて、次のメソッドが実装されています。

|メソッド|説明|
|------------|-----------------|
|[GetProcessID](../../../extensibility/debugger/reference/idebugaddress2-getprocessid.md)|このインターフェイスによって表されるオブジェクトを所有するプロセスの ID を取得します。|

## <a name="requirements"></a>必要条件
 ヘッダー: sh.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [シンボル プロバイダーのインターフェイス](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)
