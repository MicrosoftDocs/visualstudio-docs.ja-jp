---
description: 式の評価を制御するフラグの有効な値を列挙します。
title: EVALFLAGS90 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- EVALFLAGS90 enumeration
ms.assetid: 64fb0139-8b04-4726-b52c-db2e04d65498
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 32e75b938f45df5d4fa91bec4b59964dfc6a54e5
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105095928"
---
# <a name="evalflags90"></a>EVALFLAGS90
式の評価を制御するフラグの有効な値を列挙します。 この列挙によって [EVALFLAGS](../../../extensibility/debugger/reference/evalflags.md) 列挙型が拡張されます。

## <a name="syntax"></a>構文

```cpp
enum enum_EVALFLAGS90
{
    // VS 8.0 values
    EVAL90_RETURNVALUE                 = 0x0002,
    EVAL90_NOSIDEEFFECTS               = 0x0004,
    EVAL90_ALLOWBPS                    = 0x0008,
    EVAL90_ALLOWERRORREPORT            = 0x0010,
    EVAL90_FUNCTION_AS_ADDRESS         = 0x0040,
    EVAL90_NOFUNCEVAL                  = 0x0080,
    EVAL90_NOEVENTS                    = 0x1000,
    EVAL90_DESIGN_TIME_EXPR_EVAL       = 0x2000,
    EVAL90_ALLOW_IMPLICIT_VARS         = 0x4000,

    // Values added in VS 9.0
    EVAL90_FORCE_EVALUATION_NOW        = 0x8000
};
typedef DWORD EVALFLAGS90;
```

```csharp
public enum enum_EVALFLAGS90
{
    // VS 8.0 values
    EVAL90_RETURNVALUE                 = 0x0002,
    EVAL90_NOSIDEEFFECTS               = 0x0004,
    EVAL90_ALLOWBPS                    = 0x0008,
    EVAL90_ALLOWERRORREPORT            = 0x0010,
    EVAL90_FUNCTION_AS_ADDRESS         = 0x0040,
    EVAL90_NOFUNCEVAL                  = 0x0080,
    EVAL90_NOEVENTS                    = 0x1000,
    EVAL90_DESIGN_TIME_EXPR_EVAL       = 0x2000,
    EVAL90_ALLOW_IMPLICIT_VARS         = 0x4000,

    // Values added in VS 9.0
    EVAL90_FORCE_EVALUATION_NOW        = 0x8000
};
```

## <a name="fields"></a>フィールド
`EVAL90_RETURNVALUE`\
戻り値 (存在する場合) を評価することを指定します。

`EVAL90_NOSIDEEFFECTS`\
副作用を許可しないことを指定します。

`EVAL90_ALLOWBPS`\
ブレークポイントでの停止を指定します。

`EVAL90_ALLOWERRORREPORT`\
ホストへのエラー報告を許可することを指定します。 主に、Internet Explorer のスクリプトでの式の評価に使用されます。

`EVAL90_FUNCTION_AS_ADDRESS`\
関数を呼び出す代わりに、関数をアドレスとして強制的に評価します。

`EVAL90_NOFUNCEVAL`\
関数が評価されないようにします。 たとえば、式 `myExpression(int) + 10` の `int` トークンついて考えてみましょう。 この関数は、アドレスとして正しく評価できますが、値としては評価できません。

`EVAL90_NOEVENTS`\
式の評価中に発生したイベントをセッション デバッグ マネージャー (SDM) または IDE に送信しないことを示すフラグ。

`EVAL90_DESIGN_TIME_EXPR_EVAL`\
デザイン時の式の評価を有効にします。

`EVAL90_ALLOW_IMPLICIT_VARS`\
暗黙的な変数の作成を許可します。

`EVAL90_FORCE_EVALUATION_NOW`\
直ちに評価を強制的に実行します。 これは、ユーザー要求などの要求を処理する場合に便利です。

## <a name="requirements"></a>必要条件
ヘッダー: Msdbg90.h

名前空間: Microsoft.VisualStudio.Debugger.Interop

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
