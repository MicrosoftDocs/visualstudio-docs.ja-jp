---
description: このインターフェイスは、メモリのバイト数を表します。
title: IDebugMemoryBytes2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMemoryBytes2
helpviewer_keywords:
- IDebugMemoryBytes2 interface
ms.assetid: d7647575-0e06-4190-88f5-ca40b82209a4
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: b18b4575780966d9ad34fa6c5638a89274d52c3c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105058639"
---
# <a name="idebugmemorybytes2"></a>IDebugMemoryBytes2
このインターフェイスは、メモリのバイト数を表します。

## <a name="syntax"></a>構文

```
IDebugMemoryBytes2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 デバッグ エンジン (DE) では、メモリのバイトを表すために、このインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
- [GetMemoryBytes](../../../extensibility/debugger/reference/idebugprogram2-getmemorybytes.md) から、システム メモリへのアクセスを提供するために、このインターフェイスが返されます。 [GetMemoryBytes](../../../extensibility/debugger/reference/idebugproperty2-getmemorybytes.md) と [GetMemoryBytes](../../../extensibility/debugger/reference/idebugreference2-getmemorybytes.md) から、オブジェクトのバイトへのアクセスを提供するために、このインターフェイスが返されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、`IDebugMemoryBytes2` のメソッドを示します。

|メソッド|説明|
|------------|-----------------|
|[ReadAt](../../../extensibility/debugger/reference/idebugmemorybytes2-readat.md)|指定された位置から始まるバイト シーケンスを読み取ります。|
|[WriteAt](../../../extensibility/debugger/reference/idebugmemorybytes2-writeat.md)|`pStartContext` で始まる `dwCount` バイトを書き込みます。|
|[GetSize](../../../extensibility/debugger/reference/idebugmemorybytes2-getsize.md)|このインターフェイスで表されるメモリのバイト単位のサイズを取得します。|

## <a name="remarks"></a>解説
 プロパティの場合、配列を表す [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) インターフェイスから、その配列内の値にアクセスするための `IDebugMemoryBytes2` インターフェイスが提供されます。

 Visual Studio の **メモリ ビュー** により、[GetMemoryBytes](../../../extensibility/debugger/reference/idebugprogram2-getmemorybytes.md) が呼び出されて、システム メモリにアクセスするための `IDebugMemoryBytes2` インターフェイスが取得されます。 アクセスするアドレスは、アドレスとしてメモリ ビューに入力された式を解析して取得され、[EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) を使用して解析された式を評価して `IDebugProperty2` インターフェイスが取得されます。 [GetMemoryContext](../../../extensibility/debugger/reference/idebugproperty2-getmemorycontext.md) への呼び出しにより、メモリ アドレスを説明する [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md) が返されます。 このメモリ コンテキストは、次に [ReadAt](../../../extensibility/debugger/reference/idebugmemorybytes2-readat.md) および [WriteAt](../../../extensibility/debugger/reference/idebugmemorybytes2-writeat.md) に渡されます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [GetMemoryBytes](../../../extensibility/debugger/reference/idebugprogram2-getmemorybytes.md)
- [GetMemoryBytes](../../../extensibility/debugger/reference/idebugproperty2-getmemorybytes.md)
- [GetMemoryBytes](../../../extensibility/debugger/reference/idebugreference2-getmemorybytes.md)
- [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)
