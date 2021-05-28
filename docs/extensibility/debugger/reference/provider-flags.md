---
description: プログラム プロバイダーから取得する必要のあるプロパティを指定します。
title: PROVIDER_FLAGS | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- PROVIDER_FLAGS
helpviewer_keywords:
- PROVIDER_FLAGS enumeration
ms.assetid: 8cbd2312-ed2f-4477-b192-c3f25c6098c3
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ed6a93b9e2b90fc125642697b193d51713b01e69
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105086353"
---
# <a name="provider_flags"></a>PROVIDER_FLAGS
プログラム プロバイダーから取得する必要のあるプロパティを指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_PROVIDER_FLAGS {
   PFLAG_NONE                    = 0x00,
   PFLAG_REMOTE_PORT             = 0x01,
   PFLAG_DEBUGGEE                = 0x02,
   PFLAG_ATTACHED_TO_DEBUGGEE    = 0x04,
   PFLAG_REASON_WATCH            = 0x08,
   PFLAG_GET_PROGRAM_NODES       = 0x10,
   PFLAG_GET_IS_DEBUGGER_PRESENT = 0x20
};
typedef DWORD PROVIDER_FLAGS;
```

```csharp
public enum enum_PROVIDER_FLAGS {
   PFLAG_NONE                    = 0x00,
   PFLAG_REMOTE_PORT             = 0x01,
   PFLAG_DEBUGGEE                = 0x02,
   PFLAG_ATTACHED_TO_DEBUGGEE    = 0x04,
   PFLAG_REASON_WATCH            = 0x08,
   PFLAG_GET_PROGRAM_NODES       = 0x10,
   PFLAG_GET_IS_DEBUGGER_PRESENT = 0x20
};
```

## <a name="fields"></a>フィールド
 `PFLAG_NONE`\
 フラグは指定されていません。

 `PFLAG_REMOTE_PORT`\
 呼び出し元は、[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] とは異なるコンピューター上のプログラムの一覧を必要としています。

 `PFLAG_DEBUGGEE`\
 このプロセスは現在、[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] のこのインスタンスによってデバッグされています。

 `PFLAG_ATTACH_TODEBUGGEE`\
 [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] はデバッグ中のプログラムにアタッチされていますが、起動しませんでした。

 `PFLAG_REASON_WATCH`\
 [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] でイベントを監視しています。

 `PFLAG_GET_PROGRAM_NODES`\
 呼び出し元は、[PROVIDER_PROCESS_DATA](../../../extensibility/debugger/reference/provider-process-data.md) 構造体の `ProgramNodes` フィールドを必要としています。

 `PFLAG_GET_IS_DEBUGGER_PRESENT`\
 呼び出し元は、`PROVIDER_PROCESS_DATA` 構造体の `fIsTheDebuggerPresent` フィールドを必要としています。

## <a name="remarks"></a>解説
 これらのフラグは次のメソッドに渡されます。

- [WatchForProviderEvents](../../../extensibility/debugger/reference/idebugprogramprovider2-watchforproviderevents.md)

- [GetProviderProgramNode](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprogramnode.md)

- [GetProviderProcessData](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprocessdata.md)

  これらの値は、ビットごとの `OR` と組み合わせることができます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [PROVIDER_PROCESS_DATA](../../../extensibility/debugger/reference/provider-process-data.md)
- [WatchForProviderEvents](../../../extensibility/debugger/reference/idebugprogramprovider2-watchforproviderevents.md)
- [GetProviderProgramNode](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprogramnode.md)
- [GetProviderProcessData](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprocessdata.md)
