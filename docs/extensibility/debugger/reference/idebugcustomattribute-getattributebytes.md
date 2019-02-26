---
title: IDebugCustomAttribute::GetAttributeBytes |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCustomAttribute::GetAttributeBytes
helpviewer_keywords:
- IDebugCustomAttribute::GetAttributeBytes
ms.assetid: cf34583b-6530-4dcc-89f8-eb27e4e8d594
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 188cc4e8b1c58a7fd8f9f1c99b8d5f544710ef8c
ms.sourcegitcommit: b0d8e61745f67bd1f7ecf7fe080a0fe73ac6a181
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/22/2019
ms.locfileid: "56711268"
---
# <a name="idebugcustomattributegetattributebytes"></a>IDebugCustomAttribute::GetAttributeBytes
バイトの blob として属性情報を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetAttributeBytes( 
   BYTE*  ppBlob,
   DWORD* pdwLen
);
```

```csharp
int GetAttributeBytes(
   ref byte[] ppBlob,
   ref uint   pdwLen
);
```

#### <a name="parameters"></a>パラメーター
 `ppBlob`

 [入力、出力]属性データが入力する配列。

 `pdwLen`

 [入力、出力]返されるバイトの最大数を指定します、`ppBlob`配列し、配列に実際に書き込まれたバイト数を返します。

## <a name="return-value"></a>戻り値
 成功した場合、S_OK を返します。それ以外の場合、エラー コードを返します。

## <a name="remarks"></a>Remarks
 設定、`ppBlob`属性の使用可能なバイトをパラメーターに null 値の数を取得します。 配列を割り当てるしでは、その配列を渡す、`ppBlob`パラメーター。

 属性のバイトは、カスタム属性の生データを表します。

## <a name="see-also"></a>関連項目
- [IDebugCustomAttribute](../../../extensibility/debugger/reference/idebugcustomattribute.md)