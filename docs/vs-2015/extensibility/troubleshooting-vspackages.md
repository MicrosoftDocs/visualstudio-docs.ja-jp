---
title: Vspackage のトラブルシューティング |Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- VSPackages, troubleshooting
- debugging, VSPackages
ms.assetid: 274673e7-72e7-476f-a263-3411b5b874be
caps.latest.revision: 23
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: b2c9a7b57a8b15683cb202b71e33e908a1bfd1b5
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/16/2018
ms.locfileid: "51764007"
---
# <a name="troubleshooting-vspackages"></a>VSPackage のトラブルシューティング
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

一般的な問題、VSPackage に可能性のあるし、問題を解決するためのヒントを次に示します。  
  
### <a name="to-troubleshoot-a-vspackage-that-keeps-visual-studio-from-starting"></a>Visual Studio により、開始する VSPackage のトラブルシューティングを行う  
  
-   開始[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]セーフ モードでします。  
  
     開始する[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]コマンド プロンプトで、セーフ モードでは入力**devenv.exe/safemode**します。  
  
     このプロセス中に Vspackage が読み込まれていないに含まれている Vspackage を除く[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]します。  
  
### <a name="to-troubleshoot-a-vspackage-that-does-not-load"></a>読み込みません VSPackage のトラブルシューティングを行う  
  
1.  VSPackage が、通常は実験用のレジストリ ルートを実行する登録されているレジストリ ルートを使用していることを確認します。  
  
     詳細については、[、実験用インスタンス](../extensibility/the-experimental-instance.md)を参照してください。  
  
2.  VSPackage の実験用のレジストリ ルートで実行するターゲットが場合の実験的なバージョンを実行していること確認[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]します。  
  
     実験用のバージョンを実行するには、コマンド ウィンドウで、次を入力: **devenv/rootsuffix exp**します。  
  
3.  VSPackage のレジストリ エントリを確認します。  
  
     詳細については、[Vspackage の登録](http://msdn.microsoft.com/en-us/31e6050f-1457-4849-944a-a3c36b76f3dd)と[管理 Vspackage](../extensibility/managing-vspackages.md)を参照してください。  
  
4.  開く、**出力**ウィンドウのインスタンスの[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]が VSPackage の読み込みに失敗します。 VSPackage の読み込みが失敗した理由に関する情報は、そのウィンドウに表示可能性があります。  
  
    > [!NOTE]
    >  実験的なバージョンを開始する場合[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]から、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]統合開発環境 (IDE)、検査、**出力**両方のバージョンのウィンドウ。  
  
5.  アクティビティ ログを調べます。  
  
     詳細については、[方法: アクティビティ ログを使用して、](../extensibility/how-to-use-the-activity-log.md)を参照してください。  
  
6.  IDE によってスローされた例外の詳細についてをクリックして**例外**で、**デバッグ**メニュー、例外を有効にします。 **例外** ダイアログ ボックスに関する詳細情報を表示する例外の種類を選択します。  
  
### <a name="to-troubleshoot-a-vspackage-that-does-not-register"></a>登録されませんする VSPackage のトラブルシューティングを行う  
  
1.  VSPackage アセンブリが信頼できる場所に置かれていることを確認します。 RegPkg は、既定の .net のセキュリティ構成でのネットワーク共有などの信頼されていないか部分的に信頼された場所にアセンブリを登録することはできません。 警告は、ユーザーが信頼できない場所で、プロジェクトを作成するたびに表示されますが、「メッセージを表示しないこのもう一度」チェック ボックスは、再発を回避して、この警告を回避できます。  
  
### <a name="to-troubleshoot-a-command-that-is-not-visible-or-that-generates-an-error-when-you-click-a-command"></a>表示されていないか、コマンドをクリックすると、エラーを生成するコマンドのトラブルシューティングを行う  
  
1.  次のコマンドを入力して、新しいまたは変更されたメニュー コマンドと、IDE 内の既存のマージ、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]コマンド プロンプト: **devenv/rootsuffix Exp/setup**します。  
  
2.  必ず[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]VSPackage の UI.dll を見つけることができます。  
  
    1.  レジストリのパッケージ セクションでは、VSPackage の CLSID を見つけます。  
  
         HKLM\Software\Microsoft\Visual Studio\\*\<バージョン >* \Packages  
  
    2.  SatelliteDll サブキーによって指定されたパスが正しいことを確認します。  
  
### <a name="to-troubleshoot-a-vspackage-that-behaves-unexpectedly"></a>予期しない動作する VSPackage のトラブルシューティングを行う  
  
1.  コード内にブレークポイントを設定します。  
  
     デバッグ用の適切な出発点には、コンス トラクターおよび初期化メソッドです。 メニュー コマンドなど、評価する領域にブレークポイントを設定することもできます。 ブレークポイントを有効にするのには、デバッガーで実行する必要があります。  
  
    1.  **[プロジェクト]** メニューの **[プロパティ]** をクリックします。  
  
    2.  **プロパティ ページ**ダイアログ ボックスで、**デバッグ**タブ。  
  
    3.  **コマンドライン引数**ボックスに、開発環境のルートのサフィックスを入力する、VSPackage の対象とします。 たとえば、試験的ビルドを選択するには、次のように入力します。: **RootSuffix Exp**します。  
  
    4.  **デバッグ** メニューのをクリックして**デバッグの開始** F5 キーを押します。  
  
        > [!NOTE]
        >  プロジェクトをデバッグする場合は、作成またはプロジェクトの既存のインスタンスを読み込むようになりました。  
  
2.  アクティビティ ログを使用します。  
  
     重要な点でアクティビティ ログに情報を記述することで、VSPackage の動作をトレースします。 この手法は、小売環境で VSPackage を実行するときに特に便利です。 詳細については、[方法: アクティビティ ログを使用して、](../extensibility/how-to-use-the-activity-log.md)を参照してください。  
  
3.  パブリック シンボルを使用します。  
  
     デバッグ中には、読みやすさを向上させるためには、デバッガーにシンボルをアタッチできます。  
  
    1.  **ツール/オプション** メニューに移動し、**デバッグ/シンボル** ダイアログ ボックス。  
  
    2.  この追加**シンボル (.pdb) ファイルの場所**:  
  
         [http://msdl.microsoft.com/download/symbols](http://msdl.microsoft.com/download/symbols)  
  
    3.  パフォーマンスを向上させるのには、たとえばシンボル キャッシュ フォルダーを指定します。  
  
        ```  
        C:\symbols  
        ```  
  
### <a name="to-troubleshoot-a-missing-vspackage-or-one-of-its-dependencies"></a>不足している VSPackage またはその依存関係の 1 つのトラブルシューティングを行う  
  
1. マネージ コードは、参照パスが正しいことを確認します。  
  
   1.  **[プロジェクト]** メニューの **[プロパティ]** をクリックします。  
  
   2.  選択、**参照** タブで、**プロパティ ページ**のすべてのパスが正しい ダイアログ ボックスを確認します。 また、使用することができます、**オブジェクト ブラウザー**の参照先のオブジェクトをブラウズします。  
  
        マネージ コードを使用することができます、 [Fuslogvw.exe (アセンブリ バインディング ログ ビューアー)](http://msdn.microsoft.com/library/e32fa443-0778-4cc3-bf36-5c8ea297d296)失敗したアセンブリの読み込みの詳細を表示します。  
  
2. アンマネージ コードの場合で、VSPackage の CLSID を検索、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] CLSID レジストリ ノード。  
  
    HKLM\Software\Microsoft\Visual Studio\\*\<バージョン >* \CLSID  
  
   InprocServer32 エントリが VSPackage の dll のパスが正しいことを確認します。  
  
## <a name="see-also"></a>関連項目  
 [VSPackage](../extensibility/internals/vspackages.md)

