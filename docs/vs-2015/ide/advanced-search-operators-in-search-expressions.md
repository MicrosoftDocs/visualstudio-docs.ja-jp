---
title: 検索式の高度な検索演算子 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- Help Viewer 2.0, searching for keywords
- Help Viewer 2.0, searching code
- Help Viewer 2.0, searching code by programming language
- Help Viewer 2.0, searching titles
- searching code [Help Viewer 2.0]
- searching titles [Help Viewer 2.0]
ms.assetid: 0cdc1746-8481-45ec-9c53-d0d89cdcbd5e
caps.latest.revision: 11
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 9c2b8df3878f67207b22127881722aedd8caae8e
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "54775575"
---
# <a name="advanced-search-operators-in-search-expressions"></a>検索式の高度な検索演算子
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

高度な検索演算子を使用すると、単純なからより複雑な検索式を作成してコンテンツの検索を調整できます。 次の表にあるとおり、演算子はクエリが実行されるコンテキストを制限します。  
  
> [!WARNING]
>  高度な検索演算子を入力するときは、検索エンジンに認識させるために最後にコロンを付け、コロンの前にはスペースを入れません。  
  
|検索対象|使用|例|結果|  
|-------------------|---------|-------------|------------|  
|トピックのタイトルの言葉|title:|title:binaryreader|タイトルに "binaryreader" が含まれるトピック。|  
|コード サンプルの言葉|code:|code:readdouble|コード サンプルに "readdouble" が含まれるトピック。|  
|特定のプログラミング言語のサンプルの言葉|code:vb:|code:vb:string|Visual Basic サンプルに "string" が含まれるトピック。|  
|特定のインデックス キーワードに関連付けられているトピック。|keyword:|keyword:readbyte|"readbyte" というインデックス キーワードに関連付けられているトピック。|  
  
 code: 演算子を利用して任意のいくつかのプログラミング言語に関するコンテンツを検索できますが、特定のプログラミング言語でマークアップされているコンテンツのみ、結果が返されます。 次の表は、この演算子が対応しているプログラミング言語を一覧にまとめたものです。  
  
|プログラミング言語|使用|  
|--------------------------|---------|  
|Visual Basic|code:vb<br /><br /> または<br /><br /> code:visualbasic|  
|C#|code:C#<br /><br /> または<br /><br /> code:csharp|  
|C++|code:cpp<br /><br /> または<br /><br /> code:c++<br /><br /> または<br /><br /> code:cplusplus|  
|F#|code:f#<br /><br /> または<br /><br /> code:fsharp|  
|JavaScript|code:javascript<br /><br /> または<br /><br /> code:js|  
|XAML|code:xaml|  
  
## <a name="see-also"></a>関連項目  
 [検索式の論理演算子](../ide/logical-operators-in-search-expressions.md)   
 [フルテキスト検索のヒント](../ide/full-text-search-tips.md)
