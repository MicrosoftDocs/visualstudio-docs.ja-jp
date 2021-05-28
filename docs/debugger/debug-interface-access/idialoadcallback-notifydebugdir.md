---
description: .exe ファイル内でデバッグ ディレクトリが見つかったときに呼び出されます。
title: IDiaLoadCallback::NotifyDebugDir | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaLoadCallback::NotifyDebugDir method
ms.assetid: bd04e2f6-0dbf-4742-a556-96f2cd99aa19
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: ed83b79dea8f488be79a2161968876c9aa2a9a11
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634395"
---
# <a name="idialoadcallbacknotifydebugdir"></a>IDiaLoadCallback::NotifyDebugDir
.exe ファイル内でデバッグ ディレクトリが見つかったときに呼び出されます。

## <a name="syntax"></a>構文

```C++
HRESULT NotifyDebugDir ( 
   BOOL  fExecutable,
   DWORD cbData,
   BYTE  data[]
);
```

#### <a name="parameters"></a>パラメーター
 `fExecutable`

[in] デバッグ ディレクトリが、.dbg ファイルからではなく、実行可能ファイルから読み取られる場合は `TRUE`。

 `cbData`

[in] デバッグ ディレクトリ内のデータのバイト数。

 `data[]`

[in] デバッグ ディレクトリが格納される配列。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。 リターン コードは、通常無視されます。

## <a name="remarks"></a>解説
 [IDiaDataSource::loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md) メソッドは、実行可能ファイルの処理中にデバッグ ディレクトリを検出すると、このコールバックを呼び出します。

 このメソッドを使用すると、.pdb ファイルに存在しないデバッグ情報をサポートするために、クライアントで実行可能ファイルやデバッグ ファイルをリバース エンジニアリングする必要がなくなります。 このデータがあれば、クライアントは利用可能なデバッグ情報の種類を把握し、その情報が実行可能ファイルと dbg ファイルのどちらに存在するかを認識できます。

 `IDiaDataSource::loadDataForExe` メソッドは、シンボルでの必要性に応じて .pdb と dbg の両方のファイルを透過的に開くので、ほとんどのクライアントでは、このコールバックは必要になりません。

## <a name="see-also"></a>こちらもご覧ください
- [IDiaLoadCallback2](../../debugger/debug-interface-access/idialoadcallback2.md)
- [IDiaDataSource::loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)
