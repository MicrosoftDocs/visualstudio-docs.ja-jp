---
description: コードの場所にバインドする準備ができているブレークポイントの状態に関する情報を格納します。
title: PENDING_BP_STATE_INFO | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- PENDING_BP_STATE_INFO
helpviewer_keywords:
- PENDING_BP_STATE_INFO structure
ms.assetid: 4d73ceff-43f9-4e95-8dba-88e1fab2def3
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a4da8892239740c65e1fcbbe618fa1ea76183e96
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105079684"
---
# <a name="pending_bp_state_info"></a>PENDING_BP_STATE_INFO
コードの場所にバインドする準備ができているブレークポイントの状態に関する情報を格納します。

## <a name="syntax"></a>構文

```cpp
typedef struct _tagPENDING_BP_STATE_INFO { 
   PENDING_BP_STATE       state;
   PENDING_BP_STATE_FLAGS flags;
} PENDING_BP_STATE_INFO;
```

```csharp
public struct PENDING_BP_STATE_INFO { 
   public uint state;
   public uint flags;
};
```

## <a name="members"></a>メンバー
 `state`\
 保留中のブレークポイントの状態を指定する [PENDING_BP_STATE](../../../extensibility/debugger/reference/pending-bp-state.md) 列挙体の値。

 `flags`\
 ブレークポイントが仮想化されているかどうかを指定する、[PENDING_BP_STATE_FLAGS](../../../extensibility/debugger/reference/pending-bp-state-flags.md) 列挙体のフラグの組み合わせ。

## <a name="remarks"></a>解説
 この構造体は、それが入力される [GetState](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-getstate.md) メソッドに渡されます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [GetState](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-getstate.md)
- [PENDING_BP_STATE](../../../extensibility/debugger/reference/pending-bp-state.md)
- [PENDING_BP_STATE_FLAGS](../../../extensibility/debugger/reference/pending-bp-state-flags.md)
