---
description: 例外の状態を指定します。
title: EXCEPTION_STATE | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- EXCEPTION_STATE
helpviewer_keywords:
- EXCEPTION_STATE enumeration
ms.assetid: 597f4f4c-9b70-485c-b5dc-3c2e3aecc664
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 297c5de3afd2b5f81444dd29278fc294cd71aa6a
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105059445"
---
# <a name="exception_state"></a>EXCEPTION_STATE
例外の状態を指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_EXCEPTION_STATE {
    EXCEPTION_NONE                          = 0x0000,
    EXCEPTION_STOP_FIRST_CHANCE             = 0x0001,
    EXCEPTION_STOP_SECOND_CHANCE            = 0x0002,
    EXCEPTION_STOP_USER_FIRST_CHANCE        = 0x0010,
    EXCEPTION_STOP_USER_UNCAUGHT            = 0x0020,
    EXCEPTION_STOP_ALL                      = 0x00FF,
    EXCEPTION_CANNOT_BE_CONTINUED           = 0x0100,

    // These are for exception types only
    EXCEPTION_CODE_SUPPORTED                = 0x1000,
    EXCEPTION_CODE_DISPLAY_IN_HEX           = 0x2000,
    EXCEPTION_JUST_MY_CODE_SUPPORTED        = 0x4000,
    EXCEPTION_MANAGED_DEBUG_ASSISTANT       = 0x8000,

    // These are no longer used
    EXCEPTION_STOP_FIRST_CHANCE_USE_PARENT      = 0x0004,
    EXCEPTION_STOP_SECOND_CHANCE_USE_PARENT     = 0x0008,
    EXCEPTION_STOP_USER_FIRST_CHANCE_USE_PARENT = 0x0040,
    EXCEPTION_STOP_USER_UNCAUGHT_USE_PARENT     = 0x0080,
};
typedef DWORD EXCEPTION_STATE;
```

```csharp
public enum enum_EXCEPTION_STATE {
    EXCEPTION_NONE                          = 0x0000,
    EXCEPTION_STOP_FIRST_CHANCE             = 0x0001,
    EXCEPTION_STOP_SECOND_CHANCE            = 0x0002,
    EXCEPTION_STOP_USER_FIRST_CHANCE        = 0x0010,
    EXCEPTION_STOP_USER_UNCAUGHT            = 0x0020,
    EXCEPTION_STOP_ALL                      = 0x00FF,
    EXCEPTION_CANNOT_BE_CONTINUED           = 0x0100,

    // These are for exception types only
    EXCEPTION_CODE_SUPPORTED                = 0x1000,
    EXCEPTION_CODE_DISPLAY_IN_HEX           = 0x2000,
    EXCEPTION_JUST_MY_CODE_SUPPORTED        = 0x4000,
    EXCEPTION_MANAGED_DEBUG_ASSISTANT       = 0x8000,

    // These are no longer used
    EXCEPTION_STOP_FIRST_CHANCE_USE_PARENT      = 0x0004,
    EXCEPTION_STOP_SECOND_CHANCE_USE_PARENT     = 0x0008,
    EXCEPTION_STOP_USER_FIRST_CHANCE_USE_PARENT = 0x0040,
    EXCEPTION_STOP_USER_UNCAUGHT_USE_PARENT     = 0x0080,
};
```

## <a name="fields"></a>フィールド
`EXCEPTION_NONE`\
例外では停止しません。

`EXCEPTION_STOP_FIRST_CHANCE`\
初回の例外の発生時に停止します。 例外イベントを記述する場合、このフラグは例外イベントが初回例外イベントであることを示します。

`EXCEPTION_STOP_SECOND_CHANCE`\
2 回目の例外の発生時に停止します。 例外イベントを記述する場合、例外イベントが 2 回目の例外イベントであることを示します。

`EXCEPTION_STOP_USER_FIRST_CHANCE`\
ユーザー モード例外の初回発生時に停止します。 例外イベントを記述する場合、例外イベントが初回ユーザー例外イベントであることを示します。

`EXCEPTION_STOP_USER_UNCAUGHT`\
ユーザー モードの例外がキャッチされない場合に停止します。 例外イベントを記述する場合、例外イベントがキャッチされていないユーザー モード例外イベントであることを示します。

`EXCEPTION_STOP_ALL`\
すべての例外で停止します。 例外イベントの記述時には使用されません。

`EXCEPTION_CANNOT_BE_CONTINUED`\
例外イベントを記述するときに、例外をそこから続行できないことを示します。

`EXCEPTION_CODE_SUPPORTED`\
例外にサポートするコードがあることを示します。 例外の表示に使用されます

`EXCEPTION_CODE_DISPLAY_IN_HEX`\
例外コードを 16 進数で表示する必要があることを示します。 例外の表示に使用されます。

`EXCEPTION_JUST_MY_CODE_SUPPORTED`\
例外コードで JustMyCode がサポートされていることを示します。 例外の表示に使用されます。

`EXCEPTION_MANAGED_DEBUG_ASSISTANT`\
マネージド コード デバッガーにより例外を処理する必要があることを示します。 設定されていない場合、既定のデバッガーにより例外が処理されます。 これは [SetAllExceptions](../../../extensibility/debugger/reference/idebugengine3-setallexceptions.md) メソッドに渡され、[EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md) 構造体では使用されません。

`EXCEPTION_STOP_FIRST_CHANCE_USE_PARENT`\
古いので使用しないでください。

`EXCEPTION_STOP_SECOND_CHANCE_USE_PARENT`\
古いので使用しないでください。

`EXCEPTION_STOP_USER_FIRST_CHANCE_USE_PARENT`\
古いので使用しないでください。

`EXCEPTION_STOP_USER_SECOND_CHANCE_USE_PARENT`\
古いので使用しないでください。

## <a name="remarks"></a>解説
例外の状態とそれに対して実行できることを示すために、 [EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md) 構造体の `dwState` メンバーとして使用されます。

これらの値は、すべての例外の状態を設定するために [SetAllExceptions](../../../extensibility/debugger/reference/idebugengine3-setallexceptions.md) メソッドにも渡されます。

これらのフラグは、ビットごとの OR と組み合わせることができます。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: Microsoft.VisualStudio.Debugger.Interop

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md)
- [SetAllExceptions](../../../extensibility/debugger/reference/idebugengine3-setallexceptions.md)
