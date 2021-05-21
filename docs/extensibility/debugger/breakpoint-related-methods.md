---
title: ブレークポイントに関連するメソッド | Microsoft Docs
description: Visual Studio のデバッグでは、バインドされたブレークポイント (コード内の場所に正常にバインドされている) および保留中のブレークポイント (まだバインドされていない) がサポートされます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], breakpoint methods
- breakpoints, methods
ms.assetid: a6f77bf0-bf81-443f-8683-5f12075bbe10
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 06494b5ed6c1826e665f42e180ad8c71de596e30
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105055241"
---
# <a name="breakpoint-related-methods"></a>ブレークポイントに関連するメソッド
デバッグ エンジン (DE) は、ブレークポイントの設定をサポートしている必要があります。 Visual Studio のデバッグでは、次の種類のブレークポイントがサポートされます。

- Bound

     UI を通じて要求され、指定したコードの場所に正常にバインドされています。

- 保留中

     UI を通じて要求されましたが、実際の命令にまだバインドされていません。

## <a name="discussion"></a>ディスカッション
 たとえば、保留中のブレークポイントが発生するのは、命令がまだ読み込まれていないときです。 コードが読み込まれると、保留中のブレークポイントは、指定された場所のコードにバインドしようとします。つまり、コードに中断命令を挿入しようとします。 イベントが、バインディングが成功したことを示すため、またはバインド エラーが発生したことを通知するために、セッション デバッグ マネージャー (SDM) に送信されます。

 保留中のブレークポイントでも、対応するバインドされたブレークポイントの内部リストが管理されます。 1 つの保留中のブレークポイントによって、コード内に多数のブレークポイントが挿入されることがあります。 Visual Studio のデバッグ UI には、保留中のブレークポイントとそれに対応するバインドされたブレークポイントのツリー ビューが表示されます。

 保留中のブレークポイントを作成および使用するには、[IDebugEngine2::CreatePendingBreakpoint](../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md) メソッドと、[IDebugPendingBreakpoint2](../../extensibility/debugger/reference/idebugpendingbreakpoint2.md) インターフェイスの以下のメソッドの実装が必要です。

|Method|説明|
|------------|-----------------|
|[CanBind](../../extensibility/debugger/reference/idebugpendingbreakpoint2-canbind.md)|指定された保留中のブレークポイントをコードの場所にバインドできるかどうかを判定します。|
|[Bind](../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)|指定された保留中のブレークポイントを 1 つまたは複数のコードの場所にバインドします。|
|[GetState](../../extensibility/debugger/reference/idebugpendingbreakpoint2-getstate.md)|保留中のブレークポイントの状態を取得します。|
|[GetBreakpointRequest](../../extensibility/debugger/reference/idebugpendingbreakpoint2-getbreakpointrequest.md)|保留中のブレークポイントを作成するために使用されたブレークポイント要求を取得します。|
|[有効化](../../extensibility/debugger/reference/idebugpendingbreakpoint2-enable.md)|保留中のブレークポイントの有効化状態を切り替えます。|
|[EnumBoundBreakpoints](../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumboundbreakpoints.md)|保留中のブレークポイントからバインドされているすべてのブレークポイントを列挙します。|
|[EnumErrorBreakpoints](../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumerrorbreakpoints.md)|保留中のブレークポイントが原因で発生したすべてのエラー ブレークポイントを列挙します。|
|[削除](../../extensibility/debugger/reference/idebugpendingbreakpoint2-delete.md)|保留中のブレークポイントと、そこからバインドされているすべてのブレークポイントを削除します。|

 バインドされたブレークポイントとエラーのブレークポイントを列挙するには、[IEnumDebugBoundBreakpoints2](../../extensibility/debugger/reference/ienumdebugboundbreakpoints2.md) および [IEnumDebugErrorBreakpoints2](../../extensibility/debugger/reference/ienumdebugerrorbreakpoints2.md) のすべてのメソッドを実装する必要があります。

 コードの場所にバインドされる保留中のブレークポイントには、次の [IDebugBoundBreakpoint2](../../extensibility/debugger/reference/idebugboundbreakpoint2.md) メソッドの実装が必要です。

|Method|説明|
|------------|-----------------|
|[GetPendingBreakpoint](../../extensibility/debugger/reference/idebugboundbreakpoint2-getpendingbreakpoint.md)|ブレークポイントを含む保留中のブレークポイントを取得します。|
|[GetState](../../extensibility/debugger/reference/idebugboundbreakpoint2-getstate.md)|バインドされたブレークポイントの状態を取得します。|
|[GetBreakpointResolution](../../extensibility/debugger/reference/idebugboundbreakpoint2-getbreakpointresolution.md)|ブレークポイントを記述するブレークポイントの解決を取得します。|
|[有効化](../../extensibility/debugger/reference/idebugboundbreakpoint2-enable.md)|ブレークポイントを有効または無効にします。|
|[削除](../../extensibility/debugger/reference/idebugboundbreakpoint2-delete.md)|バインドされたブレークポイントを削除します。|

 解決および要求情報には、次の [IDebugBreakpointResolution2](../../extensibility/debugger/reference/idebugbreakpointresolution2.md) メソッドの実装が必要です。

|Method|説明|
|------------|-----------------|
|[GetBreakpointType](../../extensibility/debugger/reference/idebugbreakpointresolution2-getbreakpointtype.md)|解決によって表されるブレークポイントの種類を取得します。|
|[GetResolutionInfo](../../extensibility/debugger/reference/idebugbreakpointresolution2-getresolutioninfo.md)|ブレークポイントを記述するブレークポイントの解決情報を取得します。|

 バインド中に発生する可能性のあるエラーの解決には、次の [IDebugErrorBreakpoint2](../../extensibility/debugger/reference/idebugerrorbreakpoint2.md) メソッドの実装が必要です。

|Method|説明|
|------------|-----------------|
|[GetPendingBreakpoint](../../extensibility/debugger/reference/idebugerrorbreakpoint2-getpendingbreakpoint.md)|エラーのブレークポイントを含む保留中のブレークポイントを取得します。|
|[GetBreakpointResolution](../../extensibility/debugger/reference/idebugerrorbreakpoint2-getbreakpointresolution.md)|エラーのブレークポイントについて記述しているブレークポイント エラー解決方法を取得します。|

 バインド中に発生する可能性のあるエラーを解決するには、次の [IDebugErrorBreakpointResolution2](../../extensibility/debugger/reference/idebugerrorbreakpointresolution2.md) メソッドも必要です。

|Method|説明|
|------------|-----------------|
|[GetBreakpointType](../../extensibility/debugger/reference/idebugerrorbreakpointresolution2-getbreakpointtype.md)|ブレークポイントの種類を取得します。|
|[GetResolutionInfo](../../extensibility/debugger/reference/idebugerrorbreakpointresolution2-getresolutioninfo.md)|ブレークポイントの解決情報を取得します。|

 ブレークポイントのソース コードを表示するには、[IDebugStackFrame2:: GetDocumentContext](../../extensibility/debugger/reference/idebugstackframe2-getdocumentcontext.md) のメソッドまたは [IDebugStackFrame2:: GetCodeContext](../../extensibility/debugger/reference/idebugstackframe2-getcodecontext.md) のメソッド (あるいは両方) を実装する必要があります。

## <a name="see-also"></a>こちらもご覧ください
- [実行の制御と状態の評価](../../extensibility/debugger/execution-control-and-state-evaluation.md)
