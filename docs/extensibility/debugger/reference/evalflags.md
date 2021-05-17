---
description: 式の評価を制御するフラグを指定します。
title: EVALFLAGS | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- EVALFLAGS
helpviewer_keywords:
- EVALFLAGS enumeration
ms.assetid: 7b2cb14a-511a-4fef-9e4f-308139719fba
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 5bcf68b95bb905d41aaab906603cd4dd248e52ad
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105095941"
---
# <a name="evalflags"></a>EVALFLAGS
式の評価を制御するフラグを指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_EVALFLAGS {
    EVAL_RETURNVALUE = 0x0002,
    EVAL_NOSIDEEFFECTS = 0x0004,
    EVAL_ALLOWBPS = 0x0008,
    EVAL_ALLOWERRORREPORT = 0x0010,
    EVAL_FUNCTION_AS_ADDRESS = 0x0040,
    EVAL_NOFUNCEVAL = 0x0080,
    EVAL_NOEVENTS = 0x1000
};
typedef DWORD EVALFLAGS;
```

```csharp
public enum enum_EVALFLAGS {
    EVAL_RETURNVALUE = 0x0002,
    EVAL_NOSIDEEFFECTS = 0x0004,
    EVAL_ALLOWBPS = 0x0008,
    EVAL_ALLOWERRORREPORT = 0x0010,
    EVAL_FUNCTION_AS_ADDRESS = 0x0040,
    EVAL_NOFUNCEVAL = 0x0080,
    EVAL_NOEVENTS = 0x1000
}
```

## <a name="fields"></a>フィールド
`EVAL_RETURNVALUE`\
戻り値 (存在する場合) を評価することを指定します。

`EVAL_NOSIDEEFFECTS`\
副作用を許可しないことを指定します。

`EVAL_ALLOWBPS`\
ブレークポイントでの停止を指定します。

`EVAL_ALLOWERRORREPORT`\
ホストへのエラー報告を許可することを指定します。 主に、Internet Explorer のスクリプトでの式の評価に使用されます。

`EVAL_FUNCTION_AS_ADDRESS`\
関数を呼び出す代わりに、関数をアドレスとして強制的に評価します。

`EVAL_NOFUNCEVAL`\
関数が評価されないようにします。 たとえば、式 `myExpression(int) + 10` の `int` トークンついて考えてみましょう。 この関数は、アドレスとして正しく評価できますが、値としては評価できません。

`EVAL_NOEVENTS`\
式の評価中に発生したイベントをセッション デバッグ マネージャー (SDM) または IDE に送信しないことを示すフラグ。

## <a name="remarks"></a>解説
これらのフラグは、[Evaluateasync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md) と [EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) の各メソッドに引数として渡されます。

これらのフラグは、ビットごとの OR と組み合わせることができます。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: Microsoft.VisualStudio.Debugger.Interop

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)
- [EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)
