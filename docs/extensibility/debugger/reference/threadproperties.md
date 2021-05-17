---
description: スレッドのプロパティについて説明します。
title: THREADPROPERTIES | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- THREADPROPERTIES
helpviewer_keywords:
- THREADPROPERTIES structure
ms.assetid: 7d397207-db03-4ec0-9f79-3794056ed89f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 0707cb5da4c63ffd686f22fa691c103c954478c8
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105070857"
---
# <a name="threadproperties"></a>THREADPROPERTIES
スレッドのプロパティについて説明します。

## <a name="syntax"></a>構文

```cpp
typedef struct _tagTHREADPROPERTIES { 
   THREADPROPERTY_FIELDS dwFields;
   DWORD                 dwThreadId;
   DWORD                 dwSuspendCount;
   DWORD                 dwThreadState;
   BSTR                  bstrPriority;
   BSTR                  bstrName;
   BSTR                  bstrLocation;
} THREADPROPERTIES;
```

```csharp
public struct THREADPROPERTIES { 
   public uint   dwFields;
   public uint   dwThreadId;
   public uint   dwSuspendCount;
   public uint   dwThreadState;
   public string bstrPriority;
   public string bstrName;
   public string bstrLocation;
};
```

## <a name="members"></a>メンバー
 `dwFields`\
 この構造体のどのフィールドが有効であるかを示す、 [THREADPROPERTY_FIELDS](../../../extensibility/debugger/reference/threadproperty-fields.md) 列挙型のフラグの組み合わせ。

 `dwThreadId`\
 スレッド ID。

 `dwSuspendCount`\
 スレッド中断の数。

 `dwThreadState`\
 稼働中のスレッドの状態を示す [THREADSTATE](../../../extensibility/debugger/reference/threadstate.md) 列挙型の値。

 `bstrPriority`\
 スレッドの優先順位を指定する文字列。"Above Normal"、"Normal"、"Time Critical" などです。

 `bstName`\
 スレッド名。

 `bstrLocation`\
 スレッドの場所 (通常は最上位のスタック フレーム)。通常は、実行が現在、中断されているメソッドの名前として表されます。

## <a name="remarks"></a>解説
 この構造体は、[GetThreadProperties](../../../extensibility/debugger/reference/idebugthread2-getthreadproperties.md) メソッドへの呼び出しによって格納されます。 返される情報は、通常、 **[スレッド]** ウィンドウの設定に使用されます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [GetThreadProperties](../../../extensibility/debugger/reference/idebugthread2-getthreadproperties.md)
- [THREADPROPERTY_FIELDS](../../../extensibility/debugger/reference/threadproperty-fields.md)
- [THREADSTATE](../../../extensibility/debugger/reference/threadstate.md)
