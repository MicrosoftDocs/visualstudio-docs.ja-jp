---
description: この関数では、ソース管理プラグインによってサポートされているソース管理プラグイン API のバージョン番号を取得します。
title: SccGetVersion 関数 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccGetVersion
helpviewer_keywords:
- SccGetVersion function
ms.assetid: a6e786bf-744e-4272-9e21-0be44d23b1a1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: f49d33ebe70390a364d0ae8336e7f69549b6876f
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112901085"
---
# <a name="sccgetversion-function"></a>SccGetVersion 関数
この関数では、ソース管理プラグインによってサポートされているソース管理プラグイン API のバージョン番号を取得します。

## <a name="syntax"></a>構文

```cpp
LONG SccGetVersion(void);
```

#### <a name="parameters"></a>パラメーター
 [なし] :

## <a name="return-value"></a>戻り値
 サポートされているソース管理プラグイン API のバージョン番号を含む `LONG` データ型。

|WORD|説明|
|----------|-----------------|
|HIWORD|メジャー バージョン|
|LOWORD|マイナー バージョン|

## <a name="remarks"></a>解説
 たとえば、ソース管理プラグインでバージョン 1.3 のソース管理プラグイン API がサポートされている場合、この関数からは 0x0103 が返されます。

## <a name="see-also"></a>関連項目
- [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)
