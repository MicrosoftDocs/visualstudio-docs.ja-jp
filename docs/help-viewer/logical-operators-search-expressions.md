---
title: 検索式の論理演算子 (ヘルプ ビューアー)
description: Microsoft ヘルプ ビューアーで、論理演算子と高度な演算子を使用し、検索式の効果を高める方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/02/2017
ms.topic: reference
helpviewer_keywords:
- Help Viewer, logical operators in search
- logical operators in search [Help Viewer]
ms.assetid: 0c38ae7d-3e20-4d47-a020-9677cd285916
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 37e2652d04df154a45ae5f87fd62c8f8dc2e0b3e
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99944083"
---
# <a name="logical-and-advanced-operators-in-search-expressions"></a>検索式の論理演算子と高度な演算子

論理演算子と高度な検索演算子を使用して、**ヘルプ ビューアー** でヘルプ コンテンツの検索を絞り込むことができます。

## <a name="logical-operators"></a>論理演算子

論理演算子では、複数の検索用語を検索クエリでどのように組み合わせる必要があるかを指定します。 次の表に、論理演算子 AND、OR、NOT、NEAR を示します。

|検索対象|vmmblue_2|例|結果|
|-------------------|---------|-------------|------------|
|同じアーティクル内の両方の用語|AND|dib AND palette|"dib" と "palette" の両方を含むトピック。|
|アーティクル内のいずれかの用語|OR|raster OR vector|"raster" または "vector" を含むトピック。|
|同じアーティクル内の最初の用語 (2 番目の用語を含まない)|NOT|"operating system" NOT DOS|"operating system" を含むが、"DOS" を含まないトピック。|
|アーティクル内で近接する両方の用語|NEAR|user NEAR kernel|"kernel" にきわめて近い "user" を含むトピック。|

> [!IMPORTANT]
> 検索エンジンが認識できるように、論理演算子をすべて大文字で入力する必要があります。

## <a name="advanced-operators"></a>高度な演算子

高度な検索演算子は、アーティクル内で検索語句を探す場所を指定することで、コンテンツの検索を絞り込みます。 次の表は、利用できる 4 つの高度な検索演算子をまとめたものです。

|検索対象|vmmblue_2|例|結果|
|-------------------|---------|-------------|------------|
|アーティクルのタイトルの用語|`title:`|`title:binaryreader`|タイトルに "binaryreader" が含まれるトピック。|
|コード サンプルの言葉|`code:`|`code:readdouble`|コード サンプルに "readdouble" が含まれるトピック。|
|特定のプログラミング言語のサンプルの言葉|`code:vb:`|`code:vb:string`|Visual Basic コード サンプルに "string" が含まれるトピック。|
|特定のインデックス キーワードに関連付けられているアーティクル|`keyword:`|`keyword:readbyte`|"readbyte" というインデックス キーワードに関連付けられているトピック。|

> [!IMPORTANT]
> 高度な検索演算子を入力するときは、検索エンジンに認識させるために最後にコロンを付け、コロンの前にはスペースを入れません。

### <a name="programming-languages-for-code-examples"></a>コード例のプログラミング言語

`code:` 演算子を使用して、複数のプログラミング言語のいずれかに関するコンテンツを検索できます。 特定のプログラミング言語に対して例を返すには、次のプログラミング言語値のいずれかを使用します。

|プログラミング言語|検索演算子構文|
| - |---------|
|Visual Basic|`code:vb`<br/>`code:visualbasic`|
|C#|`code:c#`<br/>`code:csharp`|
|C++|`code:cpp`<br/>`code:c++`<br/>`code:cplusplus`|
|F#|`code:f#`<br/>`code:fsharp`|
|JavaScript|`code:javascript`<br/>`code:js`|
|XAML|`code:xaml`|

> [!NOTE]
> `code:` 演算子は、コードとして一般的にマークされているコンテンツではなく、プログラミング言語ラベルでマークされているコンテンツのみを検索します。

## <a name="see-also"></a>関連項目

- [方法: トピックを検索する](../help-viewer/find-topics.md)
- [Microsoft ヘルプ ビューアー](../help-viewer/overview.md)
