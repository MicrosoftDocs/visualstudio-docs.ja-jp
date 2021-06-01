---
description: このドキュメント コンテキストを含むドキュメントの表示可能な名前を取得します。
title: IDebugDocumentContext2::GetName | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocumentContext2::GetName
helpviewer_keywords:
- IDebugDocumentContext2::GetName
ms.assetid: 546c5b2e-f166-4edb-9e61-57d797ca98a1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 96f0130b09a98c4064f53337aaa2e54ad7ed887b
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105066608"
---
# <a name="idebugdocumentcontext2getname"></a>IDebugDocumentContext2::GetName
このドキュメント コンテキストを含むドキュメントの表示可能な名前を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetName(
    GETNAME_TYPE gnType,
    BSTR*        pbstrFileName
);
```

```csharp
int GetName(
    enum_GETNAME_TYPE  gnType,
    out string         pbstrFileName
);
```

## <a name="parameters"></a>パラメーター
`gnType`\
[入力] 取得する名前の種類を指定する [GETNAME_TYPE](../../../extensibility/debugger/reference/getname-type.md) 列挙型の値。

`pbstrFileName`\
[出力] ファイルの名前を返します。

## <a name="return-value"></a>戻り値
成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
このメソッドは、通常、ドキュメント コンテキストがドキュメントの名前自体を格納するように記述されている場合 (次の例のように) を除き、この呼び出しを [GetName](../../../extensibility/debugger/reference/idebugdocument2-getname.md) メソッドに転送します。

## <a name="example"></a>例
次の例は、[IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md) インターフェイスを公開するシンプルな `CDebugContext` オブジェクトにこのメソッドを実装する方法を示しています。

```cpp
HRESULT CDebugContext::GetName(GETNAME_TYPE gnType, BSTR* pbstrFileName)
{
    HRESULT hr;

    // Check for a valid file name argument.
    if (pbstrFileName)
    {
        *pbstrFileName = NULL;

        switch (gnType)
        {
            case GN_NAME:
            case GN_FILENAME:
            {
                // Copy the member file name into the local file name.
                *pbstrFileName = SysAllocString(m_sbstrFileName);
                // Check for successful copy.
                hr = (*pbstrFileName) ? S_OK : E_OUTOFMEMORY;
                break;
            }
            default:
            {
                hr = E_FAIL;
                break;
            }
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
- [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)
- [GETNAME_TYPE](../../../extensibility/debugger/reference/getname-type.md)
