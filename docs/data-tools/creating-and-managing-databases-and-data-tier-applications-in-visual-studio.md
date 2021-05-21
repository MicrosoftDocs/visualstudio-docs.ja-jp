---
title: データベース プロジェクトと DAC プロジェクト
description: データベース プロジェクトとデータ層アプリケーション (DAC) について説明します。 DB プロジェクトを使用して、新しいデータベースおよび新しい DAC を作成し、既存の DB および DAC を更新します。
ms.custom: SEO-VS-2020
ms.date: 11/21/2018
ms.topic: conceptual
helpviewer_keywords:
- databases, managing change
ms.assetid: 40b51f5a-d52c-44ac-8f84-037a0917af33
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: 8ed1dc21d0029dc8939c540d33d0743c81db93fc
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99867088"
---
# <a name="database-projects-and-data-tier-applications"></a>データベース プロジェクトとデータ層アプリケーション

データベース プロジェクトを使用して、新しいデータベースおよび新しいデータ層アプリケーション (DAC) を作成したり、既存のデータベースおよびデータ層アプリケーションを更新したりできます。 データベース プロジェクトおよび DAC プロジェクトを使用すると、バージョン コントロールとプロジェクト管理の手法を、マネージド コードまたはネイティブ コードに適用するのとほぼ同様に、データベース開発作業に適用できます。 DAC プロジェクト、データベース プロジェクト、またはサーバー プロジェクトを作成し、バージョン コントロール下に置くことで、データベースやデータベース サーバーの変更を管理する開発チームを支援できます。 チームのメンバーは、チームで共有する前に、ファイルをチェックアウトして、分離開発環境 (サンドボックス) で変更を行い、ビルドしてテストすることができます。 コードの品質を確保するために、チームはデータベースの特定のリリースに対するすべての変更をステージング環境で完了し、テストしてから、運用環境に配置できます。

データ層アプリケーションでサポートされているデータベース機能の一覧については、[SQL Server オブジェクトの DAC サポート](/sql/relational-databases/data-tier-applications/dac-support-for-sql-server-objects-and-versions)に関する記事を参照してください。 データ層アプリケーションでサポートされていない機能をデータベースで使用する場合は、代わりにデータベース プロジェクトを使用して、データベースの変更を管理する必要があります。

## <a name="common-high-level-tasks"></a>一般的なタスクの概要

| タスクの概要 | 関連する参照先 |
| - | - |
| **データ層アプリケーションの開発の開始:** データ層アプリケーション (DAC) の概念は、SQL Server 2008 で導入されました。 DAC には、SQL Server データベースの定義と、クライアント サーバー アプリケーションまたは 3 層アプリケーションで使用されるサポート インスタンス オブジェクトが含まれます。 DAC には、ログインなどのインスタンス エンティティと共に、テーブルやビューなどのデータベース オブジェクトが含まれます。 Visual Studio を使用して、DAC プロジェクトを作成し、DAC パッケージ ファイルをビルドできます。さらに、SQL Server データベース エンジンのインスタンスに配置するために、DAC パッケージ ファイルをデータベース管理者に送信できます。 | - [データ層アプリケーション](/sql/relational-databases/data-tier-applications/data-tier-applications)<br />- [SQL Server Management Studio](/sql/ssms/sql-server-management-studio-ssms) |
| **反復データベース開発の実施:** 開発者はプロジェクトの一部をチェックアウトし、分離開発環境でそれらを更新できます。 このような環境を使用することにより、チームの他のメンバーに影響を与えることなく、変更をテストできます。 変更が完了したら、ファイルをバージョン コントロールにチェックインすることで、他のチーム メンバーはそれらの変更を取得し、ビルドしてテスト サーバーに配置できます。 | - [プロジェクト指向のオフライン データベース開発 (SQL Server Data Tools)](/sql/ssdt/project-oriented-offline-database-development)<br />- [Transact-SQL デバッガー (SQL Server Management Studio)](/sql/ssms/scripting/transact-sql-debugger) |
| **プロトタイプの作成、テスト結果の検証、データベース スクリプトおよびオブジェクトの変更:** Transact-SQL エディターを使用して、これらの一般的なタスクを実行できます。 | - [クエリおよびテキスト エディター (SQL Server Management Studio)](/sql/ssms/scripting/query-and-text-editors-sql-server-management-studio) |

## <a name="see-also"></a>関連項目

- [.NET 用の Visual Studio データ ツール](../data-tools/visual-studio-data-tools-for-dotnet.md)
