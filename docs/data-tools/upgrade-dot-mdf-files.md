---
title: .mdf ファイルのアップグレード
description: 新しいバージョンの Visual Studio をインストールした後で、データベース ファイル (.mdf) をアップグレードするためのオプションを確認します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- SQL Server Express
- SQL Server LocalDB
- LocalDB
- SQLEXPRESS
- upgrading SQLExpress to SQLExpress
- upgrading to LocalDB
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: cbea7761ed5f36265464f2afe9a64550ddc5e62a
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99866308"
---
# <a name="upgrade-mdf-files"></a>.mdf ファイルのアップグレード

このトピックでは、新しいバージョンの Visual Studio をインストールした後で、データベース ファイル ( *.mdf*) をアップグレードするためのオプションについて説明します。 次のタスクの手順が含まれます。

- 新しいバージョンの SQL Server Express LocalDB を使用するようにデータベース ファイルをアップグレードする

- 新しいバージョンの SQL Server Express を使用するようにデータベース ファイルをアップグレードする

- Visual Studio でデータベース ファイルを使用するが、古いバージョンの SQL Server Express または LocalDB との互換性を維持する

- SQL Server Express を既定のデータベース エンジンにする

Visual Studio を使用して、古いバージョンの SQL Server Express または LocalDB を使用して作成されたデータベース ファイル ( *.mdf*) が含まれるプロジェクトを開くことができます。 ただし、Visual Studio でプロジェクトの開発を続けるには、Visual Studio と同じコンピューターにそのバージョンの SQL Server Express または LocalDB がインストールされているか、またはデータベース ファイルをアップグレードする必要があります。 データベース ファイルをアップグレードした場合、古いバージョンの SQL Server Express または LocalDB を使用してアクセスすることはできなくなります。

また、ファイルのバージョンが、現在インストールされている SQL Server Express または LocalDB のインスタンスと互換性がない場合にも、以前のバージョンの SQL Server Express または LocalDB を使用して作成されたデータベース ファイルをアップグレードするように求められることがあります。 問題を解決するため、Visual Studio でファイルをアップグレードするように求められます。

> [!IMPORTANT]
> アップグレードする前に、データベース ファイルをバックアップすることをお勧めします。

> [!WARNING]
> LocalDB 2014 (V12) 32 ビットで作成された *.mdf* ファイルを、LocalDB 2016 (V13) 以降にアップグレードした場合、そのファイルを 32 ビット バージョンの LocalDB で再び開くことはできなくなります。

データベースをアップグレードする前に、次の条件を考慮してください。

- 古いバージョンと新しいバージョン両方の Visual Studio でプロジェクトの作業を行う場合は、アップグレードしないでください。

- LocalDB ではなく SQL Server Express が使用される環境でアプリケーションを使用される場合は、アップグレードしないでください。

- アプリケーションでリモート接続を使用する場合、LocalDB はそれに対応していないため、アップグレードしないでください。

- アプリケーションがインターネット インフォメーション サービス (IIS) に依存している場合は、アップグレードしないでください。

- サンドボックス環境でデータベース アプリケーションをテストする必要があるが、データベースの管理はしたくない場合は、アップグレードを検討してください。

### <a name="to-upgrade-a-database-file-to-use-the-localdb-version"></a>LocalDB バージョンを使用するようにデータベース ファイルをアップグレードするには

1. **サーバー エクスプローラー** で、 **[データベースへの接続]** ボタンを選択します。

2. **[接続の追加]** ダイアログ ボックスで、次の情報を指定します。

    - **データ ソース**: `Microsoft SQL Server (SqlClient)`

    - **サーバー名**:

        - 既定のバージョンを使用するには: `(localdb)\MSSQLLocalDB`。  これにより、インストールされている Visual Studio のバージョンと、最初の LocalDB インスタンスが作成された時期に応じて、ProjectV12 または ProjectV13 のいずれかが指定されます。 **SQL Server オブジェクト エクスプローラー** の **MSSQLLocalDB** ノードに、参照しているバージョンが表示されます。

        - 特定のバージョンを使用するには: `(localdb)\ProjectsV12` または `(localdb)\ProjectsV13` (V12 が LocalDB 2014、V13 が LocalDB 2016 の場合)。

    - **データベース ファイルのアタッチ**: プライマリ *.mdf* ファイルの物理パス。

    - 論理名(&L):ファイルで使用する名前です。

3. **[OK]** ボタンを選択します。

4. プロンプトが表示されたら、 **[はい]** ボタンを選択してファイルをアップグレードします。

    データベースがアップグレードされ、LocalDB データベース エンジンにアタッチされて、古いバージョンの LocalDB と互換性がなくなります。

また、接続のショートカット メニューを開き、 **[接続の変更]** を選択することにより、LocalDB を使用するように SQL Server Express の接続を変更することもできます。 **[接続の変更]** ダイアログ ボックスで、サーバー名を `(LocalDB)\MSSQLLocalDB` に変更します。 **[詳細プロパティ]** ダイアログ ボックスで、 **[ユーザー インスタンス]** が **[False]** に設定されていることを確認します。

### <a name="to-upgrade-a-database-file-to-use-the-sql-server-express-version"></a>SQL Server Express バージョンを使用するようにデータベース ファイルをアップグレードするには

1. データベースへの接続のショートカット メニューで、 **[接続の変更]** を選択します。

2. **[接続の変更]** ダイアログ ボックスで、 **[詳細設定]** ボタンを選択します。

3. **[詳細プロパティ]** ダイアログ ボックスで、サーバー名を変更せずに **[OK]** ボタンを選択します。

    データベース ファイルが、現在のバージョンの SQL Server Express と一致するようにアップグレードされます。

### <a name="to-work-with-the-database-in-visual-studio-but-retain-compatibility-with-sql-server-express"></a>Visual Studio でデータベースを使用するが、SQL Server Express との互換性を維持するには

- Visual Studio で、アップグレードせずにプロジェクトを開きます。

  - プロジェクトを実行するには、**F5** キーを押します。

  - データベースを編集するには、**ソリューション エクスプローラー** で *.mdf* ファイルを開き、 **[サーバー エクスプローラー]** ノードを展開してデータベースを処理します。

### <a name="to-make-sql-server-express-the-default-database-engine"></a>SQL Server Express を既定のデータベース エンジンにするには

1. メニュー バーで、 **[ツール]**  >  **[オプション]** の順に選択します。

2. **[オプション]** ダイアログ ボックスで、 **[データベース ツール]** オプションを展開し、 **[データ接続]** を選択します。

3. **[SQL Server インスタンス名]** テキスト ボックスで、使用する SQL Server Express または LocalDB のインスタンスの名前を指定します。 インスタンスに名前がない場合は、`.\SQLEXPRESS or (LocalDB)\MSSQLLocalDB` を指定します。

4. **[OK]** ボタンを選択します。

    SQL Server Express が、アプリケーションの既定のデータベース エンジンになります。

## <a name="see-also"></a>関連項目

- [Visual Studio でのデータへのアクセス](accessing-data-in-visual-studio.md)
