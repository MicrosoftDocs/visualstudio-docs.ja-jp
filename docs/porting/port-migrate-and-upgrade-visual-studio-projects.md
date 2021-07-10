---
title: プロジェクトの移植、移行、およびアップグレード
description: 現在および以前のバージョンの Visual Studio で作成されたプロジェクトのサポートに関するリファレンス。
ms.date: 06/17/2021
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
ms.topic: conceptual
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload: multiple
f1_keywords:
- Win8ExpressDesktopBlock
- w8trefactor
- VS.ReviewProjectAndSolutionChangesDialog.UpgradeRetarget
- ProjectCompatibilityDlgHelpTopic
- VS.ReviewProjectAndSolutionChangesDialog.Upgrade
helpviewer_keywords:
- conversion, projects
- asset compatibility
- projects, conversion
ms.openlocfilehash: d5b562df4d644b21e306c73aedba756d33947797
ms.sourcegitcommit: 5fb4a67a8208707e79dc09601e8db70b16ba7192
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2021
ms.locfileid: "112306411"
---
# <a name="project-migration-and-upgrade-reference-for-visual-studio"></a>Visual Studio のプロジェクトの移行とアップグレードのリファレンス

::: moniker range="vs-2017"

通常、各バージョンの Visual Studio は、以前の種類のプロジェクト、ファイル、その他のアセットのほとんどに対応しています。 それらのオブジェクトは[これまでと同様に](../ide/solutions-and-projects-in-visual-studio.md)操作できます。新しい機能を利用していない場合でも、Visual Studio 2015、Visual Studio 2013、Visual Studio 2012 など、以前のバージョンとの下位互換性の維持が試みられています。 (どの機能がどのバージョンに固有の機能であるかについては、[リリース ノート](/visualstudio/releasenotes/vs2017-relnotes/)を参照してください。)

一部の種類のプロジェクトに対するサポートは、今後変更される場合もあります。 新しいバージョンの Visual Studio では、特定のプロジェクトが一切サポートされなくなったり、下位互換性がないプロジェクトの更新が必要になったりすることがあります。 移行に関する問題の現在の状況については、[Visual Studio Developer Community のサイト](https://aka.ms/feedback/suggest?space=8)を参照してください。

現在、この記事では、Visual Studio 2017 の移行が可能なプロジェクト タイプに対してのみ詳細を提供しています。 この記事では、Visual Studio 2017 でサポートされなくなったことで移行できないプロジェクト タイプは除外されています。 また、移行に関する問題がないサポート対象のプロジェクト タイプ ([対象プラットフォームと互換性](/visualstudio/productinfo/vs2017-compatibility-vs)に関するページでその一覧を確認できます) もこの記事では除外されています。

> [!IMPORTANT]
> 特定の種類のプロジェクトでは、Visual Studio インストーラーで適切なワークロードをインストールする必要があります。 ワークロードがインストールされていない場合、Visual Studio は不明な、または互換性のないプロジェクトの種類を報告します。 その場合、インストール オプションを確認して、やり直してください。 Visual Studio 2017 でサポートされているプロジェクトの詳細について、[対象プラットフォームと互換性](/visualstudio/productinfo/vs2017-compatibility-vs)に関する記事をもう一度ご覧ください。

## <a name="project-types"></a>プロジェクトの種類

次の一覧は、Visual Studio 2017 より前のバージョンで作成されたプロジェクトに対する Visual Studio 2017 でのサポートをまとめたものです。

一覧表示されるべきプロジェクトやファイルの種類が見つからない場合は、[この記事の Visual Studio 2015 バージョン](/previous-versions/visualstudio/visual-studio-2015/porting/porting-migrating-and-upgrading-visual-studio-projects?preserve-view=true&view=vs-2015)をご覧になり、このページの下にある **[Send feedback about]\(フィードバックの送信\)** の **[This page]\(このページ\)** ボタンを使用して、プロジェクトの詳細をお知らせください。 (匿名の "このページは役に立ちましたか。" コントロールを使用した場合、 フィードバックに応対できません。)

| プロジェクトの種類 | サポート |
| --- | --- |
| .NET Core プロジェクト (xproj) | Visual Studio 2015 で作成したプロジェクトでは、.xproj プロジェクト ファイルが含まれるプレビュー ツールが使用されていました。 Visual Studio 2017 では、xproj 形式は csproj 形式への移行以外ではサポートされていません。 xproj ファイルを開くと、SDK スタイルの csproj 形式にファイルを移行するように求められます。 (xproj ファイルのバックアップが作成されます。)SDK スタイルの csproj プロジェクトは、Visual Studio 2015 以前ではサポートされません。 詳細については、「[.NET Core プロジェクトから .csproj 形式への移行](/dotnet/core/migration/#visual-studio)」をご覧ください。|
| ASP.NET Web アプリケーションと ASP.NET Core Web アプリケーション (Application Insights が有効) | Visual Studio のユーザーごとのリソース情報がユーザー インスタンス別にレジストリに保存されます。 この情報は、プロジェクトを開いていない状態で Azure Application Insights データを検索するときに利用されます。 Visual Studio 2015 では、Visual Studio 2017 とは異なるレジストリの場所が使用され、競合しません。<br/><br/>ユーザーが ASP.NET Web アプリケーションまたは ASP.NET Core Web アプリケーションを作成すると、リソースは .suo ファイルに保存されます。 ユーザーは Visual Studio 2015 や 2017 でプロジェクトを開くことができます。両方のバージョンで使用されているプロジェクトとソリューションが Visual Studio でサポートされている限り、両方でリソース情報が使用されます。 ユーザーは製品ごとに 1 回認証する必要があります。 たとえば、Visual Studio 2015 で作成されたプロジェクトを Visual Studio 2017 で開く場合、Visual Studio 2017 で認証が要求されます。 |
| C#/Visual Basic Webform または Windows フォーム | プロジェクトを Visual Studio 2017 と Visual Studio 2015 で開くことができます。 |
| データベース単体テスト プロジェクト (csproj、.vbproj) | 古いデータ単体テスト プロジェクトは Visual Studio 2017 で読み込まれますが、依存関係は GAC に保存されているものが使用されます。 単体テスト プロジェクトをアップグレードし、最新の依存関係を使用するには、ソリューション エクスプローラーでプロジェクトを右クリックし、 **[SQL Server 単体テスト プロジェクトに変換する]** を選択します。 |
| F# | Visual Studio 2017 では、Visual Studio 2013 と 2015 で作成したプロジェクトを開くことができます。 ただし、これらのプロジェクトで Visual Studio 2017 機能を有効にするには、プロジェクトのプロパティを開き、ターゲットの fsharp.core を F# 4.1 に変更します。 .NET ワークロードの場合、Visual Studio インストーラーの **[F# 言語サポート]** オプションは既定では選択されないことにもご注意ください。ワークロードにこのオプションを選択するか、 **[開発作業]** の **[個別のコンポーネント]** から選択する方法で追加する必要があります。 |
| InstallShield<br/>MSI のセットアップ | Visual Studio 2010 で作成されたインストーラー プロジェクトは、[Visual Studio Installer Projects の拡張機能](https://marketplace.visualstudio.com/items?itemName=UnniRavindranathan-MSFT.MicrosoftVisualStudio2013InstallerProjects)を使って以降のバージョンで開くことができます。 「[WiX Toolset Visual Studio 2017 Extension](https://marketplace.visualstudio.com/items?itemName=RobMensching.WixToolsetVisualStudio2017Extension)」も参照してください。 InstallShield Limited Edition は、Visual Studio に付属しなくなりました。 Visual Studio 2017 で利用可能かどうかについては、[Flexera Software](https://info.flexerasoftware.com/IS-EVAL-InstallShield-Limited-Edition-Visual-Studio) にご確認ください。 |
| LightSwitch | LightSwitch は Visual Studio 2017 ではサポートされていません。 Visual Studio 2012 以前のバージョンで作成されたプロジェクトを Visual Studio 2013 または Visual Studio 2015 で開くとアップグレードされ、以後、Visual Studio 2013 または Visual Studio 2015 のみで開けるようになります。 |
| Microsoft Azure Tools for Visual Studio | これらの種類のプロジェクトを開くには、最初に [Azure SDK for .NET](https://azure.microsoft.com/downloads/)をインストールした後、プロジェクトを開きます。 必要に応じて、プロジェクトが更新されます。 |
| モデル ビュー コントローラー フレームワーク (ASP.NET MVC) | MVC バージョンと Visual Studio のサポート:<ul><li>Visual Studio 2010 SP1 は MVC 2 と MVC 3 をサポートしています。MVC 4 サポートは [ASP.NET 4 MVC 4 for Visual Studio 2010 SP1 をダウンロード](https://www.microsoft.com/download/details.aspx?id=30683)すると追加されます。</li><li>Visual Studio 2012 は MVC 3 と MVC 4 のみをサポートしています。</li><li>Visual Studio 2013 は MVC 4 と MVC 5 のみをサポートしています。</li><li>Visual Studio 2017 と Visual Studio 2015 では MVC 4 (既存のオブジェクトを開くことはできますが、新規作成はできません) と MVC 5 がサポートされています。</li></ul><br/>MVC バージョンをアップグレードする:<ul><li>MVC 2 から MVC 3 に自動的にアップグレードする方法については、「[ASP.NET MVC 3 Application Upgrader](https://archive.codeplex.com/?p=aspnet)」 (ASP.NET MVC 3 アプリケーション アップグレード プログラム) を参照してください。</li><li>MVC 2 から MVC 3 に手動でアップグレードする方法については、「 [Upgrading an ASP.NET MVC 2 Project to ASP.NET MVC 3 Tools Update (ASP.NET MVC 2 プロジェクトから ASP.NET MVC 3 Tools Update へのアップグレード)](https://archive.codeplex.com/?p=aspnet)」を参照してください。</li><li>MVC 3 から MVC 4 に手動でアップグレードする方法については、「 [Upgrading an ASP.NET MVC 3 Project to ASP.NET MVC 4 (ASP.NET MVC 3 プロジェクトから ASP.NET MVC 4 へのアップグレード)](/aspnet/whitepapers/mvc4-release-notes)」を参照してください。 .NET Framework 3.5 SP1 を対象とするプロジェクトの場合は、.NET Framework 4 を使用するようにプロジェクトの対象を変更する必要があります。</li><li>MVC 4 から MVC 5 に手動でアップグレードする方法については、「[How to Upgrade an ASP.NET MVC 4 and Web API Project to ASP.NET MVC 5 and Web API 2](https://www.asp.net/mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2) (ASP.NET MVC 4 と Web API プロジェクトを ASP.NET MVC 5 と Web API 2 にアップグレードする方法)」を参照してください。</li></ul> |
| モデリング | Visual Studio でプロジェクトを自動的に更新することを許可した場合は、Visual Studio 2015、Visual Studio 2013、または Visual Studio 2012 で開くことができます。<br/><br/>モデリング プロジェクトの形式は Visual Studio 2015 と Visual Studio 2017 の間で変わっていません。プロジェクトはいずれのバージョンでも開き、変更できます。 ただし、Visual Studio 2017 では動作に違いがあります。<ul><li>メニューとテンプレートで、モデリング プロジェクトの名称が "依存関係の検証" になりました。</li><li>UML 図は Visual Studio 2017 ではサポートされていません。 UML ファイルは以前と同様にソリューション エクスプローラーに一覧表示されますが、XML ファイルが開きます。 UML 図を表示、作成、編集するには、Visual Studio 2015 を使用してください。</li><li>Visual Studio 2017 では、モデリング プロジェクトが構築されるとき、アーキテクチャの依存関係検証がなくなりました。 代わりに、コード プロジェクトが構築されるときに検証が実行されます。 この変更がモデリング プロジェクトに影響を与えることはありませんが、検証されるコード プロジェクトを変更する必要があります。 Visual Studio 2017 では、コード プロジェクトを必要に応じて自動的に変更できます ([詳細](../modeling/validate-code-with-layer-diagrams.md?view=vs-2017&preserve-view=true#live-dependency-validation))。</li></ul> |
| MSI セットアップ (vdproj) | InstallShield プロジェクトをご覧ください。 |
| Office 2007 VSTO | Visual Studio 2017 への一方向のアップグレードが必要です。 |
| Office 2010 VSTO | .NET Framework 4 を対象とするプロジェクトの場合は、Visual Studio 2010 SP1 以降でこのプロジェクトを開くことができます。 他のすべてのプロジェクトは、一方向のアップグレードが必要です。 |
| Service Fabric (sfproj) | Service Fabric アプリケーション プロジェクトが ASP.NET Core サービス プロジェクトを参照していない限り、Service Fabric アプリケーション プロジェクトは Visual Studio 2015 または Visual Studio 2017 のいずれかで開くことができます。 Visual Studio 2017 で開かれている Visual Studio 2015 からの Service Fabric プロジェクトは、xproj 形式から csproj への一方向の移行が行われます。 この表で前述した「.NET Core プロジェクト (xproj)」を参照してください。 |
| SharePoint 2010 | SharePoint ソリューション プロジェクトを Visual Studio 2017 で開くと、SharePoint 2013 または SharePoint 2016 にアップグレードされます。 アップグレードのためには、".NET デスクトップ開発" ワークロードを Visual Studio 2017 にインストールする必要があります。<br/><br/>SharePoint プロジェクトをアップグレードする方法の詳細については、[SharePoint のアップグレードおよび更新](/sharepoint/upgrade-and-update/upgrade-and-update)に関するページを参照してください。|
| SharePoint 2016 | Office Developer Tools Preview 2 で作成された SharePoint アドイン プロジェクトを Visual Studio 2017 で開くことはできません。 この制限を回避するには、csproj vbproj ファイルで、`MinimumVisualStudioVersion` を 12.0 に、`MinimumOfficeToolsVersion` を 12.2 に更新する必要があります。 |
| Silverlight | Silverlight プロジェクトは Visual Studio 2017 ではサポートされていません。 Silverlight アプリケーションを維持するには、引き続き Visual Studio 2015 を使用してください。 |
| SQL Server Reporting Services および SQL Server Analysis Services (SSRS、SSDT、SSAS、MSAS) | これらのプロジェクト タイプのサポートは、Visual Studio ギャラリーの次の 2 つの拡張機能を通じて提供されます。[Microsoft Analysis Services Modeling Projects](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftAnalysisServicesModelingProjects) と [Microsoft Reporting Services Projects](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftReportProjectsforVisualStudio)。 Visual Studio 2017 のデータの保存と処理のワークロードには SSDT のサポートも含まれます。 詳細については、「[Visual Studio の SQL Server Data Tools (SSDT) をダウンロードし、インストールする](/sql/ssdt/download-sql-server-data-tools-ssdt)」を参照してください。|
| SQL Server Integration Services (SSIS) | Visual Studio 2017 のサポートは、SQL Server Data Tools (SSDT) から使用できます。 詳細については、「[Visual Studio の SQL Server Data Tools (SSDT) をダウンロードし、インストールする](/sql/ssdt/download-sql-server-data-tools-ssdt)」ページと「[SQL Server Integration Services (SSIS)](https://techcommunity.microsoft.com/t5/SQL-Server-Integration-Services/bg-p/SSIS)」チーム ブログを参照してください。 |
| Visual C++ | Visual Studio 2017 を使用して、Visual Studio 2010 以降の Visual Studio で作成されたプロジェクトを操作できます。 プロジェクトを初めて開いたときに、最新のコンパイラとツールセットにアップグレードするか、元のプロジェクトを引き続き使用するかを選択できます。 元のプロジェクトを引き続き使用することを選択した場合、Visual Studio 2017 はプロジェクト ファイルを変更せず、以前の Visual Studio のインストールのツールセットを使用してプロジェクトをビルドします。 元のオプションを維持すると、必要に応じて、Visual Studio の元のバージョンでプロジェクトを開くことができます。 詳細については、「[Visual Studio でネイティブ マルチ ターゲットを利用し、古いプロジェクトを作成する](/cpp/porting/use-native-multi-targeting)」を参照してください。 |
| Visual Studio 拡張性/VSIX | MinimumVersion 14.0 以前のプロジェクトは、MinimumVersion 15.0 を宣言するように更新されます。この宣言により、前のバージョンの Visual Studio でプロジェクトを開けなくなります。 前のバージョンでプロジェクトを開くには、MinimumVersion を `$(VisualStudioVersion)` に設定します。 「[方法: 機能拡張プロジェクトの Visual Studio 2017 への移行](../extensibility/how-to-migrate-extensibility-projects-to-visual-studio-2017.md)に関するページも参照してください。 |
| Visual Studio Lab Management | Microsoft Test Manager または Visual Studio 2010 SP1 以降を利用し、これらのバージョンで差制された環境を開くことができます。 ただし、Visual Studio 2010 SP1 の場合、環境を作成するには、使用している Microsoft Test Manager のバージョンが Team Foundation Server のバージョンと一致する必要があります。 |
| Visual Studio Tools for Apache Cordova | プロジェクトは Visual Studio 2017 で開くことができますが、下位互換性はありません。 Visual Studio 2015 からプロジェクトを開くと、プロジェクトを変更するように求められます。 この変更により、`taco.json` ファイルの代わりにツールセットを利用し、Cordova ライブラリのバージョン、そのプラットフォームとプラグイン、そのノード/npm 依存関係を管理するようにプロジェクトがアップグレードされます。 詳細については、[移行ガイド](/previous-versions/visualstudio/cross-platform/tools-for-cordova/first-steps/migrate-from-visual-studio-2015)を参照してください。 |
| Web 配置 (wdproj) | 発行プロファイルのサポートが追加されたことで、Visual Studio 2012 では Web 配置プロジェクトのサポートが削除されました。 Visual Studio 2017 には等価なものがないため、そのようなプロジェクトの自動移行パスはありません。 そこで、[StackOverflow](https://stackoverflow.com/a/12061065/1203388) に説明されているように、テキスト エディターで wdproj ファイルを開き、pubxml (発行プロファイル) ファイルに任意のカスタマイズをコピーおよび貼り付けます。 |
| Windows Communication Foundation、Windows Workflow Foundation | このプロジェクトは、Visual Studio 2017、Visual Studio 2015、Visual Studio 2013、Visual Studio 2012 で開くことができます。 |
| Windows Presentation Foundation | このプロジェクトは、Visual Studio 2017、Visual Studio 2013、Visual Studio 2012、Visual Studio 2010 SP1 で開くことができます。 |
| Windows ストア/フォン アプリ | Visual Studio 2017 では、Windows Store 8.1 と 8.0 または Windows Phone 8.1 と 8.0 のプロジェクトはサポートされていません。 これらのアプリを維持するには、引き続き Visual Studio 2015 を使用してください。 Windows Phone 7.x プロジェクトを維持するには、Visual Studio 2012 を使用してください。 |

## <a name="how-visual-studio-decides-when-to-migrate-a-project"></a>Visual Studio がプロジェクトを移行するタイミングを決定する方法

Visual Studio の各新規バージョンでは、一般に、バージョンが異なっても同じプロジェクトを開き、変更し、ビルドできるように、以前のバージョンとの互換性が維持されます。 ただし、時間の経過と共に、一部のプロジェクトの種類のサポート終了など、避けられない変更が発生します (Visual Studio 2017 でサポートされているプロジェクトの種類については「[Visual Studio 2017 の対象プラットフォームと互換性](/visualstudio/productinfo/vs2017-compatibility-vs)」をご覧ください)。このような場合、新しいバージョンの Visual Studio はプロジェクトを読み込まず、移行パスを提供しません。そのようなプロジェクトは、それをサポートしている以前のバージョンの Visual Studio で管理する必要があります。

つまり、新しいバージョンの Visual Studio ではプロジェクトを開くことはできますが、以前のバージョンとの互換性がなくなる可能性がある方法でプロジェクトを更新または移行する必要があります。 Visual Studio は、複数の条件を使って、このような移行が必要かどうかを判断します。

- Visual Studio 2013 RTM まで遡る、プラットフォームのターゲット バージョンとの互換性。

- 以前のバージョンの Visual Studio との、デザイン時資産の互換性 (つまり、Visual Studio 2017 の異なるチャネル、Visual Studio 2015 RTM & Update 3、Visual Studio 2013 RTM & Update 5、Visual Studio 2012 Update 4、Visual Studio 2010 SP 1)。Visual Studio 2017 は、以前のバージョンでプロジェクトをまだ開くことができるように、非推奨のデザイン時資産を、破壊することなく正常に失敗させます。

- 新しいデザイン時資産により、Visual Studio 2013 RTM & Update 5 までの以前のバージョンとの互換性がなくなるかどうか。

対象のプロジェクトの種類のエンジニアリング所有者は、これらの条件を調べて、サポート、互換性、移行に関して問題があるときは問い合わせます。 ここでも、Visual Studio は、可能であれば Visual Studio のバージョン間の透過的な互換性を維持します。つまり、Visual Studio のあるバージョンで作成および変更したプロジェクトは、他のバージョンでもそのままで動作します。

ただし、この記事で説明されている一部のプロジェクトの種類のように、このような互換性が不可能な場合は、Visual Studio はアップグレード ウィザードを開いて必要な一方向の変更を行います。

このような一方向の変更には、プロジェクト ファイルでの `ToolsVersion` プロパティの変更が含まれます。これは、最終的に必要な実行可能で配置可能なアーティファクトにプロジェクトのソース コードを変換できる MSBuild の正確なバージョンを示します。 つまり、プロジェクトと以前のバージョンの Visual Studio との互換性を損なうものは、*Visual Studio* のバージョンではなく、`ToolsVersion` によって決定される *MSBuild* のバージョンです。 お使いの Visual Studio のバージョンに、プロジェクトでの `ToolsVersion` と一致する MSBuild ツールチェーンが含まれている限り、Visual Studio をそのツールチェーンを呼び出してプロジェクトをビルドできます。

以前のバージョンで作成されたプロジェクトとの最大限の互換性を維持するため、Visual Studio 2017 には、`ToolsVersion` 15、14、12、4 をサポートするために必要な MSBuild ツールチェーンが含まれています。 これらの `ToolsVersion` 値のいずれかを使うプロジェクトでは、ビルドが成功するはずです (やはり、「[Visual Studio 2017 の対象プラットフォームと互換性](/visualstudio/productinfo/vs2017-compatibility-vs)」で説明されているように、Visual Studio 2017 がプロジェクトの種類をサポートするかどうかに依存します)。

このコンテキストでの必然的な疑問は、新しい `ToolsVersion` 値にプロジェクトを手動で更新または移行する必要があるかどうかということです。 そのような変更は不要であり、行うと、修正するにはプロジェクトの再ビルドが必要な多くのエラーと警告が発生する可能性があります。 さらに、将来 Visual Studio が特定の `ToolsVersion` をサポートしなくなった場合、プロジェクトを開くと、`ToolsVersion` の値を変更する必要があるため、プロジェクト移行プロセスが開始されます。 そのような場合、その特定のプロジェクトの種類のサブシステムは、変更が必要なものを正確に知っており、この記事で前述したように自動的にこれらの変更を行うことができます。

## <a name="next-steps"></a>次の手順

詳しくは、次の記事をご覧ください。

- [ToolsVersion ガイダンス](../msbuild/msbuild-toolset-toolsversion.md)
- [フレームワーク対象設定機能ガイダンス](../ide/visual-studio-multi-targeting-overview.md)

## <a name="see-also"></a>関連項目

- [Visual Studio 2019 のプロジェクトの移行とアップグレードのリファレンス](port-migrate-and-upgrade-visual-studio-projects.md?view=vs-2019&preserve-view=true)
- [Visual Studio の製品ライフサイクルとサービス](/visualstudio/releases/2019/servicing/)

::: moniker-end

::: moniker range="vs-2019"

新しいバージョンの Visual Studio はいずれも、ほとんどの種類のプロジェクト、ファイル、その他の資産に対応しています。 新しい機能に依存しない場合は、[これまでと同様に](../ide/solutions-and-projects-in-visual-studio.md)これらを操作できます。

Microsoft では、以前のバージョン (Visual Studio 2017、Visual Studio 2015、Visual Studio 2013、Visual Studio 2012 など) との下位互換性を維持しようとしています。 しかし、一部の種類のプロジェクトに対するサポートは、時間の経過と共に変化します。 新しいバージョンの Visual Studio では、特定のプロジェクトが一切サポートされなくなったり、下位互換性がなくったためにプロジェクトの更新が必要になったりすることがあります。

> [!NOTE]
> 移行に関する問題の現在の状況については、[Visual Studio 開発者コミュニティ](https://aka.ms/feedback/suggest?space=8)を参照してください。 また、Visual Studio のそれぞれのバージョンに固有の機能について詳しくは、[リリース ノート](/visualstudio/releases/2019/release-notes/)をご覧ください。

> [!IMPORTANT]
> 一部のプロジェクトの種類には、特定のワークロードが必要です。 ワークロードがインストールされていない場合、Visual Studio は不明な、または互換性のないプロジェクトの種類を報告します。 その場合、[Visual Studio インストーラーでインストール オプション](../install/modify-visual-studio.md)を確認して、やり直してください。 Visual Studio 2019 のプロジェクト サポートについて詳しくは、[対象プラットフォームと互換性](/visualstudio/releases/2019/compatibility)に関する記事をご覧ください。

## <a name="project-types"></a>プロジェクトの種類

次の一覧は、Visual Studio 2019 より前のバージョンで作成されたプロジェクトに対する Visual Studio 2019 でのサポートをまとめたものです。

表示されるはずのプロジェクトまたはファイルの種類が見つからない場合、[この記事の Visual Studio 2017 バージョン](?view=vs-2017&preserve-view=true)を調べてください。 このページの下部にある **[次のフィードバックを送信]**  >  **[このページ]** ボタンを使用して、プロジェクトの詳細を提供することもできます。 (匿名の "このページは役に立ちましたか。" コントロールを使用した場合、 フィードバックに応対できません。)

| プロジェクトの種類 | サポート |
| --- | --- |
| .NET Core プロジェクト (xproj) | Visual Studio 2015 で作成したプロジェクトでは、.xproj プロジェクト ファイルが含まれるプレビュー ツールが使用されていました。<br/><br/>Visual Studio 2017:xproj 形式は、csproj 形式への移行以外ではサポートされていません。 xproj ファイルを開くと、SDK スタイルの csproj 形式にファイルを移行するように求められます。 (xproj ファイルのバックアップが作成されます。)SDK スタイルの csproj プロジェクトは、Visual Studio 2015 以前ではサポートされません。 <br/><br/>Visual Studio 2019:バージョン 16.3 以降では、xproj プロジェクトの読み込みまたは移行を実行できません。 詳細については、「[.NET Core プロジェクトから .csproj 形式への移行](/dotnet/core/migration/#visual-studio)」をご覧ください。|
| ASP.NET Core Web アプリと Application Insights を使用した ASP.NET Core Web アプリが有効になっている | Visual Studio のユーザーごとのリソース情報がユーザー インスタンス別にレジストリに保存されます。 この情報は、プロジェクトを開いていない状態で Azure Application Insights データを検索するときに利用されます。 Visual Studio 2015 では、Visual Studio 2017 および Visual Studio 2019 とは異なるレジストリの場所が使用され、競合しません。<br/><br/>ユーザーが ASP.NET Web アプリケーション、ASP.NET Core Web アプリ、または ASP.NET Core Web アプリケーションを作成すると、リソースは .suo ファイルに保存されます。 ユーザーは Visual Studio 2015、Visual Studio 2017、または Visual Studio 2019 でプロジェクトを開くことができます。両方のバージョンで使用されているプロジェクトとソリューションが Visual Studio でサポートされている限り、それぞれでリソース情報が使用されます。 ユーザーは製品ごとに 1 回認証する必要があります。 たとえば、Visual Studio 2017 で作成されたプロジェクトを Visual Studio 2019 で開く場合、Visual Studio 2019 で認証が要求されます。 |
| C#/Visual Basic Webform または Windows フォーム | プロジェクトは、Visual Studio 2019、Visual Studio 2017、Visual Studio 2015 で開くことができます。 |
| コード化された UI テスト | UI 駆動型機能テストの自動化のためにコード化された UI テストは、Visual Studio 2019 では非推奨になりました。 <br/><br/>Visual Studio 2019 は、コード化された UI テストの最後のリリースとなります。 Web アプリのテストには Selenium を使用し、デスクトップと UWP アプリのテストには Appium と WinAppDriver を一緒に使用することをお勧めします。 |
| データベース単体テスト プロジェクト (csproj、.vbproj) | 古いデータ単体テスト プロジェクトは Visual Studio 2019 で読み込まれますが、依存関係は GAC に保存されているものが使用されます。 単体テスト プロジェクトをアップグレードし、最新の依存関係を使用するには、ソリューション エクスプローラーでプロジェクトを右クリックし、 **[SQL Server 単体テスト プロジェクトに変換する]** を選択します。 |
| F# | Visual Studio 2019 では、Visual Studio 2013、Visual Studio 2015、Visual Studio 2017 で作成されたプロジェクトを開くことができます。 新しいプロジェクトの以前の Visual Studio テンプレートとの主な違いは、FSharp.Core のバージョンが常に NuGet パッケージになったことです。 F# は任意の .NET ワークロードにより既定でインストールされます。|
| InstallShield<br/>MSI のセットアップ | Visual Studio 2010 で作成されたインストーラー プロジェクトは、[Visual Studio Installer Projects の拡張機能](https://marketplace.visualstudio.com/items?itemName=UnniRavindranathan-MSFT.MicrosoftVisualStudio2013InstallerProjects)を使って以降のバージョンで開くことができます。 「[WiX Toolset Visual Studio 2017 Extension](https://marketplace.visualstudio.com/items?itemName=RobMensching.WixToolsetVisualStudio2017Extension)」も参照してください。 InstallShield Limited Edition は、Visual Studio に付属しなくなりました。 Visual Studio 2019 で利用可能かどうかについては、[Flexera Software](https://info.flexerasoftware.com/IS-EVAL-InstallShield-Limited-Edition-Visual-Studio) にご確認ください。 |
| LightSwitch | LightSwitch は Visual Studio 2019 または Visual Studio 2017 ではサポートされていません。 Visual Studio 2012 以前のバージョンで作成されたプロジェクトを Visual Studio 2013 または Visual Studio 2015 で開くとアップグレードされ、以後、Visual Studio 2013 または Visual Studio 2015 のみで開けるようになります。 |
| ロード テスト | Visual Studio 2019 では、Web パフォーマンスとロード テストの機能は非推奨となっています。 <br/><br/>Visual Studio 2019 は、ロード テストの最後のリリースとなります。 Apache JMeter、Akamai CloudTest、Blazemeter など、代替のロード テスト ツールを使用してください。  |
| Microsoft Azure Tools for Visual Studio | これらの種類のプロジェクトを開くには、最初に [Azure SDK for .NET](https://azure.microsoft.com/downloads/)をインストールした後、プロジェクトを開きます。 必要に応じて、プロジェクトが更新されます。 |
| Microsoft Test Manager | Visual Studio 2019 以降、Microsoft Test Manager と Feedback Client は Visual Studio に付属しません。 <br/><br/>手動テストまたは探索的テストの必要がある場合は、Azure Test Plans (Azure DevOps の一部) をご利用ください。 詳細については、Azure DevOps ドキュメントの「[Guidance on Microsoft Test Manager usage (Microsoft Test Manager の使用に関するガイダンス)](/azure/devops/test/mtm/guidance-mtm-usage?view=azure-devops&preserve-view=true)」ページをご覧ください。 |
| モデル ビュー コントローラー フレームワーク (ASP.NET MVC) | MVC バージョンと Visual Studio のサポート:<ul><li>Visual Studio 2010 SP1 は MVC 2 と MVC 3 をサポートしています。MVC 4 サポートは [ASP.NET 4 MVC 4 for Visual Studio 2010 SP1 をダウンロード](https://www.microsoft.com/download/details.aspx?id=30683)すると追加されます。</li><li>Visual Studio 2012 は MVC 3 と MVC 4 のみをサポートしています。</li><li>Visual Studio 2013 は MVC 4 と MVC 5 のみをサポートしています。</li><li>Visual Studio 2019、Visual Studio 2017、Visual Studio 2015 では MVC 4 (既存のオブジェクトを開くことはできますが、新規作成はできません) と MVC 5 がサポートされています。</li></ul><br/>MVC バージョンをアップグレードする:<ul><li>MVC 2 から MVC 3 に自動的にアップグレードする方法については、「[ASP.NET MVC 3 Application Upgrader](https://archive.codeplex.com/?p=aspnet)」 (ASP.NET MVC 3 アプリケーション アップグレード プログラム) を参照してください。</li><li>MVC 2 から MVC 3 に手動でアップグレードする方法については、「 [Upgrading an ASP.NET MVC 2 Project to ASP.NET MVC 3 Tools Update (ASP.NET MVC 2 プロジェクトから ASP.NET MVC 3 Tools Update へのアップグレード)](https://archive.codeplex.com/?p=aspnet)」を参照してください。</li><li>MVC 3 から MVC 4 に手動でアップグレードする方法については、「 [Upgrading an ASP.NET MVC 3 Project to ASP.NET MVC 4 (ASP.NET MVC 3 プロジェクトから ASP.NET MVC 4 へのアップグレード)](/aspnet/whitepapers/mvc4-release-notes)」を参照してください。 .NET Framework 3.5 SP1 を対象とするプロジェクトの場合は、.NET Framework 4 を使用するようにプロジェクトの対象を変更する必要があります。</li><li>MVC 4 から MVC 5 に手動でアップグレードする方法については、「[How to Upgrade an ASP.NET MVC 4 and Web API Project to ASP.NET MVC 5 and Web API 2](https://www.asp.net/mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2) (ASP.NET MVC 4 と Web API プロジェクトを ASP.NET MVC 5 と Web API 2 にアップグレードする方法)」を参照してください。</li></ul> |
| モデリング | Visual Studio でプロジェクトを自動的に更新することを許可した場合は、Visual Studio 2015、Visual Studio 2013、または Visual Studio 2012 で開くことができます。<br/><br/>モデリング プロジェクトの形式は Visual Studio 2015 以来変わっていません。プロジェクトはこれらのバージョンで開いて変更することができます。 ただし、Visual Studio 2017 と Visual Studio 2019 では動作に違いがあります。<ul><li>メニューとテンプレートで、モデリング プロジェクトの名称が "依存関係の検証" になりました。</li><li>UML 図は Visual Studio 2017 と Visual Studio 2019 ではサポートされていません。 UML ファイルは以前と同様にソリューション エクスプローラーに一覧表示されますが、XML ファイルが開きます。 UML 図を表示、作成、編集するには、Visual Studio 2015 を使用してください。</li><li>Visual Studio 2019 では、モデリング プロジェクトが構築されるとき、アーキテクチャの依存関係検証がなくなりました。 代わりに、コード プロジェクトが構築されるときに検証が実行されます。 この変更がモデリング プロジェクトに影響を与えることはありませんが、検証されるコード プロジェクトを変更する必要があります。 Visual Studio 2019 では、コード プロジェクトを必要に応じて自動的に変更できます。</li></ul> |
| MSI セットアップ (vdproj) | InstallShield プロジェクトをご覧ください。 |
| Office 2007 VSTO | Visual Studio 2019 への一方向のアップグレードが必要です。 |
| Office 2010 VSTO | .NET Framework 4 を対象とするプロジェクトの場合は、Visual Studio 2010 SP1 以降でこのプロジェクトを開くことができます。 他のすべてのプロジェクトは、一方向のアップグレードが必要です。 |
| ポータブル クラス ライブラリ (PCL) | ポータブル クラス ライブラリ (PCL) はサポートされなくなりました。 Visual Studio 2019 では引き続き PCL を開いたりビルドできますが、新しい PCL プロジェクトを作成することはできません。 PCL プロジェクトのコードを .NET Standard プロジェクトに移行することをお勧めします。<br/><br/>PCL のサポートは既定では含まれなくなりますが、Visual Studio の "個々のコンポーネント" タブでは使用できます。 |
| Python ワークロード | Python Windows IoT Core アプリのサポートは、Visual Studio 2019 で削除されました。 Visual Studio 2019 には等価なものがないため、そのようなプロジェクトの自動移行パスはありません。<br/><br/>Visual Studio 2017 を引き続き使用することができます。 |
| R Tools for Visual Studio | R Tools for Visual Studio は、Visual Studio 2019 でデータ サイエンス ワークロードから削除されました。<br/><br/>Visual Studio 2017 または RStudio などの代替手段を引き続き使用することができます。 |
| Service Fabric (sfproj) | Service Fabric アプリケーション プロジェクトが ASP.NET Core サービス プロジェクトを参照していない限り、Service Fabric アプリケーション プロジェクトは Visual Studio 2015、Visual Studio 2017、Visual Studio 2019 のいずれかで開くことができます。 Visual Studio 2017 または Visual Studio 2019 で開かれている Visual Studio 2015 からの Service Fabric プロジェクトは、xproj 形式から csproj への一方向の移行が行われます。 この表で前述した「.NET Core プロジェクト (xproj)」を参照してください。 |
| SharePoint 2010 | SharePoint ソリューション プロジェクトを Visual Studio 2019 で開くと、SharePoint 2013 または SharePoint 2016 にアップグレードされます。 アップグレードのためには、".NET デスクトップ開発" ワークロードを Visual Studio 2019 にインストールする必要があります。<br/><br/>SharePoint プロジェクトをアップグレードする方法の詳細については、[SharePoint のアップグレードおよび更新](/sharepoint/upgrade-and-update/upgrade-and-update)に関するページを参照してください。|
| SharePoint 2016 | Office Developer Tools Preview 2 で作成された SharePoint アドイン プロジェクトを Visual Studio 2019 で開くことはできません。 この制限を回避するには、csproj vbproj ファイルで、`MinimumVisualStudioVersion` を 12.0 に、`MinimumOfficeToolsVersion` を 12.2 に更新する必要があります。 |
| Silverlight | Silverlight プロジェクトは Visual Studio 2019 ではサポートされていません。 Silverlight アプリケーションを維持するには、引き続き Visual Studio 2015 を使用してください。 |
| SQL - Redgate | Redgate の SQL Change Automation Core (旧称、ReadyRoll Core)、SQL Prompt Core、および SQL Search は、Visual Studio インストーラーに付属されななくなりました。<br/><br/>これらの機能には、Visual Studio 2017 を引き続き使用することができます。 Visual Studio 2019 では、Redgate の SQL Toolbelt で入手可能な有料の SQL Change Automation および SQL Prompt 製品にアップグレードすることができます。|
| SQL Server Reporting Services および SQL Server Analysis Services (SSRS、SSDT、SSAS、MSAS) | これらのプロジェクト タイプのサポートは、Visual Studio ギャラリーの次の 2 つの拡張機能を通じて提供されます。[Microsoft Analysis Services Modeling Projects](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftAnalysisServicesModelingProjects) と [Microsoft Reporting Services Projects](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftReportProjectsforVisualStudio)。 Visual Studio 2019 のデータの保存と処理のワークロードには SSDT のサポートも含まれます。 詳細については、「[Visual Studio の SQL Server Data Tools (SSDT) をダウンロードし、インストールする](/sql/ssdt/download-sql-server-data-tools-ssdt)」を参照してください。 |
| SQL Server Integration Services (SSIS) | Visual Studio 2019 のサポートを利用できます。 詳細については、「[Visual Studio の SQL Server Data Tools (SSDT) をダウンロードし、インストールする](/sql/ssdt/download-sql-server-data-tools-ssdt)」ページ、「[SQL Server Integration Services (SSIS)](https://techcommunity.microsoft.com/t5/SQL-Server-Integration-Services/bg-p/SSIS)」チーム ブログ、および Marketplace の「[SQL Server Integration Services Projects](https://marketplace.visualstudio.com/items?itemName=SSIS.SqlServerIntegrationServicesProjects&ssr=false#overview)」ページを参照してください。 |
| テスト ウィンドウ拡張機能 | Visual Studio 2019 では、前にパブリックとしてマークされていたがドキュメントに正式に記載されたことがないいくつかのテスト ウィンドウ API が削除されました。 広く利用されていた API には、拡張機能の管理者に対して早期に警告を発するために、Visual Studio 2017 で非推奨のマークが付いていました。 Microsoft の知る限りでは、これらの API に対して依存関係を築いている拡張機能はわずかです。 詳細と更新プログラムにいては、[テスト関連の非推奨の API の完全一覧](https://github.com/Microsoft/vstest/issues/1830)に関するページを参照してください。 これが自分のシナリオに影響する場合、[開発者コミュニティ](https://aka.ms/feedback/suggest?space=8)でお知らせください。 |
| Visual C++ | Visual Studio 2019 を使用して、Visual Studio 2010 以降の Visual Studio で作成されたプロジェクトを操作できます。 プロジェクトを初めて開いたときに、最新のコンパイラとツールセットにアップグレードするか、元のプロジェクトを引き続き使用するかを選択できます。 元のプロジェクトを引き続き使用することを選択した場合、Visual Studio 2019 はプロジェクト ファイルを変更せず、以前の Visual Studio のインストールのツールセットを使用してプロジェクトをビルドします。 元のオプションを維持すると、必要に応じて、Visual Studio の元のバージョンでプロジェクトを開くことができます。 詳細については、「[Visual Studio でネイティブ マルチ ターゲットを利用し、古いプロジェクトを作成する](/cpp/porting/use-native-multi-targeting)」を参照してください。 |
| Visual Studio 拡張性/VSIX | MinimumVersion 14.0 以前のプロジェクトは、MinimumVersion 15.0 を宣言するように更新されます。この宣言により、前のバージョンの Visual Studio でプロジェクトを開けなくなります。 前のバージョンでプロジェクトを開くには、MinimumVersion を `$(VisualStudioVersion)` に設定します。 「[方法: 機能拡張プロジェクトの Visual Studio 2017 への移行](../extensibility/how-to-migrate-extensibility-projects-to-visual-studio-2017.md)に関するページも参照してください。 |
| Visual Studio Lab Management | Microsoft Test Manager または Visual Studio 2010 SP1 以降を利用し、これらのバージョンで差制された環境を開くことができます。 ただし、Visual Studio 2010 SP1 の場合、環境を作成するには、使用している Microsoft Test Manager のバージョンが Team Foundation Server のバージョンと一致する必要があります。 |
| Visual Studio Tools for Apache Cordova | Apache Cordova のサポートは、Visual Studio 2019 で削除されました。 Visual Studio 2019 には等価なものがないため、そのようなプロジェクトの自動移行パスはありません。<br/><br/>Cordova Tools for Visual Studio Code 拡張機能 (Cordova の最新バージョンのサポートを提供) を使用することも、Visual Studio 2017 を引き続き使用することもできます。 |
| Web 配置 (wdproj) | 発行プロファイルのサポートが追加されたことで、Visual Studio 2012 では Web 配置プロジェクトのサポートが削除されました。 Visual Studio 2019 には等価なものがないため、そのようなプロジェクトの自動移行パスはありません。 そこで、[StackOverflow](https://stackoverflow.com/a/12061065/1203388) に説明されているように、テキスト エディターで wdproj ファイルを開き、pubxml (発行プロファイル) ファイルに任意のカスタマイズをコピーおよび貼り付けます。 |
| Windows Communication Foundation、Windows Workflow Foundation | このプロジェクトは、Visual Studio 2019、Visual Studio 2017、Visual Studio 2015、Visual Studio 2013、Visual Studio 2012 で開くことができます。 |
| Windows Presentation Foundation | このプロジェクトは、Visual Studio 2019、Visual Studio 2017、Visual Studio 2013、Visual Studio 2012、Visual Studio 2010 SP1 で開くことができます。 |
| Windows Phone アプリ | Windows Phone のプロジェクトは、Visual Studio 2019 ではサポートされていません。 <br/><br/>Windows Phone 8.x アプリを維持するには、Visual Studio 2015 を使用してください。 Windows Phone 7.x プロジェクトを維持するには、Visual Studio 2012 を使用してください。 |
| Windows ストア アプリ | JavaScript ユニバーサル Windows プロジェクトは、Visual Studio 2019 ではサポートされていません。 これらのプロジェクトを維持するには、Visual Studio 2017 を使用してください。 <br/><br/>Windows 10 Fall Creators Update (ビルド 16299) より前の Windows 10 SDK は、Visual Studio 2019 インストーラーから削除されました。 古い SDK を手動でダウンロードすることも、新しい SDK を使用するようにプロジェクトを再ターゲットすることもできます。<br/><br/>project.json を使用しているユニバーサル Windows プロジェクトはサポートされていません。 パッケージ参照を使用するようにこれらのプロジェクトをアップグレードすることをお勧めします。 または、project.json ファイルで Microsoft.NET.Test.Sdk バージョン 16.0.0.0 への参照を追加します。<br/><br/>Windows Phone 8.1 および 8.0 のプロジェクトは、Visual Studio 2019 ではサポートされていません。 これらのアプリを維持するには、引き続き Visual Studio 2015 を使用してください。 |
| Xamarin | Visual Studio および Visual Studio for Mac の Xamarin Live Player 拡張機能は削除されました。 これにより、ペアリングの画面とすべての統合が削除されます。 代わりに、Xamarin.Forms Previewer でビルドを使用してください。<br/><br/>Visual Studio Emulator for Android は、Visual Studio インストーラーから削除されました。 代わりに、Google Android エミュレーターで新しい HYPER-V サポートを使用してください。 |

## <a name="migrate-a-project"></a>プロジェクトの移行

Microsoft では、以前のバージョンとの互換性を維持しようと試みていますが、以前のバージョンと互換性のない変更が生じる可能性があります。 (Visual Studio 2019 でサポートされているプロジェクトの種類については、[ターゲット プラットフォームと互換性](/visualstudio/releases/2019/compatibility)に関するページを参照してください)。これが発生した場合、新しいバージョンの Visual Studio ではプロジェクトが読み込まれず、移行パスも提供されません。 そのプロジェクトを、以前のバージョンの Visual Studio で維持することが必要になる場合があります。

新しいバージョンの Visual Studio でプロジェクトを開ける場合があります。ただし、そこでは、以前のバージョンとの互換性がなくなる可能性がある方法で、プロジェクトを更新または移行する必要があります。 Visual Studio は、複数の条件を使って、このような移行が必要かどうかを判断します。

- Visual Studio 2013 RTM まで遡る、プラットフォームのターゲット バージョンとの互換性。

- 以前のバージョンの Visual Studio との、デザイン時資産の互換性 (つまり、さまざまなチャネルの Visual Studio 2019、Visual Studio 2017、Visual Studio 2015 RTM & Update 3、Visual Studio 2013 RTM & Update 5、Visual Studio 2012 Update 4、Visual Studio 2010 SP 1)。Visual Studio 2019 は、以前のバージョンでプロジェクトをまだ開くことができるように、非推奨のデザイン時資産を、破壊することなく正常に失敗させます。

- 新しいデザイン時資産により、Visual Studio 2013 RTM & Update 5 までの以前のバージョンとの互換性がなくなるかどうか。

そのプロジェクトの種類を所有しているエンジニアリング チームは、これらの条件を確認し、サポート、互換性、移行に関して問題があるときは問い合わせます。 ここでも、Visual Studio のバージョン間の互換性を維持して、Visual Studio のあるバージョンで作成および変更したプロジェクトが、他のバージョンでもそのままで動作するようにすることが試みられます。

場合によっては、互換性を実現できないことがあります。 その場合、Visual Studio によって、必要な一方向の変更を加えるためのアップグレード ウィザードが開かれます。 これらの一方向の変更には、プロジェクト ファイルの `ToolsVersion` プロパティの変更が含まれる場合があります。このプロパティにより、プロジェクトのソース コードを目的の実行可能で配置可能な成果物に変換できる、MSBuild の正確なバージョンが示されます。

プロジェクトと以前のバージョンの Visual Studio との互換性を損なうものは、*Visual Studio* のバージョンではなく、`ToolsVersion` によって決定される *MSBuild* のバージョンです。 お使いの Visual Studio のバージョンに、プロジェクトの `ToolsVersion` と一致する MSBuild ツールチェーンが含まれている場合、Visual Studio ではそのツールチェーンを呼び出してプロジェクトをビルドすることができます。

以前のバージョンで作成したプロジェクトとの互換性を維持するため、Visual Studio 2019 には、`ToolsVersion` 15、14、12、4 をサポートするために必要な MSBuild ツールチェーンが含まれています。 これらの `ToolsVersion` 値のいずれかを使うプロジェクトでは、ビルドが成功するはずです (やはり、[対象プラットフォームと互換性](/visualstudio/releases/2019/compatibility)に関する記事で説明されているように、Visual Studio 2019 がそのプロジェクトの種類をサポートするかどうかに依存します)。

新しい `ToolsVersion` 値にプロジェクトを手動で更新または移行しようとお考えになるかもしれません。 そのような変更は不要です。実行した場合、プロジェクトを再ビルドするために修正しなければならない多くのエラーと警告が発生する可能性があります。 また、将来特定の `ToolsVersion` が Visual Studio でサポートされなくなった場合、そのプロジェクトを開くとプロジェクトの移行プロセスがトリガーされます。その `ToolsVersion` の値を変更する必要があるためです。

## <a name="next-steps"></a>次の手順

詳しくは、次の記事をご覧ください。

- [ToolsVersion ガイダンス](../msbuild/msbuild-toolset-toolsversion.md)
- [フレームワーク対象設定機能ガイダンス](../ide/visual-studio-multi-targeting-overview.md)

## <a name="see-also"></a>関連項目

- [Visual Studio 2017 のプロジェクトの移行とアップグレードのリファレンス](?view=vs-2017&preserve-view=true)
- [Visual Studio の製品ライフサイクルとサービス](/visualstudio/releases/2019/servicing/)

::: moniker-end

::: moniker range="vs-2022"

新しいバージョンの Visual Studio はいずれも、ほとんどの種類のプロジェクト、ファイル、その他の資産に対応しています。 新しい機能に依存しない場合は、[これまでと同様に](../ide/solutions-and-projects-in-visual-studio.md)これらを操作できます。

Microsoft では、以前のバージョン (Visual Studio 2019、Visual Studio 2017、Visual Studio 2015、Visual Studio 2013、Visual Studio 2012 など) との下位互換性を維持しようとしています。 しかし、一部の種類のプロジェクトに対するサポートは、時間の経過と共に変化します。 新しいバージョンの Visual Studio では、特定のプロジェクトが一切サポートされなくなったり、下位互換性がなくったためにプロジェクトの更新が必要になったりすることがあります。

> [!NOTE]
> 移行に関する問題の現在の状況については、[Visual Studio 開発者コミュニティ](https://aka.ms/feedback/suggest?space=8)を参照してください。 また、Visual Studio のそれぞれのバージョンに固有の機能について詳しくは、[リリース ノート](/visualstudio/releases/2019/release-notes/)をご覧ください。

> [!IMPORTANT]
> 一部のプロジェクトの種類には、特定のワークロードが必要です。 ワークロードがインストールされていない場合、Visual Studio は不明な、または互換性のないプロジェクトの種類を報告します。 その場合、[Visual Studio インストーラーでインストール オプション](../install/modify-visual-studio.md)を確認して、やり直してください。 Visual Studio 2019 のプロジェクト サポートについて詳しくは、[対象プラットフォームと互換性](/visualstudio/releases/2019/compatibility)に関する記事をご覧ください。

## <a name="project-types"></a>プロジェクトの種類

次の一覧は、以前のバージョンで作成されたプロジェクトに対する Visual Studio 2022 でのサポートをまとめたものです。

表示されるはずのプロジェクトまたはファイルの種類が見つからない場合、[この記事の Visual Studio 2019 バージョン](?view=vs-2019&preserve-view=true)を調べてください。 このページの下部にある **[次のフィードバックを送信]**  >  **[このページ]** ボタンを使用して、プロジェクトの詳細を提供することもできます。 (匿名の "このページは役に立ちましたか。" コントロールを使用した場合、 フィードバックに応対できません。)

| プロジェクトの種類 | サポート |
| --- | --- |
| .NET Core プロジェクト (xproj) | Visual Studio 2015 で作成したプロジェクトでは、.xproj プロジェクト ファイルが含まれるプレビュー ツールが使用されていました。<br/><br/>Visual Studio 2017:xproj 形式は、csproj 形式への移行以外ではサポートされていません。 xproj ファイルを開くと、SDK スタイルの csproj 形式にファイルを移行するように求められます。 (xproj ファイルのバックアップが作成されます。)SDK スタイルの csproj プロジェクトは、Visual Studio 2015 以前ではサポートされません。 <br/><br/>Visual Studio 2019:バージョン 16.3 以降では、xproj プロジェクトの読み込みまたは移行を実行できません。 詳細については、「[.NET Core プロジェクトから .csproj 形式への移行](/dotnet/core/migration/#visual-studio)」をご覧ください。|
| ASP.NET Core Web アプリと Application Insights を使用した ASP.NET Core Web アプリが有効になっている | Visual Studio のユーザーごとのリソース情報がユーザー インスタンス別にレジストリに保存されます。 この情報は、プロジェクトを開いていない状態で Azure Application Insights データを検索するときに利用されます。 Visual Studio 2015 では、Visual Studio 2017、Visual Studio 2019、Visual Studio 2022 とは異なるレジストリの場所が使用され、競合しません。<br/><br/>ユーザーが ASP.NET Web アプリケーション、ASP.NET Core Web アプリ、または ASP.NET Core Web アプリケーションを作成すると、リソースは .suo ファイルに保存されます。 ユーザーは Visual Studio 2015、Visual Studio 2017、Visual Studio 2019、Visual Studio 2022 でプロジェクトを開くことができます。両方のバージョンで使用されているプロジェクトとソリューションが Visual Studio でサポートされている限り、それぞれでリソース情報が使用されます。 ユーザーは製品ごとに 1 回認証する必要があります。 たとえば、Visual Studio 2017 で作成されたプロジェクトを Visual Studio 2022 で開く場合、Visual Studio 2022 で認証が要求されます。 |
| C#/Visual Basic Webform または Windows フォーム | プロジェクトは、Visual Studio 2022、Visual Studio 2019、Visual Studio 2017、Visual Studio 2015 で開くことができます。 |
| コード化された UI テスト | UI 駆動型機能テストの自動化のためにコード化された UI テストは、Visual Studio 2019 では非推奨になりました。 <br/><br/>Visual Studio 2019 は、コード化された UI テストの最後のリリースとなります。 Web アプリのテストには Selenium を使用し、デスクトップと UWP アプリのテストには Appium と WinAppDriver を一緒に使用することをお勧めします。 |
| データベース単体テスト プロジェクト (csproj、.vbproj) | 古いデータ単体テスト プロジェクトは Visual Studio 2019 で読み込まれますが、依存関係は GAC に保存されているものが使用されます。 単体テスト プロジェクトをアップグレードし、最新の依存関係を使用するには、ソリューション エクスプローラーでプロジェクトを右クリックし、 **[SQL Server 単体テスト プロジェクトに変換する]** を選択します。 |
| F# | Visual Studio 2019 では、Visual Studio 2013、Visual Studio 2015、Visual Studio 2017 で作成されたプロジェクトを開くことができます。 新しいプロジェクトの以前の Visual Studio テンプレートとの主な違いは、FSharp.Core のバージョンが常に NuGet パッケージになったことです。 F# は任意の .NET ワークロードにより既定でインストールされます。|
| InstallShield<br/>MSI のセットアップ | Visual Studio 2010 で作成されたインストーラー プロジェクトは、[Visual Studio Installer Projects の拡張機能](https://marketplace.visualstudio.com/items?itemName=UnniRavindranathan-MSFT.MicrosoftVisualStudio2013InstallerProjects)を使って以降のバージョンで開くことができます。 「[WiX Toolset Visual Studio 2017 Extension](https://marketplace.visualstudio.com/items?itemName=RobMensching.WixToolsetVisualStudio2017Extension)」も参照してください。 InstallShield Limited Edition は、Visual Studio に付属しなくなりました。 Visual Studio 2022 で利用可能かどうかについては、[Flexera Software](https://info.flexerasoftware.com/IS-EVAL-InstallShield-Limited-Edition-Visual-Studio) にご確認ください。 |
| LightSwitch | LightSwitch は Visual Studio 2022、Visual Studio 2019、または Visual Studio 2017 ではサポートされていません。 Visual Studio 2012 以前のバージョンで作成されたプロジェクトを Visual Studio 2013 または Visual Studio 2015 で開くとアップグレードされ、以後、Visual Studio 2013 または Visual Studio 2015 のみで開けるようになります。 |
| ロード テスト | Visual Studio 2019 では、Web パフォーマンスとロード テストの機能は非推奨となっています。 <br/><br/>Visual Studio 2019 は、ロード テストの最後のリリースとなります。 Apache JMeter、Akamai CloudTest、Blazemeter など、代替のロード テスト ツールを使用してください。  |
| Microsoft Azure Tools for Visual Studio | これらの種類のプロジェクトを開くには、最初に [Azure SDK for .NET](https://azure.microsoft.com/downloads/)をインストールした後、プロジェクトを開きます。 必要に応じて、プロジェクトが更新されます。 |
| Microsoft Test Manager | Visual Studio 2019 以降、Microsoft Test Manager と Feedback Client は Visual Studio に付属しません。 <br/><br/>手動テストまたは探索的テストの必要がある場合は、Azure Test Plans (Azure DevOps の一部) をご利用ください。 詳細については、Azure DevOps ドキュメントの「[Guidance on Microsoft Test Manager usage (Microsoft Test Manager の使用に関するガイダンス)](/azure/devops/test/mtm/guidance-mtm-usage?view=azure-devops&preserve-view=true)」ページをご覧ください。 |
| モデル ビュー コントローラー フレームワーク (ASP.NET MVC) | MVC バージョンと Visual Studio のサポート:<ul><li>Visual Studio 2010 SP1 は MVC 2 と MVC 3 をサポートしています。MVC 4 サポートは [ASP.NET 4 MVC 4 for Visual Studio 2010 SP1 をダウンロード](https://www.microsoft.com/download/details.aspx?id=30683)すると追加されます。</li><li>Visual Studio 2012 は MVC 3 と MVC 4 のみをサポートしています。</li><li>Visual Studio 2013 は MVC 4 と MVC 5 のみをサポートしています。</li><li>Visual Studio 2019、Visual Studio 2017、Visual Studio 2015 では MVC 4 (既存のオブジェクトを開くことはできますが、新規作成はできません) と MVC 5 がサポートされています。</li></ul><br/>MVC バージョンをアップグレードする:<ul><li>MVC 2 から MVC 3 に自動的にアップグレードする方法については、「[ASP.NET MVC 3 Application Upgrader](https://archive.codeplex.com/?p=aspnet)」 (ASP.NET MVC 3 アプリケーション アップグレード プログラム) を参照してください。</li><li>MVC 2 から MVC 3 に手動でアップグレードする方法については、「 [Upgrading an ASP.NET MVC 2 Project to ASP.NET MVC 3 Tools Update (ASP.NET MVC 2 プロジェクトから ASP.NET MVC 3 Tools Update へのアップグレード)](https://archive.codeplex.com/?p=aspnet)」を参照してください。</li><li>MVC 3 から MVC 4 に手動でアップグレードする方法については、「 [Upgrading an ASP.NET MVC 3 Project to ASP.NET MVC 4 (ASP.NET MVC 3 プロジェクトから ASP.NET MVC 4 へのアップグレード)](/aspnet/whitepapers/mvc4-release-notes)」を参照してください。 .NET Framework 3.5 SP1 を対象とするプロジェクトの場合は、.NET Framework 4 を使用するようにプロジェクトの対象を変更する必要があります。</li><li>MVC 4 から MVC 5 に手動でアップグレードする方法については、「[How to Upgrade an ASP.NET MVC 4 and Web API Project to ASP.NET MVC 5 and Web API 2](https://www.asp.net/mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2) (ASP.NET MVC 4 と Web API プロジェクトを ASP.NET MVC 5 と Web API 2 にアップグレードする方法)」を参照してください。</li></ul> |
| モデリング | Visual Studio でプロジェクトを自動的に更新することを許可した場合は、Visual Studio 2015、Visual Studio 2013、または Visual Studio 2012 で開くことができます。<br/><br/>モデリング プロジェクトの形式は Visual Studio 2015 以来変わっていません。プロジェクトはこれらのバージョンで開いて変更することができます。 ただし、Visual Studio 2017 と Visual Studio 2019 では動作に違いがあります。<ul><li>メニューとテンプレートで、モデリング プロジェクトの名称が "依存関係の検証" になりました。</li><li>UML 図は Visual Studio 2017 と Visual Studio 2019 ではサポートされていません。 UML ファイルは以前と同様にソリューション エクスプローラーに一覧表示されますが、XML ファイルが開きます。 UML 図を表示、作成、編集するには、Visual Studio 2015 を使用してください。</li><li>Visual Studio 2019 では、モデリング プロジェクトが構築されるとき、アーキテクチャの依存関係検証がなくなりました。 代わりに、コード プロジェクトが構築されるときに検証が実行されます。 この変更がモデリング プロジェクトに影響を与えることはありませんが、検証されるコード プロジェクトを変更する必要があります。 Visual Studio 2019 では、コード プロジェクトを必要に応じて自動的に変更できます。</li></ul> |
| MSI セットアップ (vdproj) | InstallShield プロジェクトをご覧ください。 |
| Office 2007 VSTO | Visual Studio 2022 への一方向のアップグレードが必要です。 |
| Office 2010 VSTO | .NET Framework 4 を対象とするプロジェクトの場合は、Visual Studio 2010 SP1 以降でこのプロジェクトを開くことができます。 他のすべてのプロジェクトは、一方向のアップグレードが必要です。 |
| ポータブル クラス ライブラリ (PCL) | ポータブル クラス ライブラリ (PCL) はサポートされなくなりました。 Visual Studio 2019 では引き続き PCL を開いたりビルドできますが、新しい PCL プロジェクトを作成することはできません。 PCL プロジェクトのコードを .NET Standard プロジェクトに移行することをお勧めします。<br/><br/>PCL のサポートは既定では含まれなくなりますが、Visual Studio の "個々のコンポーネント" タブでは使用できます。 |
| Python ワークロード | Python Windows IoT Core アプリのサポートは、Visual Studio 2019 で削除されました。 Visual Studio 2022 には等価なものがないため、そのようなプロジェクトの自動移行パスはありません。<br/><br/>Visual Studio 2017 を引き続き使用することができます。 |
| R Tools for Visual Studio | R Tools for Visual Studio は、Visual Studio 2019 でデータ サイエンス ワークロードから削除されました。<br/><br/>Visual Studio 2017 または RStudio などの代替手段を引き続き使用することができます。 |
| Service Fabric (sfproj) | Service Fabric アプリケーション プロジェクトが ASP.NET Core サービス プロジェクトを参照していない限り、Service Fabric アプリケーション プロジェクトは Visual Studio 2015、Visual Studio 2017、Visual Studio 2019 のいずれかで開くことができます。 Visual Studio 2017 または Visual Studio 2019 で開かれている Visual Studio 2015 からの Service Fabric プロジェクトは、xproj 形式から csproj への一方向の移行が行われます。 この表で前述した「.NET Core プロジェクト (xproj)」を参照してください。 |
| SharePoint 2010 | SharePoint ソリューション プロジェクトを Visual Studio 2022 で開くと、SharePoint 2016 または SharePoint 2019 にアップグレードされます。 アップグレードのためには、".NET デスクトップ開発" ワークロードを Visual Studio にインストールする必要があります。<br/><br/>SharePoint プロジェクトをアップグレードする方法の詳細については、[SharePoint のアップグレードおよび更新](/sharepoint/upgrade-and-update/upgrade-and-update)に関するページを参照してください。|
| SharePoint 2016 | Office Developer Tools Preview 2 で作成された SharePoint アドイン プロジェクトを Visual Studio 2022 で開くことはできません。 この制限を回避するには、csproj vbproj ファイルで、`MinimumVisualStudioVersion` を 12.0 に、`MinimumOfficeToolsVersion` を 12.2 に更新する必要があります。 |
| Silverlight | Silverlight プロジェクトは Visual Studio 2022 ではサポートされていません。 Silverlight アプリケーションを維持するには、引き続き Visual Studio 2015 を使用してください。 |
| SQL - Redgate | Redgate の SQL Change Automation Core (旧称、ReadyRoll Core)、SQL Prompt Core、および SQL Search は、Visual Studio インストーラーに付属されななくなりました。<br/><br/>これらの機能には、Visual Studio 2017 を引き続き使用することができます。 Visual Studio 2019 では、Redgate の SQL Toolbelt で入手可能な有料の SQL Change Automation および SQL Prompt 製品にアップグレードすることができます。|
| SQL Server Reporting Services および SQL Server Analysis Services (SSRS、SSDT、SSAS、MSAS) | これらのプロジェクト タイプのサポートは、Visual Studio ギャラリーの次の 2 つの拡張機能を通じて提供されます。[Microsoft Analysis Services Modeling Projects](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftAnalysisServicesModelingProjects) と [Microsoft Reporting Services Projects](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftReportProjectsforVisualStudio)。 Visual Studio 2019 のデータの保存と処理のワークロードには SSDT のサポートも含まれます。 詳細については、「[Visual Studio の SQL Server Data Tools (SSDT) をダウンロードし、インストールする](/sql/ssdt/download-sql-server-data-tools-ssdt)」を参照してください。 |
| SQL Server Integration Services (SSIS) | Visual Studio 2019 のサポートを利用できます。 詳細については、「[Visual Studio の SQL Server Data Tools (SSDT) をダウンロードし、インストールする](/sql/ssdt/download-sql-server-data-tools-ssdt)」ページ、「[SQL Server Integration Services (SSIS)](https://techcommunity.microsoft.com/t5/SQL-Server-Integration-Services/bg-p/SSIS)」チーム ブログ、および Marketplace の「[SQL Server Integration Services Projects](https://marketplace.visualstudio.com/items?itemName=SSIS.SqlServerIntegrationServicesProjects&ssr=false#overview)」ページを参照してください。 |
| テスト ウィンドウ拡張機能 | Visual Studio 2019 では、前にパブリックとしてマークされていたがドキュメントに正式に記載されたことがないいくつかのテスト ウィンドウ API が削除されました。 広く利用されていた API には、拡張機能の管理者に対して早期に警告を発するために、Visual Studio 2017 で非推奨のマークが付いていました。 Microsoft の知る限りでは、これらの API に対して依存関係を築いている拡張機能はわずかです。 詳細と更新プログラムにいては、[テスト関連の非推奨の API の完全一覧](https://github.com/Microsoft/vstest/issues/1830)に関するページを参照してください。 これが自分のシナリオに影響する場合、[開発者コミュニティ](https://aka.ms/feedback/suggest?space=8)でお知らせください。 |
| Visual C++ | Visual Studio 2022 を使用して、Visual Studio 2010 以降の Visual Studio で作成されたプロジェクトを操作できます。 プロジェクトを初めて開いたときに、最新のコンパイラとツールセットにアップグレードするか、元のプロジェクトを引き続き使用するかを選択できます。 元のプロジェクトを引き続き使用することを選択した場合、Visual Studio 2019 はプロジェクト ファイルを変更せず、以前の Visual Studio のインストールのツールセットを使用してプロジェクトをビルドします。 元のオプションを維持すると、必要に応じて、Visual Studio の元のバージョンでプロジェクトを開くことができます。 詳細については、「[Visual Studio でネイティブ マルチ ターゲットを利用し、古いプロジェクトを作成する](/cpp/porting/use-native-multi-targeting)」を参照してください。 |
| Visual Studio 拡張性/VSIX | MinimumVersion 14.0 以前のプロジェクトは、MinimumVersion 15.0 を宣言するように更新されます。この宣言により、前のバージョンの Visual Studio でプロジェクトを開けなくなります。 前のバージョンでプロジェクトを開くには、MinimumVersion を `$(VisualStudioVersion)` に設定します。 「[方法: 機能拡張プロジェクトの Visual Studio 2017 への移行](../extensibility/how-to-migrate-extensibility-projects-to-visual-studio-2017.md)に関するページも参照してください。 |
| Visual Studio Lab Management | Microsoft Test Manager または Visual Studio 2010 SP1 以降を利用し、これらのバージョンで差制された環境を開くことができます。 ただし、Visual Studio 2010 SP1 の場合、環境を作成するには、使用している Microsoft Test Manager のバージョンが Team Foundation Server のバージョンと一致する必要があります。 |
| Visual Studio Tools for Apache Cordova | Apache Cordova のサポートは、Visual Studio 2019 で削除されました。 Visual Studio 2022 には等価なものがないため、そのようなプロジェクトの自動移行パスはありません。<br/><br/>Cordova Tools for Visual Studio Code 拡張機能 (Cordova の最新バージョンのサポートを提供) を使用することも、Visual Studio 2017 を引き続き使用することもできます。 |
| Web 配置 (wdproj) | 発行プロファイルのサポートが追加されたことで、Visual Studio 2012 では Web 配置プロジェクトのサポートが削除されました。 Visual Studio 2022 には等価なものがないため、そのようなプロジェクトの自動移行パスはありません。 そこで、[StackOverflow](https://stackoverflow.com/a/12061065/1203388) に説明されているように、テキスト エディターで wdproj ファイルを開き、pubxml (発行プロファイル) ファイルに任意のカスタマイズをコピーおよび貼り付けます。 |
| Windows Communication Foundation、Windows Workflow Foundation | このプロジェクトは、Visual Studio 2022、Visual Studio 2019、Visual Studio 2017、Visual Studio 2015、Visual Studio 2013、Visual Studio 2012 で開くことができます。 |
| Windows Presentation Foundation | このプロジェクトは、Visual Studio 2022、Visual Studio 2019、Visual Studio 2017、Visual Studio 2013、Visual Studio 2012、Visual Studio 2010 SP1 で開くことができます。 |
| Windows Phone アプリ | Windows Phone のプロジェクトは、Visual Studio 2022 ではサポートされていません。 <br/><br/>Windows Phone 8.x アプリを維持するには、Visual Studio 2015 を使用してください。 Windows Phone 7.x プロジェクトを維持するには、Visual Studio 2012 を使用してください。 |
| Windows ストア アプリ | JavaScript ユニバーサル Windows プロジェクトは、Visual Studio 2022 ではサポートされていません。 これらのプロジェクトを維持するには、Visual Studio 2017 を使用してください。 <br/><br/>Windows 10 Fall Creators Update (ビルド 16299) より前の Windows 10 SDK は、Visual Studio 2019 インストーラーから削除されました。 古い SDK を手動でダウンロードすることも、新しい SDK を使用するようにプロジェクトを再ターゲットすることもできます。<br/><br/>project.json を使用しているユニバーサル Windows プロジェクトはサポートされていません。 パッケージ参照を使用するようにこれらのプロジェクトをアップグレードすることをお勧めします。 または、project.json ファイルで Microsoft.NET.Test.Sdk バージョン 16.0.0.0 への参照を追加します。<br/><br/>Windows Store 8.1 および 8.0 のプロジェクトは、Visual Studio 2022 ではサポートされていません。 これらのアプリを維持するには、引き続き Visual Studio 2015 を使用してください。 |
| Xamarin | Visual Studio および Visual Studio for Mac の Xamarin Live Player 拡張機能は削除されました。 これにより、ペアリングの画面とすべての統合が削除されます。 代わりに、Xamarin.Forms Previewer でビルドを使用してください。<br/><br/>Visual Studio Emulator for Android は、Visual Studio インストーラーから削除されました。 代わりに、Google Android エミュレーターで新しい HYPER-V サポートを使用してください。 |

## <a name="migrate-a-project"></a>プロジェクトの移行

Microsoft では、以前のバージョンとの互換性を維持しようと試みていますが、以前のバージョンと互換性のない変更が生じる可能性があります。 <!--(See [Platform Targeting and Compatibility](/visualstudio/releases/2019/compatibility) for which project types are supported in Visual Studio 2022.)--> これが発生した場合、新しいバージョンの Visual Studio ではプロジェクトが読み込まれず、移行パスも提供されません。 そのプロジェクトを、以前のバージョンの Visual Studio で維持することが必要になる場合があります。

新しいバージョンの Visual Studio でプロジェクトを開ける場合があります。ただし、そこでは、以前のバージョンとの互換性がなくなる可能性がある方法で、プロジェクトを更新または移行する必要があります。 Visual Studio は、複数の条件を使って、このような移行が必要かどうかを判断します。

- Visual Studio 2013 RTM まで遡る、プラットフォームのターゲット バージョンとの互換性。

- 以前のバージョンの Visual Studio との、デザイン時資産の互換性 (つまり、さまざまなチャネルの Visual Studio 2022、Visual Studio 2019、Visual Studio 2017、Visual Studio 2015 RTM & Update 3、Visual Studio 2013 RTM & Update 5、Visual Studio 2012 Update 4、Visual Studio 2010 SP1)。Visual Studio 2022 では、以前のバージョンでプロジェクトをまだ開くことができるように、非推奨のデザイン時資産を、破壊することなく正常に失敗させます。

- 新しいデザイン時資産により、Visual Studio 2013 RTM & Update 5 までの以前のバージョンとの互換性がなくなるかどうか。

そのプロジェクトの種類を所有しているエンジニアリング チームは、これらの条件を確認し、サポート、互換性、移行に関して問題があるときは問い合わせます。 ここでも、Visual Studio のバージョン間の互換性を維持して、Visual Studio のあるバージョンで作成および変更したプロジェクトが、他のバージョンでもそのままで動作するようにすることが試みられます。

場合によっては、互換性を実現できないことがあります。 その場合、Visual Studio によって、必要な一方向の変更を加えるためのアップグレード ウィザードが開かれます。 これらの一方向の変更には、プロジェクト ファイルの `ToolsVersion` プロパティの変更が含まれる場合があります。このプロパティにより、プロジェクトのソース コードを目的の実行可能で配置可能な成果物に変換できる、MSBuild の正確なバージョンが示されます。

プロジェクトと以前のバージョンの Visual Studio との互換性を損なうものは、*Visual Studio* のバージョンではなく、`ToolsVersion` によって決定される *MSBuild* のバージョンです。 お使いの Visual Studio のバージョンに、プロジェクトの `ToolsVersion` と一致する MSBuild ツールチェーンが含まれている場合、Visual Studio ではそのツールチェーンを呼び出してプロジェクトをビルドすることができます。

以前のバージョンで作成したプロジェクトとの互換性を維持するため、Visual Studio 2019 には、`ToolsVersion` 15、14、12、4 をサポートするために必要な MSBuild ツールチェーンが含まれています。 これらの `ToolsVersion` 値のいずれかを使うプロジェクトでは、ビルドが成功するはずです (やはり、[対象プラットフォームと互換性](/visualstudio/releases/2019/compatibility)に関する記事で説明されているように、Visual Studio 2019 がそのプロジェクトの種類をサポートするかどうかに依存します)。

新しい `ToolsVersion` 値にプロジェクトを手動で更新または移行しようとお考えになるかもしれません。 そのような変更は不要です。実行した場合、プロジェクトを再ビルドするために修正しなければならない多くのエラーと警告が発生する可能性があります。 また、将来特定の `ToolsVersion` が Visual Studio でサポートされなくなった場合、そのプロジェクトを開くとプロジェクトの移行プロセスがトリガーされます。その `ToolsVersion` の値を変更する必要があるためです。

## <a name="next-steps"></a>次の手順

詳しくは、次の記事をご覧ください。

- [ToolsVersion ガイダンス](../msbuild/msbuild-toolset-toolsversion.md)
- [フレームワーク対象設定機能ガイダンス](../ide/visual-studio-multi-targeting-overview.md)

## <a name="see-also"></a>関連項目

- [Visual Studio 2019 のプロジェクトの移行とアップグレードのリファレンス](?view=vs-2019&preserve-view=true)
- [Visual Studio の製品ライフサイクルとサービス](/visualstudio/releases/2019/servicing/)

::: moniker-end