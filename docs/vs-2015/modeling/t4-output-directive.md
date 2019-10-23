---
title: T4 出力ディレクティブ |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
ms.assetid: 03a14993-47ad-4f2e-8032-57db28d5842a
caps.latest.revision: 6
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 149370bfee1b142876dff881625d08083afadea4
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72652314"
---
# <a name="t4-output-directive"></a>T4 出力ディレクティブ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] テキスト テンプレートでは、`output` ディレクティブを使用してファイル名の拡張子と変換ファイルのエンコードを定義します。

 たとえば、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] プロジェクトに、次のディレクティブを含む**MyTemplate.tt**という名前のテンプレートファイルが含まれているとします。

 `<#@output extension=".cs"#>`

 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] に、 **MyTemplate.cs**という名前のファイルが生成されます。

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
