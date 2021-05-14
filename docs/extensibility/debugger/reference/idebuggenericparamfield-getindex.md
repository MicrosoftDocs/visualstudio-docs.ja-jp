---
description: このジェネリック パラメーターのインデックスを取得します。
title: IDebugGenericParamField::GetIndex | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugGenericParamField::GetIndex
ms.assetid: 8e0bdb26-1247-44d9-8d80-ec6e35187fb4
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 210a66db89998cff2cde043ceb1c1cf21f23d8ee
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105073483"
---
# <a name="idebuggenericparamfieldgetindex"></a>IDebugGenericParamField::GetIndex
このジェネリック パラメーターのインデックスを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetIndex(
    DWORD* pIndex
);
```

```csharp
int GetIndex(
    out uint pIndex
);
```

## <a name="parameters"></a>パラメーター
`pIndex`\
[出力] このジェネリック パラメーターのインデックス値。

## <a name="return-value"></a>戻り値
成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
たとえば、Dictionary(K, V) の場合、K はインデックス 0、V はインデックス 1 です。

## <a name="example"></a>例
次の例は、[IDebugGenericParamField](../../../extensibility/debugger/reference/idebuggenericparamfield.md) インターフェイスを公開する **CDebugGenericParamFieldType** オブジェクトにこのメソッドを実装する方法を示しています。

```cpp
HRESULT CDebugGenericParamFieldType::GetIndex(DWORD* pIndex)
{
    HRESULT hr = S_OK;

    METHOD_ENTRY( CDebugGenericParamFieldType::GetIndex );

    IfFalseGo(pIndex, E_INVALIDARG );
    IfFailGo( this->LoadProps() );
    *pIndex = m_index;

Error:

    METHOD_EXIT( CDebugGenericParamFieldType::GetIndex, hr );
    return hr;
}
```

## <a name="see-also"></a>関連項目
- [IDebugGenericParamField](../../../extensibility/debugger/reference/idebuggenericparamfield.md)
