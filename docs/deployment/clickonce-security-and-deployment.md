---
title: ClickOnce のセキュリティと配置 |Microsoft Docs
description: 自己更新型の Windows ベースのアプリケーションを作成できるようにする配置テクノロジである ClickOnce の Visual Studio でのサポートについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- Windows applications, ClickOnce deployment
- deploying applications [ClickOnce]
- ClickOnce deployment
- publishing, ClickOnce
ms.assetid: abab6d34-c3c2-45c1-a8b6-43c7d3131e7a
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 8bb0bdeae09f22a2b45e3029fbc9097c00911d2a
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99930019"
---
# <a name="clickonce-security-and-deployment"></a>ClickOnce のセキュリティと配置
[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] は、ユーザーとの最小限の対話によってインストールして実行できる、自己更新型の Windows ベースのアプリケーションの作成を可能にする配置テクノロジです。 Visual Basic および Visual C# を使用してプロジェクトが開発された場合、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] では、ClickOnce テクノロジを使用して配置されたアプリケーションの発行と更新を完全にサポートします。 Visual C++ アプリケーションの配置の詳細については、「[Visual C++ アプリケーションの ClickOnce 配置](/cpp/windows/clickonce-deployment-for-visual-cpp-applications)」を参照してください。

 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 配置により、配置での 3 つの主な問題が克服されます。

- **アプリケーションの更新における問題。** Microsoft Windows インストーラー配置では、アプリケーションが更新されるたびに、ユーザーは更新プログラムと msp ファイルをインストールし、インストール済みの製品に適用することができます。[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 配置では、更新プログラムを自動的に提供できます。 アプリケーションの変更された部分のみがダウンロードされ、更新されたアプリケーションアプリケーション完全なアプリケーションは新しい side-by-side フォルダーから再インストールされます。

- **ユーザーのコンピューターへの影響。** Windows インストーラー配置では、アプリケーションは共有コンポーネントに依存することが多く、バージョン管理の競合が発生する可能性があります。[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 配置では、各アプリケーションは自己完結型であり、他のアプリケーションと干渉しません。

- **セキュリティ アクセス許可。** Windows インストーラー配置には管理アクセス許可が必要であり、限定的なユーザー インストールのみが可能です。[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 配置により、管理者以外のユーザーが、アプリケーションに必要なコード アクセス セキュリティのアクセス許可のみをインストールして付与することができます。

  これまで、これらの問題により、開発者が Windows ベースのアプリケーションではなく Web アプリケーションを作成することを決め、インストールの容易さのために機能豊富なユーザー インターフェイスを犠牲にすることがありました。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] を使用して配置されたアプリケーションを使用することにより、両方のテクノロジを最大限に活用できます。

## <a name="what-is-a-clickonce-application"></a>ClickOnce アプリケーションとは
 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションとは、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] テクノロジを使用して発行された Windows Presentation Foundation (*xbap*)、Windows フォーム ( *.exe*)、コンソール アプリケーション ( *.exe*)、または Office ソリューション ( *.dll*) です。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションは、3 つの異なる方法で発行できます (Web ページから、ネットワークファイル共有から、または CD-ROM などのメディアから)。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションは、エンド ユーザーのコンピューターにインストールし、コンピューターがオフラインのときでもローカルで実行することができます。または、エンド ユーザーのコンピューターに永続的に何もインストールすることなく、オンライン専用モードで実行できます。 詳細については、「[ClickOnce 配置ストラテジの選択](../deployment/choosing-a-clickonce-deployment-strategy.md)」を参照してください。

 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションは自己更新型にすることができます。より新しいバージョンをチェックし、利用可能になると、更新対象のファイルを自動的に置き換えることができます。 開発者は、更新動作を指定できます。また、ネットワーク管理者は、更新を必須としてマークするなど、更新方法を制御することもできます。 更新プログラムは、エンド ユーザーまたは管理者によって以前のバージョンにロールバックすることもできます。 詳細については、「[ClickOnce の更新方法の選択](../deployment/choosing-a-clickonce-update-strategy.md)」を参照してください。

 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションは分離されているため、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションをインストールまたは実行しても、既存のアプリケーションを中断することはありません。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションは自己完結型です。各 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションは、セキュリティで保護されたユーザーごと、アプリケーションごとのキャッシュにインストールされて実行されます。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションは、インターネットまたはイントラネットのセキュリティ ゾーンで実行されます。 必要であれば、アプリケーションから昇格されたセキュリティ アクセス許可を要求できます。 詳細については、「[セキュリティで保護された ClickOnce アプリケーション](../deployment/securing-clickonce-applications.md)」を参照してください。

## <a name="how-clickonce-security-works"></a>ClickOnce セキュリティのしくみ
 コア [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] セキュリティは、証明書、コード アクセス セキュリティ ポリシー、および ClickOnce 信頼プロンプトに基づいています。

### <a name="certificates"></a>証明書
 Authenticode 証明書は、アプリケーションのパブリッシャーの信頼性を検証するために使用されます。 ClickOnce は、アプリケーションの配置に Authenticode を使用することによって、有害なプログラムが確立された信頼できるソースからの正式なプログラムになりすますのを防ぎます。 必要に応じて、証明書を使用してアプリケーション マニフェストと配置マニフェストに署名し、ファイルが改ざんされていないことを証明することもできます。 詳細については、「[ClickOnce と Authenticode](../deployment/clickonce-and-authenticode.md)」を参照してください。 証明書を使用して、信頼された発行元の一覧を持つようにクライアント コンピューターを構成することもできます。 アプリケーションが信頼された発行元からのものである場合は、ユーザーの操作なしでインストールできます。 詳細については、「[信頼されたアプリケーションの配置の概要](../deployment/trusted-application-deployment-overview.md)」を参照してください。

### <a name="code-access-security"></a>コード アクセス セキュリティ
 コード アクセス セキュリティにより、コードがアクセスする対象を保護されたリソースに制限できます。 ほとんどの場合は、インターネット ゾーンまたはローカル イントラネット ゾーンを選択して、アクセス許可を制限できます。 **ProjectDesigner** の **[セキュリティ]** ページを使用して、アプリケーションに適切なゾーンを要求します。 アクセス許可が制限されたアプリケーションをデバッグして、エンド ユーザー エクスペリエンスをエミュレートすることもできます。 詳細については、「[ClickOnce アプリケーションのコード アクセス セキュリティ](../deployment/code-access-security-for-clickonce-applications.md)」を参照してください。

### <a name="clickonce-trust-prompt"></a>ClickOnce 信頼プロンプト
 アプリケーションがゾーンで許可するよりも多くのアクセス許可を要求する場合、エンド ユーザーに対して信頼の決定に関するプロンプトを表示できます。 エンド ユーザーは、Windows フォーム アプリケーション、Windows Presentation Foundation アプリケーション、コンソール アプリケーション、XAML ブラウザー アプリケーション、Office ソリューションなどの ClickOnce アプリケーションが実行に関して信頼されるかどうかを決定できます。 詳細については、「[方法: ClickOnce 信頼プロンプトの動作を構成する](../deployment/how-to-configure-the-clickonce-trust-prompt-behavior.md)」を参照してください。

## <a name="how-clickonce-deployment-works"></a>ClickOnce 配置のしくみ
 コア [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 配置アーキテクチャは、アプリケーション マニフェストと配置マニフェストの 2 つの XML マニフェスト ファイルに基づいています。 ファイルは、ClickOnce アプリケーションのインストール元、更新方法、および更新時期を記述するために使用されます。

### <a name="publish-clickonce-applications"></a>ClickOnce アプリケーションの発行
 アプリケーション マニフェストでは、アプリケーション自体について記述します。 これには、アセンブリ、アプリケーションを構成する依存関係とファイル、必要なアクセス許可、および更新プログラムが利用可能になる場所が含まれます。 アプリケーション開発者は、Visual Studio の発行ウィザードまたは [!INCLUDE[winsdklong](../deployment/includes/winsdklong_md.md)] 内のマニフェスト生成および編集ツール (*Mage.exe*) を使用して、アプリケーション マニフェストを作成します。 詳細については、「[方法: 発行ウィザードを使用して ClickOnce アプリケーションを発行する](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)」を参照してください。

 配置マニフェストでは、アプリケーションの配置方法を示します。 これには、アプリケーション マニフェストの場所と、クライアントが実行する必要があるアプリケーションのバージョンが含まれます。

### <a name="deploy-clickonce-applications"></a>ClickOnce アプリケーションの配置
 配置マニフェストを作成したら、それを配置場所にコピーします。 配置場所は、Web サーバー、ネットワーク ファイル共有、CD などのメディアのいずれでもかまいません。 アプリケーション マニフェストとすべてのアプリケーション ファイルは、配置マニフェストで指定される配置場所にもコピーされます。 これは、配置場所と同じ場所でも、別の場所でもかまいません。 Visual Studio で **発行ウィザード** を使用する場合、コピー操作は自動的に実行されます。

### <a name="install-clickonce-applications"></a>ClickOnce アプリケーションのインストール
 配置場所に配置されたら、エンド ユーザーは Web ページ上またはフォルダー内の配置マニフェスト ファイルを表すアイコンをクリックすることで、アプリケーションをダウンロードしてインストールできます。 ほとんどの場合、エンド ユーザーには、インストールの確認をユーザーに求めるシンプルなダイアログ ボックスが表示されます。確認後、追加の介入なしで、インストールが進行し、アプリケーションが起動されます。 アプリケーションでアクセス許可の昇格が必要な場合、またはアプリケーションが信頼された証明書によって署名されていない場合、ダイアログ ボックスでは、インストールを続行する前にアクセス許可を付与するようにユーザーに求めます。 ClickOnce のインストールはユーザー単位ですが、管理者特権を必要とする前提条件がある場合は、アクセス許可の昇格が必要になることがあります。 アクセス許可の昇格の詳細については、「[ClickOnce アプリケーションのセキュリティ](../deployment/securing-clickonce-applications.md)」を参照してください。

 証明書はコンピューター レベルまたはエンタープライズ レベルで信頼できます。これにより、信頼された証明書で署名された ClickOnce アプリケーションをサイレント インストールできます。 信頼された証明書の詳細については、「[信頼されたアプリケーションの配置の概要](../deployment/trusted-application-deployment-overview.md)」を参照してください。

 アプリケーションは、ユーザーの **[スタート]** メニュー、および **コントロール パネル** の **[プログラムの追加と削除]** グループに追加できます。 他の配置テクノロジとは異なり、**Program Files** フォルダーまたはレジストリには何も追加されず、インストールのために管理者権限は必要ありません。

> [!NOTE]
> また、アプリケーションを **[スタート]** メニューおよび **[プログラムの追加と削除]** グループに追加されないようにして、Web アプリケーションのように動作させることもできます。 詳細については、「[ClickOnce 配置ストラテジの選択](../deployment/choosing-a-clickonce-deployment-strategy.md)」を参照してください。

### <a name="update-clickonce-applications"></a>ClickOnce アプリケーションの更新
 アプリケーション開発者は、アプリケーションの更新されたバージョンを作成するとき、新しいアプリケーション マニフェストを生成し、ファイルを配置場所 (通常は、元のアプリケーション配置フォルダーの兄弟フォルダー) にコピーします。 管理者は、アプリケーションの新しいバージョンの場所を示すために配置マニフェストを更新します。

> [!NOTE]
> Visual Studio の **発行ウィザード** を使用して、これらの手順を実行できます。

 配置マニフェストには、配置場所だけでなく、アプリケーションで最新バージョンをチェックする更新場所 (Web ページまたはネットワーク ファイル共有) も含まれます。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] **[発行]** プロパティは、アプリケーションが更新プログラムを確認するタイミングと頻度を指定するために使用されます。 更新動作は、配置マニフェストで指定することができます。または、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] API を介してアプリケーションのユーザー インターフェイスにユーザーの選択肢として提示できます。 さらに、**[発行]** プロパティを使用して、更新を必須にしたり、以前のバージョンにロールバックしたりすることもできます。 詳細については、「[ClickOnce の更新方法の選択](../deployment/choosing-a-clickonce-update-strategy.md)」を参照してください。

### <a name="third-party-installers"></a>サードパーティのインストーラー
 ClickOnce インストーラーを、サードパーティ コンポーネントをアプリケーションと共にインストールするようにカスタマイズできます。 再頒布可能パッケージ (.exe または .msi ファイル) があり、言語に依存しない製品マニフェストと言語固有のパッケージ マニフェストによってパッケージを記述する必要があります。 詳細については、「[ブートストラップパッケージの作成](../deployment/creating-bootstrapper-packages.md)」を参照してください。

## <a name="clickonce-tools"></a>ClickOnce ツール
 次の表に、アプリケーション マニフェストと配置マニフェストの生成、編集、署名、および再署名に使用できるツールを示します。

|ツール|説明|
|----------|-----------------|
|[[セキュリティ] ページ (プロジェクト デザイナー)](../ide/reference/security-page-project-designer.md)|アプリケーション マニフェストと配置マニフェストに署名します。|
|[[発行] ページ (プロジェクト デザイナー)](../ide/reference/publish-page-project-designer.md)|Visual Basic および Visual C# アプリケーションのアプリケーション マニフェストおよび配置マニフェストを生成して編集します。|
|[*Mage.exe* (マニフェスト生成および編集ツール)](/dotnet/framework/tools/mage-exe-manifest-generation-and-editing-tool)|Visual Basic、Visual C#、および Visual C++ アプリケーションのアプリケーション マニフェストおよび配置マニフェストを生成します。<br /><br /> アプリケーション マニフェストと配置マニフェストへ署名および再署名します。<br /><br /> バッチ スクリプトとコマンド プロンプトから実行できます。|
|[*MageUI.exe* (マニフェスト生成および編集ツールのグラフィカル クライアント)](/dotnet/framework/tools/mageui-exe-manifest-generation-and-editing-tool-graphical-client)|アプリケーション マニフェストと配置マニフェストを生成して編集します。<br /><br /> アプリケーション マニフェストと配置マニフェストへ署名および再署名します。|
|[GenerateApplicationManifest タスク](../msbuild/generateapplicationmanifest-task.md)|アプリケーション マニフェストを生成します。<br /><br /> MSBuild から実行できます。 詳細については、「[MSBuild リファレンス](../msbuild/msbuild-reference.md)」を参照してください。|
|[GenerateDeploymentManifest タスク](../msbuild/generatedeploymentmanifest-task.md)|配置マニフェストを生成します。<br /><br /> MSBuild から実行できます。 詳細については、「[MSBuild リファレンス](../msbuild/msbuild-reference.md)」を参照してください。|
|[SignFile タスク](../msbuild/signfile-task.md)|アプリケーション マニフェストと配置マニフェストに署名します。<br /><br /> MSBuild から実行できます。 詳細については、「[MSBuild リファレンス](../msbuild/msbuild-reference.md)」を参照してください。|
|[Microsoft.Build.Tasks.Deployment.ManifestUtilities](/dotnet/api/microsoft.build.tasks.deployment.manifestutilities)|独自のアプリケーションを開発して、アプリケーション マニフェストと配置マニフェストを生成します。|

 次の表に、これらのブラウザーで ClickOnce アプリケーションをサポートするために必要な .NET Framework バージョンを示します。

|Browser|.NET Framework のバージョン|
|-------------|----------------------------|
|Internet Explorer|2.0、3.0、3.5、3.5 SP1、4|
|Firefox|2.0 SP1、3.5 SP1、4|
|Chrome|3.5|
|Microsoft Edge|3.5|

## <a name="see-also"></a>関連項目
- [Windows Vista の ClickOnce 配置](../deployment/clickonce-deployment-on-windows-vista.md)
- [ClickOnce アプリケーションの発行](../deployment/publishing-clickonce-applications.md)
- [ClickOnce アプリケーションのセキュリティ保護](../deployment/securing-clickonce-applications.md)
- [ClickOnce での COM コンポーネントの配置](../deployment/deploying-com-components-with-clickonce.md)
- [ClickOnce アプリケーションのコマンド ラインからのビルド](../deployment/building-clickonce-applications-from-the-command-line.md)
- [System.Deployment.Application を使用する ClickOnce アプリケーションのデバッグ](../deployment/debugging-clickonce-applications-that-use-system-deployment-application.md)
