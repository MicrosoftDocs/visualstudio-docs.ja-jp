---
description: デバッグ中のプログラムによってスローされた例外または実行時エラーを記述します。
title: EXCEPTION_INFO |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- EXCEPTION_INFO
helpviewer_keywords:
- EXCEPTION_INFO structure
ms.assetid: d046957a-b97d-420b-b46b-c67cbaef709e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 1ec97b56cc7fca8c2185d7180a8d34e87b084b11
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105059471"
---
# <a name="exception_info"></a>EXCEPTION_INFO
デバッグ中のプログラムによってスローされた例外または実行時エラーを記述します。

## <a name="syntax"></a>構文

```cpp
typedef struct tagEXCEPTION_INFO {
    IDebugProgram2* pProgram;
    BSTR            bstrProgramName;
    BSTR            bstrExceptionName;
    DWORD           dwCode;
    EXCEPTION_STATE dwState;
    GUID            guidType;
} EXCEPTION_INFO;
```

```csharp
public struct EXCEPTION_INFO {
    public IDebugProgram2 pProgram;
    public string         bstrProgramName;
    public string         bstrExceptionName;
    public uint           dwCode;
    public uint           dwState;
    public Guid           guidType;
};
```

## <a name="members"></a>メンバー
`pProgram`\
例外が発生したプログラムを表す [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) オブジェクト。

`bstrProgramName`\
例外が発生したプログラムの名前。

`bstrExceptionName`\
例外の名前。

`dwCode`\
例外または実行時エラーの識別コード。

`dwState`\
例外の状態を定義する [EXCEPTION_STATE](../../../extensibility/debugger/reference/exception-state.md) 列挙の値。

`guidType`\
GUID 言語識別子 `guidLang` 。またはのいずれか `guidEng` です。

## <a name="remarks"></a>注釈
この構造体は、パラメーターとして [setexception](../../../extensibility/debugger/reference/idebugengine2-setexception.md) および [removesetexception](../../../extensibility/debugger/reference/idebugengine2-removesetexception.md) メソッドに渡されます。 この構造体は、入力される [Getexception](../../../extensibility/debugger/reference/idebugexceptionevent2-getexception.md) メソッドにも渡されます。

## <a name="requirements"></a>要件
ヘッダー: msdbg. h

名前空間: VisualStudio。

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>こちらもご覧ください
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [EXCEPTION_STATE](../../../extensibility/debugger/reference/exception-state.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [SetException](../../../extensibility/debugger/reference/idebugengine2-setexception.md)
- [RemoveSetException](../../../extensibility/debugger/reference/idebugengine2-removesetexception.md)
- [GetException](../../../extensibility/debugger/reference/idebugexceptionevent2-getexception.md)
