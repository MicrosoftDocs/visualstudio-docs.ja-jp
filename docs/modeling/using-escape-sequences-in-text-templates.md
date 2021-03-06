---
title: テキスト テンプレートでのエスケープ シーケンスの使用
description: テキスト テンプレートでエスケープ シーケンスを使用してテキスト テンプレート タグを生成する方法と、C# コードでのみ使用可能な制御文字と引用符をエスケープする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- text templates, escape sequences
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 2a3cdabd38f2bf4ef38a31807fabed3ac837b26b
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112388452"
---
# <a name="use-escape-sequences-in-text-templates"></a>テキスト テンプレートでエスケープ シーケンスを使用する

テキスト テンプレートでエスケープ シーケンスを使用してテキスト テンプレート タグを生成することと、(C# コードでのみ) 制御文字と引用符をエスケープすることができます。

標準コード ブロックの開始タグと終了タグを出力ファイルに出力するには、次のようにタグをエスケープします。

```
\<# ... \#>
```

他のテキスト テンプレート ディレクティブとコード ブロック タグでも同じことができます。

テキスト テンプレート タグをエスケープするために使用する文字列がテキスト ブロックに含まれている場合は、次のエスケープ シーケンスを使用できます。

- テキスト テンプレート タグの前にエスケープ文字 (\\) が偶数個ある場合、テンプレート パーサーにはエスケープ文字の半分が含まれ、シーケンスはテキスト テンプレート タグとして含まれます。 たとえば、テキスト テンプレートに 4 つのエスケープ文字がある場合、生成されるファイルには "\\" という文字が 2 つあります。

- テキスト テンプレート タグの前にエスケープ文字 (\\) が奇数個ある場合、テンプレート パーサーには、"\\" 文字の半分とタグ自体 (\<# or #>) が含まれます。 タグはテキスト テンプレート タグとは見なされません。

- エスケープ文字 (\\) が制御文字または引用符をエスケープする場所以外のシーケンス内にある場合 (C# の場合のみ)、文字が直接出力されます。

## <a name="see-also"></a>関連項目

- [方法: エスケープ シーケンスを使用してテンプレートからテンプレートを生成する](../modeling/how-to-generate-templates-from-templates-by-using-escape-sequences.md)
