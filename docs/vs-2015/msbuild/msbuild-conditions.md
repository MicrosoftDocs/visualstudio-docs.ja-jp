---
title: MSBuild の条件 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, conditions
- conditions [MSBuild]
ms.assetid: 9d7aa308-b667-48ed-b4c9-a61e49eb0a85
caps.latest.revision: 17
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: cd5fb6f70504fd89c0d08f7a8aa760b3c7b68323
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "54758333"
---
# <a name="msbuild-conditions"></a>MSBuild の条件
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] は、`Condition` 属性が許可されている場所ならどこでも適用できる、特定の条件のセットをサポートしています。 次の表は、その条件を説明したものです。  
  
|条件|説明|  
|---------------|-----------------|  
|'`stringA`' == '`stringB`'|`stringA` が `stringB` に等しい場合、`true` と評価されます。<br /><br /> 次に例を示します。<br /><br /> `Condition="'$(CONFIG)'=='DEBUG'"`<br /><br /> 単純な英数字文字列またはブール値には、単一引用符は必要ありません。 ただし、空の値には単一引用符が必要です。|  
|'`stringA`' != '`stringB`'|`stringA` が `stringB` と等しくない場合、`true` と評価されます。<br /><br /> 次に例を示します。<br /><br /> `Condition="'$(CONFIG)'!='DEBUG'"`<br /><br /> 単純な英数字文字列またはブール値には、単一引用符は必要ありません。 ただし、空の値には単一引用符が必要です。|  
|\<、>、\<=、>=|オペランドの数値を評価します。 関係の評価が true の場合、`true` を返します。 オペランドは、10 進数または 16 進数として評価される必要があります。 16 進数は、"0 x" で始まる必要があります。 **注:**  XML では、文字 `<` および `>` をエスケープする必要があります。 シンボル `<` は、`<` として表されます。 シンボル `>` は、`>` として表されます。|  
|Exists('`stringA`')|`stringA` という名前のファイルまたはフォルダーが存在する場合、`true` と評価されます。<br /><br /> 次に例を示します。<br /><br /> `Condition="!Exists('$(builtdir)')"`<br /><br /> 単純な英数字文字列またはブール値には、単一引用符は必要ありません。 ただし、空の値には単一引用符が必要です。|  
|HasTrailingSlash('`stringA`')|指定した文字列の末尾にバックスラッシュ (\\) 文字かスラッシュ (/) 文字のいずれかが含まれる場合、`true` と評価されます。<br /><br /> 次に例を示します。<br /><br /> `Condition="!HasTrailingSlash('$(OutputPath)')"`<br /><br /> 単純な英数字文字列またはブール値には、単一引用符は必要ありません。 ただし、空の値には単一引用符が必要です。|  
|!|オペランドが `false` と評価される場合、`true` と評価されます。|  
|および|両方のオペランドが `true` と評価される場合、`true` と評価します。|  
|または|少なくともオペランドの 1 つが `true` と評価される場合、`true` と評価します。|  
|()|内部に含まれる式が `true` と評価される場合に `true` と評価されるグループ化機構。|  
|$if$ ( %expression% )、$else$、$endif$|指定した `%expression%` が、渡されるカスタム テンプレート パラメーターの文字列の値と一致するかどうかをチェックします。 `$if$` 条件が `true` と評価される場合、そのステートメントが実行されます。それ以外の場合、`$else$` 条件がチェックされます。 `$else$` 条件が `true` の場合、そのステートメントが実行されます。それ以外の場合、`$endif$` 条件は式の評価を終了します。<br /><br /> 使用の例については、「[Visual Studio Project/Item Template Parameter Logic (Visual Studio プロジェクト/項目テンプレート パラメーター ロジック)](http://stackoverflow.com/questions/6709057/visual-studio-project-item-template-parameter-logic)」を参照してください。|  
  
## <a name="see-also"></a>関連項目
 [MSBuild リファレンス](../msbuild/msbuild-reference.md)   
 [条件構造](../msbuild/msbuild-conditional-constructs.md)   
 [チュートリアル: MSBuild プロジェクト ファイルのゼロからの作成](../msbuild/walkthrough-creating-an-msbuild-project-file-from-scratch.md)
