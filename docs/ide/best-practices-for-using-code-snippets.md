---
title: "コード スニペットを使用するためのベスト プラクティス | Microsoft Docs"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-general
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- code snippets, best practices
- code snippets, security
ms.assetid: a293ec17-4dd7-4a99-8eeb-99f44a822a8b
caps.latest.revision: "22"
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 34424ae13a47008eaefa3634f2bf25d31daf285e
ms.sourcegitcommit: f40311056ea0b4677efcca74a285dbb0ce0e7974
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/31/2017
---
# <a name="best-practices-for-using-code-snippets"></a>コード スニペットを使用するためのベスト プラクティス
コード スニペットのコードは、最も基本的な処理方法のみを示しています。 ほとんどのアプリケーションでは、そのアプリケーションに合わせてコードを変更する必要があります。  
  
## <a name="handling-exceptions"></a>例外処理  
 通常、コード スニペットの Try…Catch ブロックは、すべての例外をキャッチして再スローします。 これは、プロジェクトにより適していない場合があります。 例外ごとに、対応方法はいくつかあります。 たとえば、「[方法: try/catch を使用して例外を処理する (C# プログラミング ガイド)](/dotnet/csharp/programming-guide/exceptions/how-to-handle-an-exception-using-try-catch)」と「[Try...Catch...Finally Statement](/dotnet/visual-basic/language-reference/statements/try-catch-finally-statement)」(Try...Catch...Finally ステートメント) を参照してください。  
  
## <a name="file-locations"></a>ファイルの位置  
 ファイルの位置をアプリケーションに採用する場合、次の点を考慮する必要があります。  
  
-   アクセス可能な場所を見つけます。 ユーザーはコンピューターの Program Files フォルダーにアクセスできない可能性があるので、アプリケーションのファイルと共にファイルを保存してもうまくいかないことがあります。  
  
-   セキュリティで保護された場所を見つけます。 ルート フォルダー (C:\\) にファイルを保存するのは安全ではありません。 アプリケーション データの場合は、\Application Data フォルダーをお勧めします。 個々のユーザー データの場合は、アプリケーションで \My Documents フォルダーに各ユーザーのファイルを作成できます。  
  
-   有効なファイル名を使用します。 <xref:System.Windows.Forms.OpenFileDialog> コントロールと <xref:System.Windows.Forms.SaveFileDialog> コントロールを利用し、無効なファイル名の可能性を減らすことができます。 ユーザーがファイルを選択してから、コードがファイルを操作するまでの時間に注意してください。その間にファイルが削除されることがあります。 また、ユーザーはファイルに書き込みアクセス許可を持っていない可能性があります。  
  
## <a name="security"></a>セキュリティ  
 スニペットのセキュリティは、ソース コードで使用する位置と、コード内でどのように変更するかによって変わります。 次の一覧は、考慮する必要がある点の一部です。  
  
-   ファイルおよびデータベースのアクセス  
  
-   コード アクセス セキュリティ  
  
-   リソース (イベント ログ、レジストリなど) の保護  
  
-   シークレットの保存  
  
-   入力の検証  
  
-   データをスクリプティング テクノロジに渡す  
  
 詳細については、「[Securing Applications](../ide/securing-applications.md)」(アプリケーションのセキュリティ保護) を参照してください。  
  
## <a name="downloaded-code-snippets"></a>ダウンロードしたコード スニペット  
 Visual Studio でインストールされる IntelliSense コード スニペット自体は、セキュリティ ハザードではありませんが、 アプリケーションのセキュリティ リスクになる可能性があります。 インターネットからダウンロードしたスニペットは、他のダウンロードしたコンテンツと同様に、十分に注意して扱ってください。  
  
-   信頼しているサイトからのみスニペットをダウンロードし、最新のウイルス対策ソフトウェアを使用します。  
  
-   ダウンロードしたすべてのスニペット ファイルはメモ帳または Visual Studio の XML エディターで開き、よく確認してからインストールします。 次の問題がないか確認します。  
  
    -   スニペット コードを実行した場合にシステムが破損する可能性があります。 ソース コードをよく読んでから実行してください。  
  
    -   スニペット ファイルのヘルプ URL ブロックには、悪意のあるスクリプト ファイルを実行する URL や、不快感を与える Web サイトを表示する URL が含まれている可能性があります。  
  
    -   スニペットには、プロジェクトに自動的に追加され、任意の場所からシステムに読み込まれる参照が含まれている可能性があります。 このような参照は、スニペットをダウンロードしたコンピューターにダウンロードされている可能性があります。 また、スニペットから、悪意のあるコードを実行する参照内のメソッドを呼び出す可能性があります。 このような攻撃から保護するには、スニペット ファイルのインポート ブロックと参照ブロックを確認します。  
  
## <a name="see-also"></a>関連項目  
 [Visual Basic の IntelliSense コード スニペット](/dotnet/visual-basic/developing-apps/using-ide/intellisense-code-snippets)   
 [アプリケーションの保護](../ide/securing-applications.md)   
 [コード スニペット](../ide/code-snippets.md)