---
title: EnsureVSTOComponent 関数
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: f99ccb4cb76f942852716abf1fcb0c0f280decbd
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62797613"
---
# <a name="ensurevstocomponent-function"></a>EnsureVSTOComponent 関数
  この API は、オフィスのインフラストラクチャをサポートしているし、コードから直接使用するものではありません。

## <a name="syntax"></a>構文

```csharp
HRESULT EnsureVSTOComponent(
    IVSTProject *pProject
);
```

#### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------------|-----------------|
|*pProject*|使用しないでください。|

## <a name="return-value"></a>戻り値
 返します、関数が成功したかどうかは**S_OK**します。 関数が失敗した場合、エラー コードを返します。
