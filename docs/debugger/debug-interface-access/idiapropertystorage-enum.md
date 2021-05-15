---
description: このセット内のプロパティの列挙子を取得します。
title: IDiaPropertyStorage::Enum | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaPropertyStorage::Enum
ms.assetid: 00e462da-980a-40b3-a2d6-75a25ee809e5
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: d113107621c3254b86356202e94eac6e3e3a8c66
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634379"
---
# <a name="idiapropertystorageenum"></a>IDiaPropertyStorage::Enum
このセット内のプロパティの列挙子を取得します。

## <a name="syntax"></a>構文

```C++
HRESULT Enum ( 
   IEnumSTATPROPSTG** ppenum
);
```

#### <a name="parameters"></a>パラメーター
 `ppenum`

[out] プロパティの列挙体を表す`IEnumSTATPROPSTG` オブジェクト (Microsoft.VisualStudio.OLE.Interop 名前空間内) を返します。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDiaPropertyStorage](../../debugger/debug-interface-access/idiapropertystorage.md)
