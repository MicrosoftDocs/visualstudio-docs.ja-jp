---
title: IDebugProviderProgramNode2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProviderProgramNode2
helpviewer_keywords:
- IDebugProviderProgramNode2
ms.assetid: f0bca1cc-afbe-44cf-b5aa-d078aa685d24
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 33c4a4914e15a8ecbea0d4f28c2325a952a042de
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66353803"
---
# <a name="idebugproviderprogramnode2"></a>IDebugProviderProgramNode2
このインターフェイスでは、プロセス境界をまたいでプログラム関連のインターフェイスをマーシャ リングします。

## <a name="syntax"></a>構文

```
IDebugProviderProgramNode2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装についてのメモ
 デバッグ エンジン (DE) を実装する同一のオブジェクトにこのインターフェイスを実装する[IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)プロセスの境界を越えてマーシャ リングのインターフェイスをサポートするためにします。

## <a name="notes-for-callers"></a>呼び出し元のノート
 呼び出す[QueryInterface](/cpp/atl/queryinterface)上、`IDebugProgramNode2`をこのインターフェイスを取得するインターフェイス。 このインターフェイスを取得できない場合、DE にはインターフェイスのマーシャ リングはサポートされません。

## <a name="methods-in-vtable-order"></a>Vtable 順序メソッド
 このインターフェイスは、次のメソッドを実装します。

|メソッド|説明|
|------------|-----------------|
|[UnmarshalDebuggeeInterface](../../../extensibility/debugger/reference/idebugproviderprogramnode2-unmarshaldebuggeeinterface.md)|プロセスの境界を越えて、指定したインターフェイスを取得します。|

## <a name="remarks"></a>Remarks
 デバッグ中のプログラムから別のプロセス領域で、DE を実行すると、このインターフェイスは実装: デバッグ中のプログラムのプロセス空間ではなく、Visual Studio のプロセス領域で、DE が実行されている場合などです。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ:Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)