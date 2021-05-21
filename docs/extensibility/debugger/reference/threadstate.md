---
description: スレッドの状態を指定します。
title: THREADSTATE | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- THREADSTATE
helpviewer_keywords:
- THREADSTATE enumeration
ms.assetid: 62efdd7c-25b1-4fd3-9d06-ac1830a418a9
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 513e90e649d71a4fb7d5bc220eb9752925151d9f
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105070818"
---
# <a name="threadstate"></a>THREADSTATE
スレッドの状態を指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_THREADSTATE { 
   THREADSTATE_RUNNING = 0x0001,
   THREADSTATE_STOPPED = 0x0002,
   THREADSTATE_FRESH   = 0x0003,
   THREADSTATE_DEAD    = 0x0004,
   THREADSTATE_FROZEN  = 0x0005
};
typedef DWORD THREADSTATE;
```

```csharp
public enum enum_THREADSTATE { 
   THREADSTATE_RUNNING = 0x0001,
   THREADSTATE_STOPPED = 0x0002,
   THREADSTATE_FRESH   = 0x0003,
   THREADSTATE_DEAD    = 0x0004,
   THREADSTATE_FROZEN  = 0x0005
};
```

## <a name="fields"></a>フィールド
 `THREADSTATE_RUNNING`\
 スレッドが実行中であることを示します。

 `THREADSTATE_STOPPED`\
 ブレークポイントが原因でスレッドが停止していることを示します。

 `THREADSTATE_FRESH`\
 スレッドは作成されましたが、まだコードが実行されていないことを示します。

 `THREADSTATE_DEAD`\
 スレッドが動作していないことを示します。

 `THREADSTATE_FROZEN`\
 スレッドが凍結している (実行できない) ことを示します。

## <a name="remarks"></a>解説
 [THREADPROPERTIES](../../../extensibility/debugger/reference/threadproperties.md) 構造体の `dwThreadState` フィールドに使用されます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [THREADPROPERTIES](../../../extensibility/debugger/reference/threadproperties.md)
