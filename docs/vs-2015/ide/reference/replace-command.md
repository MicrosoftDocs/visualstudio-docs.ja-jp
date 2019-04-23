﻿---
title: Replace コマンド | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- edit.replace
helpviewer_keywords:
- Edit.Replace command
- Replace command
ms.assetid: a15767f1-5a3d-44f5-8c77-7b0f1157f340
caps.latest.revision: 20
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 4ef58a39f1ff96a3c72cbb5a48940e378997cbca
ms.sourcegitcommit: 53aa5a413717a1b62ca56a5983b6a50f7f0663b3
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59664489"
---
# <a name="replace-command"></a>Replace コマンド
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

**[検索と置換]** ウィンドウの **[フォルダーを指定して置換]** タブにあるオプションのサブセットを使用してファイル内のテキストを置換します。  
  
## <a name="syntax"></a>構文  
  
```  
Edit.Replace findwhat replacewith [/all] [/case]  
[/doc|/proc|/open|/sel] [/hidden] [/options] [/reset] [/up]  
[/wild|/regex] [/word]  
```  
  
## <a name="arguments"></a>引数  
 `findwhat`  
 必須です。 検索するテキスト。  
  
 `replacewith`  
 必須です。 一致したテキストと置き換えるテキスト。  
  
## <a name="switches"></a>スイッチ  
 /all または /a  
 任意。 検索されたすべてのテキストを置換します。  
  
 /case または /c  
 任意。 `findwhat` 引数に指定したテキストと大文字/小文字が完全に一致する場合にだけ、一致したと見なされます。  
  
 /doc または /d  
 任意。 現現在のドキュメントだけを検索します。 使用可能な検索スコープの中から 1 つだけ指定します (`/doc`、`/proc`、`/open`、または `/sel`)。  
  
 /hidden または /h  
 任意。 デザイン時のコントロールのメタデータ、アウトライン表示のドキュメントの非表示の領域、折りたたまれているクラスやメソッドのような、折りたたまれて非表示になっているテキストを検索します。  
  
 /open または /o  
 任意。 開いているすべてのドキュメントを 1 つのドキュメントであるかのように検索します。 使用可能な検索スコープの中から 1 つだけ指定します (`/doc`、`/proc`、`/open`、または `/sel`)。  
  
 /options または /t  
 任意。 現在の検索オプションの設定の一覧を表示し、検索は行いません。  
  
 /proc または /p  
 任意。 現在のプロシージャだけを検索します。 使用可能な検索スコープの中から 1 つだけ指定します (`/doc`、`/proc`、`/open`、または `/sel`)。  
  
 /regex または /r  
 任意。 `findwhat` 引数に含まれる定義済みの特殊文字を、リテラル文字ではなく、テキストのパターンを表す表記として使います。 正規表現文字の一覧については、「[正規表現](../../ide/using-regular-expressions-in-visual-studio.md)」をご覧ください。  
  
 /reset または /e  
 任意。 検索オプションを既定の設定に戻し、検索は行いません。  
  
 /sel または /s  
 任意。 現在の選択項目だけを検索します。 使用可能な検索スコープの中から 1 つだけ指定します (`/doc`、`/proc`、`/open`、または `/sel`)。  
  
 /up または /u  
 任意。 現在の位置から上方向にファイルを検索します。 既定では、ファイルの現在位置から検索を開始し、下方向に検索されます。  
  
 /wild または /l  
 任意。 `findwhat` 引数に含まれる定義済みの特殊文字を、文字または文字のシーケンスを表す表記として使います。  
  
 /word または /w  
 任意。 単語全体と一致するもののみを検索します。  
  
## <a name="example"></a>例  
 次の例では、開いているすべてのドキュメントで `btnSend` を検索し、`btnSubmit` に置換します。  
  
```  
>Edit.Replace btnSend btnSubmit /open  
```  
  
## <a name="see-also"></a>関連項目
 [テキストの検索と置換](../../ide/finding-and-replacing-text.md)   
 [コマンド ウィンドウ](../../ide/reference/command-window.md)   
 [[検索/コマンド] ボックス](../../ide/find-command-box.md)   
 [Visual Studio のコマンド](../../ide/reference/visual-studio-commands.md)   
 [Visual Studio コマンドのエイリアス](../../ide/reference/visual-studio-command-aliases.md)
