---
description: このインターフェイスは、項目のアドレスを表します。
title: IDebugAddress | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugAddress
helpviewer_keywords:
- IDebugAddress interface
ms.assetid: bc709ff7-4966-4f36-9af2-690efe2cea1d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 89e192f61e4cda809e8e6c90106cbe081392a044
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105094420"
---
# <a name="idebugaddress"></a>IDebugAddress
このインターフェイスは、項目のアドレスを表します。 これはシンボル ハンドラーによって返されます。

## <a name="syntax"></a>構文

```
IDebugAddress : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 シンボル プロバイダーは、オブジェクトのアドレスを表すためにこのインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 多くのインターフェイスでは、多くのメソッドからこのインターフェイスを返します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 このインターフェイスには、次のメソッドが実装されています。

|メソッド|説明|
|------------|-----------------|
|[GetAddress](../../../extensibility/debugger/reference/idebugaddress-getaddress.md)|オブジェクトとその位置を記述する [DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md) 構造体を取得します。|

## <a name="remarks"></a>解説
 シンボル プロバイダーは、特定のスコープ (関数、メソッド、クラスなど) 内のオブジェクトとその位置を表すために、このインターフェイスを返します。 このインターフェイスは、シンボル プロバイダーと式エバリュエーターのさまざまなメソッドから返されたり渡されたりします。 通常、シンボル プロバイダーは、このインターフェイスの内容を解釈する必要がある唯一のエンティティです。

## <a name="requirements"></a>必要条件
 ヘッダー: sh.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [シンボル プロバイダーのインターフェイス](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md)
