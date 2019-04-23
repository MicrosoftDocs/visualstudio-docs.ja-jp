---
title: Find コマンド | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- edit.find
helpviewer_keywords:
- Find command
- Edit.Find command
ms.assetid: f0c705dc-2b97-423d-abbf-5584d4827208
caps.latest.revision: 20
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: ee744a8ab3a22d640f3d48e7291b546f36415d24
ms.sourcegitcommit: 53aa5a413717a1b62ca56a5983b6a50f7f0663b3
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59667288"
---
# <a name="find-command"></a>Find コマンド
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

**[検索と置換]** ウィンドウの **[フォルダーを指定して検索]** タブにあるオプションのサブセットを使って、ファイルを検索します。  
  
## <a name="syntax"></a>構文  
  
```  
Edit.Find findwhat [/case] [/doc | /proc | /open | /sel]   
[/markall] [/options] [/reset] [/up] [/wild | /regex] [/word]  
```  
  
## <a name="arguments"></a>引数  
 `findwhat`  
 必須です。 検索するテキスト。  
  
## <a name="switches"></a>スイッチ  
 /case または /c  
 任意。 `findwhat` 引数で指定されている語句と大文字および小文字の使い分けが正確に一致する場合にのみ、一致と見なします。  
  
 /doc または /d  
 任意。 現現在のドキュメントだけを検索します。 使用可能な検索スコープの中から 1 つだけ指定します (`/doc`、`/proc`、`/open`、または `/sel`)。  
  
 /markall または /m  
 任意。 現在のドキュメント内で、検索一致項目が含まれている各行にグラフィックを配置します。  
  
 /open または /o  
 任意。 開いているすべてのドキュメントを 1 つのドキュメントであるかのように検索します。 使用可能な検索スコープの中から 1 つだけ指定します (`/doc`、`/proc`、`/open`、または `/sel`)。  
  
 /options または /t  
 任意。 現在の検索オプションの設定の一覧を表示し、検索は行いません。  
  
 /proc または /p  
 任意。 現在のプロシージャだけを検索します。 使用可能な検索スコープの中から 1 つだけ指定します (`/doc`、`/proc`、`/open`、または `/sel`)。  
  
 /reset または /e  
 任意。 検索オプションを既定の設定に戻し、検索は行いません。  
  
 /sel または /s  
 任意。 現在の選択項目だけを検索します。 使用可能な検索スコープの中から 1 つだけ指定します (`/doc`、`/proc`、`/open`、または `/sel`)。  
  
 /up または /u  
 任意。 ファイルの現在の位置からファイルの先頭に向かって検索します。 既定では、ファイルの現在位置から検索を開始し、ファイルの末尾に向かって検索されます。  
  
 /regex または /r  
 任意。 `findwhat` 引数に含まれる定義済みの特殊文字を、リテラル文字ではなく、テキストのパターンを表す表記として使います。 正規表現文字の一覧については、「[正規表現](../../ide/using-regular-expressions-in-visual-studio.md)」をご覧ください。  
  
 /wild または /l  
 任意。 `findwhat` 引数に含まれる定義済みの特殊文字を、文字または文字のシーケンスを表す表記として使います。  
  
 /word または /w  
 任意。 単語全体と一致するもののみを検索します。  
  
## <a name="example"></a>例  
 次の例では、現在選択されているコード セクションで、"somestring" という語を、大文字と小文字を区別して検索します。  
  
```  
>Edit.Find somestring /sel /case  
```  
  
## <a name="see-also"></a>関連項目  
 [コマンド ウィンドウ](../../ide/reference/command-window.md)   
 [[検索/コマンド] ボックス](../../ide/find-command-box.md)   
 [Visual Studio のコマンド](../../ide/reference/visual-studio-commands.md)   
 [Visual Studio コマンドのエイリアス](../../ide/reference/visual-studio-command-aliases.md)
