---
description: デバッグ エンジン (DE) が停止する理由を取得します。
title: IDebugCanStopEvent2::GetReason | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCanStopEvent2::GetReason
helpviewer_keywords:
- IDebugCanStopEvent2::GetReason
ms.assetid: f5de31ca-7b8d-4029-9cf9-ba860ac66af6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 2125bb90693d5a4c5cc23ac1225d56dea636de2e
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105085053"
---
# <a name="idebugcanstopevent2getreason"></a>IDebugCanStopEvent2::GetReason
デバッグ エンジン (DE) が停止する理由を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetReason( 
   CANSTOP_REASON* pcr
);
```

```csharp
int GetReason( 
   out enum_CANSTOP_REASON pcr
);
```

## <a name="parameters"></a>パラメーター
`pcr`\
[出力] このイベントの理由を説明する [CANSTOP_REASON](../../../extensibility/debugger/reference/canstop-reason.md) 列挙型の値を返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 このメソッドは、通常、呼び出し元がゼロ以外 (`TRUE`) を `IDebugCanStopEvent2::CanStop` メソッドに渡すかどうかを判断できるように、[CanStop](../../../extensibility/debugger/reference/idebugcanstopevent2-canstop.md) メソッドの前に呼び出されます。

 停止の理由は、DE がエントリ ポイントに到達したことを意味する `CANSTOP_ENTRYPOINT`、または DE が関数にステップインしたことを意味する `CANSTOP_STEPIN` です。

## <a name="see-also"></a>関連項目
- [IDebugCanStopEvent2](../../../extensibility/debugger/reference/idebugcanstopevent2.md)
- [CANSTOP_REASON](../../../extensibility/debugger/reference/canstop-reason.md)
- [CanStop](../../../extensibility/debugger/reference/idebugcanstopevent2-canstop.md)
