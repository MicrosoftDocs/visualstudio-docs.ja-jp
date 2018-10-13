---
title: Visual Studio 2015 で問題を報告する方法 | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 24ecb76e-b7ad-432d-88ab-d9849963465d
caps.latest.revision: 15
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: fcc49f96faf043101ffb2462d544e41394b38e7b
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2018
ms.locfileid: "49290395"
---
# <a name="how-to-report-a-problem-with-visual-studio-2015"></a>Visual Studio 2015 で問題を報告する方法
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio 2017 の最新ドキュメントについては、次を参照してください。 [Visual Studio 2017 で問題を報告する方法](/visualstudio/ide/how-to-report-a-problem-with-visual-studio-2017)します。

Visual Studio 2015 で問題が発生した場合について知りたいが診断して修正できるようにします。  **[問題の報告]** ツールを使うと、問題に関する詳しい情報を収集し、数回のクリックで問題を Microsoft に送信できます。  
  
 Microsoft は、お客様のプライバシーを尊重いたします。 お客様から送信していただいたデータの扱いについて詳しくは、「 [Microsoft Visual Studio 製品ファミリのプライバシーに関する声明](https://www.visualstudio.com/en-us/dn948229)」をご覧ください。  
  
## <a name="open-the-report-a-problem-tool"></a>[問題の報告] ツールを開きます  
 タイトル バーで **[クイック起動]** の横にあるユーザー フィードバック アイコンをクリックするか、**[ヘルプ &#124; フィードバックの送信 &#124; 問題の報告]** の順にクリックします。  
  
 ![[問題の報告] メニュー項目](../ide/media/report-a-problem-menu-item.png "[問題の報告] メニュー項目")  
  
## <a name="describe-the-problem"></a>問題について説明します  
  
###  <a name="describe_the_problem"></a>  
  
1.  問題がわかりやすいタイトルを指定していただくと、適切な Visual Studio チームに転送するのに役立ちます。  
  
2.  可能であれば、問題を再現する手順など、さらに詳しい情報を記載します。  
  
3.  ドロップダウンから、問題のある領域を選択します。 不明な場合は、問題があると思われる妥当な場所を記載します。  
  
 ![[問題の報告] ダイアログ](../ide/media/report-a-problem-dialog.png "[問題の報告] ダイアログ")  
  
## <a name="provide-a-screenshot-optional"></a>スクリーンショットを提供します (オプション)  
 **[スクリーンショットを含める]** を選び、Microsoft に現在の画面を送信します。 ツールでは、画面中のこの問題が表示された部分のみにイメージをトリミングできます。 **[追加のファイルの添付]** ボタンをクリックして、その他のスクリーン ショットやファイルをさらに添付できます。  
  
## <a name="provide-a-trace-and-heap-dump-optional"></a>トレースとヒープ ダンプを提供します (省略可能)  
  
###  <a name="provide_a_trace_and_heap_dump"></a>  
  
1.  トレースとヒープ ダンプのファイルは、問題を診断するうえで非常に役立ちます。   [問題の報告] ツールで再現する手順を記録し Microsoft にデータを送信してくだされば、大変助かります。  
  
2.  **[操作を記録して問題を再現する]** の横にあるシェブロンをクリックします。 問題が原因で Visual Studio のハングやクラッシュが生じる場合、Visual Studio の別のインスタンスを開き、リスト ビューから選択します。  
  
3.  **[記録の開始]** をクリックし、問題を再現するための操作を行います。 完了したら、フローティング ウィンドウで **[記録の停止]** ボタンをクリックします。  
  
4.  記録された情報を Visual Studio が収集してパッケージ化するまで、しばらくお待ちください。 収集プロセスが完了すると、次のようなダイアログ ボックスが表示されます。  
  
     ![トレース ファイルの記録](../ide/media/record-a-trace-file.png "トレース ファイルの記録")  
  
## <a name="describe-the-workaround-if-there-is-one"></a>回避策がある場合は、記載します  
 問題を回避できた場合は、そのためのエディット ボックスに回避策を記載してください。 これは、問題の診断だけでなく、同じ問題が発生した他のユーザーのサポートにも役立ちます。  
  
## <a name="submit-the-report"></a>レポートを送信します  
 [送信] ボタンをクリックして、イメージ、トレースやダンプ ファイルと共にレポートを送信します。 **[送信]** ボタンが灰色表示の場合、タイトルと説明が記載されていることを確認します。  
  
## <a name="see-also"></a>関連項目  
 [ご意見](../ide/talk-to-us.md)

