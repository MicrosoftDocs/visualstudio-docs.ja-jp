---
title: IDebugAlias2::GetAppDomainId |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- GetAppDomainId
- IDebugAlias2::GetAppDomainId
ms.assetid: 23581aaa-5a53-4859-b264-eca49fc44bcd
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 890e215c7e575e67a4360717851bab538966f419
ms.sourcegitcommit: b0d8e61745f67bd1f7ecf7fe080a0fe73ac6a181
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/22/2019
ms.locfileid: "56715051"
---
# <a name="idebugalias2getappdomainid"></a>IDebugAlias2::GetAppDomainId
アプリケーション ドメインの識別子を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetAppDomainId (
   ULONG32* pappDomainId
);
```

```csharp
int GetAppDomainId (
   out uint pappDomainId
);
```

#### <a name="parameters"></a>パラメーター
 `pappDomainId`

 [out]アプリケーション ドメインの識別子を返します。

## <a name="return-value"></a>戻り値
 成功した場合、返します`S_OK`、それ以外のエラー コードを返します。

## <a name="remarks"></a>Remarks
 アプリケーション ドメインの識別子変更、アプリケーションが再起動されるたびに、新しいアプリケーション ドメインが作成されます。

## <a name="see-also"></a>関連項目
- [IDebugAlias2](../../../extensibility/debugger/reference/idebugalias2.md)