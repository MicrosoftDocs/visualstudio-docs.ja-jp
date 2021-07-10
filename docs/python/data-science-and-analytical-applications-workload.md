---
title: データ サイエンスと分析のアプリケーション ワークロード
description: この Visual Studio ワークロードでは、Python、F# と、そのランタイム ディストリビューション (Anaconda など) を使うことができます。 (R は Visual Studio 2017 にのみ含まれています。)
ms.date: 02/28/2019
ms.topic: overview
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.workload:
- python
- data-science
ms.openlocfilehash: 2c12c8a0979ab081ea2f09faeeccdb5a8a9d2175
ms.sourcegitcommit: 398b4d4e5ce0f978720f11990db05b209766aedc
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/11/2021
ms.locfileid: "112016308"
---
# <a name="install-data-science-support-in-visual-studio"></a>Visual Studio でのデータ サイエンス サポートのインストール

Visual Studio のインストーラーを使って選択し、インストールするデータ サイエンスと分析のアプリケーション ワークロードでは、次の言語とそのランタイム ディストリビューションを使用できます。

::: moniker range="vs-2017"
- [Python と Anaconda](../python/overview-of-python-tools-for-visual-studio.md)
- [F# と NET Framework](/dotnet/fsharp/)
- [R と Microsoft R Client](../rtvs/index.md)
::: moniker-end

::: moniker range="vs-2019"
- [Python](../python/overview-of-python-tools-for-visual-studio.md)
- [F# と NET Framework](/dotnet/fsharp/)
::: moniker-end

![Visual Studio インストーラーのデータ サイエンスと分析のアプリケーション ワークロード](media/workload/data-science-workload.png)

::: moniker range="vs-2017"
Python と R は、データ サイエンスで使用される主要な 2 つのスクリプト言語です。 いずれの言語も学習が簡単で、パッケージの機能豊富なエコシステムのサポートがあります。 それらのパッケージは、データの取得、クリーンアップ、モデルのトレーニング、展開およびプロットなどの広範囲のシナリオに対応しています。 F# も、さまざまなデータ処理タスクに適した機能第一の強力な .NET 言語です。
::: moniker-end

::: moniker range=">=vs-2019"
Python は、データ サイエンスで使用される主要なスクリプト言語です。 Python は学習が簡単で、パッケージの機能豊富なエコシステムのサポートがあります。 それらのパッケージは、データの取得、クリーンアップ、モデルのトレーニング、展開およびプロットなどの広範囲のシナリオに対応しています。 F# も、さまざまなデータ処理タスクに適した機能第一の強力な .NET 言語です。
::: moniker-end

<!--Note link on the image because this one is large -->
[![R、Python および F# が使用されている Visual Studio のスクリーンショット](media/workload/data-science-workload-screens.png)](media/workload/data-science-workload-screens.png#lightbox)

## <a name="workload-options"></a>ワークロード オプション

ワークロードは、既定で次のオプションをインストールします。これは、Visual Studio インストーラーのワークロードの [概要] セクションで変更できます。

::: moniker range=">=vs-2019"
- F# デスクトップ言語のサポート
- Python:
  - Python 言語サポート
  - Python Web サポート
::: moniker-end

::: moniker range="vs-2017"
- F# 言語サポート
- Python:
  - Python 言語サポート
  - [Anaconda3 64 ビット](https://www.continuum.io) (さまざまなデータ サイエンス ライブラリおよび Python インタープリターを含む Python ディストリビューションです。)
  - Python Web サポート
  - cookiecutter テンプレートのサポート
- R:
  - R 言語サポート
  - R 開発ツールのランタイム サポート
  - [Microsoft R Client](/machine-learning-server/r-client/what-is-microsoft-r-client) (単一ノードまたはクラスターで高速に計算を実行するための ScaleR ライブラリを含む、Microsoft 社の完全互換のコミュニティでサポートされている R インタープリターです。 [CRAN](https://cran.r-project.org/) の任意の R も使用できます。)
::: moniker-end

## <a name="sql-server-integration"></a>SQL Server の統合

::: moniker range="vs-2017"
SQL Server では、SQL Server 内で直接高度な分析を行うことが可能な Python と R の両方の使用をサポートしています。 R は SQL Server 2016 以降でサポートされており、Python は SQL Server 2017 CTP 2.0 以降でサポートされています。
::: moniker-end

::: moniker range=">=vs-2019"
SQL Server では、SQL Server 内で直接高度な分析を行うことが可能な Python の使用をサポートしています。 Python は SQL Server 2017 CTP 2.0 以降でサポートされています。
::: moniker-end

データが既にあるところでコードを実行すると、次のような利点があります。

- **データ移動が不要**: データをデータベースからアプリケーションまたはモデルに移動せずに、データベース内でアプリケーションをビルドできます。 この機能により、セキュリティ、コンプライアンス、ガバナンスおよび整合性の障壁が取り除かれ、大量のデータの移動に関係する同様の多数の問題もなくなります。 また、クライアントのマシンのメモリに入りきらないデータセットも使用できます。

- **導入が簡単**: モデルの準備ができたら、T-SQL スクリプトに単純に埋め込むことで、それを本番に導入することができます。 任意の言語で記述された任意の SQL クライアント アプリケーションで、ストアド プロシージャ呼び出しを使用して、モデルおよびインテリジェンスを利用することができます。 特定の言語統合は必要ありません。

- **エンタープライズ レベルのパフォーマンスとスケール**: メモリ内テーブルと列のストア インデックスなどの SQL Server の高度な機能を、RevoScale パッケージの高性能な拡張性の高い API と共に使用できます。 データを移動する必要がなくなるということは、データが大きくなった場合や、アプリケーションのパフォーマンスを向上させる場合のクライアント メモリの制約を回避できることも意味します。

- **拡張性が高い**: SQL Server に任意の最新のオープン ソース パッケージをインストールし実行して、SQL Server 内の大量のデータにディープ ラーニングおよび AI アプリケーションを構築できます。 SQL Server にパッケージをインストールすることは、ローカル マシンにパッケージをインストールするのと同じくらい簡単です。

- **追加コストなしで広範に利用可能**: 言語は、Express Edition を含む SQL Server 2017 以降のすべてのエディションに統合できます。

SQL Server への統合のメリットを最大限に得るには、Visual Studio インストーラーで **[SQL Server Data Tools]** オプションを使用して **データ ストレージと処理** ワークロードをインストールします。 後者のオプションにより、SQL IntelliSense、構文の強調表示および展開が可能になります。

![[データの保存と処理] ワークロード](media/workload/data-storage-workload.png) &nbsp;&nbsp;&nbsp;&nbsp; ![データの保存と処理ワークロード オプション](media/workload/data-storage-workload-options.png)

詳細情報

::: moniker range="vs-2017"
- [SQL Server と R の使用](../rtvs/integrating-sql-server-with-r.md)
- [SQL Server 2016 での R を使用したデータベース内の高度な分析 (ブログ)](https://blogs.technet.microsoft.com/dataplatforminsider/2016/03/29/in-database-advanced-analytics-with-r-in-sql-server-2016/)
::: moniker-end
- [SQL Server 2017 での Python: データベース内機械学習の強化 (ブログ)](https://blogs.technet.microsoft.com/dataplatforminsider/2017/04/19/python-in-sql-server-2017-enhanced-in-database-machine-learning/)

## <a name="additional-services-and-sdks"></a>その他のサービスと SDK

データ サイエンスと分析のアプリケーション ワークロードに直接あるものに加え、Azure Notebook サービスと Azure SDK for Python もデータ サイエンスに役立ちます。

Azure SDK for Python を使用すると、Windows、Mac、Linux で実行されているアプリケーションからの Microsoft Azure サービスの使用と管理が簡単になります。 詳細については、[Python 用 Azure SDK](/azure/python/) に関するページを参照してください。

Azure Notebook (現在プレビュー中) を使用すると、クラウドで Microsoft Azure で実行されている Jupyter Notebook に自由にオンライン アクセスできます。 このサービスには、使用を開始できるように Python、R および F# のサンプル ノートブックが含まれています。 [notebooks.azure.com](https://notebooks.azure.com/) にアクセスしてください。

<!--Note link on the image because this one is large -->
[![入門用の R のサンプルと Azure Notebooks のスクリーンショット](media/workload/data-science-workload-notebooks.png)](media/workload/data-science-workload-notebooks.png#lightbox)
