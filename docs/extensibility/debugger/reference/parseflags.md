---
description: 式の解析方法を指定します。
title: PARSEFLAGS | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- PARSEFLAGS
helpviewer_keywords:
- PARSEFLAGS enumeration
ms.assetid: 47943f0a-54cb-4493-a62e-5dba97bd4c35
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f7dabef93e8160a2319bc5cefeb189fa335f4b9f
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105082336"
---
# <a name="parseflags"></a>PARSEFLAGS
式の解析方法を指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_PARSEFLAGS { 
   PARSE_EXPRESSION            = 0x0001,
   PARSE_FUNCTION_AS_ADDRESS   = 0x0002,
   PARSE_DESIGN_TIME_EXPR_EVAL = 0x1000
};
typedef DWORD PARSEFLAGS;
```

```csharp
public enum enum_PARSEFLAGS { 
   PARSE_EXPRESSION            = 0x0001,
   PARSE_FUNCTION_AS_ADDRESS   = 0x0002,
   PARSE_DESIGN_TIME_EXPR_EVAL = 0x1000
};
```

## <a name="fields"></a>フィールド
 `PARSE_EXPRESSION`\
 式がステートメントではないことを示します。

 `PARSE_FUNCTION_AS_ADDRESS`\
 式がアドレスとして解析される (および後で評価される) ことを示します。

 `PARSE_DESIGN_TIME_EXPR_EVAL`\
 式がデザイン時 (つまり、デザイナーが開いているとき) に解析されることを示します。

## <a name="remarks"></a>解説
 [ParseText](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) メソッドおよび [Parse](../../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md) メソッドにパラメーターとして渡されます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [ParseText](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)
- [Parse](../../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md)
