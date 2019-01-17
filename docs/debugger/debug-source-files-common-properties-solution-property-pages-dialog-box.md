---
title: ソース ファイル、一般的なプロパティは、ソリューション プロパティ ページ ダイアログ ボックスのデバッグ |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.debug.options.FindSource
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
- SQL
helpviewer_keywords:
- Debug Source Files property page
- debugging [Visual Studio], specifying source and symbol files
- source files, specifying in debugger
- debugger, source files
ms.assetid: 0af11464-eeb1-4d0b-87a6-0cc96779afb1
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: a722422306a16ee7e2dc340448f0e082f8a1f014
ms.sourcegitcommit: 37fb7075b0a65d2add3b137a5230767aa3266c74
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 01/02/2019
ms.locfileid: "53931909"
---
# <a name="debug-source-files-common-properties-solution-property-pages-dialog-box"></a>[デバッグ ソース ファイル] ([ソリューション プロパティ ページ] ダイアログ ボックス - [共通プロパティ])
このプロパティ ページでは、ソリューションのデバッグ時にデバッガーによってソース ファイルが検索される場所を指定します。  
  
 **[デバッグのソース ファイル]** プロパティ ページを開くには、**ソリューション エクスプローラー**でソリューションを右クリックし、ショートカット メニューの **[プロパティ]** をクリックします。 **[共通プロパティ]** フォルダーを展開し、**[デバッグのソース ファイル]** ページをクリックします。  
  
 **ソース コードを含んでいるディレクトリ**  
 ソリューションのデバッグ時に、デバッガーによってソース ファイルが検索されるディレクトリの一覧が表示されます。 指定されたディレクトリのサブディレクトリも検索されます。  
  
 **以下のソース ファイルを探さない**  
 デバッガーによる読み取りから除外するファイルの名前を入力できます。 デバッガーは、上で指定したディレクトリのいずれかでこれらのファイルを見つけた場合、それを無視します。 デバッグ中に **[ソース ファイルの検索]** ダイアログ ボックスが表示されたときに **[キャンセル]** をクリックすると、検索中のファイルがこのリストに追加され、そのファイルの検索が中止されます。  
  
## <a name="see-also"></a>「  
 [デバッガーのセキュリティ](../debugger/debugger-security.md)   
 [デバッガーの設定と準備](../debugger/debugger-settings-and-preparation.md)