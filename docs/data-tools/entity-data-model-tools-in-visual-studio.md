---
title: Entity Framework のツール
description: Visual Studio の Entity Framework のツールについて説明します。 Entity Framework のツールは、Entity Framework (EF) アプリケーションを容易に構築できるように設計されています。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 1b06b573-84aa-4458-b3f5-e238df47bf45
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: ee4bb5e56c5ae9ffb5f5266c8ef80804c8e96597
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99866984"
---
# <a name="entity-framework-tools-in-visual-studio"></a>Visual Studio の Entity Framework のツール

Entity Framework は、.NET 開発者がドメイン固有オブジェクトを使用してリレーショナル データを操作できるようにする、オブジェクト リレーショナル マッピング テクノロジです。 これにより、開発者が通常は記述する必要のあるデータアクセス コードの大部分が不要になります。 Entity Framework は、新しい .NET アプリケーションに推奨されるオブジェクト リレーショナル マッピング (ORM) モデリング テクノロジです。

Entity Framework のツールは、Entity Framework (EF) アプリケーションを容易に構築できるように設計されています。 Entity Framework の完全なドキュメントについては、[概要 - EF 6](/ef/ef6/) に関するページを参照してください。

  > [!NOTE]
  > このページで説明されている Entity Framework のツールは、EF Core ではサポートされていない *.edmx* ファイルを生成するために使用されます。 既存のデータベースから EF Core モデルを生成するには、「[リバースエンジニアリング - EF Core](/ef/core/managing-schemas/scaffolding)」を参照してください。 EF 6 と EF Core の相違点の詳細については、「[EF Core と EF 6 を比較する](/ef/efcore-and-ef6/)」を参照してください。

Entity Framework のツールを使用すると、既存のデータベースから *概念モデル* を作成し、それをグラフィックで視覚的に表現したり、編集したりできます。 また、グラフィカルな概念モデルを作成し、そのモデルをサポートするデータベースを生成することもできます。 いずれの場合も、基になるデータベースの変更時には、モデルを自動的に更新できるだけではなく、アプリケーションのオブジェクトレイヤー コードも自動生成できます。 データベースの生成とオブジェクトレイヤー コードの生成はカスタマイズ可能です。

Entity Framework のツールは、Visual Studio インストーラーの **[データ ストレージとデータ処理]** ワークロードの一部としてインストールされます。 また、 **[SDK、ライブラリ、およびフレームワーク]** のカテゴリの下に個々のコンポーネントとしてインストールすることもできます。

これらは、Visual Studio の Entity Framework のツールを構成する固有のツールです。

- [!INCLUDE[vstecado](../data-tools/includes/vstecado_md.md)] **[!INCLUDE[adonet_edm](../data-tools/includes/adonet_edm_md.md)] Designer** (**エンティティ デザイナー**) を使用すると、エンティティ、アソシエーション、マッピング、および継承関係を視覚的に作成および変更できます。 **エンティティ デザイナー** は、[!INCLUDE[TLA#tla_cshrp](../data-tools/includes/tlasharptla_cshrp_md.md)] または [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] オブジェクトレイヤー コードも生成します。

- **[!INCLUDE[adonet_edm](../data-tools/includes/adonet_edm_md.md)] ウィザード** を使用して、既存のデータベースから概念モデルを生成し、データベース接続情報をアプリケーションに追加できます。

- **データベースの作成ウィザード** を使用して、最初に概念モデルを作成し、次にモデルをサポートするデータベースを作成します。

- **モデルの更新ウィザード** を使用して、基になるデータベースに対して変更が行われた場合に、概念モデル、ストレージ モデル、およびマッピングを更新できます。

  > [!NOTE]
  > Visual Studio 2010 以降では、Entity Framework のツールは [!INCLUDE[ss2k](../data-tools/includes/ss2k_md.md)] をサポートしていません。

これらのツールは *.edmx* ファイルを生成または変更します。 *.edmx* ファイルには、概念モデル、ストレージ モデル、およびこれらの間のマッピングの情報が含まれます。 詳細については、[EDMX](/ef/ef6/)についてのページを参照してください。

[Entity Framework Power Tools](https://marketplace.visualstudio.com/items?itemName=EntityFrameworkTeam.EntityFrameworkPowerToolsBeta4) は、Entity Data Model を使用するアプリケーションを構築するのに役立ちます。 Power Tools では、概念モデルの生成、既存のモデルの検証、概念モデルに基づくオブジェクト クラスを含むソースコード ファイルの生成、およびモデルによって生成されるビューを含むソースコード ファイルの生成を行うことができます。 詳細については、「[事前に生成されたマッピングビュー](/ef/ef6/fundamentals/performance/pre-generated-views)」を参照してください。

## <a name="related-topics"></a>関連トピック

| Title | 説明 |
| - | - |
| [ADO.NET Entity Framework](/dotnet/framework/data/adonet/ef/index) | アプリケーションを作成するために、[!INCLUDE[adonet_ef](../data-tools/includes/adonet_ef_md.md)] が提供する [!INCLUDE[adonet_edm](../data-tools/includes/adonet_edm_md.md)] ツールの使用方法について説明します。 |
| [Entity Data Model](/dotnet/framework/data/adonet/entity-data-model) | [!INCLUDE[adonet_ef](../data-tools/includes/adonet_ef_md.md)] 上に構築されたアプリケーションで使用されるデータを操作するためのリンクと情報を提供します。 |
| [Entity Framework (EF) ドキュメント](/ef/ef6/get-started) | Entity Framework を最大限に活用できるように、ビデオ、チュートリアル、および高度なドキュメントのインデックスを提供します。 |
| [ASP.NET 5 アプリケーションを新しいデータベースに](https://docs.efproject.net/en/latest/platforms/aspnetcore/new-db.html) | Entity Framework 7 を使用して新しい ASP.NET 5 アプリケーションを作成する方法について説明します。 |

## <a name="see-also"></a>関連項目

- [.NET 用の Visual Studio データ ツール](../data-tools/visual-studio-data-tools-for-dotnet.md)
