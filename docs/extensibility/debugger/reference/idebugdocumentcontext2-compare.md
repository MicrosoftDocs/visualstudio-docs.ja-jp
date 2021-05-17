---
description: このドキュメント コンテキストを、指定されたドキュメント コンテキストの配列と比較します。
title: IDebugDocumentContext2::Compare | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocumentContext2::Compare
helpviewer_keywords:
- IDebugDocumentContext2::Compare
ms.assetid: 2327b1ba-52d0-42fb-a01e-63cb4b332d2f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a680da6f33d3da37995eb26071c0ea5f1ddc2283
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105066712"
---
# <a name="idebugdocumentcontext2compare"></a>IDebugDocumentContext2::Compare
このドキュメント コンテキストを、指定されたドキュメント コンテキストの配列と比較します。

## <a name="syntax"></a>構文

```cpp
HRESULT Compare( 
   DOCCONTEXT_COMPARE       compare,
   IDebugDocumentContext2** rgpDocContextSet,
   DWORD                    dwDocContextSetLen,
   DWORD*                   pdwDocContext
);
```

```csharp
int Compare( 
   enum_ DOCCONTEXT_COMPARE compare,
   IDebugDocumentContext2[] rgpDocContextSet,
   uint                     dwDocContextSetLen,
   out uint                 pdwDocContext
);
```

## <a name="parameters"></a>パラメーター
`compare`\
[入力] 比較の種類を指定する [DOCCONTEXT_COMPARE](../../../extensibility/debugger/reference/doccontext-compare.md) 列挙型の値。

`rgpDocContextSet`\
[入力] 比較対象のドキュメント コンテキストを表す [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md) オブジェクトの配列。

`dwDocContextSetLen`\
[入力] 比較するドキュメント コンテキストの配列の長さ。

`pdwDocContext`\
[出力] 比較を満たす最初のドキュメント コンテキストの `rgpDocContextSet` 配列のインデックスを返します。

## <a name="return-value"></a>戻り値
 一致が見つかった場合は、`S_OK` を返します。 一致が見つからなかった場合は、`S_FALSE` を返します。 それ以外の場合はエラー コードを返します。

## <a name="remarks"></a>解説
 配列で渡される [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md) オブジェクトは、呼び出し中の `IDebugDocumentContext2` オブジェクトを実装するものと同じデバッグ エンジンによって実装されている必要があります。そうでない場合、比較は無効になります。

## <a name="see-also"></a>関連項目
- [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)
- [DOCCONTEXT_COMPARE](../../../extensibility/debugger/reference/doccontext-compare.md)
