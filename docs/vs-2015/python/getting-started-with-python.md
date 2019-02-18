---
title: Python の概要 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-python
ms.topic: conceptual
ms.assetid: 33f4f6fb-0ae4-4234-9df2-531f2d3af17f
caps.latest.revision: 13
author: kraigb
ms.author: kraigb
manager: jillfra
ms.openlocfilehash: 18e55aef8d95110dc44f20084eb5e45f643bf3cf
ms.sourcegitcommit: c496a77add807ba4a29ee6a424b44a5de89025ea
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 01/24/2019
ms.locfileid: "54833944"
---
# <a name="getting-started-with-python"></a>Python の概要
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Python Tools for Visual Studio (PTVS) では、無料、[オープン ソース](https://github.com/Microsoft/ptvs)強力な Python 開発エクスペリエンスを Visual Studio のプラグイン。  
  
## <a name="python-the-language"></a>言語としての Python
  
Python は、多くの大学、科学者、アプリのスクリプト作成者、一般の開発者、およびプロの開発者、アプリケーション、web サイト、およびクラウド サービスでの操作で使用される一般的なプログラミング言語です。

プログラミング言語として Python に示します。
  
- 信頼性が高い。
- クイック プログラムのスクリプトを作成、アプリのスクリプト、デスクトップ アプリ、web サーバー、web サービス、および科学技術計算に一般的に便利です。
- 簡単に学ぶことができ、正しくコーディングできるように適切に設計されている (多くの大学でプログラミングの入門コースに使用される)。
- 柔軟な命令型、機能、およびオブジェクト指向のプログラミング スタイルをサポートします。
- 無料かつオープン ソース。
- すべての主要なオペレーティング システムで適切に実行されます。  
- 無料かつ便利で適切に設計された多くのライブラリによってサポートされています。  
- 多数のドキュメント、サンプル、および強力な開発者コミュニティによってサポートされています。  

詳細については、言語、するを起動[初心者向けの Python](https://www.python.org/about/gettingstarted/) python.org でします。

Python 自体をインストールするを参照してください。 [ https://www.python.org/download/](https://www.python.org/download/)します。
 
  
## <a name="python-tools-for-visual-studio"></a>Python Tools for Visual Studio
  
Python Tools for Visual Studio からインストールできます[visualstudio.com](https://www.visualstudio.com/explore/python-vs)、次の機能を提供します。  
  
- さまざまなバージョンの CPython、IronPython、IPython など、複数のインタープリターのサポート  
- Python コードのフォルダー構造を暗黙的に取得し、またアプリ コード、テスト コード、Web ページ、JavaScript、ビルド スクリプトなどを識別できるように、明示的な制御も可能にするプロジェクト システム。  
- コンソール、Web、Azure、データ サイエンスおよび他の種類のプロジェクト用のプロジェクト テンプレート。    
- Azure SDK for Python (下記参照)    
- 構文の色分け、すべてのコードとライブラリ間でのオートコンプリート、シグネチャ ヘルプ、クラス ビュー、定義への移動、すべての参照の検索、リファクタリングなどを含む、豊富な編集とコード読解の機能。    
- 対話型 (REPL) ウィンドウ
- データ可視化を備えた IPython。
- IronPython および .NET/WPF のサポート。    
- Visual Studio プロジェクトを使用しない機能豊富なデバッグ、既存の実行可能ファイルに対する機能、混合モードのデバッグ、Windows/Linux/Mac へのリモート デバッグ、および対話型ウィンドウ内でのデバッグ。   
- プロファイル ツール。  
- テスト用ツール。  
  
使い始めるにあたり、次のリソースを参考にしてください。

- [インストール ガイド](https://github.com/Microsoft/PTVS/wiki/PTVS-Installation)    
- [概要および詳細情報の短いビデオ](https://www.youtube.com/playlist?list=PLReL099Y5nRdLgGAdrb_YeTdEnd23s6Ff)  
- インストールと機能のデモ (27 分)] (https://www.youtube.com/watch?v=JNNAOypc6Ek)  
- [ドキュメント](https://github.com/Microsoft/PTVS/wiki)  


Visual Studio が提供しないこと現時点では、埋め込まれた Python インタープリターを使用してプログラムを実質的には、Python を使用してスタンドアロン実行可能ファイルを作成するための手段に注意してください。 ただし、[StackOverflow](http://stackoverflow.com/questions/5458048/how-to-make-a-python-script-standalone-executable-to-run-without-any-dependency)で説明されているように、Python コミュニティでは、多様な実行方法が紹介されています。 また、CPython はネイティブ アプリケーション内への埋め込みをサポートしています。詳細については、ブログの投稿「[Using CPython's Embeddable Zip File](https://blogs.msdn.microsoft.com/pythonengineering/2016/04/26/cpython-embeddable-zip-file/)」(CPython の埋め込み可能な Zip ファイルの使用方法) を参照してください。
  
## <a name="building-ui-with-python"></a>Python を使用した UI の構築  

メインの提供は Python で UI を構築、 [Qt Project](https://www.qt.io/qt-for-application-development/)と呼ばれる Python のバインディング[PySide (公式バインディング)](http://wiki.qt.io/PySide) (も参照してください[PySide のダウンロード](https://download.qt.io/official_releases/pyside/.)) と[PyQt](https://wiki.python.org/moin/PyQt)します。 現在のところ、Visual Studio の Python のサポートには、UI 開発用のツールは含まれていません。

## <a name="azure-sdk-for-python"></a>Azure SDK for Python
  
Windows、Mac、および Linux をサポートしている Azure SDK for Python を使用すると、Microsoft Azure サービスの使用と管理が簡単になります。 詳細については、次のリソースを参照してください。 

- SDK をインストールするには、「[Python Package Index (Python パッケージ インデックス)](https://pypi.python.org/pypi/azure)」を使用するか、Azure ドキュメントの 「[Python と SDK のインストール](https://azure.microsoft.com/documentation/articles/python-how-to-install/)」の手順に従ってください。 
- [Azure SDK for Python デベロッパー センター](https://azure.microsoft.com/develop/python/)には、チュートリアルによるインストールからドキュメント化までの多数のヘルプがあります。  いくつかの要点を以下に示します。  
- 使い方ガイド:
  - [Python から Azure BLOB ストレージを使用する方法](https://azure.microsoft.com/develop/python/how-to-guides/blob-service/)  
  - [Python から Queue ストレージを使用する方法](https://azure.microsoft.com/develop/python/how-to-guides/queue-service/)  
  - [Python から Table ストレージを使用する方法](https://azure.microsoft.com/develop/python/how-to-guides/table-service/)  
  - [Service Bus キューの使用方法](https://azure.microsoft.com/develop/python/how-to-guides/service-bus-queues/)
  - [Service Bus のトピックとサブスクリプションの使用方法](https://azure.microsoft.com/develop/python/how-to-guides/service-bus-topics/) 
  - [Python からサービス管理を使用する方法](https://azure.microsoft.com/develop/python/how-to-guides/service-management/)  

## <a name="scientific-computing"></a>科学技術計算

すべての Python データ科学ライブラリに加えて、Python Tools for Visual Studio は、Azure でホスト可能な IPython と IPython Notebooks をサポートしています。

IPython と科学技術計算のライブラリ (matplotlib、scipy、numpy など) を[カリフォルニア大学アーバイン校](http://www.lfd.uci.edu/~gohlke/pythonlibs/#scipy-stack)から入手することをお勧めします。  
  
## <a name="see-also"></a>参照  

[PTVS の概要。Visual Studio のセットアップ](../python/getting-started-with-ptvs-setting-up-visual-studio.md)
[PTVS の概要。コーディングの開始 (プロジェクト)](../python/getting-started-with-ptvs-start-coding-projects.md)
[PTVS の概要。コードの編集](../python/getting-started-with-ptvs-editing-code.md)
[PTVS の概要。デバッグ](../python/getting-started-with-ptvs-debugging.md)
[PTVS の概要。対話型 Python](../python/getting-started-with-ptvs-interactive-python.md)
[PTVS の概要。Azure で web サイトの作成](../python/getting-started-with-ptvs-building-a-website-in-azure.md)
