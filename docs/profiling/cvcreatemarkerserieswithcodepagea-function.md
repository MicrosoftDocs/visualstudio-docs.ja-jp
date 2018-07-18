---
title: CvCreateMarkerSeriesWithCodePageA 関数 | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- cvmakers/CvCreateMarkerSeriesWithCodePageA
helpviewer_keywords:
- CvCreateMarkerSeriesWithCodePageA method
ms.assetid: 3d7ed601-2222-4be9-a557-f217db008753
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 63fe3de8c4322e378f110813ac93fa523f3453ba
ms.sourcegitcommit: 58052c29fc61c9a1ca55a64a63a7fdcde34668a4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2018
ms.locfileid: "34750377"
---
# <a name="cvcreatemarkerserieswithcodepagea-function"></a>CvCreateMarkerSeriesWithCodePageA 関数
指定されたプロバイダーとコード ページに対してマーカー系列を作成します。 この関数を利用し、マーカー API ANSI 関数で書き出されたテキストに対してコード ページを明示的に指定できます。 コード ページを設定することは、ロケールや言語が異なる別のコンピューターでトレースを記録し、解析するときに役立ちます。 既定では、GetACP() 関数により返されるコード ページが使用されます。  
  
## <a name="syntax"></a>構文  
  
```C  
HRESULT CvCreateMarkerSeriesWithCodePageA(  
   _In_ PCV_PROVIDER pProvider,  
   _In_ LPCSTR pSeriesName,  
   _In_ UINT nTextCodePage,  
   _Out_ PCV_MARKERSERIES* ppMarkerSeries  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pProvider`  
 CvInitProvider により以前に初期化されたプロバイダー オブジェクト。 Nll は指定できません。  
  
 `pSeriesName`  
 マーカー系列名。 NULL は指定できませんが、空の文字列は指定できます。  
  
 `nTextCodePage`  
 有効なコード ページ。  
  
 `ppMarkerSeries`  
 マーカー系列コンテキストを格納する出力変数のアドレス。 Nll は指定できません。  
  
## <a name="return-value"></a>戻り値  
 マーカー系列が作成されると S_OK を、エラーが発生した場合はエラー コードを返します。 SUCCEEDED/FAILED マクロを使用し、エラーの状態を確認します。  
  
## <a name="requirements"></a>必要条件  
 **ヘッダー:** *cvmarkers.h*  
  
## <a name="see-also"></a>関連項目  
 [C++ ライブラリ リファレンス](../profiling/cpp-library-reference.md)