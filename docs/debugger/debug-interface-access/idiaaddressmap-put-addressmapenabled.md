---
title: IDiaAddressMap::put_addressMapEnabled | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaAddressMap::put_addressMapEnabled method
ms.assetid: 0f205337-4e59-4383-8059-7b1d207d6dcd
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a53d66879155ae1ce2cd831c029bc5776a7dd863
ms.sourcegitcommit: 2193323efc608118e0ce6f6b2ff532f158245d56
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 01/25/2019
ms.locfileid: "54999211"
---
# <a name="idiaaddressmapputaddressmapenabled"></a>IDiaAddressMap::put_addressMapEnabled
シンボルのアドレスに変換するアドレス マップを使用するかどうかを指定します。  
  
## <a name="syntax"></a>構文  
  
```C++  
HRESULT put_addressMapEnabled (   
   BOOL NewVal  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 NewVal  
 [in]設定`TRUE`、記号の翻訳を有効にするか、`FALSE`を無効にします。  
  
## <a name="return-value"></a>戻り値  
 成功した場合、返します`S_OK`、それ以外のエラー コードを返します。  
  
## <a name="remarks"></a>解説  
 場合があります、ポスト プロセッサの実行可能ファイルは、実行可能ファイルを更新します。 DIA には、新しいレイアウトにシンボルの変換をサポートするためのメカニズムが含まれています。  
  
 PDB ファイルが読み込まれるときに、ファイルに格納されているアドレス マップが有効にします。 ただし、クライアント アプリケーションが呼び出すことによって、独自のアドレス マップを指定する必要がありますが、 [idiaaddressmap::set_addressmap](../../debugger/debug-interface-access/idiaaddressmap-set-addressmap.md)メソッド。 場合、`set_addressMap`メソッドが成功すると、クライアント アプリケーションを呼び出す必要があります、`put_addressMapEnabled`メソッドを`NewVal`パラメーターの`TRUE`アドレスにマップの使用を有効にします。  
  
 呼び出しでアドレス マップを有効になっているは、現在の状態を取得することができます、 [idiaaddressmap::get_addressmapenabled](../../debugger/debug-interface-access/idiaaddressmap-get-addressmapenabled.md)メソッド。  
  
## <a name="see-also"></a>参照  
 [IDiaAddressMap](../../debugger/debug-interface-access/idiaaddressmap.md)   
 [IDiaAddressMap::set_addressMap](../../debugger/debug-interface-access/idiaaddressmap-set-addressmap.md)   
 [IDiaAddressMap::get_addressMapEnabled](../../debugger/debug-interface-access/idiaaddressmap-get-addressmapenabled.md)