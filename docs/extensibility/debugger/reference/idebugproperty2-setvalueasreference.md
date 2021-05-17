---
description: このプロパティの値を、指定された参照の値に設定します。
title: IDebugProperty2::SetValueAsReference | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty2::SetValueAsReference
helpviewer_keywords:
- IDebugProperty2::SetValueAsReference method
ms.assetid: 341b1b89-4ab8-4e1c-abe2-fb955df5c6b0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 8b370b4caa43ce6522b415233714eb15899b3051
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105064775"
---
# <a name="idebugproperty2setvalueasreference"></a>IDebugProperty2::SetValueAsReference
このプロパティの値を、指定された参照の値に設定します。

## <a name="syntax"></a>構文

```cpp
HRESULT SetValueAsReference(
   IDebugReference2** rgpArgs,
   DWORD              dwArgCount,
   IDebugReference2*  pValue,
   DWORD              dwTimeout
);
```

```csharp
int SetValueAsReference(
   IDebugReference2[] rgpArgs,
   uint               dwArgCount,
   IDebugReference2   pValue,
   uint               dwTimeout
);
```

## <a name="parameters"></a>パラメーター
`rgpArgs`\
[入力] マネージド コードのプロパティ セッターに渡す引数の配列。 プロパティ セッターが引数を取らないか、この [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) オブジェクトがそのようなプロパティ セッターを参照しない場合、`rgpArgs` は null 値である必要があります。 通常、このパラメーターは null 値です。

`dwArgCount`\
[入力] `rgpArgs` 配列内の引数の数。

`pValue`\
[入力] このプロパティを設定するために使用する値への参照 ([IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md) オブジェクトの形式)。

`dwTimeout`\
[入力] 値を設定するのにかかる時間 (ミリ秒単位)。 一般的な値は `INFINITE` です。 これは、考えられる評価にかかる可能性がある時間の長さに影響します。

## <a name="return-value"></a>戻り値
 成功した場合は `S_OK` を返します。それ以外の場合は、エラー コード (通常は次のいずれか) を返します。

|エラー|説明|
|-----------|-----------------|
|`E_SETVALUEASREFERENCE_NOTSUPPORTED`|参照からの値の設定はサポートされていません。|
|`E_SETVALUE_VALUE_CANNOT_BE_SET`|このプロパティがメソッドを参照しているため、値を設定できません。|
|`E_SETVALUE_VALUE_IS_READONLY`|値は読み取り専用であり、設定できません。|
|`E_NOTIMPL`|このメソッドは実装されていません。|

## <a name="see-also"></a>関連項目
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)
