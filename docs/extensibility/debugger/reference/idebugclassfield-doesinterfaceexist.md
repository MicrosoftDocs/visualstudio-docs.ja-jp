---
description: クラスで特定のインターフェイスが定義されているかどうかを判断します。
title: IDebugClassField::DoesInterfaceExist | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugClassField::DoesInterfaceExist
helpviewer_keywords:
- IDebugClassField::DoesInterfaceExist method
ms.assetid: cc0c8642-1a76-4fda-a309-7018a34883c9
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 60a9a64e408f182476d6f34b19fea45f6fe8ad48
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105085026"
---
# <a name="idebugclassfielddoesinterfaceexist"></a>IDebugClassField::DoesInterfaceExist
クラスで特定のインターフェイスが定義されているかどうかを判断します。

## <a name="syntax"></a>構文

```cpp
HRESULT DoesInterfaceExist( 
   LPCOLESTR pszInterfaceName
);
```

```csharp
int DoesInterfaceExist(
   [In] string pszInterfaceName
);
```

## <a name="parameters"></a>パラメーター
`pszInterfaceName`\
[in] 検索するインターフェイス名を含む文字列。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、S_OK を返します。インターフェイスが存在しない場合は、S_FALSE を返します。それ以外の場合はエラー コードを返します。

## <a name="remarks"></a>解説
 このメソッドは、事実上、すべてのインターフェイスの列挙体を取得し、一覧を検索して、一致するインターフェイスを見つけます。

## <a name="see-also"></a>関連項目
- [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)
