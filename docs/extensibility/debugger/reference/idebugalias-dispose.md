---
title: Iデバッグエイリアス::Dポーズ |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugAlias::Dispose
helpviewer_keywords:
- IDebugAlias::Dispose method
ms.assetid: e84909a4-d378-4f48-bf25-2c014c77c8e3
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: df3a2ecc50063df8f90645b9ccaa72754c3728c1
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80736555"
---
# <a name="idebugaliasdispose"></a>IDebugAlias::Dispose
このエイリアスを削除対象としてマークします。

## <a name="syntax"></a>構文

```cpp
HRESULT Dispose();
```

```csharp
int Dispose();
```

## <a name="parameters"></a>パラメーター
 [なし] :

## <a name="return-value"></a>戻り値
 成功した場合は、S_OK返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 このメソッドが呼び出されると、エイリアスは使用できなくなります。

## <a name="see-also"></a>関連項目
- [IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md)
