---
title: IEnumDebugPrograms2::GetCount |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugPrograms2::GetCount
helpviewer_keywords:
- IEnumDebugPrograms2::GetCount
ms.assetid: 84832982-fa68-4090-a5b7-b233817876b7
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 795404d0cae2dd5cbf4f6f913b3ba71cf3fe34a0
ms.sourcegitcommit: 6196d0b7fdcb08ba6d28a8151ad36b8d1139f2cc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2019
ms.locfileid: "65223420"
---
# <a name="ienumdebugprograms2getcount"></a>IEnumDebugPrograms2::GetCount
列挙体の要素の数を返します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetCount(
   ULONG* pcelt
);
```

```csharp
int GetCount(
   out uint pcelt
);
```

## <a name="parameters"></a>パラメーター
 `pcelt`\

 [out]列挙体の要素の数を返します。

## <a name="return-value"></a>戻り値
 成功した場合、返します`S_OK`、それ以外のエラー コードを返します。

## <a name="remarks"></a>Remarks
 このメソッドだけを指定する、よく使用される列挙型の COM インターフェイスの一部でない、 `Next`、 `Clone`、 `Skip`、および`Reset`メソッドを実装する必要があります。

## <a name="see-also"></a>関連項目
- [IEnumDebugPrograms2](../../../extensibility/debugger/reference/ienumdebugprograms2.md)