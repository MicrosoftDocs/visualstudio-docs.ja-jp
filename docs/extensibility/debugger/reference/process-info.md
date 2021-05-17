---
description: プロセスに関する情報を格納します。
title: PROCESS_INFO | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- PROCESS_INFO
helpviewer_keywords:
- PROCESS_INFO structure
ms.assetid: 260c33cc-a05e-4645-84b6-536d0b3b0537
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b6fe223d67b876dca1604b2617a33a888ec8180c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105079644"
---
# <a name="process_info"></a>PROCESS_INFO
プロセスに関する情報を格納します。

## <a name="syntax"></a>構文

```cpp
typedef struct tagPROCESS_INFO { 
   PROCESS_INFO_FIELDS Fields;
   BSTR                bstrFileName;
   BSTR                bstrBaseName;
   BSTR                bstrTitle;
   AD_PROCESS_ID       ProcessId;
   DWORD               dwSessionId;
   BSTR                bstrAttachedSessionName;
   FILETIME            CreationTime;
   PROCESS_INFO_FLAGS  Flags;
} PROCESS_INFO;
```

```csharp
public struct PROCESS_INFO { 
   public uint          Fields;
   public string        bstrFileName;
   public string        bstrBaseName;
   public string        bstrTitle;
   public AD_PROCESS_ID ProcessId;
   public uint          dwSessionId;
   public string        bstrAttachedSessionName;
   public FILETIME      CreationTime;
   public uint          Flags;
};
```

## <a name="members"></a>メンバー
 `Fields`\
 入力するフィールドを指定する [PROCESS_INFO_FIELDS](../../../extensibility/debugger/reference/process-info-fields.md) 列挙体からのフラグの組み合わせ。

 `bstrFileName`\
 プロセスの完全なパス名。 パラメーター `GN_FILENAME` を指定して [GetName](../../../extensibility/debugger/reference/idebugprocess2-getname.md) メソッドを呼び出すことに相当します。

 `bstrBaseName`\
 プロセスのファイル名および拡張子。 パラメーター `GN_BASENAME` を指定して `IDebugProcess2::Getname` メソッドを呼び出すことに相当します。

 `bstrTitle`\
 プロセスのタイトル (存在する場合)。 パラメーター `GN_TITLE` を指定して `IDebugProcess2::Getname` メソッドを呼び出すことに相当します。

 `ProcessId`\
 プロセスを識別する [AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md) 構造体。 [GetPhysicalProcessId](../../../extensibility/debugger/reference/idebugprocess2-getphysicalprocessid.md) メソッドを呼び出すことに相当します。

 `dwSessionId`\
 このプロセスが実行されているデバッグ セッションの識別子。

 `bstrAttachedSessionName`\
 アタッチされたセッションの名前。 [GetAttachedSessionName](../../../extensibility/debugger/reference/idebugprocess2-getattachedsessionname.md) メソッドを呼び出すことに相当します。

 `CreationTime`\
 プロセスが作成された時刻。

 `Flags`\
 プロセスのプロパティを指定する、[PROCESS_INFO_FLAGS](../../../extensibility/debugger/reference/process-info-flags.md) 列挙体からのフラグの組み合わせ。

## <a name="remarks"></a>解説
 この構造体は、入力する [GetInfo](../../../extensibility/debugger/reference/idebugprocess2-getinfo.md) メソッドに渡されます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [PROCESS_INFO_FIELDS](../../../extensibility/debugger/reference/process-info-fields.md)
- [PROCESS_INFO_FLAGS](../../../extensibility/debugger/reference/process-info-flags.md)
- [GetInfo](../../../extensibility/debugger/reference/idebugprocess2-getinfo.md)
- [GetName](../../../extensibility/debugger/reference/idebugprocess2-getname.md)
- [GetPhysicalProcessId](../../../extensibility/debugger/reference/idebugprocess2-getphysicalprocessid.md)
- [GetAttachedSessionName](../../../extensibility/debugger/reference/idebugprocess2-getattachedsessionname.md)
