---
title: IDebugDocumentContext2::GetStatementRange |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocumentContext2::GetStatementRange
helpviewer_keywords:
- IDebugDocumentContext2::GetStatementRange
ms.assetid: bc94851a-0ec4-47ea-99c7-0a585e54e726
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 6ef4dae20a69fefcb67240e82999bdf2798d56e5
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66335295"
---
# <a name="idebugdocumentcontext2getstatementrange"></a>IDebugDocumentContext2::GetStatementRange
ドキュメント コンテキストのファイルのステートメントの範囲を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetStatementRange(
    TEXT_POSITION* pBegPosition,
    TEXT_POSITION* pEndPosition
);
```

```csharp
int GetStatementRange(
    TEXT_POSITION[] pBegPosition,
    TEXT_POSITION[] pEndPosition
);
```

## <a name="parameters"></a>パラメーター
`pBegPosition`\
[入力、出力]A [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)構造体の開始位置が入力されます。 この情報が必要でない場合は、この引数を null 値を設定します。

`pEndPosition`\
[入力、出力]A [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)構造体の終了位置が入力されます。 この情報が必要でない場合は、この引数を null 値を設定します。

## <a name="return-value"></a>戻り値
成功した場合、返します`S_OK`、それ以外のエラー コードを返します。

## <a name="remarks"></a>Remarks
ステートメントの範囲は、このドキュメントのコンテキストを参照するコードの原因である行の範囲です。

このドキュメントのコンテキスト内でソース コード (コメントを含む) の範囲を取得する呼び出し、 [GetSourceRange](../../../extensibility/debugger/reference/idebugdocumentcontext2-getsourcerange.md)メソッド。

## <a name="example"></a>例
次の例は、単純なは、このメソッドを実装する方法を示しています。`CDebugContext`を公開するオブジェクト、 [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)インターフェイス。 この例は、開始位置、null 値でない場合にのみ、終了位置に格納します。

```cpp
HRESULT CDebugContext::GetStatementRange(TEXT_POSITION* pBegPosition,
                                         TEXT_POSITION* pEndPosition)
{
    HRESULT hr;

    // Check for a valid beginning position argument pointer.
    if (pBegPosition)
    {
        // Copy the member TEXT_POSITION into the local pBegPosition.
        memcpy(pBegPosition, &m_pos, sizeof (TEXT_POSITION));

        // Check for a valid ending position argument pointer.
        if (pEndPosition)
        {
            // Copy the member TEXT_POSITION into the local pEndPosition.
            memcpy(pEndPosition, &m_pos, sizeof (TEXT_POSITION));
        }
        hr = S_OK;
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
- [GetSourceRange](../../../extensibility/debugger/reference/idebugdocumentcontext2-getsourcerange.md)
- [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)
