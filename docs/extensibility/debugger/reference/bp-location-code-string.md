---
description: ユーザーが統合開発環境 (IDE) から入力できる文字列に基づいたコード ブレークポイントを設定するために使用されます。
title: BP_LOCATION_CODE_STRING | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_LOCATION_CODE_STRING
helpviewer_keywords:
- BP_LOCATION_CODE_STRING structure
ms.assetid: a4cd71c6-5052-45fe-907b-ebc6ca1df2e4
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
ms.openlocfilehash: 9c32a75e4976a81498033a656461d897e4f298a3
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105096773"
---
# <a name="bp_location_code_string"></a>BP_LOCATION_CODE_STRING
ユーザーが統合開発環境 (IDE) から入力できる文字列に基づいたコード ブレークポイントを設定するために使用されます。

## <a name="syntax"></a>構文

```cpp
typedef struct _BP_LOCATION_CODE_STRING {
    BSTR bstrContext;
    BSTR bstrCodeExpr;
} BP_LOCATION_CODE_STRING;
```

## <a name="members"></a>メンバー
`bstrContext`\
コード内のブレークポイントのコンテキスト。通常は、呼び出し履歴に表示されるメソッドまたは関数の名前。

`bstrCodeExpr`\
コード ブレークポイントを説明するためにユーザーが入力する文字列。

## <a name="remarks"></a>解説
この構造体は、共用体の一部として [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md) 構造体のメンバーになります。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: Microsoft.VisualStudio.Debugger.Interop

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)
