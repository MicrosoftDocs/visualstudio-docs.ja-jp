---
title: EnsureVSTOComponent 関数
description: EnsureVSTOComponent API は Office および SharePoint インフラストラクチャをサポートするしくみと、自分のコードから直接使用するためのものではないことを説明します。
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
ms.openlocfilehash: 17f52a469d93a843ef776c125e15a37db22277e8
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99910471"
---
# <a name="ensurevstocomponent-function"></a>EnsureVSTOComponent 関数
  この API は、Office インフラストラクチャをサポートします。独自に作成したコードから直接使用するためのものではありません。

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
 関数が成功した場合は、**S_OK** を返します。 関数が失敗した場合はエラー コードを返します。
