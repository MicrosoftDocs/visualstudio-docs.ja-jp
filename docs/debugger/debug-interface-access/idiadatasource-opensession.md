---
description: シンボルのクエリを実行するためのセッションを開きます。
title: IDiaDataSource::openSession | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaDataSource::openSession method
ms.assetid: a3319ed0-3979-483b-9852-c0af96852c48
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: d31e30c2044332d1e299d6a734ee5fecb22ec686
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634980"
---
# <a name="idiadatasourceopensession"></a>IDiaDataSource::openSession
シンボルのクエリを実行するためのセッションを開きます。

## <a name="syntax"></a>構文

```C++
HRESULT openSession ( 
   IDiaSession** ppSession
);
```

#### <a name="parameters"></a>パラメーター
ppSession

[出力] 開いているセッションを表す [IDiaSession](../../debugger/debug-interface-access/idiasession.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。 次の表に、このメソッドで返される可能性のある戻り値を示します。

|値|説明|
|-----------|-----------------|
|E_UNEXPECTED|[IDiaDataSource](../../debugger/debug-interface-access/idiadatasource.md) オブジェクトは、以前にシンボルのソースで初期化されていません。|
|E_INVALIDARG|無効な `ppSession` パラメーター。|
|E_OUTOFMEMORY|セッションを開くためのメモリが不足しています。|

## <a name="remarks"></a>解説
このメソッドは、データ ソースの [IDiaSession](../../debugger/debug-interface-access/idiasession.md) オブジェクトを開きます。

`IDiaSession` オブジェクトは、データ ソースへのクエリを実装します。 セッションでは、デバッグ シンボルのセットごとに 1 つのアドレス空間を管理します。 データ ソース シンボルが示す .exe または .dll ファイルが複数のアドレス範囲でアクティブな場合は (複数のプロセスで読み込まれている場合など)、アドレス範囲ごとに 1 つのセッションを使用する必要があります。

## <a name="example"></a>例

```C++
IDiaSession* pSession;
HRESULT hr = pSource->openSession( &pSession );
if (FAILED(hr))
{
   // report error
}
```

## <a name="see-also"></a>関連項目
- [IDiaDataSource](../../debugger/debug-interface-access/idiadatasource.md)
- [概要](../../debugger/debug-interface-access/overview-debug-interface-access-sdk.md)
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [.Pdb ファイルの照会](../../debugger/debug-interface-access/querying-the-dot-pdb-file.md)
