---
description: このインターフェイスは、プログラムノードがこのプログラムをデバッグできるすべてのデバッグエンジン (DE) を指定するために使用されます。
title: IDebugProgramEngines2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramEngines2
helpviewer_keywords:
- IDebugProgramEngines2 interface
ms.assetid: 53d648f0-6c11-4337-badd-c43f3872b62c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e0202185d760a1e3334996906807e5922fe61e0a
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105084221"
---
# <a name="idebugprogramengines2"></a>IDebugProgramEngines2
このインターフェイスは、プログラムノードがこのプログラムをデバッグできるすべてのデバッグエンジン (DE) を指定するために使用されます。

## <a name="syntax"></a>Syntax

```
IDebugProgramEngines2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 DE またはカスタムポートサプライヤーは、特定のプログラムに使用する特定の DE の確立をサポートするために、 [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md) を実装する同じオブジェクトにこのインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 インターフェイスの [QueryInterface](/cpp/atl/queryinterface) を呼び出して、 `IDebugProgramNode2` このインターフェイスを取得します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、のメソッドを示し `IDebugProgramEngines2` ます。

|メソッド|説明|
|------------|-----------------|
|[EnumPossibleEngines](../../../extensibility/debugger/reference/idebugprogramengines2-enumpossibleengines.md)|このプログラムをデバッグできるすべての DEs を示します。|
|[SetEngine](../../../extensibility/debugger/reference/idebugprogramengines2-setengine.md)|このプログラムのデバッグに使用する DE を選択します。|

## <a name="remarks"></a>注釈
 ユーザーが DE を選択すると、 [Setengine](../../../extensibility/debugger/reference/idebugprogramengines2-setengine.md)を呼び出すことによってその選択がプログラムノードに登録されます。 選択したエンジンが、 [GetEngineInfo](../../../extensibility/debugger/reference/idebugprogramnode2-getengineinfo.md)によって返されるエンジンになります。

## <a name="requirements"></a>要件
 ヘッダー: msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>こちらもご覧ください
- [コアインターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
- [GetEngineInfo](../../../extensibility/debugger/reference/idebugprogramnode2-getengineinfo.md)
