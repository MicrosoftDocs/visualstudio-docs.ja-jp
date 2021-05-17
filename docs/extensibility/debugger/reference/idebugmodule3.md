---
description: このインターフェイスは、シンボルの別の場所と JustMyCode の状態をサポートするモジュールを表します。
title: IDebugModule3 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugModule3
helpviewer_keywords:
- IDebugModule3 interface
ms.assetid: 44f8e96e-9c59-4ffc-9a08-9c908a0e4de7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 0ccac9c260619b21079c6a277d842d322750cbc1
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105065490"
---
# <a name="idebugmodule3"></a>IDebugModule3
このインターフェイスは、シンボルの別の場所と JustMyCode の状態をサポートするモジュールを表します。

## <a name="syntax"></a>構文

```
IDebugModule3 : IDebugModule2
```

## <a name="notes-for-implementers"></a>実装側の注意
 デバッグ エンジン (DE) では、シンボルの別の場所をサポートしたり、JustMyCode の状態を操作したりするために、このインターフェイスを実装します ("JustMyCode" の定義については、「[Visual Studio デバッガーの用語集](../../../extensibility/debugger/reference/visual-studio-debugger-glossary.md)」を参照してください)。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 [GetSymbolSearchInfo](../../../extensibility/debugger/reference/idebugsymbolsearchevent2-getsymbolsearchinfo.md) を呼び出すと、このインターフェイスが返されます。 DE では、[Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md) メソッドを使用して、[IDebugSymbolSearchEvent2](../../../extensibility/debugger/reference/idebugsymbolsearchevent2.md) インターフェイスをセッション デバッグ マネージャー (SDM) に送信します。 また、[IDebugModule2](../../../extensibility/debugger/reference/idebugmodule2.md) インターフェイスで [QueryInterface](/cpp/atl/queryinterface) を呼び出すと、このインターフェイスが返されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 このインターフェイスには、[IDebugModule2](../../../extensibility/debugger/reference/idebugmodule2.md) インターフェイスのメソッドに加えて、次のメソッドが実装されています。

|メソッド|説明|
|------------|-----------------|
|[GetSymbolInfo](../../../extensibility/debugger/reference/idebugmodule3-getsymbolinfo.md)|シンボルを検索したパスの一覧と、各パスの検索結果を返します。|
|[LoadSymbols](../../../extensibility/debugger/reference/idebugmodule3-loadsymbols.md)|現在のモジュールのシンボルを読み込んで初期化します。|
|[IsUserCode](../../../extensibility/debugger/reference/idebugmodule3-isusercode.md)|モジュールがユーザーコードを表すかどうかを指定するフラグを返します。|
|[SetJustMyCodeState](../../../extensibility/debugger/reference/idebugmodule3-setjustmycodestate.md)|モジュールがユーザー コードと見なされるかどうかを指定します。|

## <a name="remarks"></a>解説
 Visual Studio は、このインターフェイスの一般的なコンシューマーです。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugModule2](../../../extensibility/debugger/reference/idebugmodule2.md)
- [IDebugSymbolSearchEvent2](../../../extensibility/debugger/reference/idebugsymbolsearchevent2.md)
- [GetSymbolSearchInfo](../../../extensibility/debugger/reference/idebugsymbolsearchevent2-getsymbolsearchinfo.md)
