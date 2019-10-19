---
title: T4 出力ディレクティブ
ms.date: 11/04/2016
ms.topic: reference
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1da8ec010e878ff80a9f46748993705b87193d99
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72606224"
---
# <a name="t4-output-directive"></a>T4 出力ディレクティブ

Visual Studio テキストテンプレートでは、`output` ディレクティブを使用して、変換されたファイルのファイル名拡張子とエンコーディングを定義します。

 たとえば、Visual Studio プロジェクトに、次のディレクティブを含む**MyTemplate.tt**という名前のテンプレートファイルが含まれているとします。

 `<#@output extension=".cs"#>`

 次に、Visual Studio によって**MyTemplate.cs**という名前のファイルが生成されます。

 `output` ディレクティブは、実行時 (前処理済み) のテキスト テンプレートには必要ありません。 その代わりに、アプリケーションは `TextTransform()` を呼び出して、生成済みの文字列を取得します。 詳細については、「 [T4 テキストテンプレートを使用した実行時テキスト生成](../modeling/run-time-text-generation-with-t4-text-templates.md)」を参照してください。

## <a name="using-the-output-directive"></a>出力ディレクティブの使用

```
<#@ output extension=".fileNameExtension" [encoding="encoding"] #>
```

 各テキスト テンプレートには複数の `output` ディレクティブを含めてはいけません。

## <a name="extension-attribute"></a>拡張属性
 生成されたテキスト出力ファイルのファイル名の拡張子を指定します。

 既定値は **.cs です。**

 例: `<#@ output extension=".txt" #>`

 `<#@ output extension=".htm" #>`

 `<#@ output extension=".cs" #>`

 `<#@ output extension=".vb" #>`

 使用できる値: 任意の有効なファイル名拡張子。

## <a name="encoding-attribute"></a>encoding 属性
 出力ファイルが生成されるときに使用するエンコードを指定します。 (例:

 `<#@ output encoding="utf-8"#>`

 既定値は、テキスト テンプレート ファイルが使用するエンコードです。

 使用可能な値: `us-ascii`

 `utf-16BE`

 `utf-16`

 `utf-8`

 `utf-7`

 `utf-32`

 `0` (システムの既定値)

 一般に、<xref:System.Text.Encoding.GetEncodings%2A?displayProperty=fullName> が返す任意のエンコードの WebName 文字列または CodePage 数値を使用できます。