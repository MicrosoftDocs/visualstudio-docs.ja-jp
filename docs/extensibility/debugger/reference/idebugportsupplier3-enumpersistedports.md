---
description: このメソッドは、永続ポートのリストを列挙できるオブジェクトを取得します。
title: IDebugPortSupplier3::EnumPersistedPorts | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortSupplier3::EnumPersistedPorts
helpviewer_keywords:
- IDebugPortSupplier3::EnumPersistedPorts
ms.assetid: 1c3dead3-5d6c-4067-8418-4015f0b0dd07
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b4fe55898f6dbc7713db6e013868b1c7f22a5faf
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105071962"
---
# <a name="idebugportsupplier3enumpersistedports"></a>IDebugPortSupplier3::EnumPersistedPorts
このメソッドは、永続ポートのリストを列挙できるオブジェクトを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT EnumPersistedPorts(
   BSTR_ARRAY         PortNames,
   IEnumDebugPorts2** ppEnum
);
```

```csharp
int EnumPersistedPorts(
   BSTR_ARRAY           PortNames,
   out IEnumDebugPorts2 ppEnum
);
```

## <a name="parameters"></a>パラメーター
`PortNames`\
[入力] 永続ポート間で検索して返すポート名のリストが格納されている [BSTR_ARRAY](../../../extensibility/debugger/reference/bstr-array.md) 構造体。 これらの名前を持つ永続ポートのみが返されます。

`ppEnum`\
[出力] [IEnumDebugPorts2](../../../extensibility/debugger/reference/ienumdebugports2.md) インターフェイスを実装するオブジェクト。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 永続ポートは、ポート サプライヤーがインスタンス化されるときに読み込まれ、ポート サプライヤーが破壊されるときに保存されます。

## <a name="see-also"></a>関連項目
- [IDebugPortSupplier3](../../../extensibility/debugger/reference/idebugportsupplier3.md)
- [IEnumDebugPorts2](../../../extensibility/debugger/reference/ienumdebugports2.md)
- [BSTR_ARRAY](../../../extensibility/debugger/reference/bstr-array.md)
