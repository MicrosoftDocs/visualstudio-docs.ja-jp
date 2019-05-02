﻿---
title: Idiasymbol::get_undecoratednameex |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_undecoratedNameEx method
ms.assetid: 579aed0b-c57d-41a1-a94a-3bf665fd4a9d
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f2a952c074e62e7fe999826882e382a552789f3a
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63400552"
---
# <a name="idiasymbolgetundecoratednameex"></a>IDiaSymbol::get_undecoratedNameEx
C++ の非装飾の名前の取得の一部またはすべての装飾 (リンケージ) 名。

## <a name="syntax"></a>構文

```C++
HRESULT get_undecoratedNameEx( 
   DWORD undecorateOptions,
   BSTR* pRetval
);
```

#### <a name="parameters"></a>パラメーター
 `undecoratedOptions`

[in]返される結果を制御するフラグの組み合わせを指定します。 特定の値とやっては「解説」を参照してください。

 `pRetVal`

[out]非装飾名を返します、C++装飾名。

## <a name="return-value"></a>戻り値
 成功した場合、返します`S_OK`。 それ以外を返します`S_FALSE`またはエラー コード。

> [!NOTE]
> 戻り値`S_FALSE`プロパティが、シンボルの使用可能なことを意味します。

## <a name="remarks"></a>Remarks
 `undecorateOptions`次のフラグの組み合わせとすることができます。

> [!NOTE]
> フラグ名は、コードに宣言を追加するか、生の値を使用する必要があるため、DIA SDK で定義されていません。

|フラグ|[値]|説明|
|----------|-----------|-----------------|
|UNDNAME_COMPLETE|0x0000|完全な undecoration を有効にします。|
|UNDNAME_NO_LEADING_UNDERSCORES|0x0001|Microsoft 拡張キーワードから先頭のアンダー スコアを削除します。|
|UNDNAME_NO_MS_KEYWORDS|0x0002|Microsoft 拡張キーワードの拡張を無効にします。|
|UNDNAME_NO_FUNCTION_RETURNS|0x0004|プライマリの宣言の戻り値の型の拡張を無効にします。|
|UNDNAME_NO_ALLOCATION_MODEL|0x0008|宣言モデルの拡張を無効にします。|
|UNDNAME_NO_ALLOCATION_LANGUAGE|0x0010|宣言の言語指定子の拡張を無効にします。|
|UNDNAME_RESERVED1|0x0020|予約済み。|
|UNDNAME_RESERVED2|0x0040|予約済み。|
|UNDNAME_NO_THISTYPE|0x0060|無効にしてすべての修飾子、`this`型。|
|UNDNAME_NO_ACCESS_SPECIFIERS|0x0080|メンバーのアクセス指定子の拡張を無効にします。|
|UNDNAME_NO_THROW_SIGNATURES|0x0100|「Throw 署名」関数および関数へのポインターの拡張を無効にします。|
|UNDNAME_NO_MEMBER_TYPE|0x0200|拡張を無効にします。`static`または`virtual`メンバー。|
|UNDNAME_NO_RETURN_UDT_MODEL|0x0400|UDT を返しますには、Microsoft のモデルの拡張を無効にします。|
|UNDNAME_32_BIT_DECODE|0x0800|32 ビットの装飾名を undecorates します。|
|UNDNAME_NAME_ONLY|0x1000|プライマリ宣言の名前のみを取得します。だけを返します [スコープ::] の名前。  テンプレート パラメーターを展開します。|
|UNDNAME_TYPE_ONLY|0x2000|入力がエンコード; 種類のみ抽象宣言子を作成します。|
|UNDNAME_HAVE_PARAMETERS|0x4000|実際のテンプレート パラメーターができます。|
|UNDNAME_NO_ECSU|0x8000|列挙型/クラス/構造体/共用体を抑制します。|
|UNDNAME_NO_IDENT_CHAR_CHECK|0x10000|有効な識別子文字のチェックを抑制します。|
|UNDNAME_NO_PTR64|0x20000|出力で ptr64 は含まれません。|

## <a name="see-also"></a>関連項目
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
