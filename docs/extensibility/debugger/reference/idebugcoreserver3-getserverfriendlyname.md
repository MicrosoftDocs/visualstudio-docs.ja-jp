---
title: IDebugCoreServer3::GetServerFriendlyName |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCoreServer3::GetServerFriendlyName
helpviewer_keywords:
- IDebugCoreServer3::GetServerFriendlyName
ms.assetid: 7035b904-b3d7-4d9b-98d9-65714b8a8b9f
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f70e8301b6a44397d351345fe3cb8fe0c3d3426e
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63414031"
---
# <a name="idebugcoreserver3getserverfriendlyname"></a>IDebugCoreServer3::GetServerFriendlyName
サーバーのフレンドリ名を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetServerFriendlyName(
   BSTR* pbstrName
);
```

```csharp
int GetServerFriendlyName(
   out string pbstrName
);
```

#### <a name="parameters"></a>パラメーター
 `pbstrName`

 [out]サーバーのフレンドリ名を返します。

> [!NOTE]
> 呼び出し元は、文字列を解放します。

## <a name="return-value"></a>戻り値
 成功した場合、返します`S_OK`、それ以外のエラー コードを返します。

## <a name="remarks"></a>Remarks
 サーバーのユーザーにリリースされた、このメソッドによって返される名前は、サーバーの完全名です。 サーバーの自動起動の名前は、マシンのサーバーが実行されていることします。

 コンピューター対象の名前では、呼び出し、 [GetServerName](../../../extensibility/debugger/reference/idebugcoreserver3-getservername.md)メソッド。

## <a name="see-also"></a>関連項目
- [IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md)
- [GetServerName](../../../extensibility/debugger/reference/idebugcoreserver3-getservername.md)