---
title: IDebugDocumentPosition2::GetRange |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocumentPosition2::GetRange
helpviewer_keywords:
- IDebugDocumentPosition2::GetRange
ms.assetid: 91a06ee7-253a-4215-be22-04bf57305aa8
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c67828e2d9e1cb0c75d272b57e7c6b610a84fdd5
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66326470"
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
[入力、出力]A [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)構造体の開始位置が入力されます。 この情報が必要でない場合は、この引数を null 値を設定します。

`pEndPosition`\
[入力、出力]A [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)構造体の終了位置が入力されます。 この情報が必要でない場合は、この引数を null 値を設定します。

## <a name="return-value"></a>戻り値
 成功した場合、返します`S_OK`、それ以外のエラー コードを返します。

## <a name="remarks"></a>Remarks
 ブレークポイントの場所のドキュメントの位置で指定された範囲は、コードを実際に貢献するステートメントを前方に検索するデバッグ エンジン (DE) によって使用されます。 次に例を示します。

```
Line 5: // comment
Line 6: x = 1;
```

 5 行目でコードをデバッグ中のプログラムは使用されません。 5 行目で、ブレークポイントを設定します。 デバッガーは、DE、一定量のコードを提供する最初の行を前方に検索する必要がある場合、デバッガーはブレークポイントを正しく配置可能性があります、その他の候補行が含まれている範囲を指定します。 DE、し、前方に検索を通じてこれらの行ブレークポイントを受け入れることができる行が見つかるまで。

## <a name="see-also"></a>関連項目
- [IDebugDocumentPosition2](../../../extensibility/debugger/reference/idebugdocumentposition2.md)
- [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)