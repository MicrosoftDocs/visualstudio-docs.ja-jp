---
description: 指定されたプロパティを現在のプロパティ セットから読み取ります。
title: IDiaPropertyStorage::ReadMultiple | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaPropertyStorage::ReadMultiple
ms.assetid: 6ccc9397-ce41-4f72-b261-72ac252cd4a5
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: c7d0191d17074ec41b5fc73b3e33ba94b845a96e
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634375"
---
# <a name="idiapropertystoragereadmultiple"></a>IDiaPropertyStorage::ReadMultiple
指定されたプロパティを現在のプロパティ セットから読み取ります。

## <a name="syntax"></a>構文

```C++
HRESULT ReadMultiple( 
   ULONG          cpspec,
   PROPSPEC const rgpspec,
   PROPVARIANT    rgvar
);
```

#### <a name="parameters"></a>パラメーター
 `cpspec`

[入力] `rgpspec` 配列内に指定されたプロパティの数。 0 の場合、このメソッドはプロパティを返しませんが、成功コードとして `S_OK` を返します。

 `rgpspec`

[入力] 読み取るプロパティの配列。 プロパティは、プロパティ ID またはオプションの文字列名のいずれかで指定できます。 配列内に特定の順序でプロパティを指定する必要はありません。 配列には重複するプロパティを含めることができます。その結果、単純なプロパティの場合は戻り時にプロパティ値が重複します。 単純でないプロパティの場合は、2 回目に開こうとしたときにアクセス拒否が返されます。 配列には、プロパティ ID と文字列 ID を混在させることができます。 この配列には、少なくとも `cpspec` 個のプロパティ値が含まれている必要があります。

 `rgvar`

[入力、出力] 各プロパティの値が格納される `PROPVARIANT` 構造体の配列 (Microsoft.VisualStudio.OLE.Interop 名前空間内)。 配列のサイズは、`cpspec` 要素以上である必要があります。 呼び出し元では、配列内の値を初期化する必要はありません。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。 1 つ以上のプロパティが見つからなかった場合は、`S_FALSE` を返します。 それ以外の場合はエラー コードを返します。

## <a name="remarks"></a>解説
 プロパティが見つからなかった場合は、`rgvar` 配列内の対応するエントリに、`VT_EMPTY` 型の `VARIANT` が格納されます。

## <a name="see-also"></a>関連項目
- [IDiaPropertyStorage](../../debugger/debug-interface-access/idiapropertystorage.md)
