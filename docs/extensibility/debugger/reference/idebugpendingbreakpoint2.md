---
description: このインターフェイスは、コードの場所にバインドする準備ができているブレークポイントを表します。
title: IDebugPendingBreakpoint2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPendingBreakpoint2
helpviewer_keywords:
- IDebugPendingBreakpoint2 interface
ms.assetid: d416b095-917e-475e-b796-ec0a03ffb8da
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: a52856cfa70491b7a7daa9079c111b1430475d22
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105053712"
---
# <a name="idebugpendingbreakpoint2"></a>IDebugPendingBreakpoint2
このインターフェイスは、コードの場所にバインドする準備ができているブレークポイントを表します。

## <a name="syntax"></a>構文

```
IDebugPendingBreakpoint2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 デバッグ エンジン (DE) では、ブレークポイントのサポートの一環としてこのインターフェイスが実装されます。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 [CreatePendingBreakpoint](../../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md) を呼び出すと、[IDebugBreakpointRequest2](../../../extensibility/debugger/reference/idebugbreakpointrequest2.md) インターフェイスから保留中のブレークポイントが作成されます。 [Bind](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md) を呼び出すと、プログラム内のバインドされたブレークポイントを表す `IDebugBreakpoint2` インターフェイスが作成されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、`IDebugPendingBreakpoint2` のメソッドを示します。

|メソッド|説明|
|------------|-----------------|
|[CanBind](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-canbind.md)|この保留中のブレークポイントをコードの場所にバインドできるかどうかを判断します。|
|[Bind](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)|この保留中のブレークポイントを 1 つまたは複数のコードの場所にバインドします。|
|[GetState](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-getstate.md)|この保留中のブレークポイントの状態を取得します。|
|[GetBreakpointRequest](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-getbreakpointrequest.md)|この保留中のブレークポイントを作成するために使用されたブレークポイント要求を取得します。|
|[Virtualize](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-virtualize.md)|この保留中のブレークポイントの仮想化状態を切り替えます。|
|[有効化](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enable.md)|この保留中のブレークポイントの有効化状態を切り替えます。|
|[SetCondition](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-setcondition.md)|この保留中のブレークポイントに関連付けられる条件を設定または変更します。|
|[SetPassCount](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-setpasscount.md)|この保留中のブレークポイントに関連付けられるパス カウントを設定または変更します。|
|[EnumBoundBreakpoints](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumboundbreakpoints.md)|この保留中のブレークポイントからバインドされているすべてのブレークポイントを列挙します。|
|[EnumErrorBreakpoints](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumerrorbreakpoints.md)|この保留中のブレークポイントが原因で発生したすべてのエラー ブレークポイントを列挙します。|
|[削除](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-delete.md)|この保留中のブレークポイントと、そこからバインドされているすべてのブレークポイントを削除します。|

## <a name="remarks"></a>解説
 `IDebugPendingBreakpoint2` は、1 つまたは複数のプログラムに適用できるコードにブレークポイントをバインドするために必要なすべての情報のプロバイダーと考えることができます。

 保留中のブレークポイントによって、複数のバインドされたブレークポイントが生成される可能性があります。 たとえば、C++ スタイルのテンプレート内のブレークポイントによって、そのテンプレートの一意のインスタンスごとにバインドされたブレークポイントが生成される場合があります。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [CreatePendingBreakpoint](../../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md)
- [GetPendingBreakpoint](../../../extensibility/debugger/reference/idebugbreakpointboundevent2-getpendingbreakpoint.md)
- [GetPendingBreakpoint](../../../extensibility/debugger/reference/idebugboundbreakpoint2-getpendingbreakpoint.md)
- [GetPendingBreakpoint](../../../extensibility/debugger/reference/idebugerrorbreakpoint2-getpendingbreakpoint.md)
