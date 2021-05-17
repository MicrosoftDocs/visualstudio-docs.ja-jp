---
description: このインターフェイスは、DLL などのモジュール (プログラムの実行可能単位) を表します。
title: IDebugModule2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugModule2
helpviewer_keywords:
- IDebugModule2 interface
ms.assetid: 24c2a126-f4ab-4891-8509-8ef99b994c08
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 848aa60ad7b8343d84489f460cfcb5fb6ec2d77d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105065555"
---
# <a name="idebugmodule2"></a>IDebugModule2
このインターフェイスは、DLL などのモジュール (プログラムの実行可能単位) を表します。

## <a name="syntax"></a>構文

```
IDebugModule2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 デバッグ エンジン (DE) では、モジュールを表したり、そのモジュールに関する情報へのアクセスを提供したりするために、このインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 [GetModule](../../../extensibility/debugger/reference/idebugmoduleloadevent2-getmodule.md) を呼び出すと、このインターフェイスが返されます。 DE では、[Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md) メソッドを使用して、[IDebugModuleLoadEvent2](../../../extensibility/debugger/reference/idebugmoduleloadevent2.md) インターフェイスをセッション デバッグ マネージャー (SDM) に送信します。

 このインターフェイスは、([EnumFrameInfo](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md) の呼び出しによって返される) [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md) 構造体でも返される可能性があります。

- [Next](../../../extensibility/debugger/reference/ienumdebugmodules2-next.md) もこのインターフェイスを返します ([EnumModules](../../../extensibility/debugger/reference/idebugprogram2-enummodules.md) は [IEnumDebugModules2](../../../extensibility/debugger/reference/ienumdebugmodules2.md) インターフェイスを返します)。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、`IDebugModule2` のメソッドを示します。

|メソッド|説明|
|------------|-----------------|
|[GetInfo](../../../extensibility/debugger/reference/idebugmodule2-getinfo.md)|このモジュールを記述する [MODULE_INFO](../../../extensibility/debugger/reference/module-info.md) を取得します。|
|[ReloadSymbols_Deprecated](../../../extensibility/debugger/reference/idebugmodule2-reloadsymbols-deprecated.md)|互換性のために残されています。 使用しないでください。 このモジュールのシンボルを再読み込みします。|

## <a name="remarks"></a>解説
 モジュール情報は、IDE の **[モジュール]** ウィンドウに表示できます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [MODULE_INFO](../../../extensibility/debugger/reference/module-info.md)
- [GetModule](../../../extensibility/debugger/reference/idebugmoduleloadevent2-getmodule.md)
- [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)
- [IEnumDebugModules2](../../../extensibility/debugger/reference/ienumdebugmodules2.md)
