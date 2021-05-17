---
description: 現在のコードの場所で停止するか、実行を続行するかを、デバッグ エンジン (DE) に通知します。
title: IDebugCanStopEvent2::CanStop | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCanStopEvent2::CanStop
helpviewer_keywords:
- IDebugCanStopEvent2::CanStop
ms.assetid: 7d61adbe-6b3d-41f3-86a1-45d9cc01a7f8
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: bc536b9a4f0bb0ce41e48c16cc85a53db11732b2
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105088602"
---
# <a name="idebugcanstopevent2canstop"></a>IDebugCanStopEvent2::CanStop
現在のコードの場所で停止するか、実行を続行するかを、デバッグ エンジン (DE) に通知します。

## <a name="syntax"></a>構文

```cpp
HRESULT CanStop ( 
   BOOL fCanStop
);
```

```csharp
int CanStop ( 
   int fCanStop
);
```

## <a name="parameters"></a>パラメーター
`fCanStop`\
[入力] DE を現在のコードの場所で停止する場合は 0 以外 (`TRUE`) の値。それ以外の場合は 0 (`FALSE`)。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 このイベントの受信者は、通常、[GetReason](../../../extensibility/debugger/reference/idebugcanstopevent2-getreason.md) メソッドを呼び出して DE が停止する理由を特定してから、適切な応答で `IDebugCanStopEvent2::CanStop` メソッドを呼び出します。

 DE が停止する場合は、停止の理由を説明するイベントが送信されます。 通常、送信されるイベントは 2 つあり、[IDebugBreakEvent2](../../../extensibility/debugger/reference/idebugbreakevent2.md) インターフェイスで表されるユーザーまたはシグナル中断と、[IDebugBreakpointEvent2](../../../extensibility/debugger/reference/idebugbreakpointevent2.md) インターフェイスで表されるブレークポイント イベントです。

## <a name="see-also"></a>関連項目
- [IDebugCanStopEvent2](../../../extensibility/debugger/reference/idebugcanstopevent2.md)
- [IDebugBreakEvent2](../../../extensibility/debugger/reference/idebugbreakevent2.md)
- [IDebugBreakpointEvent2](../../../extensibility/debugger/reference/idebugbreakpointevent2.md)
- [GetReason](../../../extensibility/debugger/reference/idebugcanstopevent2-getreason.md)
