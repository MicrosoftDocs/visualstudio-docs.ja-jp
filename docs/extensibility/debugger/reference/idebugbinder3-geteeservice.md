---
description: このメソッドは、要求されたサービスを返します。
title: IDebugBinder3::GetEEService | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBinder3::GetEEService
helpviewer_keywords:
- IDebugBinder3::GetEEService method
ms.assetid: eb07aa40-8cd9-4a52-a4c7-4affd2307a01
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ccc4d28a06d87d7c17d16470e10f259657083cc9
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105094303"
---
# <a name="idebugbinder3geteeservice"></a>IDebugBinder3::GetEEService
このメソッドは、要求されたサービスを返します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetEEService(
   [in] GUID        vendor,
   [in] GUID        language,
   [in] GUID        iid,
   [out] IUnknown** ppService
);
```

```csharp
Int GetEEService(
   Guid       vendor,
   Guid       language,
   Guid       iid,
   out object ppService
);
```

## <a name="parameters"></a>パラメーター
`vendor`\
[入力] ベンダーの `GUID` (null 値は許容されます)。

`language`\
[入力] 言語の `GUID` (null 値は許容されます)。

`iid`\
[入力] 取得するサービスの `IID`。

`ppService`\
[出力] 要求されたサービスへのインターフェイス。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 [IEEVisualizerServiceProvider](../../../extensibility/debugger/reference/ieevisualizerserviceprovider.md) インターフェイスの `IID` (`IID_IEEVisualizerServiceProvider`) を渡して、型ビジュアライザー サービスが使用可能かどうかを確認します。 その場合、式エバリュエーターでは、型ビジュアライザーをサポートする [IEEVisualizerService](../../../extensibility/debugger/reference/ieevisualizerservice.md) インターフェイスを取得できます。 詳細については、「[データの視覚化と表示](../../../extensibility/debugger/visualizing-and-viewing-data.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [IDebugBinder3](../../../extensibility/debugger/reference/idebugbinder3.md)
- [IEEVisualizerServiceProvider](../../../extensibility/debugger/reference/ieevisualizerserviceprovider.md)
- [IEEVisualizerService](../../../extensibility/debugger/reference/ieevisualizerservice.md)
- [データの視覚化と表示](../../../extensibility/debugger/visualizing-and-viewing-data.md)
