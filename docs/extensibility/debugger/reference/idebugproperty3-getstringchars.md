---
description: このプロパティに関連付けられている文字列を取得し、ユーザー指定のバッファーに格納します。
title: IDebugProperty3::GetStringChars | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty3::GetStringChars
helpviewer_keywords:
- IDebugProperty3::GetStringChars
ms.assetid: 832c37f3-85cb-4227-8ab2-f27a80eafe90
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 21baaa5e5eb7446636fcbab9038db87444d50017
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105083935"
---
# <a name="idebugproperty3getstringchars"></a>IDebugProperty3::GetStringChars
このプロパティに関連付けられている文字列を取得し、ユーザー指定のバッファーに格納します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetStringChars(
    ULONG  buflen,
    WCHAR* rgString,
    ULONG* pceltFetched
);
```

```csharp
int GetStringChars(
    uint       buflen,
    out string rgString,
    out uint   pceltFetched
);
```

## <a name="parameters"></a>パラメーター
`buflen`\
[入力] ユーザー指定のバッファーで保持できる最大文字数。

`rgString`\
[出力] 文字列を返します。

 [C++ のみ]、`rgString` は、文字列の Unicode 文字を受け取るバッファーへのポインターです。 このバッファーのサイズは、少なくとも `buflen` 文字 (バイトではない) である必要があります。

`pceltFetched`\
[出力] バッファーに実際に格納されている文字数が返されます。 (C++ では `NULL` を指定できます)。

## <a name="return-value"></a>戻り値
成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
C++ では、バッファーの長さが `buflen` Unicode 文字以上であることを保証するために注意する必要があります。 Unicode 文字は 2 バイト長であることに注意してください。

> [!NOTE]
> C++ では、返される文字列に終端の null 文字は含まれません。 指定されている場合、`pceltFetched` では文字列の文字数を指定します。

## <a name="example"></a>例

```cpp
CStringW RetrievePropertyString(IDebugProperty2 *pPropInfo)
{
    CStringW returnString = L"";
    CComQIPtr<IDebugProperty3> pProp3 = pPropInfo->pProperty;
    If (pProp3 != NULL) {
        ULONG dwStrLen = 0;
        HRESULT hr;
        hr = pProp3->GetStringCharLength(&dwStrLen);
        if (SUCCEEDED(hr) && dwStrLen > 0) {
            ULONG dwRead;
            CStrBufW buf(returnString,dwStrLen,CStrBuf::SET_LENGTH);
            hr = pProp3->GetStringChars(dwStrLen,
                                        reinterpret_cast<WCHAR*>(static_cast<CStringW::PXSTR>(buf)),
                                        &dwRead);
        }
    }
    return(returnString);
}
```

## <a name="see-also"></a>関連項目
- [GetStringCharLength](../../../extensibility/debugger/reference/idebugproperty3-getstringcharlength.md)
- [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
