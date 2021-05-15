---
description: ソースのファイル名を取得します。
title: IDiaInjectedSource::get_filename | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaInjectedSource::get_filename method
ms.assetid: 20f4fc68-335a-4971-b3a6-76501f0e8b19
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: e41b7d3b80f2e0f63a53fb9a0d6d63627af59d75
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634416"
---
# <a name="idiainjectedsourceget_filename"></a>IDiaInjectedSource::get_filename
ソースのファイル名を取得します。

## <a name="syntax"></a>構文

```C++
HRESULT get_filename ( 
   BSTR* pRetVal
);
```

#### <a name="parameters"></a>パラメーター
 pRetVal

[out] ソースのファイル名を返します。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。 このプロパティがサポートされていない場合は、`S_FALSE` を返します。 それ以外の場合はエラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDiaInjectedSource](../../debugger/debug-interface-access/idiainjectedsource.md)
