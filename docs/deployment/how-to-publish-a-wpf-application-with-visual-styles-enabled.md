---
title: Visual スタイルが有効になっている WPF アプリを発行する
description: Visual スタイルが有効になっている WPF アプリケーションを発行する方法について説明します。これにより、ユーザーが選択したテーマに基づいてコントロールの外観を変更できます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 73b22b02-fc75-42aa-82d3-51fdcaf8e5c8
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 285d624debed6dc498e3d274af2839137b5094d1
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102171280"
---
# <a name="how-to-publish-a-wpf-application-with-visual-styles-enabled"></a>方法: Visual スタイルが有効になっている WPF アプリケーションを公開する

visual スタイルを使用すると、ユーザーが選択したテーマに基づいてコモン コントロールの外観を変更できます。 既定では、Visual スタイルは、Windows Presentation Foundation (WPF) アプリケーションで有効になっていないため、手動で有効にする必要があります。 ただし、WPF アプリケーションの Visual スタイルを有効にすると、ソリューションの発行によりエラーが発生します。 このトピックでは、このエラーを解決する方法と、Visual スタイルを有効にした WPF アプリケーションを発行するためのプロセスについて説明します。 Visual スタイルの詳細については、[Visual スタイルの概要](/windows/desktop/Controls/visual-styles-overview)に関する記事をご覧ください。 エラー メッセージの詳細については、「[ClickOnce 配置の固有のエラーのトラブルシューティング](../deployment/troubleshooting-specific-errors-in-clickonce-deployments.md)」を参照してください。

 エラーを解決し、ソリューションを公開するには、次のタスクを実行します。

- [Visual スタイルを有効にせずにソリューションを公開します](#publish-the-solution-without-visual-styles-enabled)。

- [マニフェスト ファイルを作成します](#create-a-manifest-file)。

- [マニフェスト ファイルを発行済みソリューションの実行可能ファイルに埋め込みます](#embed-the-manifest-file-into-the-executable-file-of-the-published-solution)。

- [アプリケーション マニフェストと配置マニフェストに署名します](#sign-the-application-and-deployment-manifests)。

  その後、エンド ユーザーがアプリケーションをインストールする場所に、発行されたファイルを移動できます。

## <a name="publish-the-solution-without-visual-styles-enabled"></a>Visual スタイルを有効にせずにソリューションを公開するには

1. プロジェクトに有効になった Visual スタイルがないことを確認します。 最初に、プロジェクトのマニフェスト ファイルに次の XML があるかチェックします。 その後、XML がある場合は、コメント タグで XML を囲みます。

     既定では、Visual スタイルは有効になっていません。

    ```xml
    <dependency>
        <dependentAssembly>
            <assemblyIdentity type="win32" name="Microsoft.Windows.Common-Controls" version="6.0.0.0" processorArchitecture="*" publicKeyToken="6595b64144ccf1df" language="*" />
        </dependentAssembly>
    </dependency>
    ```

     次の手順は、プロジェクトに関連付けられたマニフェスト ファイルを開く方法を示します。

    **Visual Basic プロジェクトのマニフェスト ファイルを開くには**

    1. メニュー バーで、 **[プロジェクト]** 、 **[<*ProjectName*> のプロパティ]** の順に選択します。<*ProjectName*> は WPF プロジェクトの名前です。

         WPF プロジェクトのプロパティ ページが表示されます。

    2. **[アプリケーション]** タブで、**[Windows 設定の表示]** をクリックします。

         **コード エディター** で app.manifest ファイルが開きます。

    **C# プロジェクトのマニフェスト ファイルを開くには**

    1. メニュー バーで、 **[プロジェクト]** 、 **[<*ProjectName*> のプロパティ]** の順に選択します。<*ProjectName*> は WPF プロジェクトの名前です。

         WPF プロジェクトのプロパティ ページが表示されます。

    2. **[アプリケーション]** タブで、マニフェストのフィールドに表示される名前をメモします。 これは、プロジェクトに関連付けられているマニフェストの名前です。

        > [!NOTE]
        > **[マニフェストを既定の設定で埋め込みます]** または **[マニフェストなしでアプリケーションを作成する]** がマニフェスト フィールドに表示されている場合、Visual スタイルは有効になりません。 マニフェスト ファイルの名前がマニフェスト フィールドに表示されている場合は、この手順の次の手順に進みます。

    3. **ソリューション エクスプローラー** で、**[すべてのファイルを表示]** をクリックします。

         このボタンは、除外された項目や通常は表示されない項目も含め、すべてのプロジェクト項目を表示します。 マニフェスト ファイルはプロジェクト項目として表示されます。

2. ソリューションをビルドし、発行します。 ソリューションを発行する方法の詳細については、「[方法: 発行ウィザードを使用して ClickOnce アプリケーションを発行する](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)」を参照してください。

## <a name="create-a-manifest-file"></a>マニフェスト ファイルの作成

1. 次の XML をメモ帳ファイルに貼り付けます。

     この XML は、Visual スタイルをサポートするコントロールを含むアセンブリについて説明します。

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <asmv1:assembly manifestVersion="1.0"
        xmlns="urn:schemas-microsoft-com:asm.v1"
        xmlns:asmv1="urn:schemas-microsoft-com:asm.v1"
        xmlns:asmv2="urn:schemas-microsoft-com:asm.v2"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <dependency>
            <dependentAssembly>
                <assemblyIdentity type="win32" name="Microsoft.Windows.Common-Controls" version="6.0.0.0" processorArchitecture="*" publicKeyToken="6595b64144ccf1df" language="*" />
            </dependentAssembly>
        </dependency>
    </asmv1:assembly>
    ```

2. メモ帳の **[ファイル]** をクリックし、**[名前を付けて保存]** をクリックします。

3. **[名前を付けて保存]** ダイアログ ボックスの **[ファイルの種類]** ドロップダウン リストで、**[すべてのファイル]** をクリックします。

4. **[ファイル名]** ボックスで、ファイルに名前を付け、ファイル名の最後に *.manifest* を付けます。 例: *themes.manifest*。

5. **[フォルダーの参照]** ボタンをクリックしてフォルダーを選択し、**[保存]** をクリックします。

    > [!NOTE]
    > 残りの手順では、このファイルの名前が *themes.manifest* で、ファイルがコンピューターの *C:\temp* ディレクトリに格納されていることを前提とします。

## <a name="embed-the-manifest-file-into-the-executable-file-of-the-published-solution"></a>マニフェスト ファイルを発行済みソリューションの実行可能ファイルに埋め込むには

1. **Visual Studio 用開発者コマンド プロンプト** を開きます。

    Visual Studio の開発者コマンド プロンプトを開く方法の詳細については、[開発者コマンド プロンプトと開発者用 PowerShell](../ide/reference/command-prompt-powershell.md) に関する記事をご覧ください。

   > [!NOTE]
   > 残りの手順は、ソリューションに関して以下を前提とします。
   >
   > - ソリューションの名前は **MyWPFProject** です。
   > - このソリューションは、次のディレクトリに格納されます。`%UserProfile%\Documents\Visual Studio 2010\Projects\`
   >
   > - このソリューションは、次のディレクトリに発行されます。`%UserProfile%\Documents\Visual Studio 2010\Projects\publish`
   > - 発行されたアプリケーション ファイルの最新バージョンは、次のディレクトリに格納されます。`%UserProfile%\Documents\Visual Studio 2010\Projects\publish\Application Files\WPFApp_1_0_0_0`
   >
   > 上記の名前とディレクトリの場所は、いずれも使用する必要はありません。 前の名前と場所は、ソリューションの発行に必要な手順について説明するためにのみ使用されます。

2. コマンド プロンプトで、発行済みのアプリケーション ファイルの最新バージョンが含まれるディレクトリへのパスを変更します。 この手順を次の例に示します。

   ```cmd
   cd "%UserProfile%\Documents\Visual Studio 2010\Projects\MyWPFProject\publish\Application Files\WPFApp_1_0_0_0"
   ```

3. コマンド プロンプトで、次のコマンドを実行して、アプリケーションの実行可能ファイルにマニフェスト ファイルを埋め込みます。

   ```cmd
   mt -manifest c:\temp\themes.manifest -outputresource:MyWPFApp.exe.deploy
   ```

## <a name="sign-the-application-and-deployment-manifests"></a>アプリケーション マニフェストと配置マニフェストに署名します。

1. コマンド プロンプトで、次のコマンドを実行して、現在のディレクトリ内の実行可能ファイルから *.deploy* 拡張子を削除します。

   ```cmd
   ren MyWPFApp.exe.deploy MyWPFApp.exe
   ```

   > [!NOTE]
   > この例では、1 つのファイルだけが *.deploy* ファイル拡張子を持っていると仮定しています。 必ず、このディレクトリ内の *.deploy* ファイル拡張子を持つすべてのファイルの名前を変更してください。

2. コマンド プロンプトで、次のコマンドを実行してアプリケーション マニフェストに署名します。

   ```cmd
   mage -u MyWPFApp.exe.manifest -cf ..\..\..\MyWPFApp_TemporaryKey.pfx
   ```

   > [!NOTE]
   > この例では、プロジェクトの *.pfx* ファイルを使用してマニフェストに署名すると仮定しています。 マニフェストに署名しない場合は、この例で使用されている `-cf` パラメーターを省略できます。 パスワードを必要とする証明書でマニフェストに署名する場合は、`-password` オプションを指定します (`For example: mage -u MyWPFApp.exe.manifest -cf ..\..\..\MyWPFApp_TemporaryKey.pfx - password Password`)。

3. コマンド プロンプトで、次のコマンドを実行して、この手順の前の手順で名前を変更したファイルの名前に *.deploy* 拡張子を追加します。

   ```
   ren MyWPFApp.exe MyWPFApp.exe.deploy
   ```

   > [!NOTE]
   > この例では、1 つのファイルだけが *.deploy* ファイル拡張子を持っていたと仮定しています。 必ず、このディレクトリ内の以前のファイル名拡張子が *.deploy* だったすべてのファイルの名前を変更してください。

4. コマンド プロンプトで、次のコマンドを実行して配置マニフェストに署名します。

   ```
   mage -u ..\..\MyWPFApp.application -appm MyWPFApp.exe.manifest -cf ..\..\..\MyWPFApp_TemporaryKey.pfx
   ```

   > [!NOTE]
   > この例では、プロジェクトの *.pfx* ファイルを使用してマニフェストに署名すると仮定しています。 マニフェストに署名しない場合は、この例で使用されている `-cf` パラメーターを省略できます。 パスワードを必要とする証明書でマニフェストに署名する場合は、次の例のように `-password` オプションを指定します。`For example: mage -u MyWPFApp.exe.manifest -cf ..\..\..\MyWPFApp_TemporaryKey.pfx - password Password`

   これらの手順を実行した後、エンド ユーザーがアプリケーションをインストールする場所に、発行されたファイルを移動できます。 ソリューションを頻繁に更新する場合は、新しいバージョンを発行するたびに、スクリプトにこれらのコマンドを移動し、スクリプトを実行できます。

## <a name="see-also"></a>関連項目

- [ClickOnce 配置の固有のエラーのトラブルシューティング](../deployment/troubleshooting-specific-errors-in-clickonce-deployments.md)
- [Visual スタイルの概要](/windows/desktop/Controls/visual-styles-overview)
- [視覚スタイルを有効にする](/windows/desktop/Controls/cookbook-overview)
- [開発者コマンド プロンプトと開発者用 PowerShell](../ide/reference/command-prompt-powershell.md)
