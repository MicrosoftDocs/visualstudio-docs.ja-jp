---
title: IEnumDebugAddresses::Reset |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugAddresses::Reset
helpviewer_keywords:
- IEnumDebugAddresses::Reset method
ms.assetid: 3a9d7f20-5bc6-4e13-8e91-5af4092e092f
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9b470c52f7e8ecea4a8b46ec1dfa4b0353932068
ms.sourcegitcommit: 19ec963ed6d585719cb83ba677434ea6580e0d1f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66208598"
---
# <a name="ienumdebugaddressesreset"></a>IEnumDebugAddresses::Reset
このメソッドは、最初の要素を列挙型をリセットします。

## <a name="syntax"></a>構文

```cpp
HRESULT Reset(void);
```

```csharp
int Reset();
```

## <a name="parameters"></a>パラメーター
 なし

## <a name="return-value"></a>戻り値
 成功した場合、返します`S_OK`、それ以外のエラー コードを返します。

## <a name="remarks"></a>Remarks
 このメソッドが呼び出された後、次回の呼び出し[次](../../../extensibility/debugger/reference/ienumdebugaddresses-next.md)列挙体の最初の要素を返します。

## <a name="see-also"></a>関連項目
- [IEnumDebugAddresses](../../../extensibility/debugger/reference/ienumdebugaddresses.md)
- [次へ](../../../extensibility/debugger/reference/ienumdebugaddresses-next.md)