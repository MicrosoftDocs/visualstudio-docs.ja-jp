---
description: プログラムを起動および終了するためにデバッグ エンジン (DE) で使用します。
title: IDebugEngineLaunch2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngineLaunch2
helpviewer_keywords:
- IDebugEngineLaunch2 interface
ms.assetid: 5eaf2ad8-3fbf-446e-b48b-5327ad3f5255
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: a8931590ea20373b5350d880d5fe9495dfe53c4f
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105077383"
---
# <a name="idebugenginelaunch2"></a>IDebugEngineLaunch2
プログラムを起動および終了するためにデバッグ エンジン (DE) で使用します。

## <a name="syntax"></a>構文

```
IDebugEngineLaunch2 : IDebugEngine2
```

## <a name="notes-for-implementers"></a>実装側の注意
 このインターフェイスは、カスタム ポートでは完全に処理できないプロセスを起動するための特別な要件がある場合に、カスタムの DE によって実装されます。 これは通常、DE がインタープリターの一部で、デバッグ中のプロセスがスクリプトである場合に発生します。最初にインタープリターを起動してから、スクリプトを読み込んで起動する必要があります。 ポートではインタープリターを起動できますが、スクリプトに特別な処理が必要になる場合があります (ここに DE の役割があります)。 このインターフェイスは、カスタム ポートでは処理できないプログラムを起動するための固有の要件がある場合にのみ実装されます。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 このインターフェイスは、セッション デバッグ マネージャー (SDM) で (QueryInterface を使用して) [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md) インターフェイスからこのインターフェイスを取得できる場合に、SDM によって呼び出されます。 このインターフェイスを取得できる場合、SDM では、DE に特別な要件があることを認識し、ポートに起動させるのではなく、このインターフェイスを呼び出してプログラムを起動します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、`IDebugEngineLaunch2` のメソッドを示します。

|メソッド|説明|
|------------|-----------------|
|[LaunchSuspended](../../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)|DE を使用してプロセスを起動します。|
|[ResumeProcess](../../../extensibility/debugger/reference/idebugenginelaunch2-resumeprocess.md)|プロセス実行を再開します。|
|[CanTerminateProcess](../../../extensibility/debugger/reference/idebugenginelaunch2-canterminateprocess.md)|プロセスを終了できるかどうかを判断します。|
|[TerminateProcess](../../../extensibility/debugger/reference/idebugenginelaunch2-terminateprocess.md)|プロセスを終了します。|

## <a name="requirements"></a>必要条件
 ヘッダー: Msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
