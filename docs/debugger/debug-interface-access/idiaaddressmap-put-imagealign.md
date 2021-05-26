---
description: イメージの配置を設定します。
title: IDiaAddressMap::put_imageAlign | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaAddressMap::put_imageAlign method
ms.assetid: f9ce875d-c263-43e5-a534-f34c37f9866f
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 0c3027332018441efd132cc941d16aab3bcab594
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634992"
---
# <a name="idiaaddressmapput_imagealign"></a>IDiaAddressMap::put_imageAlign
イメージの配置を設定します。

## <a name="syntax"></a>構文

```C++
HRESULT put_imageAlign ( 
   DWORD NewVal
);
```

#### <a name="parameters"></a>パラメーター
 NewVal

[入力] 実行可能ファイルの新しいイメージ配置値。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 イメージ (読み込まれた実行可能ファイル) は、指定されたメモリ境界に整列されます。 この配置は、現在のシステム アーキテクチャと、コンパイルおよびリンク時のオプションの影響を受ける可能性があります。 イメージの配置は常にバイト境界上になります。 有効なイメージ配置値は、1、2、4、8、16、32、および 64 バイト境界です。

 現在のイメージの配置は、[IDiaAddressMap::get_imageAlign](../../debugger/debug-interface-access/idiaaddressmap-get-imagealign.md) メソッドを呼び出すことで取得できます。

> [!NOTE]
> このメソッドを呼び出すことができるようになるまでに、イメージは既に読み込まれています。 通常、`put_imageAlign` メソッドは、イメージが移動または変更され、新しい配置が必要な場合に使用されます。

## <a name="see-also"></a>関連項目
- [IDiaAddressMap](../../debugger/debug-interface-access/idiaaddressmap.md)
- [IDiaAddressMap::get_imageAlign](../../debugger/debug-interface-access/idiaaddressmap-get-imagealign.md)
