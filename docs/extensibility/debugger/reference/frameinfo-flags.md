---
description: スタック フレーム オブジェクトについて取得する情報を指定します。
title: FRAMEINFO_FLAGS | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- FRAMEINFO_FLAGS
helpviewer_keywords:
- FRAMEINFO_FLAGS enumeration
ms.assetid: 41578062-8455-412a-9d8b-1e1e9dc8d52e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d4214dd81945c3e7e2711a500e2e3a2b173e33e0
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105059263"
---
# <a name="frameinfo_flags"></a>FRAMEINFO_FLAGS
スタック フレーム オブジェクトについて取得する情報を指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_FRAMEINFO_FLAGS {
    FIF_FUNCNAME              = 0x00000001,
    FIF_RETURNTYPE            = 0x00000002,
    FIF_ARGS                  = 0x00000004,
    FIF_LANGUAGE              = 0x00000008,
    FIF_MODULE                = 0x00000010,
    FIF_STACKRANGE            = 0x00000020,
    FIF_FRAME                 = 0x00000040,
    FIF_DEBUGINFO             = 0x00000080,
    FIF_STALECODE             = 0x00000100,
    FIF_ANNOTATEDFRAME        = 0x00000200,
    FIF_DEBUG_MODULEP         = 0x00000400,
    FIF_FUNCNAME_FORMAT       = 0x00001000,
    FIF_FUNCNAME_RETURNTYPE   = 0x00002000,
    FIF_FUNCNAME_ARGS         = 0x00004000,
    FIF_FUNCNAME_LANGUAGE     = 0x00008000,
    FIF_FUNCNAME_MODULE       = 0x00010000,
    FIF_FUNCNAME_LINES        = 0x00020000,
    FIF_FUNCNAME_OFFSET       = 0x00040000,
    FIF_FUNCNAME_ARGS_TYPES   = 0x00100000,
    FIF_FUNCNAME_ARGS_NAMES   = 0x00200000,
    FIF_FUNCNAME_ARGS_VALUES  = 0x00400000,
    FIF_FUNCNAME_ARGS_ALL     = 0x00700000,
    FIF_ARGS_TYPES            = 0x01000000,
    FIF_ARGS_NAMES            = 0x02000000,
    FIF_ARGS_VALUES           = 0x04000000,
    FIF_ARGS_ALL              = 0x07000000,
    FIF_ARGS_NOFORMAT         = 0x08000000,
    FIF_ARGS_NO_FUNC_EVAL     = 0x10000000,
    FIF_FILTER_NON_USER_CODE  = 0x20000000,
    FIF_ARGS_NO_TOSTRING      = 0x40000000,
    FIF_DESIGN_TIME_EXPR_EVAL = 0x80000000
};
typedef DWORD FRAMEINFO_FLAGS;
```

```csharp
public enum enum_FRAMEINFO_FLAGS {
    FIF_FUNCNAME              = 0x00000001,
    FIF_RETURNTYPE            = 0x00000002,
    FIF_ARGS                  = 0x00000004,
    FIF_LANGUAGE              = 0x00000008,
    FIF_MODULE                = 0x00000010,
    FIF_STACKRANGE            = 0x00000020,
    FIF_FRAME                 = 0x00000040,
    FIF_DEBUGINFO             = 0x00000080,
    FIF_STALECODE             = 0x00000100,
    FIF_ANNOTATEDFRAME        = 0x00000200,
    FIF_DEBUG_MODULEP         = 0x00000400,
    FIF_FUNCNAME_FORMAT       = 0x00001000,
    FIF_FUNCNAME_RETURNTYPE   = 0x00002000,
    FIF_FUNCNAME_ARGS         = 0x00004000,
    FIF_FUNCNAME_LANGUAGE     = 0x00008000,
    FIF_FUNCNAME_MODULE       = 0x00010000,
    FIF_FUNCNAME_LINES        = 0x00020000,
    FIF_FUNCNAME_OFFSET       = 0x00040000,
    FIF_FUNCNAME_ARGS_TYPES   = 0x00100000,
    FIF_FUNCNAME_ARGS_NAMES   = 0x00200000,
    FIF_FUNCNAME_ARGS_VALUES  = 0x00400000,
    FIF_FUNCNAME_ARGS_ALL     = 0x00700000,
    FIF_ARGS_TYPES            = 0x01000000,
    FIF_ARGS_NAMES            = 0x02000000,
    FIF_ARGS_VALUES           = 0x04000000,
    FIF_ARGS_ALL              = 0x07000000,
    FIF_ARGS_NOFORMAT         = 0x08000000,
    FIF_ARGS_NO_FUNC_EVAL     = 0x10000000,
    FIF_FILTER_NON_USER_CODE  = 0x20000000,
    FIF_ARGS_NO_TOSTRING      = 0x40000000,
    FIF_DESIGN_TIME_EXPR_EVAL = 0x80000000
};
```

## <a name="fields"></a>フィールド
`FIF_FUNCNAME`\
`m_bstrFuncName` フィールドを初期化または使用します。

`FIF_RETURNTYPE`\
`m_bstrReturnType` フィールドを初期化または使用します。

`FIF_ARGS`\
`m_bstrArgs` フィールドを初期化または使用します。

`FIF_LANGUAGE`\
`m_bstrLanguage` フィールドを初期化または使用します。

`FIF_MODULE`\
`m_bstrModule` フィールドを初期化または使用します。

`FIF_STACKRANGE`\
`m_addrMin` および `m_addrMax` (スタック範囲) フィールドを初期化または使用します。

`FIF_FRAME`\
`m_pFrame` フィールドを初期化または使用します。

`FIF_DEBUGINFO`\
`m_fHasDebugInfo` フィールドを初期化または使用します。

`FIF_STALECODE`\
`m_fStaleCode` フィールドを初期化または使用します。

`FIF_ANNOTATEDFRAME`\
`m_fAnnotatedFrame` フィールドを初期化または使用します。

`FIF_DEBUG_MODULEP`\
`m_pModule` フィールドを初期化または使用します。

`FIF_FUNCNAME_FORMAT`\
関数名を書式設定します。 結果は `m_bstrFunName` フィールドに返され、それ以外のフィールドは入力されません。

`FIF_FUNCNAME_RETURNTYPE`\
`m_bstrFuncName` フィールドに戻り値の型を追加します。

`FIF_FUNCNAME_ARGS`\
`m_bstrFuncName` フィールドに引数を追加します。

`FIF_FUNCNAME_LANGUAGE`\
`m_bstrFuncName` フィールドに言語を追加します。

`FIF_FUNCNAME_MODULE`\
`m_bstrFuncName` フィールドにモジュール名を追加します。

`FIF_FUNCNAME_LINES`\
`m_bstrFuncName` フィールドに行の数を追加します。

`FIF_FUNCNAME_OFFSET`\
`m_bstrFuncName` が指定されている場合、行の先頭からのオフセット (バイト単位) を `FIF_FUNCNAME_LINES` フィールドに追加します。 `FIF_FUNCNAME_LINES` が指定されていない場合、または行番号が使用できない場合は、関数の先頭からのオフセット (バイト単位) を追加します。

`FIF_FUNCNAME_ARGS_TYPES`\
`m_bstrFuncName` フィールドに関数の各引数の型を追加します。

`FIF_FUNCNAME_ARGS_NAMES`\
`m_bstrFuncName` フィールドに関数の各引数の名前を追加します。

`FIF_FUNCNAME_ARGS_VALUES`\
`m_bstrFuncName` フィールドに関数の各引数の値を追加します。

`FIF_FUNCNAME_ARGS_ALL`\
`m_bstrFuncName` フィールドにすべての引数の型、名前、および値を追加します。

`FIF_ARGS_TYPES`\
引数の型が取得され、書式設定されます。

`FIF_ARGS_NAMES`\
引数の名前が取得され、書式設定されます。

`FIF_ARGS_VALUES`\
引数の値が取得され、書式設定されます。

`FIF_ARGS_ALL`\
すべての引数の型、名前、および値を取得して、書式設定します。

`FIF_ARGS_NOFORMAT`\
引数が書式設定されないことを指定します (たとえば、引数リストを始めかっこと終わりかっこで囲んだり、引数の間に区切り記号を追加したりしません)。

`FIF_ARGS_NO_FUNC_EVAL`\
引数の値を取得するときに、関数 (プロパティ) の評価を使用しないことを指定します。

`FIF_FILTER_NON_USER_CODE`\
デバッグ エンジンが、非ユーザー コード フレームをフィルター処理して、それらが含まれないようにします。

`FIF_ARGS_NO_TOSTRING`\
`ToString()`関数の引数を返すときに関数の評価または書式設定を許可しないでください。

`FIF_DESIGN_TIME_EXPR_EVAL`\
フレーム情報は、ホスト プロセスではなく、ホストされているアプリケーション ドメインから取得する必要があります。

## <a name="remarks"></a>解説
これらのフラグは、[EnumFrameInfo](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md) および [GetInfo](../../../extensibility/debugger/reference/idebugstackframe2-getinfo.md) メソッドに渡され、[FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md) 構造体 (1 つまたは複数) で初期化されるフィールドを指定します。

これらのフラグは、[FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md) 構造体のどのフィールドが使用されているか、またこの構造体が返されるときにどのフィールドが有効であるかを示すためにも使用されます。 これらの値は、ビットごとの `OR` で組み合わせることができます。

## <a name="requirements"></a>要件
ヘッダー: msdbg.h

名前空間: Microsoft.VisualStudio.Debugger.Interop

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)
- [EnumFrameInfo](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md)
- [GetInfo](../../../extensibility/debugger/reference/idebugstackframe2-getinfo.md)
