---
description: スタック フレームを説明します。
title: FRAMEINFO | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- FRAMEINFO
helpviewer_keywords:
- FRAMEINFO structure
ms.assetid: 95001b89-dddb-45bb-889d-8327994e38a5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 0df1689a6d72e972c2bb0f18082041997511843b
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105059250"
---
# <a name="frameinfo"></a>FRAMEINFO
スタック フレームを説明します。

## <a name="syntax"></a>構文

```cpp
typedef struct tagFRAMEINFO {
    FRAMEINFO_FLAGS    m_dwValidFields;
    BSTR               m_bstrFuncName;
    BSTR               m_bstrReturnType;
    BSTR               m_bstrArgs;
    BSTR               m_bstrLanguage;
    BSTR               m_bstrModule;
    UINT64             m_addrMin;
    UINT64             m_addrMax;
    IDebugStackFrame2* m_pFrame;
    IDebugModule2*     m_pModule;
    BOOL               m_fHasDebugInfo;
    BOOL               m_fStaleCode;
    BOOL               m_fAnnotatedFrame;
} FRAMEINFO;
```

```csharp
public struct FRAMEINFO {
    public uint              m_dwValidFields;
    public string            m_bstrFuncName;
    public string            m_bstrReturnType;
    public string            m_bstrArgs;
    public string            m_bstrLanguage;
    public string            m_bstrModule;
    public ulong             m_addrMin;
    public ulong             m_addrMax;
    public IDebugStackFrame2 m_pFrame;
    public IDebugModule2     m_pModule;
    public int               m_fHasDebugInfo;
    public int               m_fStaleCode;
    public int               m_fAnnotatedFrame;
} FRAMEINFO;
```

## <a name="members"></a>メンバー
`m_dwValidFields`\
入力するフィールドを指定する、[FRAMEINFO_FLAGS](../../../extensibility/debugger/reference/frameinfo-flags.md) 列挙からのフラグの組み合わせ。

`m_bstrFuncName`\
スタック フレームに関連付けられている関数名。

`m_bstrReturnType`\
スタック フレームに関連付けられている戻り値の型。

`m_bstrArgs`\
スタック フレームに関連付けられている関数の引数。

`m_bstrLanguage`\
関数の実装時に使用するプログラミング言語。

`m_bstrModule`\
スタック フレームに関連付けられているモジュール名。

`m_addrMin`\
最小物理スタック アドレス。

`m_addrMAX`\
最大物理スタック アドレス。

`m_pFrame`\
このスタック フレームを表す [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md) オブジェクト。

`m_pModule`\
このスタック フレームを含むモジュールを表す [IDebugModule2](../../../extensibility/debugger/reference/idebugmodule2.md) オブジェクト。

`m_fHasDebugInfo`\
所与のフレームにデバッグ情報が存在する場合は 0 以外 (`TRUE`)。

`m_fStaleCode`\
スタック フレームが無効になっているコードに関連付けられている場合は 0 以外 (`TRUE`)。

`m_fAnnotatedFrame`\
セッション デバッグ マネージャー (SDM) によってスタック フレームに注釈が付けられている場合は 0 以外 (`TRUE`)。

## <a name="remarks"></a>解説
この構造体は、入力対象の [GetInfo](../../../extensibility/debugger/reference/idebugstackframe2-getinfo.md) メソッドに渡されます。 この構造体は、[IEnumDebugFrameInfo2](../../../extensibility/debugger/reference/ienumdebugframeinfo2.md) インターフェイスに含まれるリストにも含まれています。これは、[EnumFrameInfo](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md) メソッドへの呼び出しから返されます。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: Microsoft.VisualStudio.Debugger.Interop

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [FRAMEINFO_FLAGS](../../../extensibility/debugger/reference/frameinfo-flags.md)
- [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)
- [IDebugModule2](../../../extensibility/debugger/reference/idebugmodule2.md)
- [GetInfo](../../../extensibility/debugger/reference/idebugstackframe2-getinfo.md)
- [IEnumDebugFrameInfo2](../../../extensibility/debugger/reference/ienumdebugframeinfo2.md)
- [EnumFrameInfo](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md)
