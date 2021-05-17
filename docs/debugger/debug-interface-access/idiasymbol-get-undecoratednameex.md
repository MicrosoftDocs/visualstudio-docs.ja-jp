---
description: C++ の装飾 (リンケージ) 名の非装飾名の一部または全部を取得します。
title: IDiaSymbol::get_undecoratedNameEx | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_undecoratedNameEx method
ms.assetid: 579aed0b-c57d-41a1-a94a-3bf665fd4a9d
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 35e1dcb2704b4a8e76fe8d7ffb172f0846fbdc78
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634588"
---
# <a name="idiasymbolget_undecoratednameex"></a>IDiaSymbol::get_undecoratedNameEx
C++ の装飾 (リンケージ) 名の非装飾名の一部または全部を取得します。

## <a name="syntax"></a>構文

```C++
HRESULT get_undecoratedNameEx( 
   DWORD undecorateOptions,
   BSTR* pRetval
);
```

#### <a name="parameters"></a>パラメーター
 `undecoratedOptions`

[入力] 返される内容を制御するフラグの組み合わせを指定します。 特定の値とその機能については、「解説」を参照してください。

 `pRetVal`

[出力] C++ の装飾名の非装飾名を返します。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。それ以外の場合は、`S_FALSE` またはエラー コードを返します。

> [!NOTE]
> 戻り値 `S_FALSE` は、プロパティがそのシンボルに使用できないことを意味します。

## <a name="remarks"></a>解説
 `undecorateOptions` には、次のフラグの組み合わせを指定できます。

> [!NOTE]
> フラグ名は DIA SDK で定義されていないため、宣言をコードに追加するか、生の値を使用する必要があります。

|フラグ|値|説明|
|----------|-----------|-----------------|
|UNDNAME_COMPLETE|0x0000|完全な装飾解除を有効にします。|
|UNDNAME_NO_LEADING_UNDERSCORES|0x0001|Microsoft 拡張キーワードから先頭のアンダースコアを削除します。|
|UNDNAME_NO_MS_KEYWORDS|0x0002|Microsoft 拡張キーワードの展開を無効にします。|
|UNDNAME_NO_FUNCTION_RETURNS|0x0004|プライマリ宣言の戻り値の型の展開を無効にします。|
|UNDNAME_NO_ALLOCATION_MODEL|0x0008|宣言モデルの展開を無効にします。|
|UNDNAME_NO_ALLOCATION_LANGUAGE|0x0010|宣言言語指定子の展開を無効にします。|
|UNDNAME_RESERVED1|0x0020|予約済み。|
|UNDNAME_RESERVED2|0x0040|予約済み。|
|UNDNAME_NO_THISTYPE|0x0060|`this` 型のすべての修飾子を無効にします。|
|UNDNAME_NO_ACCESS_SPECIFIERS|0x0080|メンバーのアクセス指定子の展開を無効にします。|
|UNDNAME_NO_THROW_SIGNATURES|0x0100|関数および関数へのポインターに対する "throw シグネチャ" の展開を無効にします。|
|UNDNAME_NO_MEMBER_TYPE|0x0200|`static` メンバーまたは `virtual` メンバーの展開を無効にします。|
|UNDNAME_NO_RETURN_UDT_MODEL|0x0400|UDT の戻り値に対する Microsoft モデルの拡張を無効にします。|
|UNDNAME_32_BIT_DECODE|0x0800|32 ビットの装飾名を装飾解除します。|
|UNDNAME_NAME_ONLY|0x1000|プライマリ宣言の名前のみを取得します。[scope::] の名前だけを返します。  テンプレート パラメーターを展開します。|
|UNDNAME_TYPE_ONLY|0x2000|入力は単なる型のエンコードです。抽象宣言子を合成します。|
|UNDNAME_HAVE_PARAMETERS|0x4000|実際のテンプレート パラメーターを使用できます。|
|UNDNAME_NO_ECSU|0x8000|列挙型/クラス/構造体/共用体を抑制します。|
|UNDNAME_NO_IDENT_CHAR_CHECK|0x10000|有効な識別子文字のチェックを抑制します。|
|UNDNAME_NO_PTR64|0x20000|出力に ptr64 を含めません。|

## <a name="see-also"></a>関連項目
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
