---
title: IDebugThread2::Resume |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugThread2::Resume
helpviewer_keywords:
- IDebugThread2::Resume
ms.assetid: 36aad682-b0b9-40a2-b3fc-f0e61d41cdbc
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 5fc7b8f5cf5cd5360a60e8c6fbf3b6bf43415575
ms.sourcegitcommit: 6196d0b7fdcb08ba6d28a8151ad36b8d1139f2cc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2019
ms.locfileid: "65225989"
---
# <a name="idebugthread2resume"></a>IDebugThread2::Resume
スレッドの実行を再開します。

## <a name="syntax"></a>構文

```cpp
HRESULT Resume ( 
   DWORD *pdwSuspendCount
);
```

```csharp
int Resume ( 
   out uint pdwSuspendCount
);
```

## <a name="parameters"></a>パラメーター
 `pdwSuspendCount`\

 [out]再開操作の後に、中断カウントを返します。

## <a name="return-value"></a>戻り値
 成功した場合、返します`S_OK`、それ以外のエラー コードを返します。

## <a name="remarks"></a>Remarks
 このメソッドをデクリメントする中断カウントを呼び出して各実行が再開に実際には 0 に達すると、どの時点で、までです。 この中断の数が表示されます、**スレッド**デバッグ ウィンドウ。

 このメソッドを呼び出すたびに、必要があります、前回の呼び出し、 [Suspend](../../../extensibility/debugger/reference/idebugthread2-suspend.md)メソッド。 何回中断カウントの決定、`IDebugThread2::Suspend`メソッドがこれまでに呼び出されます。

## <a name="see-also"></a>関連項目
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [Suspend](../../../extensibility/debugger/reference/idebugthread2-suspend.md)