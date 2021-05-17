---
description: 現在のスタック フレームで現在の例外をインターセプトするときに、デバッガーによって呼び出されます。
title: IDebugStackFrame3::InterceptCurrentException | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugStackFrame3::InterceptCurrentException
helpviewer_keywords:
- IDebugStackFrame3::InterceptCurrentException
ms.assetid: 116c7324-7645-4c15-b484-7a5cdd065ef5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 8aa2815eab2e78b373340ca1d4c60b4ae9929548
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105053244"
---
# <a name="idebugstackframe3interceptcurrentexception"></a>IDebugStackFrame3::InterceptCurrentException
現在のスタック フレームで現在の例外をインターセプトするときに、デバッガーによって呼び出されます。

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
[入力] さまざまなアクションを指定します。 現時点では、[INTERCEPT_EXCEPTION_ACTION](../../../extensibility/debugger/reference/intercept-exception-action.md) の値 `IEA_INTERCEPT` のみがサポートされているため、これを指定する必要があります。

`pqwCookie`\
[出力] 特定の例外を識別する一意の値。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、S_OK が返されます。それ以外の場合は、エラー コードが返されます。

 最も一般的なエラー通知は次のとおりです。

|エラー|説明|
|-----------|-----------------|
|`E_EXCEPTION_CANNOT_BE_INTERCEPTED`|現在の例外をインターセプトできません。|
|`E_EXCEPTION_CANNOT_UNWIND_ABOVE_CALLBACK`|現在の実行フレームでハンドラーがまだ検索されていません。|
|`E_INTERCEPT_CURRENT_EXCEPTION_NOT_SUPPORTED`|このフレームでは、このメソッドはサポートされていません。|

## <a name="remarks"></a>解説
 デバッガーでは、例外がスローされると、例外処理プロセス中の主要なポイントでランタイムから制御を取得します。 デバッガーでは、これらの主要な瞬間に、現在のスタック フレームで例外をインターセプトする必要があるかどうかを確認できます。 このように、インターセプトされた例外は、スタック フレームに例外ハンドラー (プログラム コードの try/catch ブロックなど) がない場合でも、実質的にスタック フレームの実行時の例外ハンドラーになります。

 デバッガーでは、例外をインターセプトする必要があるかどうかを確認したい場合に、現在のスタック フレーム オブジェクトでこのメソッドを呼び出します。 このメソッドでは、例外のすべての詳細を処理します。 [IDebugStackFrame3](../../../extensibility/debugger/reference/idebugstackframe3.md) インターフェイスが実装されていない場合、または `InterceptStackException` メソッドによってエラーが返された場合、デバッガーでは通常どおりに例外の処理を続行します。

> [!NOTE]
> 例外は、マネージド コード内で (つまり、デバッグ中のプログラムが .NET ランタイムで実行されている場合に) のみインターセプトできます。 もちろん、サードパーティ言語の実装者は独自のデバッグ エンジンに `InterceptStackException` を実装できます (そのような選択をした場合)。

 インターセプトが完了すると、[IDebugInterceptExceptionCompleteEvent2](../../../extensibility/debugger/reference/idebuginterceptexceptioncompleteevent2.md) が通知されます。

## <a name="see-also"></a>関連項目
- [IDebugStackFrame3](../../../extensibility/debugger/reference/idebugstackframe3.md)
- [INTERCEPT_EXCEPTION_ACTION](../../../extensibility/debugger/reference/intercept-exception-action.md)
- [IDebugInterceptExceptionCompleteEvent2](../../../extensibility/debugger/reference/idebuginterceptexceptioncompleteevent2.md)
