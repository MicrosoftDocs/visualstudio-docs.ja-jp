---
description: IDebugFunctionObject2::Evaluate は、関数を呼び出して、結果の値をオブジェクトとして返します。
title: IDebugFunctionObject2::Evaluate | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugFunctionObject2::Evaluate
ms.assetid: bc54c652-904b-4297-a6db-faa329684881
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 35b6acb64ffd894b1cff03badcf2cdea831c7260
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105063579"
---
# <a name="idebugfunctionobject2evaluate"></a>IDebugFunctionObject2::Evaluate
関数を呼び出し、結果の値をオブジェクトとして返します。

## <a name="syntax"></a>構文

```cpp
HRESULT Evaluate (
   IDebugObject** ppParams,
   DWORD          dwParams,
   DWORD          dwEvalFlags,
   DWORD          dwTimeout,
   IDebugObject** ppResult
);
```

```csharp
int Evaluate (
   IDebugObject     ppParams,
   uint             dwParams,
   uint             dwEvalFlags,
   uint             dwTimeout,
   out IDebugObject ppResult
);
```

## <a name="parameters"></a>パラメーター
`ppParams`\
[入力] 入力パラメーターを表す [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) オブジェクトの配列。 これらの各パラメーターは、このインターフェイスの Create メソッドのいずれかを使用して作成されたものです。

`dwParams`\
[入力] `ppParams` 配列内のパラメーターの数。

`dwEvalFlags`\
[入力] 評価の実行方法を指定する [EVALFLAGS](../../../extensibility/debugger/reference/evalflags.md) 列挙型のフラグの組み合わせ。

`dwTimeout`\
[入力] このメソッドから戻る前に待機する最大時間 (ミリ秒単位) を指定します。 無期限に待機するには **INFINITE** を使用します。

`ppResult`\
[出力] 関数の値をオブジェクトとして表す **IDebugObject** を返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDebugFunctionObject2](../../../extensibility/debugger/reference/idebugfunctionobject2.md)
