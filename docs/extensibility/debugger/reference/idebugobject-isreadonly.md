---
description: このオブジェクトが読み取り専用かどうかを判断します。
title: IDebugObject::IsReadOnly | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject::IsReadOnly
helpviewer_keywords:
- IDebugObject::IsReadOnly method
ms.assetid: c460f772-d08a-4b36-81f3-dff6a51a93fd
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 0b3cf66d8d540a92b937de996368ed24b18ae0b8
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105054063"
---
# <a name="idebugobjectisreadonly"></a>IDebugObject::IsReadOnly
このオブジェクトが読み取り専用かどうかを判断します。

## <a name="syntax"></a>構文

```cpp
HRESULT IsReadOnly( 
   BOOL* pfIsReadOnly
);
```

```csharp
int IsReadOnly(
   out int pfIsReadOnly
);
```

## <a name="parameters"></a>パラメーター
`pfIsReadOnly`\
[出力] このオブジェクトが読み取り専用の場合、ゼロ以外 (`TRUE`) を返します。それ以外の場合、ゼロ (`FALSE`) を返します。

## <a name="return-value"></a>戻り値
 成功した場合は、S_OK を返します。それ以外の場合はエラー コードを返します。

## <a name="remarks"></a>解説
 読み取り専用オブジェクトでは、作成後にその値を変更できません。

## <a name="see-also"></a>関連項目
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
