---
description: このスレッドのスタック フレームのリストを取得します。
title: IDebugThread2::EnumFrameInfo | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugThread2::EnumFrameInfo
helpviewer_keywords:
- IDebugThread2::EnumFrameInfo
ms.assetid: 17914a71-10ea-4b6f-8982-e364f87dca53
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 7a47371bf9af89ef3f185698ca25a9df99cad4c6
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105053075"
---
# <a name="idebugthread2enumframeinfo"></a>IDebugThread2::EnumFrameInfo
このスレッドのスタック フレームのリストを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT EnumFrameInfo ( 
   FRAMEINFO_FLAGS        dwFieldSpec,
   UINT                   nRadix,
   IEnumDebugFrameInfo2** ppEnum
);
```

```csharp
int EnumFrameInfo ( 
   enum_FRAMEINFO_FLAGS     dwFieldSpec,
   uint                     nRadix,
   out IEnumDebugFrameInfo2 ppEnum
);
```

## <a name="parameters"></a>パラメーター
`dwFieldSpec`\
[入力] [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md) 構造体の入力するフィールドを指定する [FRAMEINFO_FLAGS](../../../extensibility/debugger/reference/frameinfo-flags.md) 列挙からのフラグの組み合わせ。関数名を 1 つの文字列に書式設定するには、`FIF_FUNCNAME_FORMAT` フラグを指定します。

`nRadix`\
[入力] 列挙子の数値情報の書式設定に使用される基数。

`ppEnum`\
[出力] スタック フレームを記述した [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md) 構造体のリストを格納している [IEnumDebugFrameInfo2](../../../extensibility/debugger/reference/ienumdebugframeinfo2.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 スレッドのフレームは順番に列挙され、現在のフレームが最初に列挙され、最も古いフレームが最後に列挙されます。

## <a name="see-also"></a>関連項目
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [FRAMEINFO_FLAGS](../../../extensibility/debugger/reference/frameinfo-flags.md)
- [IEnumDebugFrameInfo2](../../../extensibility/debugger/reference/ienumdebugframeinfo2.md)
- [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)
