---
title: "Visual Studio ヘルプ ビューアーのインデックスを使用する | Microsoft Docs"
ms.custom: 
ms.date: 11/02/2017
ms.reviewer: 
ms.suite: 
ms.technology: vs-help-viewer
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Index tab [Help Viewer]
- Help Viewer, using the index
- Help Viewer, Index tab
- using the index [Help Viewer]
- index filtering [Help Viewer]
- Help Viewer, index filtering
ms.assetid: cb071e93-f297-459c-a6fa-8ae0dabc42a4
caps.latest.revision: "15"
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: ea90dba4090565143c84d510b5e4f9e998cfb5fc
ms.sourcegitcommit: ec1c7e7e3349d2f3a4dc027e7cfca840c029367d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2017
---
# <a name="finding-topics-by-using-the-help-viewer-index"></a>ヘルプ ビューアーのインデックスの使用によるトピックの検索
インデックスには、インストールされているコンテンツのトピックに関連付けられているキーワードの一覧が含まれます。 各トピックには複数のキーワードが関連付けられている場合があり、各キーワードは複数のトピックに関連付けられている場合があります。 このインデックスの使い方は本の索引と同じです。  
  
## <a name="to-find-a-topic-by-using-the-index"></a>インデックスを使ってトピックを検索するには  
**[インデックス]** タブで、以下のいずれかのタスクを実行します。
  
-   テキスト ボックスで検索するキーワードを指定します。 たとえば、"更新"、"更新済み"、"更新中" などのキーワードでトピックを検索するには、"更新" と指定します。  
  
    タブの上部にあるフィルター ボタンを選ぶと、指定したテキストを含むすべてのエントリ、または指定したテキストで始まるエントリだけを表示できます。  
  
    > [!NOTE]
    >  フィルター ボタンが境界線のある濃い色の背景で表示されているときは、エントリに、指定したテキストが_含まれている_必要があります。 背景と境界線が表示されていない場合は、エントリは、指定したテキストで_始まっている_必要があります。  
  
-   インデックスをスクロールし、キーワードを選びます。  
  
    指定したキーワードが 1 つのトピックだけに関連付けられている場合は、そのトピックが表示されます。 それ以外の場合は、そのキーワードに関連付けられているすべてのトピックの一覧が表示されます。

## <a name="index-search-tips"></a>インデックス検索のヒント  
インデックスの使用は簡単です。キーワードの最適な入力方法を理解しておけば、インデックス検索の生産性をさらに向上させることができます。  
  
### <a name="general-guidelines"></a>一般的なガイドライン  
-   インデックス エントリ間をスクロールします。 すべてのトピックに同じようにインデックスが付けられているわけではなく、お客様に最も役立つ可能性のあるものが、リスト内で予想よりも上または下にある場合があります。  
  
-   「an」や「the」などの冠詞は、インデックスでは無視されるため、省略します。  
  
-   目的のエントリが見つからない場合は、入力した単語を逆にします。  
  
    たとえば、「debugging inline assembly code」と入力しても関連するエントリが表示されない場合は、「assembly code, debugging inline」と入力してみてください。  
  
-   **[インデックス]** タブでフィルターを使用して、結果の数を減らします。  
  
### <a name="syntax-tips"></a>構文のヒント  
入力した語句のエントリが見つからない場合は、次の操作を試してください。  
  
-   その単語の最初の数文字、または語幹を入力します。 文字列の一部を入力すると、単数形または複数形のキーワードでインデックスが付けられているトピックを取得できます。  
  
    たとえば、上方の「properties」と「property」の検索を開始するには、「propert」と入力します。  
  
-   完了するタスクの動詞の動名詞 (-ing) の形式を入力します。 より特定のインデックス エントリを見つけるには、目的の項目について正確に説明する単語を追加します。  
  
    たとえば、取得するエントリをより多くするには「running」と入力し、より少なくするには「running programs」と入力します。  
  
-   独立した形容詞を入力します。 結果を絞り込むには、目的の項目について正確に説明する単語を追加します。  
  
    たとえば、取得するエントリの幅を広げるには「COM+」と入力し、より少なくするには「COM+ components」と入力します。  
  
-   探している単語または動詞の同意語を入力します。  
  
    たとえば、「building」という用語を入力した場合は、代わりに「creating」と入力してみてください。 
  
## <a name="see-also"></a>関連項目
[方法: 目次でトピックを検索する](../ide/how-to-find-topics-in-the-table-of-contents.md)  
[方法: トピックを検索する](../ide/how-to-search-for-topics.md)  
[Microsoft Help Viewer](../ide/microsoft-help-viewer.md)