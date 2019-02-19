---
title: コード スニペットを使用するためのベスト プラクティス | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- code snippets, best practices
- code snippets, security
ms.assetid: a293ec17-4dd7-4a99-8eeb-99f44a822a8b
caps.latest.revision: 26
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 750d96442f59c29a8e565e6b57eda292656ad1f7
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "54770324"
---
# <a name="best-practices-for-using-code-snippets"></a>コード スニペットを使用するためのベスト プラクティス
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

コード スニペットのコードは、最も基本的な処理方法のみを示しています。 ほとんどのアプリケーションでは、そのアプリケーションに合わせてコードを変更する必要があります。  
  
## <a name="handling-exceptions"></a>例外処理  
 通常、コード スニペットの Try…Catch ブロックは、すべての例外をキャッチして再スローします。 これは、プロジェクトにより適していない場合があります。 例外ごとに、対応方法はいくつかあります。 たとえば、「[方法:処理、例外 try/catch を使用して (c# プログラミング ガイド)](http://msdn.microsoft.com/library/ca8e3773-980e-4767-8633-7408540e9818)と[お試しください.キャッチしてください.Finally ステートメント](http://msdn.microsoft.com/library/d6488026-ccb3-42b8-a810-0d97b9d6472b)します。  
  
## <a name="file-locations"></a>ファイルの位置  
 ファイルの位置をアプリケーションに採用する場合、次の点を考慮する必要があります。  
  
-   アクセス可能な場所を見つけます。 ユーザーはコンピューターの Program Files フォルダーにアクセスできない可能性があるので、アプリケーションのファイルと共にファイルを保存してもうまくいかないことがあります。  
  
-   セキュリティで保護された場所を見つけます。 ルート フォルダー (C:\\) にファイルを保存するのは安全ではありません。 アプリケーション データの場合は、\Application Data フォルダーをお勧めします。 個々のユーザー データの場合は、アプリケーションで \My Documents フォルダーに各ユーザーのファイルを作成できます。  
  
-   有効なファイル名を使用します。 <xref:System.Windows.Forms.OpenFileDialog> コントロールと <xref:System.Windows.Forms.SaveFileDialog> コントロールを利用し、無効なファイル名の可能性を減らすことができます。 ユーザーがファイルを選択してから、コードがファイルを操作するまでの時間に注意してください。その間にファイルが削除されることがあります。 また、ユーザーはファイルに書き込みアクセス許可を持っていない可能性があります。  
  
## <a name="security"></a>セキュリティ  
 スニペットのセキュリティは、ソース コードで使用する位置と、コード内でどのように変更するかによって変わります。 次の一覧は、考慮する必要がある点の一部です。  
  
- ファイルおよびデータベースのアクセス  
  
- コード アクセス セキュリティ  
  
- リソース (イベント ログ、レジストリなど) の保護  
  
- シークレットの保存  
  
- 入力の検証  
  
- データをスクリプティング テクノロジに渡す  
  
  詳細については、「[Securing Applications](../ide/securing-applications.md)」(アプリケーションのセキュリティ保護) を参照してください。  
  
## <a name="downloaded-code-snippets"></a>ダウンロードしたコード スニペット  
 Visual Studio でインストールされる IntelliSense コード スニペット自体は、セキュリティ ハザードではありませんが、 アプリケーションのセキュリティ リスクになる可能性があります。 インターネットからダウンロードしたスニペットは、他のダウンロードしたコンテンツと同様に、十分に注意して扱ってください。  
  
-   信頼しているサイトからのみスニペットをダウンロードし、最新のウイルス対策ソフトウェアを使用します。  
  
-   ダウンロードしたすべてのスニペット ファイルはメモ帳または Visual Studio の XML エディターで開き、よく確認してからインストールします。 次の問題がないか確認します。  
  
    -   スニペット コードを実行した場合にシステムが破損する可能性があります。 ソース コードをよく読んでから実行してください。  
  
    -   スニペット ファイルのヘルプ URL ブロックには、悪意のあるスクリプト ファイルを実行する URL や、不快感を与える Web サイトを表示する URL が含まれている可能性があります。  
  
    -   スニペットには、プロジェクトに自動的に追加され、任意の場所からシステムに読み込まれる参照が含まれている可能性があります。 このような参照は、スニペットをダウンロードしたコンピューターにダウンロードされている可能性があります。 また、スニペットから、悪意のあるコードを実行する参照内のメソッドを呼び出す可能性があります。 このような攻撃から保護するには、スニペット ファイルのインポート ブロックと参照ブロックを確認します。  
  
## <a name="see-also"></a>関連項目  
 [Visual Basic の IntelliSense コード スニペット](http://msdn.microsoft.com/library/ffdde4c9-8141-4906-b09b-15181357a643)   
 [アプリケーションの保護](../ide/securing-applications.md)   
 [コード スニペット](../ide/code-snippets.md)
