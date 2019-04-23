---
title: .Mdf ファイルのアップグレード |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- SQL Server Express
- SQL Server LocalDB
- LocalDB
- SQLEXPRESS
- upgrading SQLExpress to SQLExpress
- upgrading to LocalDB
ms.assetid: 14ca6f76-f80e-4926-8020-3fee2d802b75
caps.latest.revision: 36
author: gewarren
ms.author: gewarren
manager: jillfra
robots: noindex,nofollow
ms.openlocfilehash: 6cdbb5d092f431f628e76c7ab629d5ed70429cee
ms.sourcegitcommit: 53aa5a413717a1b62ca56a5983b6a50f7f0663b3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59661504"
---
# <a name="upgrade-mdf-files"></a>.mdf ファイルのアップグレード
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このトピックでは、Visual Studio の新しいバージョンをインストールした後、データベース ファイル (.mdf) をアップグレードするためのオプションについて説明します。 手順についてには、次のタスクが含まれています。  
  
- 新しいバージョンの SQL Server Express LocalDB を使用するデータベース ファイルをアップグレードします。  
  
- SQL Server Express の新しいバージョンを使用するデータベース ファイルをアップグレードします。  
  
- Visual Studio でのデータベース ファイルを使用して機能しますが、古いバージョンの SQL Server Express または LocalDB との互換性を保持  
  
- 既定のデータベース エンジンを SQL Server Express を行う  
  
  Visual Studio を使用して、以前のバージョンの SQL Server Express または LocalDB を使用して作成されたデータベース ファイル (.mdf) を含むプロジェクトを開くことができます。 ただしを Visual Studio でプロジェクトの開発を続行するには、そのバージョンの SQL Server Express または Visual Studio と同じコンピューターにインストールされている LocalDB であるか、データベース ファイルをアップグレードする必要があります。 データベース ファイルをアップグレードする場合は、以前のバージョンの SQL Server Express または LocalDB を使用してアクセスできません。  
  
  また、ファイルのバージョンが SQL Server Express または現在インストールされている LocalDB のインスタンスとの互換性がない場合、以前のバージョンの SQL Server Express または LocalDB を通じて作成されたデータベース ファイルをアップグレードするように求め可能性があります。 この問題を解決するには、Visual Studio は、ファイルをアップグレードすることを求められます。  
  
> [!IMPORTANT]
>  アップグレードする前に、データベース ファイルをバックアップすることをお勧めします。  
  
> [!WARNING]
>  LocalDB 2016 (V13) を 32 ビットである LocalDB 2014 (V12) で作成された .mdf ファイルをアップグレードする場合、32 ビット バージョンの LocalDB でファイルを再度開くことができなきます。  更新プログラム 2 で LocalDB V13 は 64 ビットのみです。  
  
 データベースをアップグレードする前に、次の条件を考慮してください。  
  
-   以前のバージョンと新しいバージョンの Visual Studio の両方で、プロジェクトで作業する場合、アップグレードしないでください。  
  
-   SQL Server Express LocalDB はなくを使用する環境でアプリケーションを使用する場合、アップグレードしないでください。  
  
-   LocalDB から受け入れないために、アプリケーションは、リモート接続を使用する場合にアップグレードしないでください。  
  
-   アプリケーションには、インターネット インフォメーション サービス (IIS) が依存している場合、アップグレードしないでください。  
  
-   サンド ボックス環境でデータベース アプリケーションをテストするデータベースを管理するしたくない場合は、アップグレードを検討します。  
  
### <a name="to-upgrade-a-database-file"></a>データベース ファイルをアップグレードするには  
  
1. **サーバー エクスプ ローラー**を選択、**データベースへの接続**ボタンをクリックします。  
  
2. **接続の追加** ダイアログ ボックスで、次の情報を指定します。  
  
   -   **データ ソース**: `Microsoft SQL Server (SqlClient)`  
  
   -   **サーバー名**:   
  
       -   既定のバージョンを使用する:`(localdb)\MSSQLLocalDB`します。  これを指定 ProjectV12 または ProjectV13 のいずれかによっては、Visual Studio のバージョンがインストールされているし、最初の LocalDB インスタンスの作成時にします。 **MSSQLLocalDB**ノード**SQL Server オブジェクト エクスプ ローラー**ポイントにバージョンを示しています。  
  
       -   特定のバージョンを使用する:`(localdb)\ProjectsV12`または`(localdb)\ProjectsV13`V12 は LocalDB 2014、V13 は LocalDB 2016。  
  
   -   **データベース ファイルを添付**:プライマリ .mdf ファイルの物理パス。  
  
   -   **論理名**:ファイルで使用する名前です。  
  
3. **[OK]** ボタンを選択します。  
  
4. 求められたら、選択、**はい**ボタン ファイルをアップグレードします。  
  
   データベースはアップグレードされ、LocalDB データベース エンジンに接続されて、LocalDB の古いバージョンと互換性がありません。  
  
   SQL Server Express LocalDB を使用して、接続のショートカット メニューを開き、に接続を変更することもできます。**接続の変更**します。 **接続の変更** ダイアログ ボックスで、サーバー名を変更して`(LocalDB)\MSSQLLocalDB`します。 **プロパティの詳細** ダイアログ ボックスに、必ず**ユーザー インスタンス**に設定されている**False**します。  
  
### <a name="to-upgrade-to-a-newer-version-of-sql-server-express"></a>SQL Server Express の新しいバージョンにアップグレードするには  
  
1. データベースへの接続のショートカット メニューを選択**接続の変更**します。  
  
2. **接続の変更**ダイアログ ボックスで、**詳細**ボタンをクリックします。  
  
3. **プロパティの詳細**ダイアログ ボックスで、 **OK**サーバー名を変更することがなくボタン。  
  
   SQL Server Express の現在のバージョンと一致するデータベース ファイルはアップグレードされます。  
  
### <a name="to-work-with-the-database-in-visual-studio-but-retain-compatibility-with-sql-server-express"></a>Visual Studio でデータベースが SQL Server Express との互換性を保持するには  
  
-   Visual Studio では、アップグレードしなくても、プロジェクトを開きます。  
  
    -   プロジェクトを実行するには、F5 キーを選択します。  
  
    -   データベースを編集するには、.mdf ファイルを開き**ソリューション エクスプ ローラー**でノードを展開および**サーバー エクスプ ローラー**データベースを使用します。  
  
### <a name="to-make-sql-server-express-the-default-database-engine"></a>既定のデータベース エンジンを SQL Server Express を作成するには  
  
1. メニュー バーで選択**ツール** > **オプション**します。  
  
2. **オプション** ダイアログ ボックスで、展開、 **Data Tools**オプション、および選択し、**データ接続**ノード。  
  
3. **SQL Server インスタンス名**テキスト ボックスに、SQL Server Express または使用する LocalDB のインスタンスの名前を指定します。 場合は、インスタンスがという名前が指定`.\SQLEXPRESS or (localdb)\MSSQLLocalDB`します。  
  
4. **[OK]** ボタンを選択します。  
  
   SQL Server Express をアプリケーションの既定のデータベース エンジンとなります。  