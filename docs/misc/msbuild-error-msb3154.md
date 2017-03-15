---
title: "MSBuild エラー MSB3154 | Microsoft Docs"
ms.custom: ""
ms.date: "10/29/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "MSBuild.GenerateBootstrapper.ProductCultureNotFound"
helpviewer_keywords: 
  - "MSB3154"
ms.assetid: 513b70fa-15f5-4137-bdbc-5974607fb75a
caps.latest.revision: 6
caps.handback.revision: 6
author: "mikeblome"
ms.author: "mblome"
manager: "douge"
---
# MSBuild エラー MSB3154
**MSB3154: 項目 '\<パッケージ\>' の文字列リソースが見つかりませんでした。**  
  
 このエラーは、指定されたパッケージにカルチャ固有の情報が指定されていない場合に生成されます。  package.xml ファイルが存在しないか、package.xml ファイルに `Culture` 属性が指定されていません。  
  
### このエラーを解決するには  
  
-   正しい `Culture` タグが指定された、有効な package.xml ファイルを提供します。