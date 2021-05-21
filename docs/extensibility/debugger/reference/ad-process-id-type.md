---
description: AD_PROCESS_ID 構造体でプロセス ID を解釈する方法を指定します。
title: AD_PROCESS_ID_TYPE | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- AD_PROCESS_ID_TYPE
helpviewer_keywords:
- AD_PROCESS_ID_TYPE enumeration
ms.assetid: 0aab80e9-285a-4697-94ac-c864d42a6aaa
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9ae50fc827debd540faa99c33e10ddd217fc691f
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105094563"
---
# <a name="ad_process_id_type"></a>AD_PROCESS_ID_TYPE
[AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md) 構造体でプロセス ID を解釈する方法を指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_AD_PROCESS_ID {
    AD_PROCESS_ID_SYSTEM = 0,
    AD_PROCESS_ID_GUID   = 1
};
typedef DWORD AD_PROCESS_ID_TYPE;
```

```csharp
public enum enum_AD_PROCESS_ID {
    AD_PROCESS_ID_SYSTEM = 0,
    AD_PROCESS_ID_GUID   = 1
};
```

## <a name="fields"></a>フィールド
`AD_PROCESS_ID_SYSTEM`\
プロセス ID はシステム識別子です。 [AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md) 構造体の `ProcessId.dwProcessId` フィールドを使用します。

`AD_PROCESS_ID_GUID`\
プロセス ID は GUID です。 `AD_PROCESS_ID` 構造体の `ProcessId.guidProcessId` フィールドを使用します。

## <a name="remarks"></a>解説
[AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md) 構造体に含まれているプロセス ID の種類を識別するために、この構造体の `ProcessIdType` メンバーに対して使用されます。 構造体の `ProcessId` 共用体を解釈する方法を決定します。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: Microsoft.VisualStudio.Debugger.Interop

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md)
