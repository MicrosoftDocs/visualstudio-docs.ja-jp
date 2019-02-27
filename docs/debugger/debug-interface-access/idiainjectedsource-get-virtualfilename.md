---
title: Idiainjectedsource::get_virtualfilename |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaInjectedSource::get_virtualFilename method
ms.assetid: b9977075-8fd1-4b11-bfff-d87e9f2586dc
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4ad241532454cf1a086f8e85c4f2e16c29c76b26
ms.sourcegitcommit: d0425b6b7d4b99e17ca6ac0671282bc718f80910
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 02/21/2019
ms.locfileid: "56618654"
---
# <a name="idiainjectedsourcegetvirtualfilename"></a>IDiaInjectedSource::get_virtualFilename
ファイル以外のソース コードに与えられた名前を取得します。挿入されたコードは、します。

## <a name="syntax"></a>構文

```C++
HRESULT get_virtualFilename ( 
   BSTR* pRetVal
);
```

#### <a name="parameters"></a>パラメーター
 `pRetVal`

[out]挿入されたファイル以外のソース コードに与えられた名前を返します。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。 返します`S_FALSE`場合、このプロパティはサポートされていません。 それ以外の場合はエラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDiaInjectedSource](../../debugger/debug-interface-access/idiainjectedsource.md)