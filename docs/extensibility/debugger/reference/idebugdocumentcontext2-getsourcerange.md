---
description: このドキュメント コンテキストのソース コードの範囲を取得します。
title: IDebugDocumentContext2::GetSourceRange | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocumentContext2::GetSourceRange
helpviewer_keywords:
- IDebugDocumentContext2::GetSourceRange
ms.assetid: 5903c75e-5390-4d13-9314-1ee276255313
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a66f1b99793b1c8fa8036771d7815f95a395462a
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105066595"
---
# <a name="idebugdocumentcontext2getsourcerange"></a>IDebugDocumentContext2::GetSourceRange
このドキュメント コンテキストのソース コードの範囲を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetSourceRange( 
   TEXT_POSITION* pBegPosition,
   TEXT_POSITION* pEndPosition
);
```

```csharp
int GetSourceRange( 
   TEXT_POSITION[] pBegPosition,
   TEXT_POSITION[] pEndPosition
);
```

## <a name="parameters"></a>パラメーター
`pBegPosition`\
[入力、出力] 開始位置が入力される [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md) 構造体。 この情報が不要な場合は、この引数を null 値に設定します。

`pEndPosition`\
[入力、出力] 終了位置が入力される [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md) 構造体。 この情報が不要な場合は、この引数を null 値に設定します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 ソース範囲は、現在のステートメントからさかのぼって、コードを構成していた前のステートメントの直後にまで及ぶ、ソース コードの範囲全体です。 ソース範囲は通常、コメントを含むソース ステートメントを、逆アセンブリ ウィンドウ内のコードと混在させるために使用されます。

 このドキュメント コンテキスト内に含まれるコード ステートメントのみの範囲を取得するには、[GetStatementRange](../../../extensibility/debugger/reference/idebugdocumentcontext2-getstatementrange.md) メソッドを呼び出します。

## <a name="see-also"></a>関連項目
- [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)
- [GetStatementRange](../../../extensibility/debugger/reference/idebugdocumentcontext2-getstatementrange.md)
- [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)
