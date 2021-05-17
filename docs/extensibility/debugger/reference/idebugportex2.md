---
description: このインターフェイスを使用すると、ポートで実行中のプログラムとプロセスをセッション デバッグ マネージャー (SDM) で制御できます。
title: IDebugPortEx2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortEx2
helpviewer_keywords:
- IDebugPortEx2 interface
ms.assetid: 144724d0-38ee-4c9b-87ca-8a504371182b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e26fec4b47a301bfb266f40b41fd88216ccf671f
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105072430"
---
# <a name="idebugportex2"></a>IDebugPortEx2
このインターフェイスを使用すると、ポートで実行中のプログラムとプロセスをセッション デバッグ マネージャー (SDM) で制御できます。

## <a name="syntax"></a>構文

```
IDebugPortEx2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 カスタム ポート サプライヤーでは、[IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md) を実装するのと同じオブジェクトにこのインターフェイスが実装されます。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 SDM では、`IDebugPort2` インターフェイスの [QueryInterface](/cpp/atl/queryinterface) を呼び出してこのインターフェイスを取得します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、`IDebugPortEx2` のメソッドを示します。

|メソッド|説明|
|------------|-----------------|
|[LaunchSuspended](../../../extensibility/debugger/reference/idebugportex2-launchsuspended.md)|実行可能ファイルを起動します。|
|[ResumeProcess](../../../extensibility/debugger/reference/idebugportex2-resumeprocess.md)|プロセスの実行を再開します。|
|[CanTerminateProcess](../../../extensibility/debugger/reference/idebugportex2-canterminateprocess.md)|プロセスを終了できるかどうかを判断します。|
|[TerminateProcess](../../../extensibility/debugger/reference/idebugportex2-terminateprocess.md)|プロセスを終了します。|
|[GetPortProcessId](../../../extensibility/debugger/reference/idebugportex2-getportprocessid.md)|ポート自体のプロセス ID を取得します。|
|[GetProgram](../../../extensibility/debugger/reference/idebugportex2-getprogram.md)|プログラム ノードに関連付けられているプログラムを取得します。|

## <a name="remarks"></a>解説
 このインターフェイスは、通常、SDM とカスタム ポート サプライヤーの間でプライベートです。

 必要に応じて、デバッグ エンジン (DE) では、[LaunchSuspended](../../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md) に渡された [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md) インターフェイスでこのインターフェイスを検索し、[LaunchSuspended](../../../extensibility/debugger/reference/idebugportex2-launchsuspended.md) を使用してプログラムを起動できます。 ただし、これは必須ではありません。また、DE では、要求プログラムを起動するために必要な操作を実行できます。

## <a name="requirements"></a>必要条件
 ヘッダー: portpriv.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)
