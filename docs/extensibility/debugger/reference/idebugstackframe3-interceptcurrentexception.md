---
title: IDebugStackFrame3::InterceptCurrentException |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugStackFrame3::InterceptCurrentException
helpviewer_keywords:
- IDebugStackFrame3::InterceptCurrentException
ms.assetid: 116c7324-7645-4c15-b484-7a5cdd065ef5
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 4341542c48465af026280d5b7b13a8e10bafe40a
ms.sourcegitcommit: 19ec963ed6d585719cb83ba677434ea6580e0d1f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66203259"
---
# <a name="idebugstackframe3interceptcurrentexception"></a>IDebugStackFrame3::InterceptCurrentException
現在の例外をインターセプトする必要がある場合に、現在のスタック フレーム上のデバッガーによって呼び出されます。

## <a name="syntax"></a>構文

```cpp
HRESULT InterceptCurrentException(
   INTERCEPT_EXCEPTION_ACTION dwFlags,
   UINT64*                    pqwCookie
);
```

```csharp
int InterceptCurrentException(
   uint dwFlags,
   out  ulong pqwCookie
);
```

## <a name="parameters"></a>パラメーター
`dwFlags`\
[in]さまざまなアクションを指定します。 現時点では、のみ、 [INTERCEPT_EXCEPTION_ACTION](../../../extensibility/debugger/reference/intercept-exception-action.md)値`IEA_INTERCEPT`はサポートされており、指定する必要があります。

`pqwCookie`\
[out]特定の例外を識別する一意の値。

## <a name="return-value"></a>戻り値
 成功した場合、S_OK を返します。それ以外の場合、エラー コードを返します。

 最も一般的なエラーを返します。 次に示します。

|Error|説明|
|-----------|-----------------|
|`E_EXCEPTION_CANNOT_BE_INTERCEPTED`|現在の例外を受け取ることができません。|
|`E_EXCEPTION_CANNOT_UNWIND_ABOVE_CALLBACK`|実行の現在のフレームはまだまだハンドラーの検索されました。|
|`E_INTERCEPT_CURRENT_EXCEPTION_NOT_SUPPORTED`|このメソッドはこのフレームのサポートされていません。|

## <a name="remarks"></a>Remarks
 例外がスローされたときに、デバッガーは例外プロセスを処理中に重要なポイントで実行時からコントロールを取得します。 これらのキーの時間中に、デバッガーは、特定、フレームが例外をインターセプトするか、現在のスタック フレームを依頼できます。 この方法では、傍受した例外は、スタック フレームは、例外ハンドラー (たとえば、プログラム コードでの try/catch ブロックなど) を持っていない場合でもその場で例外ハンドラーのスタック フレームの本質的です。

 デバッガーが例外を受け取るかどうかを把握したい場合は、現在のスタック フレーム オブジェクトにこのメソッドを呼び出します。 このメソッドは、例外のすべての詳細を処理するためです。 場合、 [IDebugStackFrame3](../../../extensibility/debugger/reference/idebugstackframe3.md)インターフェイスが実装されていません、または`InterceptStackException`メソッドには、すべてのエラーが返されますし、デバッガーは、通常、例外の処理を続行します。

> [!NOTE]
> 例外をインターセプトできます、マネージ コードでのみ、デバッグ中のプログラムが .NET ランタイムで実行されている場合。 もちろん、サード パーティの言語実装者を実装できる`InterceptStackException`希望する場合は、独自のデバッグ エンジンでします。

 インターセプションが完了した後、 [IDebugInterceptExceptionCompleteEvent2](../../../extensibility/debugger/reference/idebuginterceptexceptioncompleteevent2.md)がシグナルを受け取る。

## <a name="see-also"></a>関連項目
- [IDebugStackFrame3](../../../extensibility/debugger/reference/idebugstackframe3.md)
- [INTERCEPT_EXCEPTION_ACTION](../../../extensibility/debugger/reference/intercept-exception-action.md)
- [IDebugInterceptExceptionCompleteEvent2](../../../extensibility/debugger/reference/idebuginterceptexceptioncompleteevent2.md)