---
title: '[正規表現を使用する]'
ms.date: 03/26/2018
ms.topic: conceptual
f1_keywords:
- vsregularexpressionhelp
- vs.regularexpressionhelp
- vs.wildcardsbuilder
- vs.netregularexpressionhelp
- vs.wildcards
helpviewer_keywords:
- regular expressions [Visual Studio]
- regular expressions
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a5421599d2ffa006a445e0410088671d8897cc52
ms.sourcegitcommit: 21d667104199c2493accec20c2388cf674b195c3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2019
ms.locfileid: "55923253"
---
# <a name="use-regular-expressions-in-visual-studio"></a>Visual Studio での正規表現の使用

Visual Studio は、テキストの検索と置換をするときに、[.NET Framework の正規表現](/dotnet/standard/base-types/regular-expressions)を使います。

## <a name="replacement-patterns"></a>置換パターン

番号付きキャプチャ グループを使うには、正規表現パターンにおいてグループをかっこで囲みます。 置換パターンで特定の番号付きグループを指定するには、`$number` を使います。`number` は、1 から始まる整数です。 たとえば、グループ化された正規表現 `(\d)([a-z])` では、2 つのグループが定義されています。1 番目のグループには 1 つの 10 進数字が含まれ、2 番目のグループには **a** から **z** の 1 つの文字が含まれます。 この式では、**1a 3c 2b 4d** という文字列の中で、4 つの一致が見つかります。 置換文字列 `z$1` は最初のグループのみを参照し、この文字列を **z1 z2 z3 z4** に変換します。

置換パターンでよく使われる正規表現については、「[正規表現での置換](/dotnet/standard/base-types/substitutions-in-regular-expressions)」(.NET ガイド) を参照してください。

## <a name="regular-expression-examples"></a>正規表現の例

次にいくつかの例を示します。

|目的|正規表現|例|
|-------------|----------------|-------------|
|(改行を除く) 任意の 1 文字に一致します。|.|`a.o` は、"around" の "aro" および "about" の "abo" には一致しますが、"across" の "acro" には一致しません。|
|直前の正規表現の 0 回以上の繰り返しに一致します (一致する文字列の長さを最大限にします)。|*|`a*r` は、"rack" の中の "r"、"ark" の中の "ar"、"aardvark" の中の "aar" に一致します。|
|0 回以上の任意の文字に一致します (ワイルドカード *)|.*|`c.*e` は、"racket" の中の "cke"、"comment" の中の "comme"、"code" の中の "code" に一致します。|
|直前の正規表現の 1 回以上の繰り返しに一致します (一致する文字列の長さを最大限にします)。|+|`e.+d` は、"feeder" の中の "eed" に一致しますが、"ed" には一致しません。|
|1 回以上の任意の文字に一致します (ワイルドカード ?)|.+|`e.+e` は、"feeder" の中の "eede" に一致しますが、"ee" には一致しません。|
|直前の正規表現の 0 回以上の繰り返しに一致します (一致する文字列の長さを最小限にします)。|*?|`e.*?e` は、"feeder" の中の "ee" に一致しますが、"eede" には一致しません。|
|直前の正規表現の 1 回以上の繰り返しを検索します (一致する文字列の長さを最小限にします)。|+?|`e.+?e` は、"enterprise" 中の "ente" および "erprise" には一致しますが、単語全体 "enterprise" には一致しません。|
|一致文字列を、行頭または文字列の先頭に固定します。|^|`^car` は、単語 "car" が行の先頭に登場する場合のみ、その単語に一致します。|
|一致文字列を、行末に固定します。|\r?$|`end\r?$` は、"end" が行末に登場する場合のみ、その単語に一致します。|
|一致文字列を、ファイルの末尾に固定します。|$|`end$` は、"end" がファイルの末尾に登場する場合のみ、その単語に一致します。|
|セット内の任意の 1 文字と一致します。|[abc]|`b[abc]` は、"ba"、"bb"、および "bc" に一致します。|
|範囲内の任意の文字に一致します|[a-f]|`be[n-t]` は、"between" の中の "bet"、"beneath" の中の "ben"、および "beside" の中の "bes" には一致しますが、"below" の中の "bel" には一致しません。|
|かっこで囲まれた表現を 1 つのまとまりとして扱い、その表現に対して暗黙的に番号を付けます。|()|`([a-z])X\1` は、"aXa" および "bXb" に一致しますが、"aXb" には一致しません。 "\1"は、最初の表現グループ "[a-z]" を指します。|
|一致を否定します。|(?!abc)|`real(?!ity)` は、"realty" や "really" の中の "real" に一致しますが、"reality" の中の "real" には一致しません。 また、"realityreal" の中の 2 番目の "real" に一致します (一方、最初の "real" には一致しません)。|
|指定された一連の文字の中に含まれていない任意の文字と一致します。|[^abc]|`be[^n-t]` は、"before" の中の "bef"、"behind" の中の "beh"、および "below" の中の "bel" に一致しますが、"beneath" の中の "ben" には一致しません。|
|記号の前にある表現、または後にある表現のいずれかに一致します。|&#124;|`(sponge\|mud) bath` は "sponge bath" および "mud bath" に一致します。|
|円記号の後の文字をエスケープ処理します。| \\ |`\^` は、^ 文字に一致します。|
|直前の文字またはグループが登場する回数を指定します。|{x}、ここで x は登場する回数です。|`x(ab){2}x` は "xababx" に一致し、`x(ab){2,3}x` は "xababx" および "xabababx" に一致しますが、"xababababx" には一致しません。|
|Unicode 文字クラスに含まれるテキストに一致します。 Unicode 文字クラスの詳細については、次を参照してください。<br /><br /> [Unicode 規格 5.2 の文字のプロパティ](http://www.unicode.org/versions/Unicode5.2.0/ch04.pdf)。|\p{X}、ここで "X" は Unicode 番号です。|`\p{Lu}` は "Thomas Doe" の中の "T" および "D" に一致します。|
|ワード境界に一致します。|\b (文字クラス `\b` の外部にあるときはワード境界を指定し、文字クラス `\b` の内部にあるときはバックスペースを指定します)。|`\bin` は、"inside" の中の "in" と一致しますが、"pinto" には一致しません。|
|改行 (つまり、キャリッジ リターンとそれに続く新しい行) に一致します。|\r?\n|`End\r?\nBegin` は、"End" が行の最後の文字列で、"Begin" が次の行の先頭の文字列である場合のみ、単語 "End" と "Begin" に一致します。|
|任意の英数字 1 文字に一致します。|\w|`a\wd` は、"add" および "a1d" に一致しますが、"a d" には一致しません。|
|任意の空白文字と一致します。|(?([^\r\n])\s)|`Public\sInterface` は、語句 "Public Interface" に一致します。|
|任意の数字 1 文字に一致します。|\d|`\d` は、"3456" の中の "3"、"23" の中の "2"、および "1" の中の "1" に一致します。|
|Unicode 文字に一致します。|\uXXXX、ここで XXXX は、Unicode 文字の値を指定します。|`\u0065` は、^ 文字に一致します。|
|識別子に一致します|\b[\_\w-[0-9]][\_\w]*\b|"type1" に一致しますが、"&type1" や "#define" には一致しません。|
|引用符の内側にある文字列と一致します|((\\".+?\\")&#124;('.+?'))|単一引用符または二重引用符の内部にある任意の文字列に一致します。|
|16 進数に一致します|\b0[xX]([0-9a-fA-F]\)\b|"0xc67f" 一致しますが、"0xc67fc67f" には一致しません。|
|整数と小数に一致します|\b[0-9]*\\.\*[0-9]+\b|"1.333" に一致します。|

> [!TIP]
> Windows オペレーティング システムでは、ほとんどの行は、"\r\n" (キャリッジ リターンと、それに続く新しい行) で終わります。 これらの文字は表示されませんが、エディターの中に存在し、.NET の正規表現のサービスに渡されます。

## <a name="see-also"></a>関連項目

- [テキストの検索と置換](../ide/finding-and-replacing-text.md)
