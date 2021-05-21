---
description: ブレークポイント エラーの解決情報を取得します。
title: IDebugErrorBreakpointResolution2::GetResolutionInfo | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugErrorBreakpointResolution2::GetResolutionInfo
helpviewer_keywords:
- IDebugErrorBreakpointResolution2::GetResolutionInfo
ms.assetid: d94c4f60-8796-4848-86ee-186bbaa613f5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9329302a81fd7dd93bbb96dce5c5747edf40bf1c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105065789"
---
# <a name="idebugerrorbreakpointresolution2getresolutioninfo"></a>IDebugErrorBreakpointResolution2::GetResolutionInfo
ブレークポイント エラーの解決情報を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetResolutionInfo( 
    BPERESI_FIELDS            dwFields,
    BP_ERROR_RESOLUTION_INFO* pErrorResolutionInfo
);
```

```csharp
int GetResolutionInfo( 
    enum_BPERESI_FIELDS        dwFields,
    BP_ERROR_RESOLUTION_INFO[] pErrorResolutionInfo
);
```

## <a name="parameters"></a>パラメーター
`dwFields`\
[in] 入力する `pErrorResolutionInfo` のフィールドを判断する [BPERESI_FIELDS](../../../extensibility/debugger/reference/bperesi-fields.md) 列挙体のフラグの組み合わせ。

`pErrorResolutionInfo`\
[in, out] ブレークポイントの解決の説明が入力されている [BP_ERROR_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-error-resolution-info.md) 構造体。

## <a name="return-value"></a>戻り値
正常に終了した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="example"></a>例
次の例では、[IDebugErrorBreakpointResolution2](../../../extensibility/debugger/reference/idebugerrorbreakpointresolution2.md) インターフェイスを公開するシンプルな `CDebugErrorBreakpointResolution` オブジェクトに対して、このメソッドを実装しています。

```cpp
HRESULT CDebugErrorBreakpointResolution::GetResolutionInfo(
    BPERESI_FIELDS dwFields,
    BP_ERROR_RESOLUTION_INFO* pBPErrorResolutionInfo)
{
    HRESULT hr;

    if (pBPErrorResolutionInfo)
    {
        // Copy the specified fields of the request information from the class member
        // variable to the local BP_ERROR_RESOLUTION_INFO variable.
        hr = CopyBP_ERROR_RESOLUTION_INFO(m_bpErrorResolutionInfo,
                                          *pBPErrorResolutionInfo,
                                          dwFields);
    }
    else
    {
        hr = E_INVALIDARG;
    }

    return hr;
}

HRESULT CDebugErrorBreakpointResolution::CopyBP_ERROR_RESOLUTION_INFO(
    BP_ERROR_RESOLUTION_INFO& bpResSrc,
    BP_ERROR_RESOLUTION_INFO& bpResDest,
    DWORD dwFields)
{
    HRESULT hr = S_OK;

    // Start with a raw copy.
    memcpy(&bpResDest, &bpResSrc, sizeof(BP_ERROR_RESOLUTION_INFO));

    // The fields in the destination is the result of the AND of bpInfoSrc.dwFields
    // and dwFields.
    bpResDest.dwFields = dwFields & bpResSrc.dwFields;

    // Fill in the bp location information if the BPERESI_BPRESLOCATION flag
    // is set in BPERESI_FIELDS.
    if (IsFlagSet(bpResDest.dwFields, BPERESI_BPRESLOCATION))
    {
        // Switch on the BP_TYPE.
        switch (bpResSrc.bpResLocation.bpType)
        {
            case BPT_CODE:
            {
                // AddRef the IDebugCodeContext2 of the BP_RESOLUTION_CODE structure.
                bpResDest.bpResLocation.bpResLocation.bpresCode.pCodeContext->AddRef();
                break;
            }
            case BPT_DATA:
            {
                // Copy the bstrDataExpr, bstrFunc, and bstrImage of the
                // BP_RESOLUTION_DATA structure.
                bpResDest.bpResLocation.bpResLocation.bpresData.bstrDataExpr =
                SysAllocString(bpResSrc.bpResLocation.bpResLocation.bpresData.bstrDataExpr);
                bpResDest.bpResLocation.bpResLocation.bpresData.bstrFunc =
                SysAllocString(bpResSrc.bpResLocation.bpResLocation.bpresData.bstrFunc);
                bpResSrc.bpResLocation.bpResLocation.bpresData.bstrImage =
                SysAllocString(bpResSrc.bpResLocation.bpResLocation.bpresData.bstrImage);
                break;
            }
            default:
            {
                assert(FALSE);
                // Clear the BPERESI_BPRESLOCATION flag of the BPERESI_FIELDS
                // in the destination BP_ERROR_RESOLUTION_INFO.
                ClearFlag(bpResDest.dwFields, BPERESI_BPRESLOCATION);
                break;
            }
        }
    }
    // AddRef the IDebugProgram2 if the BPRESI_PROGRAM flag is set in the BPRESI_FIELDS.
    if (IsFlagSet(bpResDest.dwFields, BPERESI_PROGRAM))
    {
        bpResDest.pProgram->AddRef();
    }
    // AddRef the IDebuThread2 if the BPRESI_THREAD flag is set in the BPRESI_FIELDS.
    if (IsFlagSet(bpResDest.dwFields, BPERESI_THREAD))
    {
        bpResDest.pThread->AddRef();
    }
    // Check if the BPERESI_MESSAGE flag is set in the BPRESI_FIELDS.
    if (IsFlagSet(bpResDest.dwFields, BPERESI_MESSAGE))
    {
        // Copy the source bstrMessage into the destination bstrMessage.
        bpResDest.bstrMessage = SysAllocString(bpResSrc.bstrMessage);
        // Clear the destination flag if there is no message.
        if (!bpResDest.bstrMessage)
        {
            ClearFlag(bpResDest.dwFields, BPERESI_MESSAGE);
        }
    }

    return hr;
}
```

## <a name="see-also"></a>関連項目

- [IDebugErrorBreakpointResolution2](../../../extensibility/debugger/reference/idebugerrorbreakpointresolution2.md)
- [BPERESI_FIELDS](../../../extensibility/debugger/reference/bperesi-fields.md)
- [BP_ERROR_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-error-resolution-info.md)
