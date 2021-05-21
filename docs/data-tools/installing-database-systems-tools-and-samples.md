---
title: データベースの互換性
description: Microsoft SQL Server、Oracle、MySQL、PostgreSQL、SQLite、Firebird など、Visual Studio と互換性のあるデータベース システムを確認します。
ms.custom: SEO-VS-2020
ms.date: 09/06/2017
ms.topic: conceptual
helpviewer_keywords:
- database systems
- database compatibility
- databases for Visual Studio
ms.assetid: 821de34b-eaa9-40af-b9aa-b8305de16899
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: 41cf31c6cae310eb151969df0776788d6ea5b1e1
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99866698"
---
# <a name="compatible-database-systems-for-visual-studio"></a>Visual Studio 向けの互換性のあるデータベース システム

Visual Studio でデータ接続アプリケーションを開発するには、通常、データベース システムをローカル環境の開発用コンピューターにインストールした後、準備ができたらアプリケーションとデータベースを運用環境に配置します。 Visual Studio により、**データの保存と処理** ワークロードの一部として、SQL Server Express LocalDB がコンピューターにインストールされます。 この LocalDB インスタンスは、データ接続アプリケーションを迅速かつ簡単に開発するのに役立ちます。

データベース システムを、.NET アプリケーションからアクセスできるようにし、Visual Studio のデータ ツール ウィンドウに表示されるようにするには、ADO.NET データ プロバイダーが必要です。 .NET アプリケーションで Entity Data Model を使用する予定がある場合は、プロバイダーによって Entity Framework がサポートされている必要があります。 NuGet パッケージ マネージャーまたは Visual Studio Marketplace を通じて、多くのプロバイダーが提供されています。

Azure Storage API を使用している場合は、運用環境にデプロイする準備ができるまで料金がかからないよう、開発の間はローカル コンピューターに Azure ストレージ エミュレーターをインストールします。 詳細については、「[開発とテストのための Azure Storage Emulator 使用する](/azure/storage/common/storage-use-emulator)」を参照してください。

次の一覧には、Visual Studio プロジェクトで使用できる一般的なデータベース システムが含まれます。 この一覧はすべてを網羅しているわけではありません。 Visual Studio ツールと緊密に統合できる ADO.NET データ プロバイダーを提供しているサードパーティ ベンダーの一覧については、[ADO.NET データ プロバイダー](/dotnet/framework/data/adonet/data-providers)に関する記事を参照してください。

## <a name="microsoft-sql-server"></a>Microsoft SQL Server

SQL Server は、Microsoft の主要なデータベース オファリングです。 SQL Server 2016 を利用すると、画期的なパフォーマンス、高度なセキュリティ、豊富で統合されたレポートと分析が提供されます。 拡張性が高く高パフォーマンスのビジネス分析から、1 台のコンピューターでの使用まで、異なる用途向けに設計されたさまざまなエディションが用意されています。 SQL Server Express は、再配布と埋め込み用に調整されている SQL Server のフル機能エディションです。  LocalDB は SQL Server Express の簡素化されたエディションであり、構成を必要とせず、アプリケーションのプロセスで実行されます。 どちらの製品も、[SQL Server Express のダウンロード ページ](https://www.microsoft.com/sql-server/sql-server-editions-express)からダウンロードできます。 このセクションの SQL の例の多くでは、SQL Server LocalDB が使用されています。 SQL Server Management Studio (SSMS) は、Visual Studio SQL Server オブジェクト エクスプローラーで提供されるより多くの機能を備えたスタンドアロンのデータベース管理アプリケーションです。 前記のリンクから SSMS を取得できます。

## <a name="oracle"></a>Oracle

Oracle データベースの有料または無料のエディションは、[Oracle テクノロジ ネットワーク](https://www.oracle.com/database/technologies/oracle-database-software-downloads.html)のページからダウンロードできます。 Entity Framework と TableAdapter のデザイン時サポートのためには、[Oracle Developer tools For Visual Studio](https://www.oracle.com/database/technologies/developer-tools/visual-studio/) が必要です。 Oracle Instant Client など、その他の Oracle 公式製品は、NuGet パッケージ マネージャーを通じて入手できます。 [Oracle のオンライン ドキュメント](https://docs.oracle.com/cd/E11882_01/server.112/e10831/toc.htm)に記載されている手順に従って、Oracle のサンプル スキーマをダウンロードできます。

## <a name="mysql"></a>MySQL

MySQL は、企業や Web サイトで広く使用されている、人気のあるオープンソースのデータベース システムです。 MySQL、MySQL for Visual Studio、および関連する製品は、[Windows 上の MySQL](https://www.mysql.com/why-mysql/windows/) に関するページからダウンロードできます。 サードパーティから、さまざまな Visual Studio 拡張機能と、MySQL 用のスタンドアロン管理アプリケーションが提供されています。 NuGet パッケージ マネージャー ( **[ツール]**  >  **[NuGet パッケージ マネージャー]**  >  **[ソリューションの NuGet パッケージの管理]** ) でオファリングを参照できます。

## <a name="postgresql"></a>PostgreSQL

PostgreSQL は、オープンソースで無料のオブジェクト リレーショナル データベース システムです。 Windows にインストールするには、[PostgreSQL のダウンロード ページ](https://www.postgresql.org/download/windows/)からダウンロードできます。 また、ソース コードから PostgreSQL をビルドすることもできます。 PostgreSQL のコア システムには、C 言語インターフェイスが含まれています。 多くのサードパーティから、.NET アプリケーションで PostgreSQL を使用するための NuGet パッケージが提供されています。 NuGet パッケージ マネージャー ( **[ツール]**  >  **[NuGet パッケージ マネージャー]**  >  **[ソリューションの NuGet パッケージの管理]** ) でオファリングを参照できます。 おそらく、最も一般的なパッケージは [npgsql.org](http://www.npgsql.org) によって提供されているものです。

## <a name="sqlite"></a>SQLite

SQLite は、アプリケーション自体のプロセスで実行される埋め込み SQL データベース エンジンです。 [SQLite のダウンロード ページ](https://www.sqlite.org/download.html)からダウンロードできます。 多くのサードパーティ製の SQLite 用 NuGet パッケージも利用できます。 NuGet パッケージ マネージャー ( **[ツール]**  >  **[NuGet パッケージ マネージャー]**  >  **[ソリューションの NuGet パッケージの管理]** ) でオファリングを参照できます。

## <a name="firebird"></a>Firebird

Firebird は、オープンソースの SQL データベース システムです。 [Firebird のダウンロード ページ](http://firebirdsql.org/en/downloads/)からダウンロードできます。 ADO.NET データ プロバイダーは、NuGet パッケージ マネージャーから入手できます。

## <a name="see-also"></a>関連項目

- [Visual Studio でのデータへのアクセス](../data-tools/accessing-data-in-visual-studio.md)
- [SQL Server とそのコンポーネントのバージョン、エディション、および更新レベルを決定する方法](https://support.microsoft.com/help/321185/how-to-determine-the-version-edition-and-update-level-of-sql-server-an)
