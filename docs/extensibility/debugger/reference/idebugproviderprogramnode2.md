---
description: このインターフェイスは、プロセスの境界を越えてプログラムに関連するインターフェイスをマーシャリングします。
title: IDebugProviderProgramNode2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProviderProgramNode2
helpviewer_keywords:
- IDebugProviderProgramNode2
ms.assetid: f0bca1cc-afbe-44cf-b5aa-d078aa685d24
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 3d09046d70d6bc766d17963ea4cdd6469c0981fb
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105083675"
---
# <a name="idebugproviderprogramnode2"></a>IDebugProviderProgramNode2
このインターフェイスは、プロセスの境界を越えてプログラムに関連するインターフェイスをマーシャリングします。

## <a name="syntax"></a>構文

```
IDebugProviderProgramNode2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 デバッグ エンジン (DE) では、プロセスの境界を越えたインターフェイスのマーシャリングをサポートするために、[IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md) を実装する同じオブジェクトにこのインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 `IDebugProgramNode2` インターフェイスを取得するには、このインターフェイスの [QueryInterface](/cpp/atl/queryinterface) を呼び出します。 このインターフェイスを取得できない場合、DE ではインターフェイスのマーシャリングをサポートしません。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 このインターフェイスには、次のメソッドが実装されています。

|メソッド|説明|
|------------|-----------------|
|[UnmarshalDebuggeeInterface](../../../extensibility/debugger/reference/idebugproviderprogramnode2-unmarshaldebuggeeinterface.md)|プロセス境界を越えて、指定されたインターフェイスを取得します。|

## <a name="remarks"></a>解説
 このインターフェイスは、デバッグ中のプログラムとは別のプロセス領域で DE が実行されるときに実装されます。たとえば、デバッグ中のプログラムのプロセス領域ではなく、Visual Studio のプロセス領域で DE が実行されている場合などです。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
