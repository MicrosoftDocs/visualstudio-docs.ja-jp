---
description: 指定されたプログラムが変則的に終了したこと、および DE がプログラムへのすべての参照をクリーンアップしてプログラムの破棄イベントを送信する必要があることを、デバッグ エンジン (DE) に通知します。
title: IDebugEngine2::DestroyProgram | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine2::DestroyProgram
helpviewer_keywords:
- IDebugEngine2::DestroyProgram
ms.assetid: 0c9e2698-c70f-4770-a7bb-39650e9c3a1f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c0a58dd5893c3235ded9c7eeb5f5d47e3ddcb380
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105093848"
---
# <a name="idebugengine2destroyprogram"></a>IDebugEngine2::DestroyProgram
指定されたプログラムが変則的に終了したこと、および DE がプログラムへのすべての参照をクリーンアップしてプログラムの破棄イベントを送信する必要があることを、デバッグ エンジン (DE) に通知します。

## <a name="syntax"></a>構文

```cpp
HRESULT DestroyProgram( 
   IDebugProgram2* pProgram
);
```

```cpp
int DestroyProgram( 
   IDebugProgram2 pProgram
);
```

## <a name="parameters"></a>パラメーター
`pProgram`\
[入力] 変則的に終了されたプログラムを表す [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) オブジェクト。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 このメソッドが呼び出された後、DE は、[IDebugProgramDestroyEvent2](../../../extensibility/debugger/reference/idebugprogramdestroyevent2.md) イベントをセッション デバッグ マネージャー (SDM) に返します。

 DE がデバッグ中のプログラムと同じプロセスで実行される場合、このメソッドは実装されません (`E_NOTIMPL` を返します)。 このメソッドは、DE が SDM と同じプロセスで実行される場合にのみ実装されます。

## <a name="see-also"></a>関連項目
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
- [IDebugProgramDestroyEvent2](../../../extensibility/debugger/reference/idebugprogramdestroyevent2.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
