---
description: プログラムのプロパティを取得します。
title: IDebugProgram2::GetDebugProperty | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::GetDebugProperty
helpviewer_keywords:
- IDebugProgram2::GetDebugProperty
ms.assetid: d194224e-f0e6-46ab-85d4-9e2639e28946
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 60e551829a1f424a9bb7f89642f1d692db8d8032
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105075979"
---
# <a name="idebugprogram2getdebugproperty"></a>IDebugProgram2::GetDebugProperty
プログラムのプロパティを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetDebugProperty( 
   IDebugProperty2** ppProperty
);
```

```csharp
int GetDebugProperty( 
   out IDebugProperty2 ppProperty
);
```

## <a name="parameters"></a>パラメーター
`ppProperty`\
[出力] プログラムのプロパティを表す [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 このメソッドから返されるプロパティは、プログラムに固有です。 プログラムから複数のプロパティを返す必要がある場合、このメソッドから返される [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) オブジェクトは追加のプロパティのコンテナーです。また、[EnumChildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md) メソッドを呼び出すと、すべてのプロパティの一覧が返されます。

 プログラムにより、`IDebugProperty2` インターフェイスを介して記述できる任意の数と型の追加のプロパティを公開することができます。 IDE には、汎用プロパティ ブラウザーのユーザー インターフェイスを介して追加のプログラム プロパティが表示される場合があります。

## <a name="see-also"></a>関連項目
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [EnumChildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)
