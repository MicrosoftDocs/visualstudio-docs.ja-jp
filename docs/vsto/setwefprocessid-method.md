---
title: SetWefProcessId メソッド
description: SetWefProcessId メソッドが Web Extensions Framework (WEF) コンテンツを実行するプロセス識別子をどのように提供するかについて説明します。
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
ms.openlocfilehash: 9c3d745f14185d46dce08d46b8c56391b108627d
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99882409"
---
# <a name="setwefprocessid-method"></a>SetWefProcessId メソッド
  Web Extensions Framework (WEF) コンテンツを実行するプロセス識別子を提供します。

## <a name="syntax"></a>構文

```csharp
HRESULT SetWefProcessId(
    [in] DWORD dwProcessId
);
```

#### <a name="parameters"></a>パラメーター

|パラメーター|Description|
|---------------|-----------------|
|*dwProcessId*|WEF コンテンツを実行するために使用されるプロセス識別子。|

## <a name="return-value"></a>戻り値
 メソッドが正常に完了したかどうかを示す HRESULT 値。

## <a name="remarks"></a>解説
 このメソッドは、WEF コンテンツプロセスを作成した後、WEF コンテンツを実行する前に呼び出す必要があります。

 開発環境で、WEF コンテンツプロセスにデバッガーをアタッチする場合は、このメソッドの実装でこの操作を実行する必要があります。
