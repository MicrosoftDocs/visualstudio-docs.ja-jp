---
title: Office ソリューションの配置のトラブルシューティング
description: Office ソリューションを配置するときに発生する可能性がある一般的な問題を解決する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: troubleshooting
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ClickOnce deployment [Office development in Visual Studio], troubleshooting
- Office development in Visual Studio, troubleshooting
- deploying applications [Office development in Visual Studio], troubleshooting
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 59b5e36eb02ff2c8db9e2e206a4040757e130716
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99968841"
---
# <a name="troubleshoot-office-solution-deployment"></a>Office ソリューションの配置のトラブルシューティング
  このトピックでは、Office ソリューションを配置するときに発生する可能性がある一般的な問題を解決する方法について説明します。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

## <a name="troubleshoot-office-solutions-by-using-the-event-viewer"></a>イベント ビューアーを使用した Office ソリューションのトラブルシューティング
 Windows のイベント ビューアーを使用すると、Office ソリューションのインストール時またはアンインストール時に [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] でキャプチャされるエラー メッセージを表示できます。 イベント ロガーからのこれらのメッセージを使用して、インストールと配置の問題を解決できます。 詳細については、「[Office ソリューションのイベント ログ](../vsto/event-logging-for-office-solutions.md)」を参照してください。

## <a name="change-the-assembly-name-causes-conflicts"></a>アセンブリ名を変更すると競合が発生する
 ソリューションを配置した後に、 **[プロジェクト デザイナー]** の **[アプリケーション]** ページで **[アセンブリ名]** の値を変更すると、発行ツールによってセットアップ パッケージが変更され、1 つの *Setup.exe* ファイルに 2 つの配置マニフェストが存在することになります。 2 つのマニフェスト ファイルを配置すると、次のような状況が発生する場合があります。

- エンド ユーザーが両方のバージョンをインストールすると、アプリケーションは両方の VSTO アドインを読み込みます。

- VSTO アドインがインストールされている状態でアセンブリの名前を変更すると、エンド ユーザーが更新を受け取ることはなくなります。

  これらの状況を回避するには、ソリューションを配置した後にソリューションの **[アセンブリ名]** の値を変更しないようにします。

## <a name="check-for-updates-takes-a-long-time"></a>更新プログラムのチェックに長い時間がかかる
 Visual Studio 2010 Tools for Office ランタイムには、マニフェストやソリューションをダウンロードするときのタイムアウト値を設定するために管理者が使用できるように、レジストリ エントリが用意されています。

#### <a name="to-set-the-time-out-value"></a>タイムアウト値を設定するには

1. レジストリで、次のキーに移動します。

     **HKEY_CURRENT_USER\Software\Microsoft\VSTA**

2. **AddInTimeout** サブキーに、タイムアウト値をミリ秒単位で設定します。

     **[AddInTimeout]** サブキーが存在しない場合は、DWORD として作成します。

## <a name="cant-update-or-publish-to-a-network-file-share"></a>ネットワーク ファイル共有に対する更新または発行ができない
 ネットワーク ファイル共有にある Office ソリューションは、更新の発行プロセスでソリューションの *Setup.exe* ファイルがロックされると、誤解を招くメッセージを表示することがあります。 たとえば、"'setup.exe' を Web サイトに追加できません。 ファイル 'setup.exe' はこの Web サイトに既に存在します。" というメッセージが表示されることがあります。

 ファイルがロックされないようにするには、エンド ユーザーに対して共有を読み取り専用に設定します。 ただし、共有上にドキュメントがあると、このドキュメントもエンド ユーザーに対して読み取り専用になります。

## <a name="prerequisites-for-microsoft-office-arent-installed"></a>Microsoft Office の必須コンポーネントがインストールされていない
 セットアップ パッケージには、Office ソリューションと共に配置される必須コンポーネントとして、.NET Framework、 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]、および Office プライマリ相互運用機能アセンブリを追加できます。 プライマリ相互運用機能アセンブリをインストールする方法の詳細については、「[Office ソリューションを開発できるようにコンピューターを構成する](../vsto/configuring-a-computer-to-develop-office-solutions.md)」および「[方法: Office のプライマリ相互運用機能アセンブリをインストールする](../vsto/how-to-install-office-primary-interop-assemblies.md)」を参照してください。

## <a name="publish-using-localhost-can-cause-installation-problems"></a>Localhost を使用して発行するとインストールに問題が生じることがある
 ドキュメント レベルのソリューションの発行場所またはインストール先として `http://localhost` を使用した場合、この文字列は **[発行ウィザード]** で実際のコンピューター名に変換されません。 この場合は、ソリューションを開発用コンピューター上にインストールする必要があります。 配置ソリューションに開発用コンピューター上の IIS を使用させるには、HTTP、HTTPS、FTP のすべての場所について、localhost ではなく完全修飾名を使用します。

## <a name="cached-assemblies-are-loaded-instead-of-updated-assemblies"></a>更新済みのアセンブリではなくキャッシュしたアセンブリが読み込まれる
 プロジェクトの出力パスがネットワーク ファイル共有上にあり、アセンブリが厳密な名前で署名されていて、カスタマイズ アセンブリのバージョンが変更されていない場合、.NET Framework アセンブリ ローダーである fusion は、キャッシュしたアセンブリのコピーを読み込みます。 アセンブリを更新しても、これらの条件が満たされるとキャッシュしたコピーが読み込まれるため、プロジェクトを次回実行するときに更新は表示されません。

 Visual Studio を構成し、プロジェクトを実行するたびに fusion がアセンブリをダウンロードするように設定できます。

### <a name="to-download-assemblies-instead-of-loading-cached-copies"></a>キャッシュしたコピーではなくアセンブリをダウンロードするには

1. メニュー バーで、 **[プロジェクト]**、[ _ProjectName_**のプロパティ]**」を参照してください。

2. **[アプリケーション]** ページで、 **[アセンブリ情報]** を選択します。

3. **[アセンブリのバージョン]** のリビジョン番号、3 番目のフィールドを、ワイルド カード (\*) に設定します。 たとえば、"1.0.*" です。  次に、 **[OK]** ボタンを選択します。

   アセンブリのバージョンを変更したら、厳密な名前でアセンブリに署名します。fusion が最新バージョンのカスタマイズを読み込むようになります。

 [!NOTE]
> Visual Studio 2017 以降では、アセンブリのバージョンでワイルド カードを使用しようとすると、ビルド エラーが発生します。  これは、アセンブリのバージョンのワイルド カードによって MSBuild Deterministic 機能が損なわれるためです。 ワイルドカードをアセンブリのバージョンから削除するか、決定性を無効にするよう指示されます。  Deterministic 機能の詳細については、「[MSBuild プロジェクトの共通プロパティ](../msbuild/common-msbuild-project-properties.md)」および「[ビルドのカスタマイズ](../msbuild/customize-your-build.md)」を参照してください

## <a name="installation-fails-when-the-uri-has-characters-that-arent-us-ascii"></a>URI に US-ASCII 以外の文字が含まれているとインストールが失敗する
 Office ソリューションを HTTP、HTTPS、または FTP のいずれかの場所に発行する場合、US-ASCII ではない Unicode 文字をパスに含めることはできません。 これらの文字を使用すると、セットアップ プログラムで一貫性のない動作が実行されることがあります。 インストール パスには、US-ASCII 文字を使用してください。

## <a name="prompt-to-manually-uninstall-appears-when-you-publish-and-install-a-solution-on-the-development-computer"></a>開発用コンピューターにソリューションを発行およびインストールすると手動でアンインストールするよう求めるプロンプトが表示される
 Office ソリューションをビルドすると、そのビルド バージョンが自動的に登録されます。 開発用コンピューターに同じソリューションを以前に発行およびインストールしていた場合は、次のビルド後、リビルド後、または発行後に、発行されたバージョンとビルドされたバージョンのインストール パスが違うことが [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] によって検出されます。 "現在他のバージョンがインストールされており、この場所からアップグレードすることはできないため、このカスタマイズをインストールすることはできません。" というエラー メッセージが表示されます。 レジストリ キーは、ソリューションがビルドされるたびに更新されます。 したがって、新しいバージョンを発行、デバッグ、または実行する前に、以前のバージョンをアンインストールする必要があります。

 このメッセージが表示されないようにするには、開発用コンピューターで別のユーザー アカウントを作成して配置をテストします。 または、次回のソリューションの発行、デバッグ、またはリビルドの前に、コンピューター上にインストールされているプログラムの一覧からそのバージョンをアンインストールできます。

## <a name="uncaught-exception-or-method-not-found-error-when-you-install-a-solution"></a>ソリューションをインストールするときキャッチされない例外やメソッドが見つからないエラーが発生する
 配置マニフェスト ( *.vsto* ファイル)、Office アプリケーション、ドキュメント、またはブックを開いて Office ソリューションをインストールすると、次の状態に対するエラー メッセージが表示される場合があります。

- メソッドが見つからない

- MissingMethodException

- キャッチされない例外

  これらのエラー メッセージが表示されないようにするには、セットアップ プログラムを実行することにより、ソリューションをインストールします。

  セットアップ プログラムを実行せずにソリューションをインストールする場合、インストーラーでは、必須コンポーネントの有無のチェックや、それらのインストールは行われません。 セットアップ プログラムは、正しいバージョンの必須コンポーネントをチェックし、必要に応じて、これらをインストールします。

## <a name="manifest-registry-keys-for-add-ins-change-after-an-installshield-limited-edition-project-is-built"></a>InstallShield Limited Edition プロジェクトをビルドした後にアドイン用マニフェスト レジストリ キーが変わる
 VSTO アドイン セットアップ プログラムに含まれるマニフェスト レジストリ キーが、InstallShield Limited Edition プロジェクトのビルド時に *.vsto* から *.dll.manifest* に変わる場合があります。

 この問題の発生を防ぐには、InstallShield Limited Edition プロジェクトを別のソリューションで作成するか、レジストリ キー値として VSTO アドイン名が含まれる CompanyName.AddinName を使用します。

## <a name="the-clickonce-installer-for-your-office-solution-doesnt-install-the-primary-interop-assemblies"></a>Office ソリューションの ClickOnce インストーラーがプライマリ相互運用機能アセンブリをインストールしない
 Office ソリューション用に ClickOnce が作成するセットアップ プログラムを実行すると、Office プライマリ相互運用機能アセンブリ (PIA) がまだインストールされていない場合のみ、PIA のインストーラーが実行されます。

 セットアップ プログラムで PIA が正しくインストールされない場合、インストール ディレクトリから *o2007pia.msi* というインストーラー ファイルを実行して PIA を手動でインストールします。

## <a name="reinstall-office-solutions-causes-an-argument-out-of-range-exception"></a>Office ソリューションを再インストールすると、引数が範囲外という例外が発生する
 Office ソリューションを再インストールするときに、 <xref:System.ArgumentOutOfRangeException> 例外が発生し、"指定された引数は、有効な値の範囲内にありません" というエラー メッセージが表示される場合があります。

 インストール場所の URL の大文字と小文字が違っていると、この状況が発生します。 このエラーは、たとえば、最初に `http://fabrikam.com/ExcelSolution.vsto` から Office ソリューションをインストールし、2 回目に `http://fabrikam.com/excelsolution.vsto` を使用した場合に表示されます。

 このエラー メッセージが表示されないようにするには、Office ソリューションのインストール時に、同じ大文字と小文字の組み合わせを使用します。

## <a name="cant-install-a-clickonce-solution-by-opening-the-deployment-manifest-from-the-web"></a>Web で配置マニフェストを開いても ClickOnce ソリューションをインストールできない
 ユーザーは、Web で配置マニフェストを開くことにより、Office ソリューションをインストールできます。 ただし、一部のインターネット インフォメーション サービス (IIS) がインストールされていると、 *.vsto* ファイル名拡張子はブロックされます。 IIS を使用して Office ソリューションを配置する前に、IIS で MIME の種類を定義する必要があります。

 IIS 7 で MIME の種類を定義する方法については、「[MIME の種類を追加する (IIS7)](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc725608(v=ws.10))」をご覧ください。

 拡張子を **.vsto** に、MIME の種類を " **application/x-ms-vsto**" に設定します。

## <a name="see-also"></a>関連項目

- [ClickOnce 配置のトラブルシューティング](../deployment/troubleshooting-clickonce-deployments.md)
- [Office ソリューションを配置する](../vsto/deploying-an-office-solution.md)
- [Visual Studio トラブルシューティング](/troubleshoot/visualstudio/welcome-visual-studio/)