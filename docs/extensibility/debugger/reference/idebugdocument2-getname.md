---
title: IDebugDocument2::GetName |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocument2::GetName
helpviewer_keywords:
- IDebugDocument2::GetName
ms.assetid: 6f09ff09-b0cf-4472-8fc8-143991f0ceb1
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 3f1ef243afd607a565e2c7a8e6f557f0b9906c86
ms.sourcegitcommit: b0d8e61745f67bd1f7ecf7fe080a0fe73ac6a181
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/22/2019
ms.locfileid: "56701018"
---
# <a name="idebugdocument2getname"></a>IDebugDocument2::GetName
いくつかの形式のいずれかで、ドキュメントの名前を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetName( 
   GETNAME_TYPE gnType,
   BSTR*        pbstrFileName
);
```

```csharp
int GetName( 
   enum_GETNAME_TYPE gnType,
   out string        pbstrFileName
);
```

#### <a name="parameters"></a>パラメーター
 `gnType`

 [in]値、 [GETNAME_TYPE](../../../extensibility/debugger/reference/getname-type.md)返す名の種類を決定する列挙型。

 `pbstrFileName`

 [out]ドキュメント名を含む文字列を返します。

## <a name="return-value"></a>戻り値
 成功した場合、返します`S_OK`、それ以外のエラー コードを返します。

## <a name="remarks"></a>Remarks
 このメソッドは、タイトル、またはファイル名またはファイル名の偶数の一部として、ドキュメントの名前を返すなどのことができます。

## <a name="see-also"></a>関連項目
- [IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)
- [GETNAME_TYPE](../../../extensibility/debugger/reference/getname-type.md)