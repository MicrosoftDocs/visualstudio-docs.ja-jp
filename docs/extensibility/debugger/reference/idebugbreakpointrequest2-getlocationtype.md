---
description: このブレークポイント要求のブレークポイント場所の種類を取得します。
title: IDebugBreakpointRequest2::GetLocationType | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBreakpointRequest2::GetLocationType
helpviewer_keywords:
- IDebugBreakpointRequest2::GetLocationType
ms.assetid: b6d14c59-d3aa-48ff-8278-f6b5bba9c2f3
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 1bd254d5bfd9126a65ad7364212f628b1b45cb61
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105054518"
---
# <a name="idebugbreakpointrequest2getlocationtype"></a>IDebugBreakpointRequest2::GetLocationType
このブレークポイント要求のブレークポイント場所の種類を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetLocationType(
    BP_LOCATION_TYPE* pBPLocationType
);
```

```csharp
int GetLocationType(
    out enum_BP_LOCATION_TYPE pBPLocationType
);
```

## <a name="parameters"></a>パラメーター
`pBPLocationType`\
[出力] このブレークポイント要求の場所を表す [BP_LOCATION_TYPE](../../../extensibility/debugger/reference/bp-location-type.md) 列挙型から値を返します。

## <a name="return-value"></a>戻り値
成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。 関連付けられている [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md) 構造体に含まれる `bpLocation` フィールドが無効な場合、`E_FAIL` を返します。

## <a name="example"></a>例
次の例は、[IDebugBreakpointRequest2](../../../extensibility/debugger/reference/idebugbreakpointrequest2.md) インターフェイスを公開する単純な `CDebugBreakpointRequest` オブジェクトに対してこのメソッドを実装する方法を示しています。

```
HRESULT CDebugBreakpointRequest::GetLocationType(BP_LOCATION_TYPE* pBPLocationType)
{
    HRESULT hr;

    if (pBPLocationType)
    {
        // Set default BP_LOCATION_TYPE.
        *pBPLocationType = BPLT_NONE;

        // Check if the BPREQI_BPLOCATION flag is set in BPREQI_FIELDS.
        if (IsFlagSet(m_bpRequestInfo.dwFields, BPREQI_BPLOCATION))
        {
            // Get the new BP_LOCATION_TYPE.
            *pBPLocationType = m_bpRequestInfo.bpLocation.bpLocationType;
            hr = S_OK;
        }
        else
        {
            hr = E_FAIL;
        }
    }
    else
    {
        hr = E_INVALIDARG;
    }

    return hr;
}
```

## <a name="see-also"></a>関連項目
- [IDebugBreakpointRequest2](../../../extensibility/debugger/reference/idebugbreakpointrequest2.md)
- [BP_LOCATION_TYPE](../../../extensibility/debugger/reference/bp-location-type.md)
- [BPREQI_FIELDS](../../../extensibility/debugger/reference/bpreqi-fields.md)
- [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)
