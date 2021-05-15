---
description: イメージ テキストのバイトをコントリビュートしたコンパイル単位のシンボルへの参照を取得します。
title: IDiaLineNumber::get_compiland | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaLineNumber::get_compiland method
ms.assetid: c476d0b8-c473-47eb-96f5-c4e8f577b1c9
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 2700ffb00c14a0f9f62f274157ffadecb0abee26
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634888"
---
# <a name="idialinenumberget_compiland"></a>IDiaLineNumber::get_compiland
イメージ テキストのバイトをコントリビュートしたコンパイル単位のシンボルへの参照を取得します。

## <a name="syntax"></a>構文

```C++
HRESULT get_compiland ( 
   IDiaSymbol** pRetVal
);
```

#### <a name="parameters"></a>パラメーター
 pRetVal

[出力] イメージ テキストのバイトをコントリビュートしたコンパイル単位の [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。 このプロパティがサポートされていない場合は、`S_FALSE` を返します。 それ以外の場合はエラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDiaLineNumber](../../debugger/debug-interface-access/idialinenumber.md)
