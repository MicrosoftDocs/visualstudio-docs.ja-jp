---
description: このコード コンテキストに対応するドキュメント コンテキストを取得します。
title: IDebugCodeContext2::GetDocumentContext | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCodeContext2::GetDocumentContext
helpviewer_keywords:
- IDebugCodeContext2::GetDocumentContext
ms.assetid: d552cc92-963f-43c1-949f-ae6b63a427b8
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 80420f12369ef038c2faccb51c9b1bfc9b0073a4
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105088420"
---
# <a name="idebugcodecontext2getdocumentcontext"></a>IDebugCodeContext2::GetDocumentContext
このコード コンテキストに対応するドキュメント コンテキストを取得します。 ドキュメント コンテキストは、この命令を生成したソース コードに対応するソース ファイル内の位置を表します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetDocumentContext( 
   IDebugDocumentContext2** ppSrcCxt
);
```

```csharp
int GetDocumentContext( 
   out IDebugDocumentContext2 ppSrcCxt
);
```

## <a name="parameters"></a>パラメーター
`ppSrcCxt`\
[出力] コード コンテキストに対応する [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md) オブジェクトを返します。 `S_OK` が返された場合、これは `null` 以外である必要があります。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。 コード コンテキストにソース位置が関連付けられていない場合など、`out` パラメーターが `null` の場合、デバッグ エンジンは `E_FAIL` などの失敗コードを返す必要があります。

## <a name="remarks"></a>解説
 一般に、コード コンテキストは実行ストリーム内のコード命令の位置であるのに対し、ドキュメント コンテキストはソース ファイル内の位置と考えることができます。

## <a name="see-also"></a>関連項目
- [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)
- [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)
