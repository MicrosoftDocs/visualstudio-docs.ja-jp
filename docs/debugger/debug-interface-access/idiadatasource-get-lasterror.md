---
description: 最後の読み込みエラーのファイル名を取得します。
title: IDiaDataSource::get_lastError | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaDataSource::get_lastError method
ms.assetid: cf08850b-8b75-4e8c-90bd-bd0214756f99
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 7edce9a2af6c849371360526d617d20738973cba
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634986"
---
# <a name="idiadatasourceget_lasterror"></a>IDiaDataSource::get_lastError
最後の読み込みエラーのファイル名を取得します。

## <a name="syntax"></a>構文

```C++
HRESULT get_lastError (
   BSTR* pRetVal
);
```

#### <a name="parameters"></a>パラメーター
 pRetVal

[出力] 最後の読み込みエラーに関連付けられた .pdb ファイル名を含む文字列を返します。

## <a name="return-value"></a>戻り値
 読み込み操作によって発生した最後のエラー コードを返します。 `pRetVal` パラメーターが `NULL` の場合は、`E_INVALIDARG` を返します。

## <a name="example"></a>例

```C++
BSTR    fileName;
HRESULT errorCode = pSource->get_lastError( &fileName );
```

## <a name="see-also"></a>関連項目
- [IDiaDataSource](../../debugger/debug-interface-access/idiadatasource.md)
