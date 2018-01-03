---
title: "[クイック起動] ([オプション] ダイアログ ボックス - [環境]) | Microsoft Docs"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-general
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- VS.ToolsOptionsPages.Environment.QuickLaunch
- vs.quicklaunch
helpviewer_keywords:
- searching IDE
- IDE, searching
ms.assetid: 4200f297-d065-4723-9a30-d91ff2e26c9d
caps.latest.revision: "11"
author: gewarren
ms.author: gewarren
manager: ghogen
ms.workload: multiple
ms.openlocfilehash: 0f71cca51a27c8ed9d6467d99425d4d3b721d195
ms.sourcegitcommit: 32f1a690fc445f9586d53698fc82c7debd784eeb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/22/2017
---
# <a name="quick-launch-environment-options-dialog-box"></a>[クイック起動] \([オプション] ダイアログ ボックス - [環境])
**クイック起動**を使用すると、オプション、テンプレート、メニューなどの IDE アセットのアクションをすばやく検索して実行できます。 **クイック起動**を使用してコードおよびシンボルを検索できません。 **クイック起動**の検索ボックスは、メニュー バーの右上隅にあり、Ctrl キーを押しながら Q キーを押すとアクセスできます。 ボックスに検索文字列を入力します。 @ を含む文字列を検索するには、'@@' を使用します。  
  
 Visual Studio をインストールすると、**クイック起動**は既定で有効になります。 メニュー バーで、**[ツール]**、**[オプション]** の順にクリックし、**クイック起動**を表示または非表示にできます。 **[環境]** ノードを展開し、**[クイック起動]** をクリックします。 **[クイック起動を有効にする]** チェック ボックスをオンまたはオフにします。 また、このページの検索カテゴリを有効または無効にできます。  
  
## <a name="category-list"></a>カテゴリの一覧  
 クイック起動の検索結果は、**[直前に使用]**、**[メニュー]**、**[オプション]**、および **[開かれているドキュメント]** という 4 つのカテゴリで項目の数と共に表示されます。 検索結果をカテゴリ別に走査するには、Ctrl キーを押しながら Q キーを押して、次のカテゴリのすべての結果を表示します。 最後のカテゴリが表示された後、Ctrl キーを押しながら Q キーを押すと、各カテゴリのいくつかの結果が表示されます。 Ctrl キーと Shift キーを押しながら Q キーを押すと、カテゴリ間を逆の順序で移動できます。 各カテゴリのすべての検索結果を表示するには、カテゴリ名を選択します。  
  
 次のショートカットを使用して、検索を特定のカテゴリに限定できます。  
  
|カテゴリ|ショートカット|ショートカットの説明|  
|--------------|--------------|--------------------------|  
|直前に使用|@mru<br /><br /> たとえば、`@mru font`|**直前に使用**した項目が最大 5 つ表示されます。|  
|メニュー|@menu<br /><br /> たとえば、`@menu font`|検索をメニュー項目に制限します。|  
|オプション|@opt<br /><br /> たとえば、`@opt font`|検索を **[オプション]** ダイアログ ボックスの設定に制限します。|  
|ドキュメント|@doc<br /><br /> たとえば、`@doc font`|検索を検索条件の開いているドキュメントのファイル名とパスに限定しますが、ファイル内のテキストは検索されません。|  
  
> [!NOTE]
>  ショートカット キーは、**[オプション]** ダイアログ ボックスにある **[全般]** の **[キーボード]** ページで変更できます。  
  
## <a name="show-previous-results"></a>前の結果の表示  
 既定では、入力した検索用語は検索セッション間で保持されません。 語句を検索し、カーソルを**クイック起動**領域の外側に移動させてから戻した場合は、検索文字列がクリアされます。 検索結果を保持するには、**[オプション]** ダイアログ ボックスに移動して、**[クイック起動]** をクリックし、**[クイック起動がアクティブ化されたときに以前の検索結果を表示する]** チェック ボックスをオンにします。 次回に検索を実行し、クイック起動領域の外側に移動してから戻ると、クイック起動で最後に使用された検索用語が保持され、検索結果が表示されます。  
  
 **クイック起動**の使用に関する最新のヒントとテクニックについては、「[The Visual Studio Blog](http://go.microsoft.com/fwlink/?LinkId=236054)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [一般的なユーザー インターフェイス要素 (Visual Studio)](../../ide/reference/general-user-interface-elements-visual-studio.md)   
 [[環境] ([オプション] ダイアログ ボックス)](../../ide/reference/environment-options-dialog-box.md)