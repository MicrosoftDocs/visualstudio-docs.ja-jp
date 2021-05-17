---
description: このドキュメントの位置の範囲を取得します。
title: IDebugDocumentPosition2::GetRange | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocumentPosition2::GetRange
helpviewer_keywords:
- IDebugDocumentPosition2::GetRange
ms.assetid: 91a06ee7-253a-4215-be22-04bf57305aa8
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 14aefb2e1ccc481a71cd32813f2ebf882834f12c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105066452"
---
# <a name="idebugdocumentposition2getrange"></a>IDebugDocumentPosition2::GetRange
このドキュメントの位置の範囲を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetRange( 
   TEXT_POSITION* pBegPosition,
   TEXT_POSITION* pEndPosition
);
```

```csharp
int GetRange( 
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
 ドキュメント位置内で位置ブレークポイントのために指定された範囲は、実際にコードを構成するステートメントを事前に検索するために、デバッグ エンジン (DE) によって使用されます。 次に例を示します。

```
Line 5: // comment
Line 6: x = 1;
```

 行 5 は、デバッグ中のプログラムのコードを構成しません。 5 行目にブレークポイントを設定するデバッガーで、コードを構成する最初の行を特定の分量のコードから DE に前方検索させたい場合、デバッガーでは、ブレークポイントが適切に配置される可能性がある追加の候補行を含む範囲を指定します。 DE はその後、ブレークポイントの受け入れが可能な行が見つかるまで、それらの行を前方検索します。

## <a name="see-also"></a>関連項目
- [IDebugDocumentPosition2](../../../extensibility/debugger/reference/idebugdocumentposition2.md)
- [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)
