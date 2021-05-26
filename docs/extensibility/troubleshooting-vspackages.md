---
title: VSPackage のトラブルシューティング | Microsoft Docs
description: VSPackage で発生する可能性がある一般的な問題と、問題を解決するためのトラブルシューティングのヒントについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: troubleshooting
helpviewer_keywords:
- VSPackages, troubleshooting
- debugging, VSPackages
ms.assetid: 274673e7-72e7-476f-a263-3411b5b874be
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e1a52e6e659a3841214db5da7a44431b68ea98e7
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105073756"
---
# <a name="troubleshooting-vspackages"></a>VSPackage のトラブルシューティング
VSPackage で発生する可能性がある一般的な問題と、問題を解決するためのヒントを以下に示します。

### <a name="to-troubleshoot-a-vspackage-that-keeps-visual-studio-from-starting"></a>Visual Studio の起動を妨げる VSPackage の問題を解決するには

- [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] をセーフ モードで起動します。

   [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] をセーフ モードで起動するには、コマンド プロンプトで「**devenv.exe /safemode**」と入力します。

   このプロセスでは、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] に含まれている VSPackage を除き、VSPackage は読み込まれません。

### <a name="to-troubleshoot-a-vspackage-that-does-not-load"></a>読み込まれない VSPackage の問題を解決するには

1. VSPackage が実行されるように登録されているレジストリ ルートを使用していることを確認します。通常は実験用レジストリ ルートです。

    詳しくは、「[実験用インスタンス](../extensibility/the-experimental-instance.md)」を参照してください。

2. VSPackage が実験用レジストリ ルートで実行されるように設定されている場合は、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] の実験用バージョンを実行していることを確認します。

    実験用バージョンを実行するには、コマンド ウィンドウで「**devenv /rootsuffix exp**」と入力します。

3. VSPackage レジストリ エントリを確認します。

    詳細については、[VSPackage の登録](registering-and-unregistering-vspackages.md)に関するページと「[VSPackage を管理する](../extensibility/managing-vspackages.md)」を参照してください。

4. VSPackage の読み込みに失敗している [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] のインスタンスの **[出力]** ウィンドウを開きます。 VSPackage が読み込みに失敗している理由に関する情報が、そのウィンドウに表示されることがあります。

   > [!NOTE]
   > [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] の実験用バージョンを [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 統合開発環境 (IDE) から起動している場合は、両方のバージョンの **[出力]** ウィンドウを調べます。

5. アクティビティ ログを調べます。

    詳細については、「[方法: アクティビティ ログを使用する](../extensibility/how-to-use-the-activity-log.md)」を参照してください。

6. IDE によってスローされた例外の詳細については、 **[デバッグ]** メニューの **[例外]** をクリックして例外を有効にします。 **[例外]** ダイアログ ボックスで、詳細情報が必要な例外の種類を選択します。

### <a name="to-troubleshoot-a-vspackage-that-does-not-register"></a>登録されない VSPackage の問題を解決するには

1. VSPackage アセンブリが信頼できる場所にあることを確認します。 RegPkg では、既定の .net セキュリティ構成のネットワーク共有など、信頼されていない場所または部分的に信頼されている場所にアセンブリを登録することはできません。 信頼できない場所にユーザーがプロジェクトを作成するたびに警告が表示されますが、[今後、このメッセージを表示しない] チェック ボックスによってこの警告が再度表示されなくなることがあります。

### <a name="to-troubleshoot-a-command-that-is-not-visible-or-that-generates-an-error-when-you-click-a-command"></a>表示されないコマンド、またはコマンドをクリックしたときにエラーが発生するコマンドの問題を解決するには

1. [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] コマンド プロンプトで「**devenv /rootsuffix Exp /setup**」と入力して、新規または変更されたメニュー コマンドと IDE 内の既存のコマンドをマージします。

2. [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] で VSPackage の UI.dll が見つかることを確認します。

   1. レジストリの Packages セクションで、VSPackage の CLSID を探します。

        HKLM\Software\Microsoft\Visual Studio\\ *\<version>* \Packages

   2. SatelliteDll サブキーによって指定されたパスが正しいことを確認します。

### <a name="to-troubleshoot-a-vspackage-that-behaves-unexpectedly"></a>予期しない動作をする VSPackage の問題を解決するには

1. コード内にブレークポイントを設定します。

     デバッグの開始点としては、コンストラクターと初期化メソッドを使用することをお勧めします。 また、メニュー コマンドなど、評価する領域にブレークポイントを設定することもできます。 ブレークポイントを有効にするには、デバッガーで実行する必要があります。

    1. **[プロジェクト]** メニューの **[プロパティ]** をクリックします。

    2. **[プロパティ ページ]** ダイアログ ボックスで、 **[デバッグ]** タブをクリックします。

    3. **[コマンド ライン引数]** ボックスに、VSPackage が対象とする開発環境のルート サフィックスを入力します。 たとえば、実験用ビルドを選択するには、「 **/RootSuffix Exp**」と入力します。

    4. **[デバッグ]** メニューで **[デバッグの開始]** をクリックするか、F5 キーを押します。

        > [!NOTE]
        > プロジェクトをデバッグする場合は、ここでプロジェクトを作成するか、既存のインスタンスを読み込みます。

2. アクティビティ ログを使用します。

     キー ポイントでアクティビティ ログに情報を書き込むことによって、VSPackage の動作をトレースします。 この手法は、製品版環境で VSPackage を実行する場合に特に役に立ちます。 詳細については、「[方法: アクティビティ ログを使用する](../extensibility/how-to-use-the-activity-log.md)」を参照してください。

3. パブリック シンボルを使用します。

     デバッグ中の読みやすさを向上させるために、デバッガーにシンボルをアタッチできます。

    1. **[ツール] - [オプション]** メニューを選択し、 **[デバッグ] - [シンボル]** ダイアログ ボックスに移動します。

    2. 以下の **[シンボル ファイル (.pdb) の場所]** を追加します。

         `https://msdl.microsoft.com/download/symbols`

    3. パフォーマンスを向上させるには、シンボル キャッシュ フォルダーを指定します。次に例を示します。

        ```
        C:\symbols
        ```

### <a name="to-troubleshoot-a-missing-vspackage-or-one-of-its-dependencies"></a>不足している VSPackage またはその依存関係のいずれかの問題を解決するには

1. マネージド コードの場合は、参照パスが正しいことを確認します。

   1. **[プロジェクト]** メニューの **[プロパティ]** をクリックします。

   2. **[プロパティ ページ]** ダイアログ ボックスの **[参照]** タブを選択し、すべてのパスが正しいことを確認します。 または、**オブジェクト ブラウザー** を使用して、参照先オブジェクトを参照することもできます。

        マネージド コードの場合は、[Fuslogvw.exe (アセンブリ バインディング ログ ビューアー)](/dotnet/framework/tools/fuslogvw-exe-assembly-binding-log-viewer) を使用して、失敗したアセンブリの読み込みの詳細を表示できます。

2. アンマネージド コードの場合は、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] CLSID レジストリノードで VSPackage の CLSID を見つけます。

    HKLM\Software\Microsoft\Visual Studio\\ *\<version>* \CLSID

   InprocServer32 エントリに VSPackage dll の正しいパスが含まれていることを確認します。

## <a name="see-also"></a>関連項目
- [VSPackages](../extensibility/internals/vspackages.md)
- [Visual Studio トラブルシューティング](/troubleshoot/visualstudio/welcome-visual-studio/)
