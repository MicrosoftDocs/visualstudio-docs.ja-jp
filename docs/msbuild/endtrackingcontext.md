---
title: EndTrackingContext | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
apiname:
- EndTrackingContext
apilocation:
- filetracker.dll
apitype: COM
helpviewer_keywords:
- EndTrackingContext
ms.assetid: c2c5d794-8dc8-4594-8717-70dc79a0e75d
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b7f837e7a983d0f2c2520d7e379ffb49f332c75c
ms.sourcegitcommit: d0425b6b7d4b99e17ca6ac0671282bc718f80910
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/21/2019
ms.locfileid: "56609983"
---
# <a name="endtrackingcontext"></a>EndTrackingContext
現在のコンテキストの追跡を終了します。

## <a name="syntax"></a>構文

```cpp
HRESULT WINAPI EndTrackingContext();
```

## <a name="return-value"></a>戻り値
コンテキストの追跡が終了した場合、**HRESULT** に **SUCCEEDED** ビットが設定されます。

## <a name="requirements"></a>要件
**ヘッダー:***FileTracker.h*

## <a name="see-also"></a>関連項目
- [StartTrackingContext](../msbuild/starttrackingcontext.md)
