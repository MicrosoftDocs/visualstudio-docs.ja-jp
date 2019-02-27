---
title: EndTrackingContext | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
api_name:
- EndTrackingContext
api_location:
- filetracker.dll
api_type:
- COM
helpviewer_keywords:
- EndTrackingContext
ms.assetid: c2c5d794-8dc8-4594-8717-70dc79a0e75d
caps.latest.revision: 7
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 5c31753d5e5155156006d67d621490a8b2c4077a
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "54772417"
---
# <a name="endtrackingcontext"></a>EndTrackingContext
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
現在のコンテキストの追跡を終了します。  
  
## <a name="syntax"></a>構文  
  
```  
HRESULT WINAPI EndTrackingContext();  
```  
  
## <a name="return-value"></a>戻り値  
 コンテキストの追跡が終了した場合、[HRESULT](<!-- TODO: review code entity reference <xref:assetId:///HRESULT?qualifyHint=False&amp;autoUpgrade=True>  -->) に [SUCCEEDED](<!-- TODO: review code entity reference <xref:assetId:///SUCCEEDED?qualifyHint=False&amp;autoUpgrade=True>  -->) ビットが設定されます。  
  
## <a name="requirements"></a>要件  
 **ヘッダー:** FileTracker.h  
  
## <a name="see-also"></a>関連項目  
 [StartTrackingContext](../msbuild/starttrackingcontext.md)
