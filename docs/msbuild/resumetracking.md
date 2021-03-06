---
title: ResumeTracking | Microsoft Docs
description: 現在のコンテキストでの追跡を再開する MSBuild ResumeTracking の構文、要件、および戻り値について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
apiname:
- ResumeTracking
apilocation:
- filetracker.dll
apitype: COM
helpviewer_keywords:
- ResumeTracking
ms.assetid: d637e019-7c50-4b0a-812e-bc822001e697
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: fd6722ca0b930d66a386732dac466a8e4fe36976
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99937915"
---
# <a name="resumetracking"></a>ResumeTracking

現在のコンテキストで追跡を再開します。

## <a name="syntax"></a>構文

```cpp
HRESULT WINAPI ResumeTracking();
```

## <a name="return-value"></a>戻り値

 追跡が再開された場合、**HRESULT** に **SUCCEEDED** ビットが設定されます。 コンテキストが利用できず、追跡を再開できない場合、**E_FAIL** が返されます。

## <a name="requirements"></a>必要条件

 **ヘッダー:** *FileTracker.h*

## <a name="see-also"></a>関連項目

- [SuspendTracking](../msbuild/suspendtracking.md)