---
title: IDebugAddress |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugAddress
helpviewer_keywords:
- IDebugAddress interface
ms.assetid: bc709ff7-4966-4f36-9af2-690efe2cea1d
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7b9aba2be92516bab86f39eee55a3df4586eb09c
ms.sourcegitcommit: b0d8e61745f67bd1f7ecf7fe080a0fe73ac6a181
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/22/2019
ms.locfileid: "56677966"
---
# <a name="idebugaddress"></a>IDebugAddress
このインターフェイスは、項目のアドレスを表します。 これは、シンボル ハンドラーによって返されます。

## <a name="syntax"></a>構文

```
IDebugAddress : IUnknown
```

## <a name="notes-for-implementers"></a>実装についてのメモ
 シンボル プロバイダーは、オブジェクトのアドレスを表すためには、このインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元のノート
 多くのインターフェイスの多くのメソッドは、このインターフェイスを返します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 このインターフェイスは、次のメソッドを実装します。

|メソッド|説明|
|------------|-----------------|
|[GetAddress](../../../extensibility/debugger/reference/idebugaddress-getaddress.md)|取得、 [DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md)オブジェクトとその場所を記述する構造体。|

## <a name="remarks"></a>Remarks
 シンボル プロバイダーは、オブジェクトと (たとえば、関数、メソッド、またはクラス) の特定のスコープ内での位置を表すには、このインターフェイスを返します。 このインターフェイスがから返され、シンボル プロバイダーと式のさまざまなメソッドに渡されるエバリュエーター。 通常、シンボル プロバイダーは、このインターフェイスの内容を解釈する必要がある唯一のエンティティです。

## <a name="requirements"></a>必要条件
 ヘッダー: sh.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ:Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [シンボルプロバイダーのインターフェイス](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md)