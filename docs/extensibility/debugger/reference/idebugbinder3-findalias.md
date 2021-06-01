---
description: このメソッドでは、名前を指定してエイリアスを検索します。
title: IDebugBinder3::FindAlias | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBinder3::FindAlias
helpviewer_keywords:
- IDebugBinder3::FindAlias method
ms.assetid: b8333701-2718-4983-8513-0875fb7cb730
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9958c1c2b93d6547f1f3453bafc9e331f9061844
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105089057"
---
# <a name="idebugbinder3findalias"></a>IDebugBinder3::FindAlias
このメソッドでは、名前を指定してエイリアスを検索します。 これにより、プログラム内のすべてのエイリアスが検索されます。

## <a name="syntax"></a>構文

```cpp
HRESULT FindAlias(
   LPCOLESTR     pcstrName,
   IDebugAlias** ppAlias
);
```

```csharp
int FindAlias(
   string          pcstrName,
   out IDebugAlias ppAlias
);
```

## <a name="parameters"></a>パラメーター
`pcstrName`\
[入力] 検索するエイリアスの名前。

`ppAlias`\
[出力] [IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md) インターフェイスによって表される検出されたエイリアス (存在する場合)。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は `S_FALSE` (エイリアスが見つからない場合) またはエラー コードを返します。

## <a name="remarks"></a>解説
 このメソッドでは、呼び出す前に対象オブジェクトを null に初期化します。その後、null 値をテストし、エイリアスが見つかったかどうかを判断します。

## <a name="see-also"></a>関連項目
- [IDebugBinder3](../../../extensibility/debugger/reference/idebugbinder3.md)
- [IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md)
