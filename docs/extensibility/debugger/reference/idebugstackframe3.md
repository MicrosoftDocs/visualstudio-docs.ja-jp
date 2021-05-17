---
description: このインターフェイスによって IDebugStackFrame2 が拡張され、インターセプトされた例外が処理されます。
title: IDebugStackFrame3 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugStackFrame3
helpviewer_keywords:
- IDebugStackFrame3 interface
ms.assetid: 39af2f57-0a01-42b8-b093-b7fbc61e2909
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 4049b728842e630a0f0b300130362b8efa8ceec0
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105053205"
---
# <a name="idebugstackframe3"></a>IDebugStackFrame3
このインターフェイスによって [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md) が拡張され、インターセプトされた例外が処理されます。

## <a name="syntax"></a>構文

```
IDebugStackFrame3 : IDebugStackFrame2
```

## <a name="notes-for-implementers"></a>実装側の注意
 デバッグ エンジン (DE) では、インターセプトされた例外をサポートするために、[IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md) インターフェイスを実装する同じオブジェクトにこのインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 `IDebugStackFrame2` インターフェイスを取得するには、このインターフェイスの [QueryInterface](/cpp/atl/queryinterface) を呼び出します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 `IDebugStackFrame3` では、[IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md) から継承されたメソッドに加えて以下のメソッドが公開されます。

|メソッド|説明|
|------------|-----------------|
|[InterceptCurrentException](../../../extensibility/debugger/reference/idebugstackframe3-interceptcurrentexception.md)|通常の例外処理の前に、現在のスタック フレームの例外を処理します。|
|[GetUnwindCodeContext](../../../extensibility/debugger/reference/idebugstackframe3-getunwindcodecontext.md)|スタック アンワインドが発生した場合に、コード コンテキストを返します。|

## <a name="remarks"></a>解説
 インターセプトされた例外は、通常の例外処理ルーチンがランタイムによって呼び出される前にデバッガーで例外を処理できることを意味します。 例外をインターセプトすると、実質的に、例外ハンドラーが存在しなくても存在するものとしてランタイムが動作します。

- [InterceptCurrentException](../../../extensibility/debugger/reference/idebugstackframe3-interceptcurrentexception.md) は、通常のすべての例外コールバック イベントの発生時に呼び出されます (唯一の例外は、混合モード コード (マネージドおよびアンマネージド コード) をデバッグする場合です。この場合、最後のコールバック時に例外をインターセプトできません)。 DE に `IDebugStackFrame3` が実装されていない場合、または DE で IDebugStackFrame3::`InterceptCurrentException` のエラー (`E_NOTIMPL` など) が返された場合、デバッガーでは通常どおりに例外を処理します。

 デバッガーで例外をインターセプトすると、ユーザーがデバッグ中のプログラムの状態を変更してから、例外がスローされた時点から実行を再開できるようになります。

> [!NOTE]
> インターセプトされた例外は、マネージド コード (つまり、共通言語ランタイム (CLR) で実行されているプログラム) でのみ使用できます。

 デバッグ エンジンでは、実行時に `SetMetric` 関数を使用して "metricExceptions" の値を 1 に設定することで、例外のインターセプトをサポートしていることを示します。 詳細については、「[デバッグ用の SDK ヘルパー](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)」を参照してください。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)
- [デバッグ用 SDK ヘルパー](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)
