---
description: 現在のドキュメント位置の範囲を取得します。
title: IDebugDocumentPositionOffset2::GetRange | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugDocumentPositionOffset2::GetRange
ms.assetid: 27da7130-0932-4f97-abde-05e6fb018606
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 66184ba67dd0623a886ca37e28d311aebc6633bd
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105066348"
---
# <a name="idebugdocumentpositionoffset2getrange"></a>IDebugDocumentPositionOffset2::GetRange
現在のドキュメント位置の範囲を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetRange(
   DWORD* pdwBegOffset,
   DWORD* pdwEndOffset
);
```

```csharp
public int GetRange(
   ref uint pdwBegOffset,
   ref uint pdwEndOffset
);
```

## <a name="parameters"></a>パラメーター
`pdwBegOffset`\
[入力、出力] 範囲の開始位置のオフセット。 この情報が不要な場合は、このパラメーターを null 値に設定します。

`pdwEndOffset`\
[入力、出力] 範囲の終了位置のオフセット。 この情報が不要な場合は、このパラメーターを null 値に設定します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 ドキュメント位置内で位置ブレークポイントのために指定された範囲は、実際にコードを構成するステートメントを事前に検索するために、デバッグ エンジン (DE) によって使用されます。 次に例を示します。

```
Line 5: // comment
Line 6: x = 1;
```

 行 5 は、デバッグ中のプログラムのコードを構成しません。 5 行目にブレークポイントを設定するデバッガーで、コードを構成する最初の行を特定の分量のコードから DE に前方検索させたい場合、デバッガーでは、ブレークポイントが正しく配置される可能性がある追加の候補行を含む範囲を指定します。 DE はその後、ブレークポイントの受け入れが可能な行が見つかるまで、それらの行を前方検索します。

## <a name="see-also"></a>関連項目
- [IDebugDocumentPositionOffset2](../../../extensibility/debugger/reference/idebugdocumentpositionoffset2.md)
- [GetRange](../../../extensibility/debugger/reference/idebugdocumentposition2-getrange.md)
