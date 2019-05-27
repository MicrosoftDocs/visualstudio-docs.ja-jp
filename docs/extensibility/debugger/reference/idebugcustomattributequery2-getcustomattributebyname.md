---
title: IDebugCustomAttributeQuery2::GetCustomAttributeByName |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCustomAttributeQuery2::GetCustomAttributeByName
helpviewer_keywords:
- IDebugCustomAttributeQuery2::GetCustomAttributeByName
ms.assetid: 7428dfeb-8929-41b2-9b99-cb343a86c02d
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 780f1c357ef4c8f8a8114689e7495f7882af9723
ms.sourcegitcommit: 19ec963ed6d585719cb83ba677434ea6580e0d1f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66205204"
---
# <a name="idebugcustomattributequery2getcustomattributebyname"></a>IDebugCustomAttributeQuery2::GetCustomAttributeByName
カスタム属性の名前を指定されたカスタム属性のバイト数を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetCustomAttributeByName( 
   LPCOLESTR pszCustomAttributeName,
   BYTE*     ppBlob,
   DWORD*    pdwLen
);
```

```csharp
int GetCustomAttributeByName(
   [In] string        pszCustomAttributeName,
   [In, Out] byte[]   ppBlob,
   [In, Out] ref uint pdwLen
);
```

## <a name="parameters"></a>パラメーター
`pszCustomAttributeName`\
[in]検索するカスタム属性の名前を含む文字列。

`ppBlob`\
[入力、出力]カスタム属性データが入力する配列。

`pdwLen`\
[入力、出力]返されるバイトの最大数を指定します、`ppBlob`配列し、配列に実際に書き込まれたバイト数を返します。

## <a name="return-value"></a>戻り値
 成功した場合は S_OK を返します。 または、カスタム属性が存在しない場合は S_FALSE を返します。 それ以外の場合はエラー コードを返します。

## <a name="remarks"></a>Remarks
 設定、`ppBlob`属性の使用可能なバイトをパラメーターに null 値の数を取得します。 配列を割り当てるしでは、その配列を渡す、`ppBlob`パラメーター。

 属性のバイトは、カスタム属性の生データを表します。

 場合、`ppBlob`と`pdwLen`パラメーターが null 値に設定されて、このメソッドは、カスタム属性の存在だけ確認に使用できます。 呼び出すことです、簡単に別の方法、 [IsCustomAttributeDefined](../../../extensibility/debugger/reference/idebugcustomattributequery2-iscustomattributedefined.md)メソッド。

## <a name="see-also"></a>関連項目
- [IDebugCustomAttributeQuery2](../../../extensibility/debugger/reference/idebugcustomattributequery2.md)
- [IsCustomAttributeDefined](../../../extensibility/debugger/reference/idebugcustomattributequery2-iscustomattributedefined.md)