---
title: Visual Studio での正規表現の使用 | Microsoft Docs
ms.custom: ''
ms.date: 2018-06-30
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vsregularexpressionhelp
- vs.regularexpressionhelp
- vs.wildcardsbuilder
- vs.netregularexpressionhelp
- vs.wildcards
helpviewer_keywords:
- regular expressions [Visual Studio]
- regular expressions
- Visual Studio, regular expressions
ms.assetid: 718a617d-0e05-47e1-a218-9746971527f4
caps.latest.revision: 56
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: c74ed503b13e9f5efab3e6bf0df2fab75d34e7cb
ms.sourcegitcommit: 55f7ce2d5d2e458e35c45787f1935b237ee5c9f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2018
ms.locfileid: "47535702"
---
# <a name="use-regular-expressions-in-visual-studio"></a>Visual Studio での正規表現を使用します。
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このトピックの最新バージョンをご覧[Visual Studio で正規表現を使用して](https://docs.microsoft.com/visualstudio/ide/using-regular-expressions-in-visual-studio)します。

Visual Studio では、テキスト検索し、置換を .NET Framework の正規表現を使用します。 .NET の正規表現の詳細については、「[.NET Framework の正規表現](http://msdn.microsoft.com/library/521b3f6d-f869-42e1-93e5-158c54a6895d)」を参照してください。

Visual Studio 2012 より前、Visual Studio は [検索と置換] ウィンドウでカスタムの正規表現構文を使用していました。 より一般的に使用されているカスタム正規表現のシンボルの一部を .NET のバージョンに変換する方法については、「[Visual Studio での正規表現の使用](https://msdn.microsoft.com/library/2k3te2cs\(v=vs.110\).aspx)」を参照してください。

> [!TIP]
> Windows オペレーティング システムでは、ほとんどの行は、"\r\n" (キャリッジ リターンと、それに続く新しい行) で終わります。 これらの文字は表示されませんが、エディターの中に存在し、.NET の正規表現のサービスに渡されます。

> [!TIP]
> 置換パターンでよく使用される正規表現の詳細については、「[置換](http://msdn.microsoft.com/library/d1f52431-1c7d-4dc6-8792-6b988256892e)」を参照してください。 番号付きのキャプチャ グループを使用する場合の構文は、番号付きグループを指定する `$1` と、該当のグループを指定する `(x)` です。 たとえば、グループ化正規表現 `(\d)([a-z])` を使用すると、"**1a 3c 2b 4d**" という文字列の中で、4 つの一致が見つかります。 置換文字列 `z$1` を使用すると、この文字列は "**z1 z2 z3 z4**" に変換されます。

## <a name="regular-expression-examples"></a>正規表現の例

次にいくつかの例を示します。

|目的|正規表現|例|
|-------------|----------------|-------------|
|(改行を除く) 任意の 1 文字に一致します。|.|`a.o` は、"around" の "aro" および "about" の "abo" には一致しますが、"across" の "acro" には一致しません。|
|直前の正規表現の 0 回以上の繰り返しに一致します (一致する文字列の長さを最大限にします)。|*|`a*r` は、"rack" の中の "r"、"ark" の中の "ar"、"aardvark" の中の "aar" に一致します。|
|0 回以上の任意の文字に一致します (ワイルドカード *)|.*|c.*e は、"racket" の中の "cke"、"comment" の中の "comme"、"code" の中の "code" に一致します。|
|直前の正規表現の 1 回以上の繰り返しに一致します (一致する文字列の長さを最大限にします)。|+|`e.+e` は、"feeder" の中の "eede" に一致しますが、"ee" には一致しません。|
|1 回以上の任意の文字に一致します (ワイルドカード ?)|.+|e.+e は、"feeder" の中の "eede" に一致しますが、"ee" には一致しません。|
|直前の正規表現の 0 回以上の繰り返しに一致します (一致する文字列の長さを最小限にします)。|*?|`e.*?e` は、"feeder" の中の "ee" に一致しますが、"eede" には一致しません。|
|直前の正規表現の 1 回以上の繰り返しを検索します (一致する文字列の長さを最小限にします)。|+?|`e.+?e` は、"enterprise" 中の "ente" および "erprise" には一致しますが、単語全体 "enterprise" には一致しません。|
|一致文字列を、行頭または文字列の先頭に固定します。|^|`^car` は、単語 "car" が行の先頭に登場する場合のみ、その単語に一致します。|
|一致文字列を、行末に固定します。|\r?$|`End\r?$` は、"end" が行末に登場する場合のみ、その単語に一致します。|
|セット内の任意の 1 文字と一致します。|[abc]|`b[abc]` は、"ba"、"bb"、および "bc" に一致します。|
|範囲内の任意の文字に一致します|[a-f]|`be[n-t]` は、"between" の中の "bet"、"beneath" の中の "ben"、および "beside" の中の "bes" には一致しますが、"below" の中の "bel" には一致しません。|
|かっこで囲まれた表現を 1 つのまとまりとして扱い、その表現に対して暗黙的に番号を付けます。|()|`([a-z])X\1` は、"aXa" および "bXb" に一致しますが、"aXb" には一致しません。 ". "\1"は、最初の表現グループ "[a-z]" を指します。|
|一致を否定します。|(?!abc)|`real (?!ity)` は、"realty" や "really" の中の "real" に一致しますが、"reality" の中の "real" には一致しません。 また、"realityreal" の中の 2 番目の "real" に一致します (一方、最初の "real" には一致しません)。|
|指定された一連の文字の中に含まれていない任意の文字と一致します。|[^abc]|`be[^n-t]` は、"before" の中の "bef"、"behind" の中の "beh"、および "below" の中の "bel" に一致しますが、"beneath" の中の "ben" には一致しません。|
|記号の前にある表現、または後にある表現のいずれかに一致します。|&#124;|`(sponge&#124;mud) bath` は "sponge bath" および "mud bath" に一致します。|
|円記号の後の文字をエスケープ処理します。|\|`\^` 文字と一致 ^ です。|
|直前の文字またはグループが登場する回数を指定します。|{x}、ここで x は登場する回数です。|`x(ab){2}x` は "xababx" に一致し、`x(ab){2,3}x` は "xababx" および "xabababx" に一致しますが、"xababababx" には一致しません。|
|Unicode 文字クラスに含まれるテキストに一致します。ここで、"X" は Unicode 番号です。 Unicode 文字クラスの詳細については、次を参照してください。<br /><br /> [Unicode 規格 5.2 の文字のプロパティ](http://www.unicode.org/versions/Unicode5.2.0/ch04.pdf)。|\p{X}|`\p{Lu}` は "Thomas Doe" の中の "T" および "D" に一致します。|
|ワード境界に一致します。|`\b` (\b が文字クラスの外部にあるときはワード境界を指定し、文字クラスの内部にあるときはバックスペースを指定します)。|`\bin` は、"inside" の中の "in" と一致しますが、"pinto" には一致しません。|
|改行 (つまり、キャリッジ リターンとそれに続く新しい行) に一致します。|\r?\n|`End\r?\nBegin` は、"End" が行の最後の文字列で、"Begin" が次の行の先頭の文字列である場合のみ、単語 "End" と "Begin" に一致します。|
|任意の英数字 1 文字に一致します。|\w|`a\wd` は、"add" および "a1d" に一致しますが、"a d" には一致しません。|
|任意の空白文字と一致します。|(?([^\r\n])\s)|`Public\sInterface` は、語句 "Public Interface" に一致します。|
|任意の数字 1 文字に一致します。|\d|`\d` は、"3456" の中の "3"、"23" の中の "2"、および "1" の中の "1" に一致します。|
|Unicode 文字に一致します。|\uXXXX、ここで XXXX は、Unicode 文字の値を指定します。|`\u0065` は、^ 文字に一致します。|
|識別子に一致します|\b(_\w+&#124;[\w-[0-9\_]]\w*)\b|"type1" に一致しますが、&type1" や "#define" に一致しません。|
|引用符の内側にある文字列と一致します|((\\".+?\\")&#124;('.+?'))|単一引用符または二重引用符の内部にある任意の文字列に一致します。|
|16 進数に一致します|\b0[xX]([0-9a-fA-F]\)\b|"0xc67f" 一致しますが、"0xc67fc67f" には一致しません。|
|整数と小数に一致します|\b[0-9]*\\.\*[0-9]+\b|"1.333" に一致します。|