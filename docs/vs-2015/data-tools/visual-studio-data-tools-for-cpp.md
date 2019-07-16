---
title: C++ 用の visual Studio データ ツール |Microsoft Docs
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.date: 11/15/2016
ms.topic: conceptual
ms.assetid: 3a3849d9-1bc7-47d1-805e-1755223ccba2
caps.latest.revision: 12
author: gewarren
ms.author: gewarren
manager: jillfra
robots: noindex,nofollow
ms.openlocfilehash: 85978a79fc1e0110e5b13d6dc0e3198d20ac674a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "68146581"
---
# <a name="visual-studio-data-tools-for-c"></a>C++ 用の Visual Studio データ ツール
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

多くの場合、ネイティブ C++ は、データ ソースにアクセスするときに、最速のパフォーマンスを提供します。 ただし、ツールの Visual Studio での C++ アプリケーションのデータは、.NET アプリケーションはそれほど高度ではありません。 たとえば、ドラッグ アンド ドロップを C++ のデザイン画面にデータ ソースをデータ ソースの windows を使用できません。 オブジェクト リレーショナル レイヤーを必要な場合は独自に作成またはサード パーティ製の製品を使用する必要があります。  Microsoft Foundation Class ライブラリを使用するアプリケーションはメモリにデータを格納し、ユーザーに表示するドキュメントとビュー、と共に、いくつかのデータベース クラスを使用することもできますも、データ バインディング機能についても同様です。 詳細については、次を参照してください。 [Visual c でのデータ アクセス](https://msdn.microsoft.com/library/7wtdsdkh.aspx)します。  
  
 SQL データベースに接続するには、ネイティブ C++ アプリケーションは、ODBC および OLE DB ドライバーおよび ADO プロバイダーは、Windows に含まれているを使用できます。     これらは、それらのインターフェイスをサポートする任意のデータベースに接続できます。 ODBC ドライバーは、標準です。 OLE DB は、旧バージョンとの互換性のために提供されます。 このようなデータ テクノロジの詳細については、次を参照してください[Windows Data Access Components。](https://msdn.microsoft.com/library/windows/desktop/aa968814\(v=vs.85\).aspx)  
  
 SQL Server 2005 でのカスタム機能を利用し、後で、使用して、 [SQL Server Native Client](https://msdn.microsoft.com/sqlserver/aa937733)します。 ネイティブ クライアントでは、SQL Server ODBC ドライバーと 1 つのネイティブ ダイナミック リンク ライブラリ (DLL) で SQL Server OLE DB プロバイダーも含まれています。 これらは、Microsoft SQL Server にネイティブ コード Api (ODBC、OLE DB と ADO) を使用してアプリケーションをサポートします。  SQL Server Native Client は、SQL Server Data Tools と共にインストールされます。 プログラミング ガイドは、ここでは。[SQL Server Native Client プログラミング](https://msdn.microsoft.com/library/ms130892.aspx)します。  
  
## <a name="to-connect-to-localdb-through-odbc-and-sql-native-client-from-a-c-application"></a>C++ アプリケーションから ODBC および SQL Native Client で localDB に接続するには  
  
1. SQL Server Data Tools をインストールします。  
  
2. サンプル SQL データベースに接続する場合は、Northwind データベースをダウンロードし、新しい場所に解凍します。  
  
3. SQL Server Management Studio を使用して、localDB を解凍した Northwind.mdf ファイルをアタッチします。 SQL Server Management Studio の起動時には、「(localdb) \MSSQLLocalDB に接続します。  
  
    ![SSMS 接続ダイアログ](../data-tools/media/raddata-ssms-connect-dialog.png "raddata SSMS 接続ダイアログ")  
  
    左側のウィンドウで [localdb] ノードを右クリックしを選択し、**アタッチ**します。  
  
    ![データベースのアタッチの SSMS](../data-tools/media/raddata-ssms-attach-database.png "raddata データベースの SSMS のアタッチ")  
  
4. ODBC の Windows SDK サンプルをダウンロードして、新しい場所に解凍します。 このサンプルでは、データベースと問題のクエリとコマンドへの接続に使用される ODBC の基本的なコマンドを示します。 これらの関数に関する詳細については、 [Microsoft Open Database Connectivity (ODBC)](https://msdn.microsoft.com/library/windows/desktop/ms710252\(v=vs.85\).aspx)します。 最初に読み込む (C++ フォルダーには) ソリューション、ソリューションを Visual Studio の現在のバージョンにアップグレードする Visual Studio が提供されます。 **[はい]** をクリックします。  
  
5. ネイティブ クライアントを使用するには、そのヘッダー ファイルと lib ファイルが必要です。 これらのファイルには、関数および sql.h で定義された ODBC 関数以外の SQL Server に固有の定義が含まれます。 **プロジェクト** > **プロパティ** > **vc++ ディレクトリ**次のインクルード ディレクトリを追加します。  
  
   **\<システム ドライブ >: \Program Files\Microsoft SQL Server\110\SDK\Include**し、このライブラリ ディレクトリ。  
  
   **c:\Program Files\Microsoft SQL Server\110\SDK\Lib**  
  
6. Odbcsql.cpp でこれらの行を追加します。 #Define コンパイルされない無関係な OLE DB 定義を防止します。  
  
   ```  
   #define _SQLNCLI_ODBC_  
   #include <sqlncli.h>  
   ```  
  
    そのサンプルで実際に使用されない、ネイティブ クライアントの機能のため、上記の手順はコンパイルして実行する必要はありませんに注意してください。 ただし、この機能を使用するため、プロジェクトが構成されているようになりました。 詳細については、「 [SQL Server Native Client プログラミング](https://msdn.microsoft.com/library/ms130892\(v=sql.130\).aspx)」を参照してください。  
  
7. ODBC サブシステムで使用するドライバーを指定します。 サンプルでは、コマンドライン引数としてのドライバー接続文字列の属性を渡します。 **プロジェクト** > **プロパティ** > **デバッグ**、このコマンドの引数を追加します。  
  
   ```  
   DRIVER="SQL Server Native Client 11.0"  
   ```  
  
8. F5 キーを押してアプリケーションをビルドし、実行します。 データベースを入力するように求められますドライバーからのダイアログ ボックスを表示する必要があります。 入力`(localdb)\MSSQLLocalDB`、確認と**セキュリティ接続を使用**します。 **[OK]** を押します。 接続に成功を示すメッセージをコンソールに表示されます。 表示されます、コマンド プロンプトで SQL ステートメントを入力することができます。 次の画面には、クエリの例と、結果が表示されます。  
  
    ![ODBC のサンプル クエリの出力](../data-tools/media/raddata-odbc-sample-query-output.png "raddata ODBC のサンプル クエリの出力")  
  
## <a name="see-also"></a>関連項目  
 [Visual Studio でのデータへのアクセス](../data-tools/accessing-data-in-visual-studio.md)
