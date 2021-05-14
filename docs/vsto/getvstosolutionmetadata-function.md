---
title: GetVstoSolutionMetadata 関数
description: GetVstoSolutionMetadata API が Office インフラストラクチャをサポートする仕組みと、独自のコードから直接使用することが意図されていないことを説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: eaf58f312afd379fb1f16d208c323777ec725231
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99860608"
---
# <a name="getvstosolutionmetadata-function"></a>GetVstoSolutionMetadata 関数
  この API は、Office インフラストラクチャをサポートします。独自のたコードから直接使用するためのものではありません。

## <a name="syntax"></a>構文

```csharp
HRESULT WINAPI GetVstoSolutionMetadata(
    LPCWSTR lpwszSolutionMetadataKey,
    ISolutionMetadata** ppSolutionInfo
);
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------------|-----------------|
|*lpwszSolutionMetadataKey*|使用しないでください。|
|*ppSolutionInfo*|使用しないでください。|

## <a name="return-value"></a>戻り値
 関数が成功した場合は、**S_OK** を返します。 関数が失敗した場合はエラー コードを返します。
