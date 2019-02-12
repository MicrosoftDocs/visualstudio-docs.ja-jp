﻿---
title: テキスト テンプレートでのエスケープ シーケンスの使用
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- text templates, escape sequences
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6de30faec90fd59531187d09f7eef76c3db7b043
ms.sourcegitcommit: 21d667104199c2493accec20c2388cf674b195c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2019
ms.locfileid: "55910442"
---
# <a name="using-escape-sequences-in-text-templates"></a>テキスト テンプレートでのエスケープ シーケンスの使用
テキスト テンプレートのタグを生成したり、(C# コードにおいてのみ) エスケープ制御文字や引用符をエスケープするために、テンプレートでエスケープ シーケンスを使用することができます。

 出力ファイルに標準のコード ブロックの始めと終わりのタグを印刷するには、次のように、タグをエスケープします。

```
\<# ... \#>
```

 その他のテキスト テンプレート ディレクティブおよびコード ブロック タグも同じようにすることができます。

 テキスト ブロックに、テキスト テンプレート タグをエスケープするために使用される文字列が含まれている場合は、次のエスケープ シーケンスを使用することがあります。

-   テキスト テンプレートのタグの前に偶数個のエスケープ文字 (\\) がある場合、テンプレート パーサーはそのエスケープ文字の半分とテキスト テンプレート タグの文字列が含まれます。 たとえば、テキスト テンプレートに 4 つのエスケープ文字がある場合、生成されたファイル内には、2 つの "\\" 文字があります。

-   テキスト テンプレートのタグの前に奇数個のエスケープ文字 (\\) がある場合、テンプレート パーサーはそのエスケープ\\文字の半分とタグ自体 (\<# または #>) が含まれます。 タグは、テキスト テンプレートのタグであると見なされません。

-    (C# の場合のみ) エスケープ文字 (\\) が、制御文字または引用符をエスケープする並び以外の任意の場所で現れたら、文字が直接出力されます。

## <a name="see-also"></a>関連項目

- [方法: エスケープ シーケンスを使用してテンプレートからテンプレートを生成します。](../modeling/how-to-generate-templates-from-templates-by-using-escape-sequences.md)
