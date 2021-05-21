---
description: このエイリアスに関連付けられている値を表すマネージド コード インターフェイスを取得します。
title: IDebugAlias::GetICorDebugValue | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugAlias::GetICorDebugValue
helpviewer_keywords:
- IDebugAlias::GetICorDebugValue method
ms.assetid: b9eb39ee-84af-4ace-9cfe-236b3d48aff5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ad6cd04d077245d3e893099aab8820ddc8ccf559
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105095915"
---
# <a name="idebugaliasgeticordebugvalue"></a>IDebugAlias::GetICorDebugValue
このエイリアスに関連付けられている値を表すマネージド コード インターフェイスを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetICorDebugValue(
   IUnknown** ppUnk
);
```

```csharp
int GetICorDebugValue(
   out object ppUnk
);
```

## <a name="parameters"></a>パラメーター
`ppUnk`\
[出力] このエイリアスに関連付けられている値を表す `IUnknown` インターフェイス。 このインターフェイスは、`ICorDebugValue` インターフェイスに対してクエリを実行できます。

## <a name="return-value"></a>戻り値
 成功した場合は、S_OK を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 このメソッドはマネージド値にのみ適用されます (`ICorDebugValue` は .NET Framework で利用できるインターフェイスであり、.NET Framework SDK の cordebug.idl ファイルに定義されています)。

## <a name="see-also"></a>関連項目
- [IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md)
