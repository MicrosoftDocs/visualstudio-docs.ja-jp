---
description: カスタム属性の名前を指定して、カスタム属性バイトを取得します。
title: IDebugCustomAttributeQuery2::GetCustomAttributeByName | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCustomAttributeQuery2::GetCustomAttributeByName
helpviewer_keywords:
- IDebugCustomAttributeQuery2::GetCustomAttributeByName
ms.assetid: 7428dfeb-8929-41b2-9b99-cb343a86c02d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: dd8b1793bad585dd808ebd812b610cd68aabc129
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105077604"
---
# <a name="idebugcustomattributequery2getcustomattributebyname"></a>IDebugCustomAttributeQuery2::GetCustomAttributeByName
カスタム属性の名前を指定して、カスタム属性バイトを取得します。

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
[入力] 検索するカスタム属性の名前が格納されている文字列。

`ppBlob`\
[入力、出力] カスタム属性バイトが格納される配列。

`pdwLen`\
[入力、出力] `ppBlob` 配列で返す最大バイト数を指定し、実際に配列に書き込まれたバイト数を返します。

## <a name="return-value"></a>戻り値
 成功した場合は、S_OK を返します。カスタム属性が存在しない場合は、S_FALSE を返します。 それ以外の場合はエラー コードを返します。

## <a name="remarks"></a>解説
 `ppBlob` パラメーターを null 値に設定すると、使用可能な属性バイト数を返すことができます。 次に、配列を割り当て、その配列を `ppBlob` パラメーターに対して渡します。

 属性バイトは、カスタム属性の生データを表します。

 `ppBlob` および `pdwLen` パラメーターが null 値に設定されている場合、このメソッドを使用して、カスタム属性が単に存在するかどうかを判断できます。 ただし、より簡単な代替方法は、[IsCustomAttributeDefined](../../../extensibility/debugger/reference/idebugcustomattributequery2-iscustomattributedefined.md) メソッドを呼び出すことです。

## <a name="see-also"></a>関連項目
- [IDebugCustomAttributeQuery2](../../../extensibility/debugger/reference/idebugcustomattributequery2.md)
- [IsCustomAttributeDefined](../../../extensibility/debugger/reference/idebugcustomattributequery2-iscustomattributedefined.md)
