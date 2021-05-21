---
description: IDiaSession::findInlineFramesByAddr は、指定のアドレス上のすべてのインライン フレームをクライアントが反復処理できるようにする列挙子を取得します。
title: IDiaSession::findInlineFramesByAddr | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
ms.assetid: e7dc1ac7-bb09-45be-96d2-365a9b7336e4
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: b063828522a0ab1579b7ade1d5f780b01598e96f
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634818"
---
# <a name="idiasessionfindinlineframesbyaddr"></a>IDiaSession::findInlineFramesByAddr
指定のアドレス上のすべてのインライン フレームをクライアントが反復処理できるようにする列挙子を取得します。

## <a name="syntax"></a>構文

```C++
HRESULT findInlineFramesByAddr ( 
   IDiaSymbol*       parent,   DWORD             isect,
   DWORD             offset,
   IDiaEnumSymbols** ppResult
);
```

#### <a name="parameters"></a>パラメーター
 `parent`

[入力] 親を表す `IDiaSymbol` オブジェクト。

 `isect`

[入力] アドレスのセクション部分を指定します。

 `offset`

[入力] アドレスのオフセット部分を指定します。

 `ppResult`

[出力] 取得したフレームの一覧を含む `IDiaEnumSymbols` オブジェクトを保持します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [SymTagEnum 列挙型](../../debugger/debug-interface-access/symtagenum.md)
- [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)
