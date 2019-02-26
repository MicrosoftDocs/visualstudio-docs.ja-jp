---
title: IDebugFunctionObject2::Evaluate |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugFunctionObject2::Evaluate
ms.assetid: bc54c652-904b-4297-a6db-faa329684881
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 441126724c78c2045e3e870fcdf7baa23f9149c3
ms.sourcegitcommit: b0d8e61745f67bd1f7ecf7fe080a0fe73ac6a181
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/22/2019
ms.locfileid: "56708785"
---
# <a name="idebugfunctionobject2evaluate"></a>IDebugFunctionObject2::Evaluate
関数の呼び出しをオブジェクトとして結果の値を返します。

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

#### <a name="parameters"></a>パラメーター
 `ppParams`

 [in]配列の[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)入力パラメーターを表すオブジェクト。 これらの各パラメーターは、このインターフェイスの作成方法のいずれかを使用して作成されました。

 `dwParams`

 [in]パラメーターの数、`ppParams`配列。

 `dwEvalFlags`

 [in]フラグの組み合わせ、 [EVALFLAGS](../../../extensibility/debugger/reference/evalflags.md)評価を実行する方法を指定する列挙体。

 `dwTimeout`

 [in]このメソッドから戻る前に待機するミリ秒単位で最大の時間を指定します。 使用**無限**を無期限に待機します。

 `ppResult`

 [out]返します、 **IDebugObject**オブジェクトとして関数の値を表します。

## <a name="return-value"></a>戻り値
 成功した場合、返します`S_OK`、それ以外のエラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDebugFunctionObject2](../../../extensibility/debugger/reference/idebugfunctionobject2.md)