---
title: Idiadatasource::get_lasterror |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaDataSource::get_lastError method
ms.assetid: cf08850b-8b75-4e8c-90bd-bd0214756f99
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 34954cd32b350a7c5f9c176deffd9943f8e05100
ms.sourcegitcommit: d0425b6b7d4b99e17ca6ac0671282bc718f80910
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 02/21/2019
ms.locfileid: "56641391"
---
# <a name="idiadatasourcegetlasterror"></a>IDiaDataSource::get_lastError
最後の読み込みエラーのファイル名を取得します。

## <a name="syntax"></a>構文

```C++
HRESULT get_lastError (
   BSTR* pRetVal
);
```

#### <a name="parameters"></a>パラメーター
 pRetVal

[out]最後の読み込みエラーに関連付けられている .pdb ファイル名を含む文字列を返します。

## <a name="return-value"></a>戻り値
 読み込み操作による最後のエラー コードを返します。 返します`E_INVALIDARG`場合、`pRetVal`パラメーターが`NULL`します。

## <a name="example"></a>例

```C++
BSTR    fileName;
HRESULT errorCode = pSource->get_lastError( &fileName );
```

## <a name="see-also"></a>関連項目
- [IDiaDataSource](../../debugger/debug-interface-access/idiadatasource.md)