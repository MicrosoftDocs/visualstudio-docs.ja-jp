---
title: CvInitProvider 関数 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- cvmarkers/CvInitProvider
helpviewer_keywords:
- CvInitProvider method
ms.assetid: ba1863ad-e35f-4d34-a2f2-5e68957d1915
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a97be63cd782397e984fd8dbce7da844efa07540
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62552668"
---
# <a name="cvinitprovider-function"></a>CvInitProvider 関数
マーカー プロバイダーを初期化します。 他のコンカレンシー ビジュアライザー SDK 関数の前に呼び出す必要があります。

## <a name="syntax"></a>構文

```C
HRESULT CvInitProvider(
   _In_ const GUID* pGuid,
   _Out_ PCV_PROVIDER* ppProvider
);
```

#### <a name="parameters"></a>パラメーター
 `pGuid` プロバイダ GUID。 Nll は指定できません。

 `ppProvider` プロバイダー コンテキストを格納する出力変数のアドレス。 Nll は指定できません。

## <a name="return-value"></a>戻り値
 プロバイダーが初期化されると S_OK を、エラーが発生した場合はエラー コードを返します。 SUCCEEDED/FAILED マクロを使用し、エラーの状態を確認します。

## <a name="requirements"></a>要件
 **ヘッダー:** *cvmarkers.h*

## <a name="see-also"></a>関連項目
- [C++ ライブラリ リファレンス](../profiling/cpp-library-reference.md)