---
title: Visual Studio Professional 2019 のワークロード ID とコンポーネント ID
titleSuffix: ''
description: ワークロード ID とコンポーネント ID を使用して、コマンドラインを使用して Visual Studio をインストールするか、VSIX マニフェストで依存関係として指定します。
keywords: ''
author: j-martens
ms.author: jmartens
manager: jmartens
ms.date: 05/24/2021
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.topic: include
ms.openlocfilehash: 94b9a330c207513f20571c0a577aaca5502a9ebe
ms.sourcegitcommit: 18e7300d4878f2fcd0263a4aff31a755ae8fc289
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/25/2021
ms.locfileid: "110449722"
---
## <a name="visual-studio-core-editor-included-with-visual-studio-professional-2019"></a>Visual Studio のコア エディター (Visual Studio Professional 2019 に付属)

**ID:** Microsoft.VisualStudio.Workload.CoreEditor

**説明:** 構文認識コード編集機能、ソース コード管理、作業項目管理などの Visual Studio の基本的なシェル エクスペリエンス。

### <a name="components-included-by-this-workload"></a>このワークロードに含まれるコンポーネント

コンポーネント ID | 名前 | バージョン | 依存関係の種類
--- | --- | --- | ---
Microsoft.VisualStudio.Component.CoreEditor | Visual Studio のコア エディター | 16.1.28811.260 | 必須
Microsoft.VisualStudio.Component.StartPageExperiment.Cpp | C++ ユーザー用 Visual Studio スタート ページ | 16.0.28315.86 | Optional

## <a name="azure-development"></a>Azure の開発

**ID:** Microsoft.VisualStudio.Workload.Azure

**説明:** .NET および .NET Framework を使用したクラウド アプリの開発とリソースの作成のための Azure SDK、ツール、プロジェクト。 Docker のサポートなど、アプリケーションをコンテナー化するためのツールも含まれています。

### <a name="components-included-by-this-workload"></a>このワークロードに含まれるコンポーネント

コンポーネント ID | 名前 | バージョン | 依存関係の種類
--- | --- | --- | ---
Component.Microsoft.VisualStudio.RazorExtension | Razor 言語サービス | 16.10.31205.252 | 必須
Component.Microsoft.VisualStudio.Web.AzureFunctions | Azure WebJobs ツール | 16.10.31205.252 | 必須
Component.Microsoft.Web.LibraryManager | ライブラリ マネージャー | 16.10.31205.180 | 必須
Component.Microsoft.WebTools.BrowserLink.WebLivePreview | Web ライブ プレビュー | 0.7.22.39845 | 必須
Microsoft.Component.MSBuild | MSBuild | 16.5.29515.121 | 必須
Microsoft.ComponentGroup.ClickOnce.Publish | .NET の ClickOnce 発行  | 16.10.31303.231 | 必須
Microsoft.Net.Component.4.5.2.TargetingPack | .NET Framework 4.5.2 Targeting Pack | 16.0.28517.75 | 必須
Microsoft.Net.Component.4.5.TargetingPack | .NET Framework 4.5 Targeting Pack | 16.0.28517.75 | 必須
Microsoft.Net.Component.4.6.1.TargetingPack | .NET Framework 4.6.1 Targeting Pack | 16.0.28517.75 | 必須
Microsoft.Net.Component.4.7.2.TargetingPack | .NET Framework 4.7.2 Targeting Pack | 16.10.31205.252 | 必須
Microsoft.Net.Component.4.8.SDK | .NET Framework 4.8 SDK | 16.4.29313.120 | 必須
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | .NET Framework 4.7.2 開発ツール | 16.3.29207.166 | 必須
Microsoft.NetCore.Component.DevelopmentTools | .NET 開発ツール | 16.10.31303.231 | 必須
Microsoft.NetCore.Component.Runtime.3.1 | .NET Core 3.1 ランタイム (LTS) | 16.10.31320.204 | 必須
Microsoft.NetCore.Component.Runtime.5.0 | .NET 5.0 ランタイム | 16.10.31320.204 | 必須
Microsoft.NetCore.Component.SDK | .NET SDK | 16.10.31320.204 | 必須
Microsoft.NetCore.Component.Web | .NET 開発ツール | 16.10.31303.231 | 必須
Microsoft.VisualStudio.Component.Azure.AuthoringTools | Azure Authoring Tools | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.Azure.ClientLibs | .NET 用 Azure ライブラリ | 16.0.28315.86 | 必須
Microsoft.VisualStudio.Component.Azure.Compute.Emulator | Azure コンピューティング エミュレーター | 16.10.31205.252 | 必須
Microsoft.VisualStudio.Component.Azure.Storage.Emulator | Azure Storage エミュレーター | 16.4.29313.120 | 必須
Microsoft.VisualStudio.Component.CloudExplorer | Cloud Explorer | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.Common.Azure.Tools | 接続および発行ツール | 16.4.29409.204 | 必須
Microsoft.VisualStudio.Component.DockerTools | コンテナー開発ツール | 16.4.29409.204 | 必須
Microsoft.VisualStudio.Component.FSharp | F# 言語サポート | 16.0.28315.86 | 必須
Microsoft.VisualStudio.Component.FSharp.WebTemplates | Web プロジェクト用の F# 言語サポート | 16.3.29207.166 | 必須
Microsoft.VisualStudio.Component.IISExpress | IIS Express  | 16.0.28315.86 | 必須
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | JavaScript 診断 | 16.0.28517.75 | 必須
Microsoft.VisualStudio.Component.JavaScript.TypeScript | JavaScript および TypeScript の言語サポート | 16.10.31303.231 | 必須
Microsoft.VisualStudio.Component.ManagedDesktop.Core | Managed Desktop Workload コア | 16.4.29318.151 | 必須
Microsoft.VisualStudio.Component.MSODBC.SQL | SQL Server ODBC Driver | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.MSSQL.CMDLnUtils | SQL Server コマンド ライン ユーティリティ | 16.0.28707.177 | 必須
Microsoft.VisualStudio.Component.NuGet | NuGet パッケージ マネージャー | 16.1.28829.92 | 必須
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# および Visual Basic Roslyn コンパイラ | 16.0.28714.129 | 必須
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# および Visual Basic | 16.10.31205.252 | 必須
Microsoft.VisualStudio.Component.SQL.ADAL | SQL ADAL ランタイム | 16.0.28517.75 | 必須
Microsoft.VisualStudio.Component.SQL.CLR | SQL Server の CLR データ型 | 16.0.28315.86 | 必須
Microsoft.VisualStudio.Component.SQL.DataSources | SQL Server サポートのためのデータ ソース | 16.0.28315.86 | 必須
Microsoft.VisualStudio.Component.SQL.LocalDB.Runtime | SQL Server Express 2016 LocalDB | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.SQL.SSDT | SQL Server Data Tools | 16.3.29207.166 | 必須
Microsoft.VisualStudio.Component.TextTemplating | テキスト テンプレート変換 | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.TypeScript.4.2 | TypeScript 4.2 SDK | 16.0.31303.231 | 必須
Microsoft.VisualStudio.Component.Web | ASP.NET と Web の開発ツール | 16.10.31205.252 | 必須
Microsoft.VisualStudio.ComponentGroup.Azure.Prerequisites | Azure 開発の前提条件 | 16.10.31303.231 | 必須
Microsoft.VisualStudio.ComponentGroup.AzureFunctions | Azure WebJobs ツール | 16.10.31205.180 | 必須
Microsoft.VisualStudio.ComponentGroup.Web | ASP.NET と Web の開発ツールの前提条件 | 16.10.31205.180 | 必須
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | ASP.NET と Web 開発 | 16.10.31205.180 | 必須
Microsoft.Component.Azure.DataLake.Tools | Azure Data Lake と Stream Analytics ツール | 16.10.31205.252 | 推奨
Microsoft.Net.Component.4.5.1.TargetingPack | .NET Framework 4.5.1 Targeting Pack | 16.0.28517.75 | 推奨
Microsoft.Net.Component.4.6.TargetingPack | .NET Framework 4.6 Targeting Pack | 16.0.28517.75 | 推奨
Microsoft.Net.Component.4.TargetingPack | .NET Framework 4 Targeting Pack | 16.0.28517.75 | 推奨
Microsoft.Net.ComponentGroup.TargetingPacks.Common | .NET Framework 4 – 4.6 開発ツール | 16.0.28516.191 | 推奨
Microsoft.VisualStudio.Component.AspNet45 | 高度な ASP.NET 機能 | 16.10.31205.252 | 推奨
Microsoft.VisualStudio.Component.Azure.Kubernetes.Tools | Visual Studio Tools for Kubernetes | 16.10.31205.252 | 推奨
Microsoft.VisualStudio.Component.Azure.Powershell | Azure Powershell | 16.5.29515.121 | 推奨
Microsoft.VisualStudio.Component.Azure.ResourceManager.Tools | Azure Resource Manager コア ツール | 16.4.29409.204 | 推奨
Microsoft.VisualStudio.Component.Azure.ServiceFabric.Tools | Service Fabric Tools | 16.4.29313.120 | 推奨
Microsoft.VisualStudio.Component.Azure.Waverton | Azure Cloud Services コア ツール | 16.10.31205.252 | 推奨
Microsoft.VisualStudio.Component.Azure.Waverton.BuildTools | Azure Cloud Services ビルド ツール | 16.10.31205.252 | 推奨
Microsoft.VisualStudio.Component.DiagnosticTools | .NET プロファイル ツール | 16.10.31205.252 | 推奨
Microsoft.VisualStudio.Component.IntelliCode | IntelliCode | 16.10.31305.154 | 推奨
Microsoft.VisualStudio.Component.WebDeploy | Web 配置 | 16.0.28517.75 | 推奨
Microsoft.VisualStudio.ComponentGroup.Azure.CloudServices | Azure Cloud Services ツール | 16.10.31205.180 | 推奨
Microsoft.VisualStudio.ComponentGroup.Azure.ResourceManager.Tools | Azure Resource Manager ツール | 16.0.28528.71 | 推奨
Microsoft.Net.Component.4.6.2.TargetingPack | .NET Framework 4.6.2 Targeting Pack | 16.0.28517.75 | Optional
Microsoft.Net.Component.4.7.1.TargetingPack | .NET Framework 4.7.1 Targeting Pack | 16.10.31205.252 | Optional
Microsoft.Net.Component.4.7.TargetingPack | .NET Framework 4.7 Targeting Pack | 16.10.31205.252 | Optional
Microsoft.Net.Component.4.8.TargetingPack | .NET Framework 4.8 Targeting Pack | 16.4.29313.120 | Optional
Microsoft.Net.ComponentGroup.4.6.1.DeveloperTools | .NET Framework 4.6.1 開発ツール | 16.3.29207.166 | Optional
Microsoft.Net.ComponentGroup.4.6.2.DeveloperTools | .NET Framework 4.6.2 開発ツール | 16.3.29207.166 | Optional
Microsoft.Net.ComponentGroup.4.7.1.DeveloperTools | .NET Framework 4.7.1 開発ツール | 16.3.29207.166 | Optional
Microsoft.Net.ComponentGroup.4.7.DeveloperTools | .NET Framework 4.7 開発ツール | 16.3.29207.166 | Optional
Microsoft.Net.ComponentGroup.4.8.DeveloperTools | .NET Framework 4.8 開発ツール | 16.4.29318.151 | Optional
Microsoft.Net.Core.Component.SDK.2.1 | .NET Core 2.1 ランタイム (LTS) | 16.10.31320.204 | Optional
Microsoft.VisualStudio.Component.Azure.Storage.AzCopy | Azure Storage AzCopy | 16.0.28517.75 | Optional
Microsoft.VisualStudio.Component.Wcf.Tooling | Windows Communication Foundation | 16.0.28625.61 | Optional

## <a name="data-storage-and-processing"></a>データ ストレージとデータ処理

**ID:** Microsoft.VisualStudio.Workload.Data

**説明:** SQL Server、Azure Data Lake、Hadoop を使用してデータ ソリューションの接続、開発、テストを行います。

### <a name="components-included-by-this-workload"></a>このワークロードに含まれるコンポーネント

コンポーネント ID | 名前 | バージョン | 依存関係の種類
--- | --- | --- | ---
Component.Microsoft.VisualStudio.RazorExtension | Razor 言語サービス | 16.10.31205.252 | 推奨
Component.Microsoft.Web.LibraryManager | ライブラリ マネージャー | 16.10.31205.180 | 推奨
Component.Microsoft.WebTools.BrowserLink.WebLivePreview | Web ライブ プレビュー | 0.7.22.39845 | 推奨
Microsoft.Component.Azure.DataLake.Tools | Azure Data Lake と Stream Analytics ツール | 16.10.31205.252 | 推奨
Microsoft.Component.MSBuild | MSBuild | 16.5.29515.121 | 推奨
Microsoft.Net.Component.4.5.1.TargetingPack | .NET Framework 4.5.1 Targeting Pack | 16.0.28517.75 | 推奨
Microsoft.Net.Component.4.5.2.TargetingPack | .NET Framework 4.5.2 Targeting Pack | 16.0.28517.75 | 推奨
Microsoft.Net.Component.4.5.TargetingPack | .NET Framework 4.5 Targeting Pack | 16.0.28517.75 | 推奨
Microsoft.Net.Component.4.6.TargetingPack | .NET Framework 4.6 Targeting Pack | 16.0.28517.75 | 推奨
Microsoft.Net.Component.4.7.2.TargetingPack | .NET Framework 4.7.2 Targeting Pack | 16.10.31205.252 | 推奨
Microsoft.Net.Component.4.8.SDK | .NET Framework 4.8 SDK | 16.4.29313.120 | 推奨
Microsoft.Net.Component.4.TargetingPack | .NET Framework 4 Targeting Pack | 16.0.28517.75 | 推奨
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | .NET Framework 4.7.2 開発ツール | 16.3.29207.166 | 推奨
Microsoft.Net.ComponentGroup.TargetingPacks.Common | .NET Framework 4 – 4.6 開発ツール | 16.0.28516.191 | 推奨
Microsoft.NetCore.Component.Runtime.3.1 | .NET Core 3.1 ランタイム (LTS) | 16.10.31320.204 | 推奨
Microsoft.NetCore.Component.Runtime.5.0 | .NET 5.0 ランタイム | 16.10.31320.204 | 推奨
Microsoft.NetCore.Component.SDK | .NET SDK | 16.10.31320.204 | 推奨
Microsoft.VisualStudio.Component.Azure.AuthoringTools | Azure Authoring Tools | 16.0.28625.61 | 推奨
Microsoft.VisualStudio.Component.Azure.ClientLibs | .NET 用 Azure ライブラリ | 16.0.28315.86 | 推奨
Microsoft.VisualStudio.Component.Azure.Compute.Emulator | Azure コンピューティング エミュレーター | 16.10.31205.252 | 推奨
Microsoft.VisualStudio.Component.Azure.Storage.Emulator | Azure Storage エミュレーター | 16.4.29313.120 | 推奨
Microsoft.VisualStudio.Component.Azure.Waverton | Azure Cloud Services コア ツール | 16.10.31205.252 | 推奨
Microsoft.VisualStudio.Component.Azure.Waverton.BuildTools | Azure Cloud Services ビルド ツール | 16.10.31205.252 | 推奨
Microsoft.VisualStudio.Component.CloudExplorer | Cloud Explorer | 16.0.28625.61 | 推奨
Microsoft.VisualStudio.Component.Common.Azure.Tools | 接続および発行ツール | 16.4.29409.204 | 推奨
Microsoft.VisualStudio.Component.DockerTools | コンテナー開発ツール | 16.4.29409.204 | 推奨
Microsoft.VisualStudio.Component.IISExpress | IIS Express  | 16.0.28315.86 | 推奨
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | JavaScript 診断 | 16.0.28517.75 | 推奨
Microsoft.VisualStudio.Component.JavaScript.TypeScript | JavaScript および TypeScript の言語サポート | 16.10.31303.231 | 推奨
Microsoft.VisualStudio.Component.ManagedDesktop.Core | Managed Desktop Workload コア | 16.4.29318.151 | 推奨
Microsoft.VisualStudio.Component.MSODBC.SQL | SQL Server ODBC Driver | 16.0.28625.61 | 推奨
Microsoft.VisualStudio.Component.MSSQL.CMDLnUtils | SQL Server コマンド ライン ユーティリティ | 16.0.28707.177 | 推奨
Microsoft.VisualStudio.Component.NuGet | NuGet パッケージ マネージャー | 16.1.28829.92 | 推奨
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# および Visual Basic Roslyn コンパイラ | 16.0.28714.129 | 推奨
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# および Visual Basic | 16.10.31205.252 | 推奨
Microsoft.VisualStudio.Component.SQL.ADAL | SQL ADAL ランタイム | 16.0.28517.75 | 推奨
Microsoft.VisualStudio.Component.SQL.CLR | SQL Server の CLR データ型 | 16.0.28315.86 | 推奨
Microsoft.VisualStudio.Component.SQL.DataSources | SQL Server サポートのためのデータ ソース | 16.0.28315.86 | 推奨
Microsoft.VisualStudio.Component.SQL.LocalDB.Runtime | SQL Server Express 2016 LocalDB | 16.0.28625.61 | 推奨
Microsoft.VisualStudio.Component.SQL.SSDT | SQL Server Data Tools | 16.3.29207.166 | 推奨
Microsoft.VisualStudio.Component.TextTemplating | テキスト テンプレート変換 | 16.0.28625.61 | 推奨
Microsoft.VisualStudio.Component.TypeScript.4.2 | TypeScript 4.2 SDK | 16.0.31303.231 | 推奨
Microsoft.VisualStudio.Component.Web | ASP.NET と Web の開発ツール | 16.10.31205.252 | 推奨
Microsoft.VisualStudio.ComponentGroup.Web | ASP.NET と Web の開発ツールの前提条件 | 16.10.31205.180 | 推奨
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | ASP.NET と Web 開発 | 16.10.31205.180 | 推奨
Microsoft.Net.Component.4.6.1.TargetingPack | .NET Framework 4.6.1 Targeting Pack | 16.0.28517.75 | Optional
Microsoft.VisualStudio.Component.FSharp.Desktop | F# デスクトップ言語のサポート | 16.0.28315.86 | Optional

## <a name="data-science-and-analytical-applications"></a>データ サイエンスと分析のアプリケーション

**ID:** Microsoft.VisualStudio.Workload.DataScience

**説明:** データ サイエンス アプリケーションを作成するための言語とツール (Python と F# が含まれます)。

### <a name="components-included-by-this-workload"></a>このワークロードに含まれるコンポーネント

コンポーネント ID | 名前 | バージョン | 依存関係の種類
--- | --- | --- | ---
Microsoft.Component.PythonTools | Python 言語サポート | 16.10.31313.127 | 推奨
Microsoft.Component.PythonTools.Minicondax64 | Python miniconda (サポート対象外) | 16.10.31313.127 | 推奨
Microsoft.Component.PythonTools.Web | Python Web サポート | 16.10.31205.252 | 推奨
Microsoft.Net.Component.4.6.1.TargetingPack | .NET Framework 4.6.1 Targeting Pack | 16.0.28517.75 | 推奨
Microsoft.VisualStudio.Component.Common.Azure.Tools | 接続および発行ツール | 16.4.29409.204 | 推奨
Microsoft.VisualStudio.Component.FSharp.Desktop | F# デスクトップ言語のサポート | 16.0.28315.86 | 推奨
Microsoft.VisualStudio.Component.JavaScript.TypeScript | JavaScript および TypeScript の言語サポート | 16.10.31303.231 | 推奨
Microsoft.VisualStudio.Component.NuGet | NuGet パッケージ マネージャー | 16.1.28829.92 | 推奨
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# および Visual Basic Roslyn コンパイラ | 16.0.28714.129 | 推奨
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# および Visual Basic | 16.10.31205.252 | 推奨
Microsoft.VisualStudio.Component.TypeScript.4.2 | TypeScript 4.2 SDK | 16.0.31303.231 | 推奨
Microsoft.VisualStudio.Component.WebDeploy | Web 配置 | 16.0.28517.75 | 推奨
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | ASP.NET と Web 開発 | 16.10.31205.180 | 推奨
Microsoft.ComponentGroup.PythonTools.NativeDevelopment | Python ネイティブ開発ツール | 16.10.31205.180 | Optional
Microsoft.VisualStudio.Component.Graphics.Tools | DirectX 用グラフィックス デバッガーおよび GPU プロファイラー | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.VC.CoreIde | C++ コア機能 | 16.10.31205.252 | Optional
Microsoft.VisualStudio.Component.VC.DiagnosticTools | C++ のプロファイル ツール | 16.5.29515.121 | Optional
Microsoft.VisualStudio.Component.VC.Tools.x86.x64 | MSVC v142 - VS 2019 C++ x64/x86 ビルド ツール (最新) | 16.10.31205.252 | Optional
Microsoft.VisualStudio.Component.Windows10SDK | Windows ユニバーサル C ランタイム | 16.4.29409.204 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.19041 | Windows 10 SDK (10.0.19041.0) | 16.10.31205.252 | Optional

## <a name="net-desktop-development"></a>.NET デスクトップ開発

**ID:** Microsoft.VisualStudio.Workload.ManagedDesktop

**説明:** .NET および .NET Framework で C#、Visual Basic、F# を使用して、WPF、Windows フォーム、コンソール アプリケーションをビルドします。

### <a name="components-included-by-this-workload"></a>このワークロードに含まれるコンポーネント

コンポーネント ID | 名前 | バージョン | 依存関係の種類
--- | --- | --- | ---
Microsoft.Component.MSBuild | MSBuild | 16.5.29515.121 | 必須
Microsoft.Net.Component.4.7.2.TargetingPack | .NET Framework 4.7.2 Targeting Pack | 16.10.31205.252 | 必須
Microsoft.Net.Component.4.8.SDK | .NET Framework 4.8 SDK | 16.4.29313.120 | 必須
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | .NET Framework 4.7.2 開発ツール | 16.3.29207.166 | 必須
Microsoft.NetCore.Component.Runtime.3.1 | .NET Core 3.1 ランタイム (LTS) | 16.10.31320.204 | 必須
Microsoft.NetCore.Component.Runtime.5.0 | .NET 5.0 ランタイム | 16.10.31320.204 | 必須
Microsoft.NetCore.Component.SDK | .NET SDK | 16.10.31320.204 | 必須
Microsoft.VisualStudio.Component.ManagedDesktop.Core | Managed Desktop Workload コア | 16.4.29318.151 | 必須
Microsoft.VisualStudio.Component.ManagedDesktop.Prerequisites | .NET デスクトップ開発ツール | 16.10.31205.180 | 必須
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# および Visual Basic Roslyn コンパイラ | 16.0.28714.129 | 必須
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# および Visual Basic | 16.10.31205.252 | 必須
Microsoft.VisualStudio.Component.SQL.CLR | SQL Server の CLR データ型 | 16.0.28315.86 | 必須
Microsoft.VisualStudio.Component.TextTemplating | テキスト テンプレート変換 | 16.0.28625.61 | 必須
Component.Microsoft.VisualStudio.LiveShare | Live Share | 1.0.4062 | 推奨
Microsoft.ComponentGroup.Blend | Blend for Visual Studio | 16.0.28315.86 | 推奨
Microsoft.ComponentGroup.ClickOnce.Publish | .NET の ClickOnce 発行  | 16.10.31303.231 | 推奨
Microsoft.Net.Component.4.5.1.TargetingPack | .NET Framework 4.5.1 Targeting Pack | 16.0.28517.75 | 推奨
Microsoft.Net.Component.4.5.2.TargetingPack | .NET Framework 4.5.2 Targeting Pack | 16.0.28517.75 | 推奨
Microsoft.Net.Component.4.5.TargetingPack | .NET Framework 4.5 Targeting Pack | 16.0.28517.75 | 推奨
Microsoft.Net.Component.4.6.1.TargetingPack | .NET Framework 4.6.1 Targeting Pack | 16.0.28517.75 | 推奨
Microsoft.Net.Component.4.6.TargetingPack | .NET Framework 4.6 Targeting Pack | 16.0.28517.75 | 推奨
Microsoft.Net.Component.4.TargetingPack | .NET Framework 4 Targeting Pack | 16.0.28517.75 | 推奨
Microsoft.Net.ComponentGroup.TargetingPacks.Common | .NET Framework 4 – 4.6 開発ツール | 16.0.28516.191 | 推奨
Microsoft.NetCore.Component.DevelopmentTools | .NET 開発ツール | 16.10.31303.231 | 推奨
Microsoft.VisualStudio.Component.Common.Azure.Tools | 接続および発行ツール | 16.4.29409.204 | 推奨
Microsoft.VisualStudio.Component.Debugger.JustInTime | Just-In-Time デバッガー | 16.0.28517.75 | 推奨
Microsoft.VisualStudio.Component.DiagnosticTools | .NET プロファイル ツール | 16.10.31205.252 | 推奨
Microsoft.VisualStudio.Component.DotNetModelBuilder | ML.NET モデル ビルダー (プレビュー) | 16.10.31205.252 | 推奨
Microsoft.VisualStudio.Component.EntityFramework | Entity Framework 6 Tools | 16.0.28315.86 | 推奨
Microsoft.VisualStudio.Component.FSharp | F# 言語サポート | 16.0.28315.86 | 推奨
Microsoft.VisualStudio.Component.IntelliCode | IntelliCode | 16.10.31305.154 | 推奨
Microsoft.VisualStudio.Component.JavaScript.TypeScript | JavaScript および TypeScript の言語サポート | 16.10.31303.231 | 推奨
Microsoft.VisualStudio.Component.NuGet | NuGet パッケージ マネージャー | 16.1.28829.92 | 推奨
Microsoft.VisualStudio.Component.TypeScript.4.2 | TypeScript 4.2 SDK | 16.0.31303.231 | 推奨
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | ASP.NET と Web 開発 | 16.10.31205.180 | 推奨
Component.Dotfuscator | PreEmptive Protection - Dotfuscator | 16.10.31205.252 | Optional
Component.Microsoft.VisualStudio.RazorExtension | Razor 言語サービス | 16.10.31205.252 | Optional
Component.Microsoft.Web.LibraryManager | ライブラリ マネージャー | 16.10.31205.180 | 省略可能
Component.Microsoft.WebTools.BrowserLink.WebLivePreview | Web ライブ プレビュー | 0.7.22.39845 | Optional
Microsoft.Net.Component.4.6.2.TargetingPack | .NET Framework 4.6.2 Targeting Pack | 16.0.28517.75 | Optional
Microsoft.Net.Component.4.7.1.TargetingPack | .NET Framework 4.7.1 Targeting Pack | 16.10.31205.252 | Optional
Microsoft.Net.Component.4.7.TargetingPack | .NET Framework 4.7 Targeting Pack | 16.10.31205.252 | Optional
Microsoft.Net.Component.4.8.TargetingPack | .NET Framework 4.8 Targeting Pack | 16.4.29313.120 | Optional
Microsoft.Net.ComponentGroup.4.6.1.DeveloperTools | .NET Framework 4.6.1 開発ツール | 16.3.29207.166 | Optional
Microsoft.Net.ComponentGroup.4.6.2.DeveloperTools | .NET Framework 4.6.2 開発ツール | 16.3.29207.166 | Optional
Microsoft.Net.ComponentGroup.4.7.1.DeveloperTools | .NET Framework 4.7.1 開発ツール | 16.3.29207.166 | Optional
Microsoft.Net.ComponentGroup.4.7.DeveloperTools | .NET Framework 4.7 開発ツール | 16.3.29207.166 | Optional
Microsoft.Net.ComponentGroup.4.8.DeveloperTools | .NET Framework 4.8 開発ツール | 16.4.29318.151 | Optional
Microsoft.Net.Core.Component.SDK.2.1 | .NET Core 2.1 ランタイム (LTS) | 16.10.31320.204 | Optional
Microsoft.VisualStudio.Component.DockerTools | コンテナー開発ツール | 16.4.29409.204 | Optional
Microsoft.VisualStudio.Component.FSharp.Desktop | F# デスクトップ言語のサポート | 16.0.28315.86 | Optional
Microsoft.VisualStudio.Component.IISExpress | IIS Express  | 16.0.28315.86 | Optional
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | JavaScript 診断 | 16.0.28517.75 | Optional
Microsoft.VisualStudio.Component.MSODBC.SQL | SQL Server ODBC Driver | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.MSSQL.CMDLnUtils | SQL Server コマンド ライン ユーティリティ | 16.0.28707.177 | Optional
Microsoft.VisualStudio.Component.PortableLibrary | .NET ポータブル ライブラリ Targeting Pack | 16.10.31205.252 | Optional
Microsoft.VisualStudio.Component.SQL.ADAL | SQL ADAL ランタイム | 16.0.28517.75 | Optional
Microsoft.VisualStudio.Component.SQL.DataSources | SQL Server サポートのためのデータ ソース | 16.0.28315.86 | Optional
Microsoft.VisualStudio.Component.SQL.LocalDB.Runtime | SQL Server Express 2016 LocalDB | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.SQL.SSDT | SQL Server Data Tools | 16.3.29207.166 | Optional
Microsoft.VisualStudio.Component.Wcf.Tooling | Windows Communication Foundation | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.Web | ASP.NET と Web の開発ツール | 16.10.31205.252 | Optional
Microsoft.VisualStudio.ComponentGroup.MSIX.Packaging | MSIX パッケージ化ツール | 16.10.31205.180 | Optional
Microsoft.VisualStudio.ComponentGroup.Web | ASP.NET と Web の開発ツールの前提条件 | 16.10.31205.180 | Optional

## <a name="game-development-with-unity"></a>Unity でのゲーム開発

**ID:** Microsoft.VisualStudio.Workload.ManagedGame

**説明:** 強力なクロスプラットフォーム開発環境である Unity を使って、2D および 3D ゲームを作成します。

### <a name="components-included-by-this-workload"></a>このワークロードに含まれるコンポーネント

コンポーネント ID | 名前 | バージョン | 依存関係の種類
--- | --- | --- | ---
Microsoft.Net.Component.3.5.DeveloperTools | .NET Framework 3.5 開発ツール | 16.0.28517.75 | 必須
Microsoft.Net.Component.4.7.1.TargetingPack | .NET Framework 4.7.1 Targeting Pack | 16.10.31205.252 | 必須
Microsoft.VisualStudio.Component.NuGet | NuGet パッケージ マネージャー | 16.1.28829.92 | 必須
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# および Visual Basic Roslyn コンパイラ | 16.0.28714.129 | 必須
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# および Visual Basic | 16.10.31205.252 | 必須
Microsoft.VisualStudio.Component.Unity | Visual Studio Tools for Unity | 16.0.28315.86 | 必須
Component.UnityEngine.x64 | Unity Hub | 16.10.31205.252 | 推奨
Component.UnityEngine.x86 | Unity 5.6 32 ビット エディター | 16.1.28811.260 | 推奨

## <a name="linux-development-with-c"></a>C++ による Linux 開発

**ID:** Microsoft.VisualStudio.Workload.NativeCrossPlat

**説明:** Linux 環境で実行するアプリケーションを作成およびデバッグします。

### <a name="components-included-by-this-workload"></a>このワークロードに含まれるコンポーネント

コンポーネント ID | 名前 | バージョン | 依存関係の種類
--- | --- | --- | ---
Component.MDD.Linux | Linux 開発用 C++ | 16.5.29515.121 | 必須
Microsoft.VisualStudio.Component.VC.CoreIde | C++ コア機能 | 16.10.31205.252 | 必須
Component.Linux.CMake | Linux 用の C++ CMake ツール | 16.2.29003.222 | 推奨
Microsoft.VisualStudio.Component.IntelliCode | IntelliCode | 16.10.31305.154 | 推奨
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | ASP.NET と Web 開発 | 16.10.31205.180 | 推奨
Component.MDD.Linux.GCC.arm | 埋め込み開発ツールと IoT 開発ツール | 16.5.29515.121 | Optional

## <a name="desktop-development-with-c"></a>C++ によるデスクトップ開発

**ID:** Microsoft.VisualStudio.Workload.NativeDesktop

**説明:** MSVC、Clang、CMake、または MSBuild など、自分で選択したツールを利用し、Windows 向けの C++ アプリをビルドします。

### <a name="components-included-by-this-workload"></a>このワークロードに含まれるコンポーネント

コンポーネント ID | 名前 | バージョン | 依存関係の種類
--- | --- | --- | ---
Microsoft.Component.MSBuild | MSBuild | 16.5.29515.121 | 必須
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# および Visual Basic Roslyn コンパイラ | 16.0.28714.129 | 必須
Microsoft.VisualStudio.Component.TextTemplating | テキスト テンプレート変換 | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.VC.CoreIde | C++ コア機能 | 16.10.31205.252 | 必須
Microsoft.VisualStudio.Component.VC.Redist.14.Latest | C++ 2019 再頒布可能パッケージの更新プログラム | 16.5.29515.121 | 必須
Microsoft.VisualStudio.ComponentGroup.NativeDesktop.Core | C++ コア デスクトップ機能 | 16.2.29012.281 | 必須
Component.Microsoft.VisualStudio.LiveShare | Live Share | 1.0.4062 | 推奨
Microsoft.VisualStudio.Component.Debugger.JustInTime | Just-In-Time デバッガー | 16.0.28517.75 | 推奨
Microsoft.VisualStudio.Component.Graphics.Tools | DirectX 用グラフィックス デバッガーおよび GPU プロファイラー | 16.0.28625.61 | 推奨
Microsoft.VisualStudio.Component.IntelliCode | IntelliCode | 16.10.31305.154 | 推奨
Microsoft.VisualStudio.Component.JavaScript.TypeScript | JavaScript および TypeScript の言語サポート | 16.10.31303.231 | 推奨
Microsoft.VisualStudio.Component.NuGet | NuGet パッケージ マネージャー | 16.1.28829.92 | 推奨
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# および Visual Basic | 16.10.31205.252 | 推奨
Microsoft.VisualStudio.Component.TypeScript.4.2 | TypeScript 4.2 SDK | 16.0.31303.231 | 推奨
Microsoft.VisualStudio.Component.VC.ASAN | C++ AddressSanitizer | 16.10.31205.252 | 推奨
Microsoft.VisualStudio.Component.VC.ATL | 最新 v142 ビルド ツールの C++ ATL (x86 & x64) | 16.4.29313.120 | 推奨
Microsoft.VisualStudio.Component.VC.CMake.Project | Windows 用 C++ CMake ツール | 16.3.29103.31 | 推奨
Microsoft.VisualStudio.Component.VC.DiagnosticTools | C++ のプロファイル ツール | 16.5.29515.121 | 推奨
Microsoft.VisualStudio.Component.VC.TestAdapterForBoostTest | Test Adapter for Boost.Test | 16.0.28517.75 | 推奨
Microsoft.VisualStudio.Component.VC.TestAdapterForGoogleTest | Test Adapter for Google Test | 16.0.28517.75 | 推奨
Microsoft.VisualStudio.Component.VC.Tools.x86.x64 | MSVC v142 - VS 2019 C++ x64/x86 ビルド ツール (最新) | 16.10.31205.252 | 推奨
Microsoft.VisualStudio.Component.Windows10SDK.19041 | Windows 10 SDK (10.0.19041.0) | 16.10.31205.252 | 推奨
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | ASP.NET と Web 開発 | 16.10.31205.180 | 推奨
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions.CMake | JSON エディター | 16.10.31205.180 | 推奨
Component.Incredibuild | IncrediBuild - ビルドのアクセラレーション | 16.10.31205.252 | Optional
Component.IncredibuildMenu | IncrediBuildMenu | 1.5.0.13 | Optional
Microsoft.Component.VC.Runtime.UCRTSDK | Windows Universal CRT SDK | 16.0.28625.61 | Optional
Microsoft.Net.Component.4.6.1.TargetingPack | .NET Framework 4.6.1 Targeting Pack | 16.0.28517.75 | Optional
Microsoft.Net.Component.4.8.SDK | .NET Framework 4.8 SDK | 16.4.29313.120 | Optional
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | JavaScript 診断 | 16.0.28517.75 | Optional
Microsoft.VisualStudio.Component.VC.140 | MSVC v140 - VS 2015 C++ ビルド ツール (v14.00) | 16.10.31205.252 | Optional
Microsoft.VisualStudio.Component.VC.ATLMFC | 最新 v142 ビルド ツールの C++ MFC (x86 & x64) | 16.4.29313.120 | Optional
Microsoft.VisualStudio.Component.VC.CLI.Support | v142 ビルド ツール用 C++/CLI サポート (最新) | 16.10.31205.252 | Optional
Microsoft.VisualStudio.Component.VC.Llvm.Clang | Windows 用 C++ Clang コンパイラ (11.0.0) | 16.10.31205.252 | Optional
Microsoft.VisualStudio.Component.VC.Llvm.ClangToolset | v142 ビルド ツールの C++ Clang-cl (x64/x86) | 16.3.29207.166 | Optional
Microsoft.VisualStudio.Component.VC.Modules.x86.x64 | v142 ビルド ツール用の C++ モジュール (x64/x86 – 実験) | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.VC.Tools.ARM64 | MSVC v142 - VS 2019 C++ ARM64 ビルド ツール (最新) | 16.10.31205.252 | Optional
Microsoft.VisualStudio.Component.VC.v141.x86.x64 | MSVC v141 - VS 2017 C++ x64/x86 ビルド ツール (v14.16) | 16.10.31205.252 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.16299 | Windows 10 SDK (10.0.16299.0) | 16.10.31205.252 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.17134 | Windows 10 SDK (10.0.17134.0) | 16.10.31205.252 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.17763 | Windows 10 SDK (10.0.17763.0) | 16.0.28517.75 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.18362 | Windows 10 SDK (10.0.18362.0) | 16.1.28829.92 | Optional
Microsoft.VisualStudio.ComponentGroup.NativeDesktop.Llvm.Clang | Windows 用 C++ Clang ツール (11.0.0 - x64/x86) | 16.10.31205.180 | Optional

## <a name="game-development-with-c"></a>C++ によるゲーム開発

**ID:** Microsoft.VisualStudio.Workload.NativeGame

**説明:** C++ を最大限に活用して、DirectX、Unreal、Cocos2d を利用するプロフェッショナルなゲームを構築します。

### <a name="components-included-by-this-workload"></a>このワークロードに含まれるコンポーネント

コンポーネント ID | 名前 | バージョン | 依存関係の種類
--- | --- | --- | ---
Microsoft.VisualStudio.Component.VC.CoreIde | C++ コア機能 | 16.10.31205.252 | 必須
Microsoft.VisualStudio.Component.VC.Redist.14.Latest | C++ 2019 再頒布可能パッケージの更新プログラム | 16.5.29515.121 | 必須
Microsoft.VisualStudio.Component.VC.Tools.x86.x64 | MSVC v142 - VS 2019 C++ x64/x86 ビルド ツール (最新) | 16.10.31205.252 | 必須
Microsoft.VisualStudio.Component.Windows10SDK | Windows ユニバーサル C ランタイム | 16.4.29409.204 | 必須
Microsoft.VisualStudio.Component.Graphics.Tools | DirectX 用グラフィックス デバッガーおよび GPU プロファイラー | 16.0.28625.61 | 推奨
Microsoft.VisualStudio.Component.IntelliCode | IntelliCode | 16.10.31305.154 | 推奨
Microsoft.VisualStudio.Component.VC.ASAN | C++ AddressSanitizer | 16.10.31205.252 | 推奨
Microsoft.VisualStudio.Component.VC.DiagnosticTools | C++ のプロファイル ツール | 16.5.29515.121 | 推奨
Microsoft.VisualStudio.Component.Windows10SDK.19041 | Windows 10 SDK (10.0.19041.0) | 16.10.31205.252 | 推奨
Component.Android.NDK.R16B | Android NDK (R16B) | 16.10.31320.204 | Optional
Component.Android.SDK25.Private | Android SDK セットアップ (API レベル 25) (C++ を使用したモバイル開発のためにローカルにインストール) | 16.0.28625.61 | Optional
Component.Ant | Apache Ant (1.9.3) | 1.9.3.8 | Optional
Component.Cocos | Cocos | 16.0.28315.86 | Optional
Component.Incredibuild | IncrediBuild - ビルドのアクセラレーション | 16.10.31205.252 | Optional
Component.IncredibuildMenu | IncrediBuildMenu | 1.5.0.13 | Optional
Component.MDD.Android | C++ Android 開発ツール | 16.0.28517.75 | Optional
Component.OpenJDK | OpenJDK (Microsoft ディストリビューション) | 16.10.31303.311 | Optional
Component.Unreal | Unreal Engine のインストーラー | 16.1.28810.153 | Optional
Component.Unreal.Android | Unreal Engine 用の Android IDE サポート | 16.1.28810.153 | Optional
Microsoft.Net.Component.4.5.1.TargetingPack | .NET Framework 4.5.1 Targeting Pack | 16.0.28517.75 | Optional
Microsoft.Net.Component.4.5.2.TargetingPack | .NET Framework 4.5.2 Targeting Pack | 16.0.28517.75 | Optional
Microsoft.Net.Component.4.5.TargetingPack | .NET Framework 4.5 Targeting Pack | 16.0.28517.75 | Optional
Microsoft.Net.Component.4.6.2.TargetingPack | .NET Framework 4.6.2 Targeting Pack | 16.0.28517.75 | Optional
Microsoft.Net.Component.4.6.TargetingPack | .NET Framework 4.6 Targeting Pack | 16.0.28517.75 | Optional
Microsoft.Net.Component.4.7.2.TargetingPack | .NET Framework 4.7.2 Targeting Pack | 16.10.31205.252 | Optional
Microsoft.Net.Component.4.8.SDK | .NET Framework 4.8 SDK | 16.4.29313.120 | Optional
Microsoft.Net.Component.4.TargetingPack | .NET Framework 4 Targeting Pack | 16.0.28517.75 | Optional
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | .NET Framework 4.7.2 開発ツール | 16.3.29207.166 | Optional
Microsoft.Net.ComponentGroup.TargetingPacks.Common | .NET Framework 4 – 4.6 開発ツール | 16.0.28516.191 | Optional
Microsoft.VisualStudio.Component.NuGet.BuildTools | NuGet ターゲットとビルド タスク | 16.1.28829.92 | Optional
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# および Visual Basic Roslyn コンパイラ | 16.0.28714.129 | Optional
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# および Visual Basic | 16.10.31205.252 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.16299 | Windows 10 SDK (10.0.16299.0) | 16.10.31205.252 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.17134 | Windows 10 SDK (10.0.17134.0) | 16.10.31205.252 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.17763 | Windows 10 SDK (10.0.17763.0) | 16.0.28517.75 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.18362 | Windows 10 SDK (10.0.18362.0) | 16.1.28829.92 | Optional

## <a name="mobile-development-with-c"></a>C++ でのモバイル開発

**ID:** Microsoft.VisualStudio.Workload.NativeMobile

**説明:** iOS、Android、Windows 向けのクロスプラットフォーム アプリケーションを、C++ を使って構築します。

### <a name="components-included-by-this-workload"></a>このワークロードに含まれるコンポーネント

コンポーネント ID | 名前 | バージョン | 依存関係の種類
--- | --- | --- | ---
Component.Android.SDK25.Private | Android SDK セットアップ (API レベル 25) (C++ を使用したモバイル開発のためにローカルにインストール) | 16.0.28625.61 | 必須
Component.OpenJDK | OpenJDK (Microsoft ディストリビューション) | 16.10.31303.311 | 必須
Microsoft.VisualStudio.Component.VC.CoreIde | C++ コア機能 | 16.10.31205.252 | 必須
Component.Android.NDK.R16B | Android NDK (R16B) | 16.10.31320.204 | 推奨
Component.Ant | Apache Ant (1.9.3) | 1.9.3.8 | 推奨
Component.MDD.Android | C++ Android 開発ツール | 16.0.28517.75 | 推奨
Microsoft.VisualStudio.Component.IntelliCode | IntelliCode | 16.10.31305.154 | 推奨
Component.Android.NDK.R16B_3264 | Android NDK (R16B) (32 ビット) | 16.10.31320.204 | Optional
Component.Google.Android.Emulator.API25.Private | Google Android Emulator (API レベル 25) (ローカル インストール) | 16.1.28810.153 | Optional
Component.HAXM.Private | Intel Hardware Accelerated Execution Manager (HAXM) (ローカル インストール) | 16.0.28528.71 | Optional
Component.Incredibuild | IncrediBuild - ビルドのアクセラレーション | 16.10.31205.252 | Optional
Component.IncredibuildMenu | IncrediBuildMenu | 1.5.0.13 | Optional
Component.MDD.IOS | C++ iOS 開発ツール | 16.0.28517.75 | Optional

## <a name="net-cross-platform-development"></a>.NET クロスプラットフォーム開発

**ID:** Microsoft.VisualStudio.Workload.NetCoreTools

**説明:** .NET、ASP.NET Core、HTML または JavaScript、Containers (Docker サポートを含む) を使用して、クロスプラットフォーム アプリケーションをビルドします。

### <a name="components-included-by-this-workload"></a>このワークロードに含まれるコンポーネント

コンポーネント ID | 名前 | バージョン | 依存関係の種類
--- | --- | --- | ---
Component.Microsoft.VisualStudio.RazorExtension | Razor 言語サービス | 16.10.31205.252 | 必須
Component.Microsoft.Web.LibraryManager | ライブラリ マネージャー | 16.10.31205.180 | 必須
Component.Microsoft.WebTools.BrowserLink.WebLivePreview | Web ライブ プレビュー | 0.7.22.39845 | 必須
Microsoft.Component.MSBuild | MSBuild | 16.5.29515.121 | 必須
Microsoft.ComponentGroup.ClickOnce.Publish | .NET の ClickOnce 発行  | 16.10.31303.231 | 必須
Microsoft.Net.Component.4.5.2.TargetingPack | .NET Framework 4.5.2 Targeting Pack | 16.0.28517.75 | 必須
Microsoft.Net.Component.4.5.TargetingPack | .NET Framework 4.5 Targeting Pack | 16.0.28517.75 | 必須
Microsoft.Net.Component.4.6.1.TargetingPack | .NET Framework 4.6.1 Targeting Pack | 16.0.28517.75 | 必須
Microsoft.Net.Component.4.7.2.TargetingPack | .NET Framework 4.7.2 Targeting Pack | 16.10.31205.252 | 必須
Microsoft.Net.Component.4.8.SDK | .NET Framework 4.8 SDK | 16.4.29313.120 | 必須
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | .NET Framework 4.7.2 開発ツール | 16.3.29207.166 | 必須
Microsoft.NetCore.Component.DevelopmentTools | .NET 開発ツール | 16.10.31303.231 | 必須
Microsoft.NetCore.Component.Runtime.3.1 | .NET Core 3.1 ランタイム (LTS) | 16.10.31320.204 | 必須
Microsoft.NetCore.Component.Runtime.5.0 | .NET 5.0 ランタイム | 16.10.31320.204 | 必須
Microsoft.NetCore.Component.SDK | .NET SDK | 16.10.31320.204 | 必須
Microsoft.NetCore.Component.Web | .NET 開発ツール | 16.10.31303.231 | 必須
Microsoft.VisualStudio.Component.Common.Azure.Tools | 接続および発行ツール | 16.4.29409.204 | 必須
Microsoft.VisualStudio.Component.DockerTools | コンテナー開発ツール | 16.4.29409.204 | 必須
Microsoft.VisualStudio.Component.FSharp | F# 言語サポート | 16.0.28315.86 | 必須
Microsoft.VisualStudio.Component.FSharp.WebTemplates | Web プロジェクト用の F# 言語サポート | 16.3.29207.166 | 必須
Microsoft.VisualStudio.Component.IISExpress | IIS Express  | 16.0.28315.86 | 必須
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | JavaScript 診断 | 16.0.28517.75 | 必須
Microsoft.VisualStudio.Component.JavaScript.TypeScript | JavaScript および TypeScript の言語サポート | 16.10.31303.231 | 必須
Microsoft.VisualStudio.Component.ManagedDesktop.Core | Managed Desktop Workload コア | 16.4.29318.151 | 必須
Microsoft.VisualStudio.Component.MSODBC.SQL | SQL Server ODBC Driver | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.MSSQL.CMDLnUtils | SQL Server コマンド ライン ユーティリティ | 16.0.28707.177 | 必須
Microsoft.VisualStudio.Component.NuGet | NuGet パッケージ マネージャー | 16.1.28829.92 | 必須
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# および Visual Basic Roslyn コンパイラ | 16.0.28714.129 | 必須
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# および Visual Basic | 16.10.31205.252 | 必須
Microsoft.VisualStudio.Component.SQL.ADAL | SQL ADAL ランタイム | 16.0.28517.75 | 必須
Microsoft.VisualStudio.Component.SQL.CLR | SQL Server の CLR データ型 | 16.0.28315.86 | 必須
Microsoft.VisualStudio.Component.SQL.DataSources | SQL Server サポートのためのデータ ソース | 16.0.28315.86 | 必須
Microsoft.VisualStudio.Component.SQL.LocalDB.Runtime | SQL Server Express 2016 LocalDB | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.SQL.SSDT | SQL Server Data Tools | 16.3.29207.166 | 必須
Microsoft.VisualStudio.Component.TextTemplating | テキスト テンプレート変換 | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.TypeScript.4.2 | TypeScript 4.2 SDK | 16.0.31303.231 | 必須
Microsoft.VisualStudio.ComponentGroup.Web | ASP.NET と Web の開発ツールの前提条件 | 16.10.31205.180 | 必須
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | ASP.NET と Web 開発 | 16.10.31205.180 | 必須
Component.Microsoft.VisualStudio.LiveShare | Live Share | 1.0.4062 | 推奨
Component.Microsoft.VisualStudio.Web.AzureFunctions | Azure WebJobs ツール | 16.10.31205.252 | 推奨
Microsoft.VisualStudio.Component.AppInsights.Tools | Developer Analytics Tools | 16.5.29515.121 | 推奨
Microsoft.VisualStudio.Component.Azure.AuthoringTools | Azure Authoring Tools | 16.0.28625.61 | 推奨
Microsoft.VisualStudio.Component.Azure.ClientLibs | .NET 用 Azure ライブラリ | 16.0.28315.86 | 推奨
Microsoft.VisualStudio.Component.Azure.Compute.Emulator | Azure コンピューティング エミュレーター | 16.10.31205.252 | 推奨
Microsoft.VisualStudio.Component.Azure.Storage.Emulator | Azure Storage エミュレーター | 16.4.29313.120 | 推奨
Microsoft.VisualStudio.Component.CloudExplorer | Cloud Explorer | 16.0.28625.61 | 推奨
Microsoft.VisualStudio.Component.Debugger.JustInTime | Just-In-Time デバッガー | 16.0.28517.75 | 推奨
Microsoft.VisualStudio.Component.DiagnosticTools | .NET プロファイル ツール | 16.10.31205.252 | 推奨
Microsoft.VisualStudio.Component.DotNetModelBuilder | ML.NET モデル ビルダー (プレビュー) | 16.10.31205.252 | 推奨
Microsoft.VisualStudio.Component.IntelliCode | IntelliCode | 16.10.31305.154 | 推奨
Microsoft.VisualStudio.Component.Web | ASP.NET と Web の開発ツール | 16.10.31205.252 | 推奨
Microsoft.VisualStudio.Component.WebDeploy | Web 配置 | 16.0.28517.75 | 推奨
Microsoft.VisualStudio.Component.WslDebugging | .NET での WSL 2 を使用したデバッグ | 16.10.31303.231 | 推奨
Microsoft.VisualStudio.ComponentGroup.AzureFunctions | Azure WebJobs ツール | 16.10.31205.180 | 推奨
Microsoft.VisualStudio.ComponentGroup.Web.CloudTools | Web 開発用クラウド ツール | 16.10.31205.180 | 推奨
Microsoft.Net.Core.Component.SDK.2.1 | .NET Core 2.1 ランタイム (LTS) | 16.10.31320.204 | Optional
Microsoft.VisualStudio.ComponentGroup.IISDevelopment | 開発時の IIS サポート | 16.10.31205.180 | Optional
Microsoft.VisualStudio.ComponentGroup.MSIX.Packaging | MSIX パッケージ化ツール | 16.10.31205.180 | Optional

## <a name="mobile-development-with-net"></a>.NET によるモバイル開発

**ID:** Microsoft.VisualStudio.Workload.NetCrossPlat

**説明:** iOS、Android、Windows 向けのクロスプラットフォーム アプリケーションを、Xamarin を使って構築します。

### <a name="components-included-by-this-workload"></a>このワークロードに含まれるコンポーネント

コンポーネント ID | 名前 | バージョン | 依存関係の種類
--- | --- | --- | ---
Component.OpenJDK | OpenJDK (Microsoft ディストリビューション) | 16.10.31303.311 | 必須
Component.Xamarin | Xamarin | 16.10.31205.252 | 必須
Component.Xamarin.RemotedSimulator | Xamarin Remoted Simulator | 16.10.31205.252 | 必須
Microsoft.Component.MSBuild | MSBuild | 16.5.29515.121 | 必須
Microsoft.ComponentGroup.ClickOnce.Publish | .NET の ClickOnce 発行  | 16.10.31303.231 | 必須
Microsoft.Net.Component.4.6.1.TargetingPack | .NET Framework 4.6.1 Targeting Pack | 16.0.28517.75 | 必須
Microsoft.Net.Component.4.7.2.TargetingPack | .NET Framework 4.7.2 Targeting Pack | 16.10.31205.252 | 必須
Microsoft.Net.Component.4.8.SDK | .NET Framework 4.8 SDK | 16.4.29313.120 | 必須
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | .NET Framework 4.7.2 開発ツール | 16.3.29207.166 | 必須
Microsoft.NetCore.Component.DevelopmentTools | .NET 開発ツール | 16.10.31303.231 | 必須
Microsoft.NetCore.Component.Runtime.3.1 | .NET Core 3.1 ランタイム (LTS) | 16.10.31320.204 | 必須
Microsoft.NetCore.Component.Runtime.5.0 | .NET 5.0 ランタイム | 16.10.31320.204 | 必須
Microsoft.NetCore.Component.SDK | .NET SDK | 16.10.31320.204 | 必須
Microsoft.VisualStudio.Component.FSharp | F# 言語サポート | 16.0.28315.86 | 必須
Microsoft.VisualStudio.Component.Merq | Xamarin の一般的な内部ツール | 16.2.29012.281 | 必須
Microsoft.VisualStudio.Component.MonoDebugger | Mono デバッガー | 16.0.28517.75 | 必須
Microsoft.VisualStudio.Component.NuGet | NuGet パッケージ マネージャー | 16.1.28829.92 | 必須
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# および Visual Basic Roslyn コンパイラ | 16.0.28714.129 | 必須
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# および Visual Basic | 16.10.31205.252 | 必須
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions.TemplateEngine | ASP.NET テンプレート エンジン | 16.10.31205.180 | 必須
Component.Android.SDK30 | Android SDK セットアップ (API レベル 30) | 16.10.31205.252 | 推奨
Microsoft.VisualStudio.Component.IntelliCode | IntelliCode | 16.10.31305.154 | 推奨

## <a name="aspnet-and-web-development"></a>ASP.NET と Web 開発

**ID:** Microsoft.VisualStudio.Workload.NetWeb

**説明:** ASP.NET Core、ASP.NET、HTML/JavaScript、コンテナー (Docker サポートなど) を使用して、Web アプリケーションをビルドします。

### <a name="components-included-by-this-workload"></a>このワークロードに含まれるコンポーネント

コンポーネント ID | 名前 | バージョン | 依存関係の種類
--- | --- | --- | ---
Component.Microsoft.VisualStudio.RazorExtension | Razor 言語サービス | 16.10.31205.252 | 必須
Component.Microsoft.Web.LibraryManager | ライブラリ マネージャー | 16.10.31205.180 | 必須
Component.Microsoft.WebTools.BrowserLink.WebLivePreview | Web ライブ プレビュー | 0.7.22.39845 | 必須
Microsoft.Component.MSBuild | MSBuild | 16.5.29515.121 | 必須
Microsoft.ComponentGroup.ClickOnce.Publish | .NET の ClickOnce 発行  | 16.10.31303.231 | 必須
Microsoft.Net.Component.4.5.2.TargetingPack | .NET Framework 4.5.2 Targeting Pack | 16.0.28517.75 | 必須
Microsoft.Net.Component.4.5.TargetingPack | .NET Framework 4.5 Targeting Pack | 16.0.28517.75 | 必須
Microsoft.Net.Component.4.6.1.TargetingPack | .NET Framework 4.6.1 Targeting Pack | 16.0.28517.75 | 必須
Microsoft.Net.Component.4.7.2.TargetingPack | .NET Framework 4.7.2 Targeting Pack | 16.10.31205.252 | 必須
Microsoft.Net.Component.4.8.SDK | .NET Framework 4.8 SDK | 16.4.29313.120 | 必須
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | .NET Framework 4.7.2 開発ツール | 16.3.29207.166 | 必須
Microsoft.NetCore.Component.DevelopmentTools | .NET 開発ツール | 16.10.31303.231 | 必須
Microsoft.NetCore.Component.Runtime.3.1 | .NET Core 3.1 ランタイム (LTS) | 16.10.31320.204 | 必須
Microsoft.NetCore.Component.Runtime.5.0 | .NET 5.0 ランタイム | 16.10.31320.204 | 必須
Microsoft.NetCore.Component.SDK | .NET SDK | 16.10.31320.204 | 必須
Microsoft.NetCore.Component.Web | .NET 開発ツール | 16.10.31303.231 | 必須
Microsoft.VisualStudio.Component.Common.Azure.Tools | 接続および発行ツール | 16.4.29409.204 | 必須
Microsoft.VisualStudio.Component.DockerTools | コンテナー開発ツール | 16.4.29409.204 | 必須
Microsoft.VisualStudio.Component.FSharp | F# 言語サポート | 16.0.28315.86 | 必須
Microsoft.VisualStudio.Component.FSharp.WebTemplates | Web プロジェクト用の F# 言語サポート | 16.3.29207.166 | 必須
Microsoft.VisualStudio.Component.IISExpress | IIS Express  | 16.0.28315.86 | 必須
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | JavaScript 診断 | 16.0.28517.75 | 必須
Microsoft.VisualStudio.Component.JavaScript.TypeScript | JavaScript および TypeScript の言語サポート | 16.10.31303.231 | 必須
Microsoft.VisualStudio.Component.ManagedDesktop.Core | Managed Desktop Workload コア | 16.4.29318.151 | 必須
Microsoft.VisualStudio.Component.MSODBC.SQL | SQL Server ODBC Driver | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.MSSQL.CMDLnUtils | SQL Server コマンド ライン ユーティリティ | 16.0.28707.177 | 必須
Microsoft.VisualStudio.Component.NuGet | NuGet パッケージ マネージャー | 16.1.28829.92 | 必須
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# および Visual Basic Roslyn コンパイラ | 16.0.28714.129 | 必須
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# および Visual Basic | 16.10.31205.252 | 必須
Microsoft.VisualStudio.Component.SQL.ADAL | SQL ADAL ランタイム | 16.0.28517.75 | 必須
Microsoft.VisualStudio.Component.SQL.CLR | SQL Server の CLR データ型 | 16.0.28315.86 | 必須
Microsoft.VisualStudio.Component.SQL.DataSources | SQL Server サポートのためのデータ ソース | 16.0.28315.86 | 必須
Microsoft.VisualStudio.Component.SQL.LocalDB.Runtime | SQL Server Express 2016 LocalDB | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.SQL.SSDT | SQL Server Data Tools | 16.3.29207.166 | 必須
Microsoft.VisualStudio.Component.TextTemplating | テキスト テンプレート変換 | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.TypeScript.4.2 | TypeScript 4.2 SDK | 16.0.31303.231 | 必須
Microsoft.VisualStudio.Component.Web | ASP.NET と Web の開発ツール | 16.10.31205.252 | 必須
Microsoft.VisualStudio.ComponentGroup.Web | ASP.NET と Web の開発ツールの前提条件 | 16.10.31205.180 | 必須
Microsoft.VisualStudio.ComponentGroup.Web.Client | ASP.NET と Web の開発ツール | 16.10.31205.180 | 必須
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | ASP.NET と Web 開発 | 16.10.31205.180 | 必須
Component.Microsoft.VisualStudio.LiveShare | Live Share | 1.0.4062 | 推奨
Component.Microsoft.VisualStudio.Web.AzureFunctions | Azure WebJobs ツール | 16.10.31205.252 | 推奨
Microsoft.Net.Component.4.5.1.TargetingPack | .NET Framework 4.5.1 Targeting Pack | 16.0.28517.75 | 推奨
Microsoft.Net.Component.4.6.TargetingPack | .NET Framework 4.6 Targeting Pack | 16.0.28517.75 | 推奨
Microsoft.Net.Component.4.TargetingPack | .NET Framework 4 Targeting Pack | 16.0.28517.75 | 推奨
Microsoft.Net.ComponentGroup.TargetingPacks.Common | .NET Framework 4 – 4.6 開発ツール | 16.0.28516.191 | 推奨
Microsoft.VisualStudio.Component.AppInsights.Tools | Developer Analytics Tools | 16.5.29515.121 | 推奨
Microsoft.VisualStudio.Component.AspNet45 | 高度な ASP.NET 機能 | 16.10.31205.252 | 推奨
Microsoft.VisualStudio.Component.Azure.AuthoringTools | Azure Authoring Tools | 16.0.28625.61 | 推奨
Microsoft.VisualStudio.Component.Azure.ClientLibs | .NET 用 Azure ライブラリ | 16.0.28315.86 | 推奨
Microsoft.VisualStudio.Component.Azure.Compute.Emulator | Azure コンピューティング エミュレーター | 16.10.31205.252 | 推奨
Microsoft.VisualStudio.Component.Azure.Storage.Emulator | Azure Storage エミュレーター | 16.4.29313.120 | 推奨
Microsoft.VisualStudio.Component.CloudExplorer | Cloud Explorer | 16.0.28625.61 | 推奨
Microsoft.VisualStudio.Component.Debugger.JustInTime | Just-In-Time デバッガー | 16.0.28517.75 | 推奨
Microsoft.VisualStudio.Component.DiagnosticTools | .NET プロファイル ツール | 16.10.31205.252 | 推奨
Microsoft.VisualStudio.Component.EntityFramework | Entity Framework 6 Tools | 16.0.28315.86 | 推奨
Microsoft.VisualStudio.Component.IntelliCode | IntelliCode | 16.10.31305.154 | 推奨
Microsoft.VisualStudio.Component.WebDeploy | Web 配置 | 16.0.28517.75 | 推奨
Microsoft.VisualStudio.Component.WslDebugging | .NET での WSL 2 を使用したデバッグ | 16.10.31303.231 | 推奨
Microsoft.VisualStudio.ComponentGroup.AzureFunctions | Azure WebJobs ツール | 16.10.31205.180 | 推奨
Microsoft.VisualStudio.ComponentGroup.Web.CloudTools | Web 開発用クラウド ツール | 16.10.31205.180 | 推奨
Microsoft.Net.Component.4.6.2.TargetingPack | .NET Framework 4.6.2 Targeting Pack | 16.0.28517.75 | Optional
Microsoft.Net.Component.4.7.1.TargetingPack | .NET Framework 4.7.1 Targeting Pack | 16.10.31205.252 | Optional
Microsoft.Net.Component.4.7.TargetingPack | .NET Framework 4.7 Targeting Pack | 16.10.31205.252 | Optional
Microsoft.Net.Component.4.8.TargetingPack | .NET Framework 4.8 Targeting Pack | 16.4.29313.120 | Optional
Microsoft.Net.ComponentGroup.4.6.1.DeveloperTools | .NET Framework 4.6.1 開発ツール | 16.3.29207.166 | Optional
Microsoft.Net.ComponentGroup.4.6.2.DeveloperTools | .NET Framework 4.6.2 開発ツール | 16.3.29207.166 | Optional
Microsoft.Net.ComponentGroup.4.7.1.DeveloperTools | .NET Framework 4.7.1 開発ツール | 16.3.29207.166 | Optional
Microsoft.Net.ComponentGroup.4.7.DeveloperTools | .NET Framework 4.7 開発ツール | 16.3.29207.166 | Optional
Microsoft.Net.ComponentGroup.4.8.DeveloperTools | .NET Framework 4.8 開発ツール | 16.4.29318.151 | Optional
Microsoft.Net.Core.Component.SDK.2.1 | .NET Core 2.1 ランタイム (LTS) | 16.10.31320.204 | Optional
Microsoft.VisualStudio.Component.Wcf.Tooling | Windows Communication Foundation | 16.0.28625.61 | Optional
Microsoft.VisualStudio.ComponentGroup.AdditionalWebProjectTemplates | 追加のプロジェクト テンプレート (以前のバージョン) | 16.10.31205.180 | Optional
Microsoft.VisualStudio.ComponentGroup.IISDevelopment | 開発時の IIS サポート | 16.10.31205.180 | Optional

## <a name="nodejs-development"></a>Node.js 開発

**ID:** Microsoft.VisualStudio.Workload.Node

**説明:** Node.js (非同期、イベント ドリブン JavaScript ランタイム) を使用してスケーラブルなネットワーク アプリケーションをビルドします。 

### <a name="components-included-by-this-workload"></a>このワークロードに含まれるコンポーネント

コンポーネント ID | 名前 | バージョン | 依存関係の種類
--- | --- | --- | ---
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | JavaScript 診断 | 16.0.28517.75 | 必須
Microsoft.VisualStudio.Component.JavaScript.TypeScript | JavaScript および TypeScript の言語サポート | 16.10.31303.231 | 必須
Microsoft.VisualStudio.Component.Node.Tools | Node.js 開発ツール | 16.5.29515.121 | 必須
Microsoft.VisualStudio.Component.TypeScript.4.2 | TypeScript 4.2 SDK | 16.0.31303.231 | 必須
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | ASP.NET と Web 開発 | 16.10.31205.180 | 必須
Component.Microsoft.VisualStudio.LiveShare | Live Share | 1.0.4062 | 推奨
Microsoft.VisualStudio.Component.Debugger.JustInTime | Just-In-Time デバッガー | 16.0.28517.75 | 推奨
Microsoft.VisualStudio.Component.IntelliCode | IntelliCode | 16.10.31305.154 | 推奨
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# および Visual Basic Roslyn コンパイラ | 16.0.28714.129 | 推奨
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# および Visual Basic | 16.10.31205.252 | 推奨
Microsoft.VisualStudio.Component.WebDeploy | Web 配置 | 16.0.28517.75 | 推奨
Microsoft.VisualStudio.Component.AppInsights.Tools | Developer Analytics Tools | 16.5.29515.121 | Optional
Microsoft.VisualStudio.Component.Common.Azure.Tools | 接続および発行ツール | 16.4.29409.204 | Optional
Microsoft.VisualStudio.Component.VC.CoreIde | C++ コア機能 | 16.10.31205.252 | Optional
Microsoft.VisualStudio.Component.VC.Tools.x86.x64 | MSVC v142 - VS 2019 C++ x64/x86 ビルド ツール (最新) | 16.10.31205.252 | Optional

## <a name="officesharepoint-development"></a>Office/SharePoint 開発

**ID:** Microsoft.VisualStudio.Workload.Office

**説明:** C#、VB、JavaScript を使用して、Office アドイン、SharePoint アドイン、SharePoint ソリューション、VSTO アドインを作成します。

### <a name="components-included-by-this-workload"></a>このワークロードに含まれるコンポーネント

コンポーネント ID | 名前 | バージョン | 依存関係の種類
--- | --- | --- | ---
Component.Microsoft.VisualStudio.RazorExtension | Razor 言語サービス | 16.10.31205.252 | 必須
Component.Microsoft.Web.LibraryManager | ライブラリ マネージャー | 16.10.31205.180 | 必須
Component.Microsoft.WebTools.BrowserLink.WebLivePreview | Web ライブ プレビュー | 0.7.22.39845 | 必須
Microsoft.Component.MSBuild | MSBuild | 16.5.29515.121 | 必須
Microsoft.Net.Component.4.5.2.TargetingPack | .NET Framework 4.5.2 Targeting Pack | 16.0.28517.75 | 必須
Microsoft.Net.Component.4.5.TargetingPack | .NET Framework 4.5 Targeting Pack | 16.0.28517.75 | 必須
Microsoft.Net.Component.4.6.1.TargetingPack | .NET Framework 4.6.1 Targeting Pack | 16.0.28517.75 | 必須
Microsoft.Net.Component.4.7.2.TargetingPack | .NET Framework 4.7.2 Targeting Pack | 16.10.31205.252 | 必須
Microsoft.Net.Component.4.8.SDK | .NET Framework 4.8 SDK | 16.4.29313.120 | 必須
Microsoft.Net.Component.4.TargetingPack | .NET Framework 4 Targeting Pack | 16.0.28517.75 | 必須
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | .NET Framework 4.7.2 開発ツール | 16.3.29207.166 | 必須
Microsoft.NetCore.Component.Runtime.3.1 | .NET Core 3.1 ランタイム (LTS) | 16.10.31320.204 | 必須
Microsoft.NetCore.Component.Runtime.5.0 | .NET 5.0 ランタイム | 16.10.31320.204 | 必須
Microsoft.NetCore.Component.SDK | .NET SDK | 16.10.31320.204 | 必須
Microsoft.VisualStudio.Component.AppInsights.Tools | Developer Analytics Tools | 16.5.29515.121 | 必須
Microsoft.VisualStudio.Component.Common.Azure.Tools | 接続および発行ツール | 16.4.29409.204 | 必須
Microsoft.VisualStudio.Component.DockerTools | コンテナー開発ツール | 16.4.29409.204 | 必須
Microsoft.VisualStudio.Component.IISExpress | IIS Express  | 16.0.28315.86 | 必須
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | JavaScript 診断 | 16.0.28517.75 | 必須
Microsoft.VisualStudio.Component.JavaScript.TypeScript | JavaScript および TypeScript の言語サポート | 16.10.31303.231 | 必須
Microsoft.VisualStudio.Component.ManagedDesktop.Core | Managed Desktop Workload コア | 16.4.29318.151 | 必須
Microsoft.VisualStudio.Component.ManagedDesktop.Prerequisites | .NET デスクトップ開発ツール | 16.10.31205.180 | 必須
Microsoft.VisualStudio.Component.MSODBC.SQL | SQL Server ODBC Driver | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.MSSQL.CMDLnUtils | SQL Server コマンド ライン ユーティリティ | 16.0.28707.177 | 必須
Microsoft.VisualStudio.Component.NuGet | NuGet パッケージ マネージャー | 16.1.28829.92 | 必須
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# および Visual Basic Roslyn コンパイラ | 16.0.28714.129 | 必須
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# および Visual Basic | 16.10.31205.252 | 必須
Microsoft.VisualStudio.Component.Sharepoint.Tools | Office Developer Tools for Visual Studio | 16.4.29409.204 | 必須
Microsoft.VisualStudio.Component.SQL.ADAL | SQL ADAL ランタイム | 16.0.28517.75 | 必須
Microsoft.VisualStudio.Component.SQL.CLR | SQL Server の CLR データ型 | 16.0.28315.86 | 必須
Microsoft.VisualStudio.Component.SQL.DataSources | SQL Server サポートのためのデータ ソース | 16.0.28315.86 | 必須
Microsoft.VisualStudio.Component.SQL.LocalDB.Runtime | SQL Server Express 2016 LocalDB | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.SQL.SSDT | SQL Server Data Tools | 16.3.29207.166 | 必須
Microsoft.VisualStudio.Component.TextTemplating | テキスト テンプレート変換 | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.TypeScript.4.2 | TypeScript 4.2 SDK | 16.0.31303.231 | 必須
Microsoft.VisualStudio.Component.Wcf.Tooling | Windows Communication Foundation | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.Web | ASP.NET と Web の開発ツール | 16.10.31205.252 | 必須
Microsoft.VisualStudio.Component.Workflow | Windows Workflow Foundation | 16.0.28315.86 | 必須
Microsoft.VisualStudio.ComponentGroup.Web | ASP.NET と Web の開発ツールの前提条件 | 16.10.31205.180 | 必須
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | ASP.NET と Web 開発 | 16.10.31205.180 | 必須
Microsoft.VisualStudio.Component.IntelliCode | IntelliCode | 16.10.31305.154 | 推奨
Microsoft.VisualStudio.Component.TeamOffice | Visual Studio Tools for Office (VSTO) | 16.4.29409.204 | 推奨
Microsoft.VisualStudio.Component.WebDeploy | Web 配置 | 16.0.28517.75 | 推奨
Microsoft.Net.Component.4.6.2.TargetingPack | .NET Framework 4.6.2 Targeting Pack | 16.0.28517.75 | Optional
Microsoft.Net.Component.4.7.1.TargetingPack | .NET Framework 4.7.1 Targeting Pack | 16.10.31205.252 | Optional
Microsoft.Net.Component.4.7.TargetingPack | .NET Framework 4.7 Targeting Pack | 16.10.31205.252 | Optional
Microsoft.Net.Component.4.8.TargetingPack | .NET Framework 4.8 Targeting Pack | 16.4.29313.120 | Optional
Microsoft.Net.ComponentGroup.4.6.1.DeveloperTools | .NET Framework 4.6.1 開発ツール | 16.3.29207.166 | Optional
Microsoft.Net.ComponentGroup.4.6.2.DeveloperTools | .NET Framework 4.6.2 開発ツール | 16.3.29207.166 | Optional
Microsoft.Net.ComponentGroup.4.7.1.DeveloperTools | .NET Framework 4.7.1 開発ツール | 16.3.29207.166 | Optional
Microsoft.Net.ComponentGroup.4.7.DeveloperTools | .NET Framework 4.7 開発ツール | 16.3.29207.166 | Optional
Microsoft.Net.ComponentGroup.4.8.DeveloperTools | .NET Framework 4.8 開発ツール | 16.4.29318.151 | Optional
Microsoft.VisualStudio.ComponentGroup.Sharepoint.WIF | Windows Identity Foundation 3.5 | 16.0.28621.142 | Optional

## <a name="python-development"></a>Python 開発

**ID:** Microsoft.VisualStudio.Workload.Python

**説明:** Python の編集、デバッグ、対話型開発、ソース管理。

### <a name="components-included-by-this-workload"></a>このワークロードに含まれるコンポーネント

コンポーネント ID | 名前 | バージョン | 依存関係の種類
--- | --- | --- | ---
Microsoft.Component.PythonTools | Python 言語サポート | 16.10.31313.127 | 必須
Component.CPython3.x64 | Python 3 64 ビット (3.7.8) | 3.7.8 | 推奨
Component.CPython2.x64 | Python 2 64 ビット (2.7.18) (サポート対象外) | 2.7.18.2 | Optional
Component.CPython2.x86 | Python 2 32 ビット (2.7.18) (サポート対象外) | 2.7.18.2 | Optional
Component.CPython3.x86 | Python 3 32 ビット (3.7.8) | 3.7.8 | Optional
Component.Microsoft.VisualStudio.LiveShare | Live Share | 1.0.4062 | Optional
Component.Microsoft.VisualStudio.RazorExtension | Razor 言語サービス | 16.10.31205.252 | Optional
Component.Microsoft.Web.LibraryManager | ライブラリ マネージャー | 16.10.31205.180 | 省略可能
Component.Microsoft.WebTools.BrowserLink.WebLivePreview | Web ライブ プレビュー | 0.7.22.39845 | オプション
Microsoft.Component.IronPython | IronPython (サポート対象外) | 16.10.31303.231 | Optional
Microsoft.Component.MSBuild | MSBuild | 16.5.29515.121 | Optional
Microsoft.Component.PythonTools.Minicondax64 | Python miniconda (サポート対象外) | 16.10.31313.127 | オプション
Microsoft.Component.PythonTools.Web | Python Web サポート | 16.10.31205.252 | Optional
Microsoft.ComponentGroup.PythonTools.NativeDevelopment | Python ネイティブ開発ツール | 16.10.31205.180 | Optional
Microsoft.Net.Component.4.5.2.TargetingPack | .NET Framework 4.5.2 Targeting Pack | 16.0.28517.75 | Optional
Microsoft.Net.Component.4.5.TargetingPack | .NET Framework 4.5 Targeting Pack | 16.0.28517.75 | Optional
Microsoft.Net.Component.4.7.2.TargetingPack | .NET Framework 4.7.2 Targeting Pack | 16.10.31205.252 | Optional
Microsoft.Net.Component.4.8.SDK | .NET Framework 4.8 SDK | 16.4.29313.120 | Optional
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | .NET Framework 4.7.2 開発ツール | 16.3.29207.166 | Optional
Microsoft.NetCore.Component.Runtime.3.1 | .NET Core 3.1 ランタイム (LTS) | 16.10.31320.204 | 省略可能
Microsoft.NetCore.Component.Runtime.5.0 | .NET 5.0 ランタイム | 16.10.31320.204 | Optional
Microsoft.NetCore.Component.SDK | .NET SDK | 16.10.31320.204 | Optional
Microsoft.VisualStudio.Component.Azure.AuthoringTools | Azure Authoring Tools | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.Azure.ClientLibs | .NET 用 Azure ライブラリ | 16.0.28315.86 | Optional
Microsoft.VisualStudio.Component.Azure.Compute.Emulator | Azure コンピューティング エミュレーター | 16.10.31205.252 | Optional
Microsoft.VisualStudio.Component.Azure.Storage.Emulator | Azure Storage エミュレーター | 16.4.29313.120 | Optional
Microsoft.VisualStudio.Component.Azure.Waverton | Azure Cloud Services コア ツール | 16.10.31205.252 | Optional
Microsoft.VisualStudio.Component.Azure.Waverton.BuildTools | Azure Cloud Services ビルド ツール | 16.10.31205.252 | Optional
Microsoft.VisualStudio.Component.Common.Azure.Tools | 接続および発行ツール | 16.4.29409.204 | Optional
Microsoft.VisualStudio.Component.Debugger.JustInTime | Just-In-Time デバッガー | 16.0.28517.75 | Optional
Microsoft.VisualStudio.Component.DockerTools | コンテナー開発ツール | 16.4.29409.204 | Optional
Microsoft.VisualStudio.Component.Graphics.Tools | DirectX 用グラフィックス デバッガーおよび GPU プロファイラー | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.IISExpress | IIS Express  | 16.0.28315.86 | Optional
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | JavaScript 診断 | 16.0.28517.75 | Optional
Microsoft.VisualStudio.Component.JavaScript.TypeScript | JavaScript および TypeScript の言語サポート | 16.10.31303.231 | Optional
Microsoft.VisualStudio.Component.ManagedDesktop.Core | Managed Desktop Workload コア | 16.4.29318.151 | Optional
Microsoft.VisualStudio.Component.MSODBC.SQL | SQL Server ODBC Driver | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.MSSQL.CMDLnUtils | SQL Server コマンド ライン ユーティリティ | 16.0.28707.177 | Optional
Microsoft.VisualStudio.Component.NuGet | NuGet パッケージ マネージャー | 16.1.28829.92 | Optional
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# および Visual Basic Roslyn コンパイラ | 16.0.28714.129 | Optional
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# および Visual Basic | 16.10.31205.252 | Optional
Microsoft.VisualStudio.Component.SQL.ADAL | SQL ADAL ランタイム | 16.0.28517.75 | Optional
Microsoft.VisualStudio.Component.SQL.CLR | SQL Server の CLR データ型 | 16.0.28315.86 | Optional
Microsoft.VisualStudio.Component.SQL.DataSources | SQL Server サポートのためのデータ ソース | 16.0.28315.86 | Optional
Microsoft.VisualStudio.Component.SQL.LocalDB.Runtime | SQL Server Express 2016 LocalDB | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.SQL.SSDT | SQL Server Data Tools | 16.3.29207.166 | Optional
Microsoft.VisualStudio.Component.TextTemplating | テキスト テンプレート変換 | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.TypeScript.4.2 | TypeScript 4.2 SDK | 16.0.31303.231 | Optional
Microsoft.VisualStudio.Component.VC.CoreIde | C++ コア機能 | 16.10.31205.252 | Optional
Microsoft.VisualStudio.Component.VC.DiagnosticTools | C++ のプロファイル ツール | 16.5.29515.121 | Optional
Microsoft.VisualStudio.Component.VC.Tools.x86.x64 | MSVC v142 - VS 2019 C++ x64/x86 ビルド ツール (最新) | 16.10.31205.252 | Optional
Microsoft.VisualStudio.Component.Web | ASP.NET と Web の開発ツール | 16.10.31205.252 | オプション
Microsoft.VisualStudio.Component.WebDeploy | Web 配置 | 16.0.28517.75 | Optional
Microsoft.VisualStudio.Component.Windows10SDK | Windows ユニバーサル C ランタイム | 16.4.29409.204 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.19041 | Windows 10 SDK (10.0.19041.0) | 16.10.31205.252 | Optional
Microsoft.VisualStudio.ComponentGroup.Web | ASP.NET と Web の開発ツールの前提条件 | 16.10.31205.180 | Optional
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | ASP.NET と Web 開発 | 16.10.31205.180 | Optional

## <a name="universal-windows-platform-development"></a>ユニバーサル Windows プラットフォーム開発

**ID:** Microsoft.VisualStudio.Workload.Universal

**説明:** C#、VB、または C++ (オプション) を使ってユニバーサル Windows プラットフォームのアプリケーションを作成します。

### <a name="components-included-by-this-workload"></a>このワークロードに含まれるコンポーネント

コンポーネント ID | 名前 | バージョン | 依存関係の種類
--- | --- | --- | ---
Microsoft.Component.NetFX.Native | .NET Native | 16.5.29515.121 | 必須
Microsoft.ComponentGroup.Blend | Blend for Visual Studio | 16.0.28315.86 | 必須
Microsoft.Net.Component.4.5.TargetingPack | .NET Framework 4.5 Targeting Pack | 16.0.28517.75 | 必須
Microsoft.NetCore.Component.Runtime.3.1 | .NET Core 3.1 ランタイム (LTS) | 16.10.31320.204 | 必須
Microsoft.NetCore.Component.Runtime.5.0 | .NET 5.0 ランタイム | 16.10.31320.204 | 必須
Microsoft.NetCore.Component.SDK | .NET SDK | 16.10.31320.204 | 必須
Microsoft.VisualStudio.Component.AppInsights.Tools | Developer Analytics Tools | 16.5.29515.121 | 必須
Microsoft.VisualStudio.Component.DiagnosticTools | .NET プロファイル ツール | 16.10.31205.252 | 必須
Microsoft.VisualStudio.Component.Graphics | イメージ エディターと 3D モデル エディター | 16.10.31205.252 | 必須
Microsoft.VisualStudio.Component.NuGet | NuGet パッケージ マネージャー | 16.1.28829.92 | 必須
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# および Visual Basic Roslyn コンパイラ | 16.0.28714.129 | 必須
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# および Visual Basic | 16.10.31205.252 | 必須
Microsoft.VisualStudio.Component.SQL.CLR | SQL Server の CLR データ型 | 16.0.28315.86 | 必須
Microsoft.VisualStudio.Component.Windows10SDK.19041 | Windows 10 SDK (10.0.19041.0) | 16.10.31205.252 | 必須
Microsoft.VisualStudio.ComponentGroup.MSIX.Packaging | MSIX パッケージ化ツール | 16.10.31205.180 | 必須
Microsoft.VisualStudio.ComponentGroup.UWP.NetCoreAndStandard | .NET ネイティブと .NET Standard | 16.3.29102.218 | 必須
Microsoft.VisualStudio.ComponentGroup.UWP.Support | ユニバーサル Windows プラットフォーム ツール | 16.10.31205.180 | 必須
Microsoft.VisualStudio.ComponentGroup.UWP.Xamarin | Xamarin 用ユニバーサル Windows プラットフォーム ツール | 16.10.31205.180 | 必須
Microsoft.VisualStudio.Component.IntelliCode | IntelliCode | 16.10.31305.154 | 推奨
Microsoft.Net.Component.4.8.SDK | .NET Framework 4.8 SDK | 16.4.29313.120 | Optional
Microsoft.VisualStudio.Component.Graphics.Tools | DirectX 用グラフィックス デバッガーおよび GPU プロファイラー | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.UWP.VC.ARM64 | v142 ビルド ツールの C++ ユニバーサル Windows プラットフォーム サポート (ARM64) | 16.3.29207.166 | Optional
Microsoft.VisualStudio.Component.UWP.VC.ARM64EC | v142 ビルド ツールの C++ ユニバーサル Windows プラットフォーム サポート (ARM64EC – 試験段階) | 16.10.31303.231 | Optional
Microsoft.VisualStudio.Component.VC.CoreIde | C++ コア機能 | 16.10.31205.252 | Optional
Microsoft.VisualStudio.Component.VC.Tools.ARM | MSVC v142 - VS 2019 C++ ARM ビルド ツール (最新) | 16.10.31205.252 | Optional
Microsoft.VisualStudio.Component.VC.Tools.ARM64 | MSVC v142 - VS 2019 C++ ARM64 ビルド ツール (最新) | 16.10.31205.252 | オプション
Microsoft.VisualStudio.Component.VC.Tools.ARM64EC | MSVC v142 - VS 2019 C++ ARM64EC ビルド ツール (最新 – 試験段階) | 16.10.31205.252 | Optional
Microsoft.VisualStudio.Component.VC.Tools.x86.x64 | MSVC v142 - VS 2019 C++ x64/x86 ビルド ツール (最新) | 16.10.31205.252 | Optional
Microsoft.VisualStudio.Component.VC.v141.ARM | MSVC v141 - VS 2017 C++ ARM ビルド ツール (v14.16) | 16.10.31205.252 | Optional
Microsoft.VisualStudio.Component.VC.v141.ARM64 | MSVC v141 - VS 2017 C++ ARM64 ビルド ツール (v14.16) | 16.10.31205.252 | Optional
Microsoft.VisualStudio.Component.VC.v141.x86.x64 | MSVC v141 - VS 2017 C++ x64/x86 ビルド ツール (v14.16) | 16.10.31205.252 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.16299 | Windows 10 SDK (10.0.16299.0) | 16.10.31205.252 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.17134 | Windows 10 SDK (10.0.17134.0) | 16.10.31205.252 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.17763 | Windows 10 SDK (10.0.17763.0) | 16.0.28517.75 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.18362 | Windows 10 SDK (10.0.18362.0) | 16.1.28829.92 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.IpOverUsb | USB デバイスの接続 | 16.10.31205.252 | Optional
Microsoft.VisualStudio.ComponentGroup.UWP.VC | C++ (v142) ユニバーサル Windows プラットフォーム ツール | 16.10.31205.180 | Optional
Microsoft.VisualStudio.ComponentGroup.UWP.VC.v141 | C++ (v141) ユニバーサル Windows プラットフォーム ツール | 16.1.28810.153 | Optional

## <a name="visual-studio-extension-development"></a>Visual Studio 拡張機能の開発

**ID:** Microsoft.VisualStudio.Workload.VisualStudioExtension

**説明:** Visual Studio 用のアドオンや拡張機能 (新しいコマンド、コード アナライザー、ツール ウィンドウを含みます) を作成します。

### <a name="components-included-by-this-workload"></a>このワークロードに含まれるコンポーネント

コンポーネント ID | 名前 | バージョン | 依存関係の種類
--- | --- | --- | ---
Microsoft.Component.MSBuild | MSBuild | 16.5.29515.121 | 必須
Microsoft.Net.Component.4.6.TargetingPack | .NET Framework 4.6 Targeting Pack | 16.0.28517.75 | 必須
Microsoft.Net.Component.4.7.2.TargetingPack | .NET Framework 4.7.2 Targeting Pack | 16.10.31205.252 | 必須
Microsoft.Net.Component.4.8.SDK | .NET Framework 4.8 SDK | 16.4.29313.120 | 必須
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | .NET Framework 4.7.2 開発ツール | 16.3.29207.166 | 必須
Microsoft.VisualStudio.Component.NuGet | NuGet パッケージ マネージャー | 16.1.28829.92 | 必須
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# および Visual Basic Roslyn コンパイラ | 16.0.28714.129 | 必須
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# および Visual Basic | 16.10.31205.252 | 必須
Microsoft.VisualStudio.Component.VSSDK | Visual Studio SDK | 16.0.28315.86 | 必須
Microsoft.VisualStudio.ComponentGroup.VisualStudioExtension.Prerequisites | Visual Studio 拡張機能の開発の前提条件 | 16.10.31205.180 | 必須
Microsoft.VisualStudio.Component.DiagnosticTools | .NET プロファイル ツール | 16.10.31205.252 | 推奨
Microsoft.VisualStudio.Component.IntelliCode | IntelliCode | 16.10.31305.154 | 推奨
Microsoft.VisualStudio.Component.TextTemplating | テキスト テンプレート変換 | 16.0.28625.61 | 推奨
Microsoft.Component.CodeAnalysis.SDK | .NET Compiler Platform SDK | 16.2.29003.222 | Optional
Microsoft.VisualStudio.Component.AppInsights.Tools | Developer Analytics Tools | 16.5.29515.121 | Optional
Microsoft.VisualStudio.Component.DslTools | Modeling SDK | 16.0.28315.86 | Optional

## <a name="unaffiliated-components"></a>関連付けられていないコンポーネント

以下のコンポーネントはどのワークロードにも含まれていませんが、個別のコンポーネントとして選択できます。

コンポーネント ID | 名前 | バージョン
--- | --- | ---
Component.GitHub.VisualStudio | Visual Studio 用の GitHub 拡張機能 | 2.5.9.5485
Component.Xamarin.Profiler | Xamarin Profiler | 16.0.28315.86
Microsoft.Component.ClickOnce | ClickOnce Publishing | 16.4.29409.204
Microsoft.Component.HelpViewer | ヘルプ ビューアー | 16.0.28625.61
Microsoft.Net.Component.4.6.1.SDK | .NET Framework 4.6.1 SDK | 16.4.29409.204
Microsoft.Net.Component.4.6.2.SDK | .NET Framework 4.6.2 SDK | 16.4.29409.204
Microsoft.Net.Component.4.7.1.SDK | .NET Framework 4.7.1 SDK | 16.4.29409.204
Microsoft.Net.Component.4.7.2.SDK | .NET Framework 4.7.2 SDK | 16.4.29409.204
Microsoft.Net.Component.4.7.SDK | .NET Framework 4.7 SDK | 16.4.29409.204
Microsoft.Net.Core.Component.SDK.2.2 | .NET Core 2.2 ランタイム (サポート対象外) | 16.10.31205.252
Microsoft.Net.Core.Component.SDK.3.0 | .NET Core 3.0 ランタイム (サポート対象外) | 16.10.31320.204
Microsoft.NetCore.ComponentGroup.DevelopmentTools.2.1 | 開発ツール + .NET Core 2.1 | 16.10.31205.252
Microsoft.NetCore.ComponentGroup.Web.2.1 | Web 開発ツール + .NET Core 2.1 | 16.10.31205.252
Microsoft.VisualStudio.Component.AzureDevOps.OfficeIntegration | Azure DevOps Office Integration | 16.0.28625.61
Microsoft.VisualStudio.Component.ClassDesigner | クラス デザイナー | 16.0.28528.71
Microsoft.VisualStudio.Component.DependencyValidation.Community | 依存関係検証 | 16.0.28517.75
Microsoft.VisualStudio.Component.Git | Git for Windows | 16.0.28625.61
Microsoft.VisualStudio.Component.GraphDocument | DGML エディター | 16.0.28625.61
Microsoft.VisualStudio.Component.LinqToSql | LINQ to SQL ツール | 16.0.28625.61
Microsoft.VisualStudio.Component.VC.14.20.ARM | MSVC v142 - VS 2019 C++ ARM ビルド ツール (v14.20) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.20.ARM.Spectre | MSVC v142 - VS 2019 C++ ARM Spectre 軽減ライブラリ (v14.20) | 16.5.29515.121
Microsoft.VisualStudio.Component.VC.14.20.ARM64 | MSVC v142 - VS 2019 C++ ARM64 ビルド ツール (v14.20) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.20.ARM64.Spectre | MSVC v142 - VS 2019 C++ ARM64 Spectre 軽減ライブラリ (v14.20) | 16.5.29515.121
Microsoft.VisualStudio.Component.VC.14.20.ATL | v142 ビルド ツールの C++ v14.20 ATL (x86 & x64) | 16.1.28829.92
Microsoft.VisualStudio.Component.VC.14.20.ATL.ARM | v142 ビルド ツールの C++ v14.20 ATL (ARM) | 16.5.29515.121
Microsoft.VisualStudio.Component.VC.14.20.ATL.ARM.Spectre | v142 ビルド ツール用 C++ v14.20 ATL と Spectre 軽減策 (ARM) | 16.5.29721.120
Microsoft.VisualStudio.Component.VC.14.20.ATL.ARM64 | v142 ビルド ツールの C++ v14.20 ATL (ARM64) | 16.5.29515.121
Microsoft.VisualStudio.Component.VC.14.20.ATL.ARM64.Spectre | v142 ビルド ツール用 C++ v14.20 ATL と Spectre 軽減策 (ARM64) | 16.5.29515.121
Microsoft.VisualStudio.Component.VC.14.20.ATL.Spectre | v142 ビルド ツール用 C++ v14.20 ATL と Spectre 軽減策 (x86 & x64) | 16.5.29515.121
Microsoft.VisualStudio.Component.VC.14.20.CLI.Support | v142 ビルド ツールの C++/CLI サポート (14.20) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.20.MFC | v142 ビルド ツールの C++ v14.20 MFC (x86 & x64) | 16.2.29003.222
Microsoft.VisualStudio.Component.VC.14.20.MFC.ARM | v142 ビルド ツールの C++ v14.20 MFC (ARM) | 16.5.29515.121
Microsoft.VisualStudio.Component.VC.14.20.MFC.ARM.Spectre | v142 ビルド ツール用 C++ v14.20 MFC と Spectre 軽減策 (ARM) | 16.5.29515.121
Microsoft.VisualStudio.Component.VC.14.20.MFC.ARM64 | v142 ビルド ツール用 C++ v14.20 MFC (ARM64) | 16.5.29515.121
Microsoft.VisualStudio.Component.VC.14.20.MFC.ARM64.Spectre | v142 ビルド ツール用 C++ v14.20 MFC と Spectre 軽減策 (ARM64) | 16.5.29515.121
Microsoft.VisualStudio.Component.VC.14.20.MFC.Spectre | v142 ビルド ツール用 C++ v14.20 MFC と Spectre 軽減策 (x86 & x64) | 16.5.29515.121
Microsoft.VisualStudio.Component.VC.14.20.x86.x64 | MSVC v142 - VS 2019 C++ x64/x86 ビルド ツール (v14.20) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.20.x86.x64.Spectre | MSVC v142 - VS 2019 C++ x64/x86 Spectre 軽減ライブラリ (v14.20) | 16.5.29515.121
Microsoft.VisualStudio.Component.VC.14.21.ARM | MSVC v142 - VS 2019 C++ ARM ビルド ツール (v14.21) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.21.ARM.Spectre | MSVC v142 - VS 2019 C++ ARM Spectre 軽減ライブラリ (v14.21) | 16.5.29515.121
Microsoft.VisualStudio.Component.VC.14.21.ARM64 | MSVC v142 - VS 2019 C++ ARM64 ビルド ツール (v14.21) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.21.ARM64.Spectre | MSVC v142 - VS 2019 C++ ARM64 Spectre 軽減ライブラリ (v14.21) | 16.5.29515.121
Microsoft.VisualStudio.Component.VC.14.21.ATL | v142 ビルド ツールの C++ v14.21 ATL (x86 & x64) | 16.2.29019.55
Microsoft.VisualStudio.Component.VC.14.21.ATL.ARM | v142 ビルド ツールの C++ v14.21 ATL (ARM) | 16.2.29019.55
Microsoft.VisualStudio.Component.VC.14.21.ATL.ARM.Spectre | v142 ビルド ツール用 C++ v14.21 ATL と Spectre 軽減策 (ARM) | 16.5.29721.120
Microsoft.VisualStudio.Component.VC.14.21.ATL.ARM64 | v142 ビルド ツールの C++ v14.21 ATL (ARM64) | 16.2.29019.55
Microsoft.VisualStudio.Component.VC.14.21.ATL.ARM64.Spectre | v142 ビルド ツール用 C++ v14.21 ATL と Spectre 軽減策 (ARM64) | 16.5.29515.121
Microsoft.VisualStudio.Component.VC.14.21.ATL.Spectre | v142 ビルド ツール用 C++ v14.21 ATL と Spectre 軽減策 (x86 & x64) | 16.5.29515.121
Microsoft.VisualStudio.Component.VC.14.21.CLI.Support | v142 ビルド ツールの C++/CLI サポート (14.21) | 16.3.29207.166
Microsoft.VisualStudio.Component.VC.14.21.MFC | v142 ビルド ツールの C++ v14.21 MFC (x86 & x64) | 16.2.29019.55
Microsoft.VisualStudio.Component.VC.14.21.MFC.ARM | v142 ビルド ツールの C++ v14.21 MFC (ARM) | 16.2.29019.55
Microsoft.VisualStudio.Component.VC.14.21.MFC.ARM.Spectre | v142 ビルド ツール用 C++ v14.21 MFC と Spectre 軽減策 (ARM) | 16.5.29515.121
Microsoft.VisualStudio.Component.VC.14.21.MFC.ARM64 | v142 ビルド ツール用 C++ v14.21 MFC (ARM64) | 16.2.29019.55
Microsoft.VisualStudio.Component.VC.14.21.MFC.ARM64.Spectre | v142 ビルド ツール用 C++ v14.21 MFC と Spectre 軽減策 (ARM64) | 16.5.29515.121
Microsoft.VisualStudio.Component.VC.14.21.MFC.Spectre | v142 ビルド ツール用 C++ v14.21 MFC と Spectre 軽減策 (x86 & x64) | 16.5.29515.121
Microsoft.VisualStudio.Component.VC.14.21.x86.x64 | MSVC v142 - VS 2019 C++ x64/x86 ビルド ツール (v14.21) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.21.x86.x64.Spectre | MSVC v142 - VS 2019 C++ x64/x86 Spectre 軽減ライブラリ (v14.21) | 16.5.29515.121
Microsoft.VisualStudio.Component.VC.14.22.ARM | MSVC v142 - VS 2019 C++ ARM ビルド ツール (v14.22) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.22.ARM.Spectre | MSVC v142 - VS 2019 C++ ARM Spectre 軽減ライブラリ (v14.22) | 16.5.29515.121
Microsoft.VisualStudio.Component.VC.14.22.ARM64 | MSVC v142 - VS 2019 C++ ARM64 ビルド ツール (v14.22) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.22.ARM64.Spectre | MSVC v142 - VS 2019 C++ ARM64 Spectre 軽減ライブラリ (v14.22) | 16.5.29515.121
Microsoft.VisualStudio.Component.VC.14.22.ATL | v142 ビルド ツールの C++ v14.22 ATL (x86 & x64) | 16.4.29313.120
Microsoft.VisualStudio.Component.VC.14.22.ATL.ARM | v142 ビルド ツールの C++ v14.22 ATL (ARM) | 16.4.29313.120
Microsoft.VisualStudio.Component.VC.14.22.ATL.ARM.Spectre | v142 ビルド ツール用 C++ v14.22 ATL と Spectre 軽減策 (ARM) | 16.5.29721.120
Microsoft.VisualStudio.Component.VC.14.22.ATL.ARM64 | v142 ビルド ツールの C++ v14.22 ATL (ARM64) | 16.4.29313.120
Microsoft.VisualStudio.Component.VC.14.22.ATL.ARM64.Spectre | v142 ビルド ツール用 C++ v14.22 ATL と Spectre 軽減策 (ARM64) | 16.5.29515.121
Microsoft.VisualStudio.Component.VC.14.22.ATL.Spectre | v142 ビルド ツール用 C++ v14.22 ATL と Spectre 軽減策 (x86 & x64) | 16.5.29515.121
Microsoft.VisualStudio.Component.VC.14.22.CLI.Support | v142 ビルド ツールの C++/CLI サポート (14.22) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.22.MFC | v142 ビルド ツールの C++ v14.22 MFC (x86 & x64) | 16.4.29313.120
Microsoft.VisualStudio.Component.VC.14.22.MFC.ARM | v142 ビルド ツールの C++ v14.22 MFC (ARM) | 16.4.29313.120
Microsoft.VisualStudio.Component.VC.14.22.MFC.ARM.Spectre | v142 ビルド ツール用 C++ v14.22 MFC と Spectre 軽減策 (ARM) | 16.5.29515.121
Microsoft.VisualStudio.Component.VC.14.22.MFC.ARM64 | v142 ビルド ツール用 C++ v14.22 MFC (ARM64) | 16.4.29313.120
Microsoft.VisualStudio.Component.VC.14.22.MFC.ARM64.Spectre | v142 ビルド ツール用 C++ v14.22 MFC と Spectre 軽減策 (ARM64) | 16.5.29515.121
Microsoft.VisualStudio.Component.VC.14.22.MFC.Spectre | v142 ビルド ツール用 C++ v14.22 MFC と Spectre 軽減策 (x86 & x64) | 16.5.29515.121
Microsoft.VisualStudio.Component.VC.14.22.x86.x64 | MSVC v142 - VS 2019 C++ x64/x86 ビルド ツール (v14.22) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.22.x86.x64.Spectre | MSVC v142 - VS 2019 C++ x64/x86 Spectre 軽減ライブラリ (v14.22) | 16.5.29515.121
Microsoft.VisualStudio.Component.VC.14.23.ARM | MSVC v142 - VS 2019 C++ ARM ビルド ツール (v14.23) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.23.ARM.Spectre | MSVC v142 - VS 2019 C++ ARM Spectre 軽減ライブラリ (v14.23) | 16.5.29515.121
Microsoft.VisualStudio.Component.VC.14.23.ARM64 | MSVC v142 - VS 2019 C++ ARM64 ビルド ツール (v14.23) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.23.ARM64.Spectre | MSVC v142 - VS 2019 C++ ARM64 Spectre 軽減ライブラリ (v14.23) | 16.5.29515.121
Microsoft.VisualStudio.Component.VC.14.23.ATL | v142 ビルド ツール用 C++ v14.23 ATL (x86 & x64) | 16.5.29515.121
Microsoft.VisualStudio.Component.VC.14.23.ATL.ARM | v142 ビルド ツール用 C++ v14.23 ATL (ARM) | 16.5.29515.121
Microsoft.VisualStudio.Component.VC.14.23.ATL.ARM.Spectre | v142 ビルド ツール用 C++ v14.23 ATL と Spectre 軽減策 (ARM) | 16.5.29721.120
Microsoft.VisualStudio.Component.VC.14.23.ATL.ARM64 | v142 ビルド ツール用 C++ v14.23 ATL (ARM64) | 16.5.29515.121
Microsoft.VisualStudio.Component.VC.14.23.ATL.ARM64.Spectre | v142 ビルド ツール用 C++ v14.23 ATL と Spectre 軽減策 (ARM64) | 16.5.29515.121
Microsoft.VisualStudio.Component.VC.14.23.ATL.Spectre | v142 ビルド ツール用 C++ v14.23 ATL と Spectre 軽減策 (x86 & x64) | 16.5.29515.121
Microsoft.VisualStudio.Component.VC.14.23.CLI.Support | v142 ビルド ツールの C++/CLI サポート (14.23) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.23.MFC | v142 ビルド ツール用 C++ v14.23 MFC (x86 & x64) | 16.5.29515.121
Microsoft.VisualStudio.Component.VC.14.23.MFC.ARM | v142 ビルド ツール用 C++ v14.23 MFC (ARM) | 16.5.29515.121
Microsoft.VisualStudio.Component.VC.14.23.MFC.ARM.Spectre | v142 ビルド ツール用 C++ v14.23 MFC と Spectre 軽減策 (ARM) | 16.5.29515.121
Microsoft.VisualStudio.Component.VC.14.23.MFC.ARM64 | v142 ビルド ツール用 C++ v14.23 MFC (ARM64) | 16.5.29515.121
Microsoft.VisualStudio.Component.VC.14.23.MFC.ARM64.Spectre | v142 ビルド ツール用 C++ v14.23 MFC と Spectre 軽減策 (ARM64) | 16.5.29515.121
Microsoft.VisualStudio.Component.VC.14.23.MFC.Spectre | v142 ビルド ツール用 C++ v14.23 MFC と Spectre 軽減策 (x86 & x64) | 16.5.29515.121
Microsoft.VisualStudio.Component.VC.14.23.x86.x64 | MSVC v142 - VS 2019 C++ x64/x86 ビルド ツール (v14.23) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.23.x86.x64.Spectre | MSVC v142 - VS 2019 C++ x64/x86 Spectre 軽減ライブラリ (v14.23) | 16.5.29515.121
Microsoft.VisualStudio.Component.VC.14.24.ARM | MSVC v142 - VS 2019 C++ ARM ビルド ツール (v14.24) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.24.ARM.Spectre | MSVC v142 - VS 2019 C++ ARM Spectre 軽減ライブラリ (v14.24) | 16.5.29721.120
Microsoft.VisualStudio.Component.VC.14.24.ARM64 | MSVC v142 - VS 2019 C++ ARM64 ビルド ツール (v14.24) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.24.ARM64.Spectre | MSVC v142 - VS 2019 C++ ARM64 Spectre 軽減ライブラリ (v14.24) | 16.5.29721.120
Microsoft.VisualStudio.Component.VC.14.24.ATL | v142 ビルド ツール用 C++ v14.24 ATL (x86 & x64) | 16.5.29721.120
Microsoft.VisualStudio.Component.VC.14.24.ATL.ARM | v142 ビルド ツール用 C++ v14.24 ATL (ARM) | 16.5.29721.120
Microsoft.VisualStudio.Component.VC.14.24.ATL.ARM.Spectre | v142 ビルド ツール用 C++ v14.24 ATL と Spectre 軽減策 (ARM) | 16.5.29721.120
Microsoft.VisualStudio.Component.VC.14.24.ATL.ARM64 | v142 ビルド ツール用 C++ v14.24 ATL (ARM64) | 16.5.29721.120
Microsoft.VisualStudio.Component.VC.14.24.ATL.ARM64.Spectre | v142 ビルド ツール用 C++ v14.24 ATL と Spectre 軽減策 (ARM64) | 16.5.29721.120
Microsoft.VisualStudio.Component.VC.14.24.ATL.Spectre | v142 ビルド ツール用 C++ v14.24 ATL と Spectre 軽減策 (x86 & x64) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.24.CLI.Support | v142 ビルド ツールの C++/CLI サポート (14.24) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.24.MFC | v142 ビルド ツール用 C++ v14.24 MFC (x86 & x64) | 16.5.29721.120
Microsoft.VisualStudio.Component.VC.14.24.MFC.ARM | v142 ビルド ツール用 C++ v14.24 MFC (ARM) | 16.5.29721.120
Microsoft.VisualStudio.Component.VC.14.24.MFC.ARM.Spectre | v142 ビルド ツール用 C++ v14.24 MFC と Spectre 軽減策 (ARM) | 16.5.29721.120
Microsoft.VisualStudio.Component.VC.14.24.MFC.ARM64 | v142 ビルド ツール用 C++ v14.24 MFC (ARM64) | 16.5.29721.120
Microsoft.VisualStudio.Component.VC.14.24.MFC.ARM64.Spectre | v142 ビルド ツール用 C++ v14.24 MFC と Spectre 軽減策 (ARM64) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.24.MFC.Spectre | v142 ビルド ツール用 C++ v14.24 MFC と Spectre 軽減策 (x86 & x64) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.24.x86.x64 | MSVC v142 - VS 2019 C++ x64/x86 ビルド ツール (v14.24) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.24.x86.x64.Spectre | MSVC v142 - VS 2019 C++ x64/x86 Spectre 軽減ライブラリ (v14.24) | 16.5.29721.120
Microsoft.VisualStudio.Component.VC.14.25.ARM | MSVC v142 - VS 2019 C++ ARM ビルド ツール (v14.25) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.25.ARM.Spectre | MSVC v142 - VS 2019 C++ ARM Spectre 軽減ライブラリ (v14.25) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.25.ARM64 | MSVC v142 - VS 2019 C++ ARM64 ビルド ツール (v14.25) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.25.ARM64.Spectre | MSVC v142 - VS 2019 C++ ARM64 Spectre 軽減ライブラリ (v14.25) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.25.ATL | v142 ビルド ツール用 C++ v14.25 ATL (x86 & x64) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.25.ATL.ARM | v142 ビルド ツール用 C++ v14.25 ATL (ARM) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.25.ATL.ARM.Spectre | v142 ビルド ツール用 C++ v14.25 ATL と Spectre 軽減策 (ARM) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.25.ATL.ARM64 | v142 ビルド ツール用 C++ v14.25 ATL (ARM64) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.25.ATL.ARM64.Spectre | v142 ビルド ツール用 C++ v14.25 ATL と Spectre 軽減策 (ARM64) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.25.ATL.Spectre | v142 ビルド ツール用 C++ v14.25 ATL と Spectre 軽減策 (x86 & x64) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.25.CLI.Support | v142 ビルド ツールの C++/CLI サポート (14.25) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.25.MFC | v142 ビルド ツール用 C++ v14.25 MFC (x86 & x64) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.25.MFC.ARM | v142 ビルド ツール用 C++ v14.25 MFC (ARM) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.25.MFC.ARM.Spectre | v142 ビルド ツール用 C++ v14.25 MFC と Spectre 軽減策 (ARM) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.25.MFC.ARM64 | v142 ビルド ツール用 C++ v14.25 MFC (ARM64) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.25.MFC.ARM64.Spectre | v142 ビルド ツール用 C++ v14.25 MFC と Spectre 軽減策 (ARM64) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.25.MFC.Spectre | v142 ビルド ツール用 C++ v14.25 MFC と Spectre 軽減策 (x86 & x64) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.25.x86.x64 | MSVC v142 - VS 2019 C++ x64/x86 ビルド ツール (v14.25) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.25.x86.x64.Spectre | MSVC v142 - VS 2019 C++ x64/x86 Spectre 軽減ライブラリ (v14.25) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.26.ARM | MSVC v142 - VS 2019 C++ ARM ビルド ツール (v14.26) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.26.ARM.Spectre | MSVC v142 - VS 2019 C++ ARM Spectre 軽減ライブラリ (v14.26) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.26.ARM64 | MSVC v142 - VS 2019 C++ ARM64 ビルド ツール (v14.26) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.26.ARM64.Spectre | MSVC v142 - VS 2019 C++ ARM64 Spectre 軽減ライブラリ (v14.26) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.26.ATL | v142 ビルド ツール用 C++ v14.26 ATL (x86 & x64) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.26.ATL.ARM | v142 ビルド ツール用 C++ v14.26 ATL (ARM) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.26.ATL.ARM.Spectre | v142 ビルド ツール用 C++ v14.26 ATL と Spectre 軽減策 (ARM) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.26.ATL.ARM64 | v142 ビルド ツール用 C++ v14.26 ATL (ARM64) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.26.ATL.ARM64.Spectre | v142 ビルド ツール用 C++ v14.26 ATL と Spectre 軽減策 (ARM64) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.26.ATL.Spectre | v142 ビルド ツール用 C++ v14.26 ATL と Spectre 軽減策 (x86 & x64) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.26.CLI.Support | v142 ビルド ツールの C++/CLI サポート (14.26) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.26.MFC | v142 ビルド ツール用 C++ v14.26 MFC (x86 & x64) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.26.MFC.ARM | v142 ビルド ツール用 C++ v14.26 MFC (ARM) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.26.MFC.ARM.Spectre | v142 ビルド ツール用 C++ v14.26 MFC と Spectre 軽減策 (ARM) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.26.MFC.ARM64 | v142 ビルド ツール用 C++ v14.26 MFC (ARM64) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.26.MFC.ARM64.Spectre | v142 ビルド ツール用 C++ v14.26 MFC と Spectre 軽減策 (ARM64) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.26.MFC.Spectre | v142 ビルド ツール用 C++ v14.26 MFC と Spectre 軽減策 (x86 & x64) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.26.x86.x64 | MSVC v142 - VS 2019 C++ x64/x86 ビルド ツール (v14.26) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.26.x86.x64.Spectre | MSVC v142 - VS 2019 C++ x64/x86 Spectre 軽減ライブラリ (v14.26) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.27.ARM | MSVC v142 - VS 2019 C++ ARM ビルド ツール (v14.27) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.27.ARM.Spectre | MSVC v142 - VS 2019 C++ ARM Spectre 軽減ライブラリ (v14.27) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.27.ARM64 | MSVC v142 - VS 2019 C++ ARM64 ビルド ツール (v14.27) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.27.ARM64.Spectre | MSVC v142 - VS 2019 C++ ARM64 Spectre 軽減ライブラリ (v14.27) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.27.ATL | v142 ビルド ツール用 C++ v14.27 ATL (x86 & x64) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.27.ATL.ARM | v142 ビルド ツール用 C++ v14.27 ATL (ARM) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.27.ATL.ARM.Spectre | v142 ビルド ツール用 C++ v14.27 ATL と Spectre 軽減策 (ARM) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.27.ATL.ARM64 | v142 ビルド ツール用 C++ v14.27 ATL (ARM64) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.27.ATL.ARM64.Spectre | v142 ビルド ツール用 C++ v14.27 ATL と Spectre 軽減策 (ARM64) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.27.ATL.Spectre | v142 ビルド ツール用 C++ v14.27 ATL と Spectre 軽減策 (x86 & x64) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.27.CLI.Support | v142 ビルド ツールの C++/CLI サポート (14.27) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.27.MFC | v142 ビルド ツール用 C++ v14.27 MFC (x86 & x64) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.27.MFC.ARM | v142 ビルド ツール用 C++ v14.27 MFC (ARM) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.27.MFC.ARM.Spectre | v142 ビルド ツール用 C++ v14.27 MFC と Spectre 軽減策 (ARM) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.27.MFC.ARM64 | v142 ビルド ツール用 C++ v14.27 MFC (ARM64) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.27.MFC.ARM64.Spectre | v142 ビルド ツール用 C++ v14.27 MFC と Spectre 軽減策 (ARM64) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.27.MFC.Spectre | v142 ビルド ツール用 C++ v14.27 MFC と Spectre 軽減策 (x86 & x64) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.27.x86.x64 | MSVC v142 - VS 2019 C++ x64/x86 ビルド ツール (v14.27) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.27.x86.x64.Spectre | MSVC v142 - VS 2019 C++ x64/x86 Spectre 軽減ライブラリ (v14.27) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.28.16.9.ARM | MSVC v142 - VS 2019 C++ ARM ビルド ツール (v14.28-16.9) | 16.10.31303.231
Microsoft.VisualStudio.Component.VC.14.28.16.9.ARM.Spectre | MSVC v142 - VS 2019 C++ ARM Spectre 軽減ライブラリ (v14.28-16.9) | 16.10.31303.231
Microsoft.VisualStudio.Component.VC.14.28.16.9.ARM64 | MSVC v142 - VS 2019 C++ ARM64 ビルド ツール (v14.28-16.9) | 16.10.31303.231
Microsoft.VisualStudio.Component.VC.14.28.16.9.ARM64.Spectre | MSVC v142 - VS 2019 C++ ARM64 Spectre 軽減ライブラリ (v14.28-16.9) | 16.10.31303.231
Microsoft.VisualStudio.Component.VC.14.28.16.9.ATL | v142 ビルド ツール用 C++ v14.28 (16.9) ATL (x86 & x64) | 16.10.31303.231
Microsoft.VisualStudio.Component.VC.14.28.16.9.ATL.ARM | v142 ビルド ツール用 C++ v14.28 (16.9) ATL (ARM) | 16.10.31303.231
Microsoft.VisualStudio.Component.VC.14.28.16.9.ATL.ARM.Spectre | v142 ビルド ツール用 C++ v14.28 (16.9) ATL と Spectre 軽減策 (ARM) | 16.10.31303.231
Microsoft.VisualStudio.Component.VC.14.28.16.9.ATL.ARM64 | v142 ビルド ツール用 C++ v14.28 (16.9) ATL (ARM64) | 16.10.31303.231
Microsoft.VisualStudio.Component.VC.14.28.16.9.ATL.ARM64.Spectre | v142 ビルド ツール用 C++ v14.28 (16.9) ATL と Spectre 軽減策 (ARM64) | 16.10.31303.231
Microsoft.VisualStudio.Component.VC.14.28.16.9.ATL.Spectre | v142 ビルド ツール用 C++ v14.28 (16.9) ATL と Spectre 軽減策 (x86 & x64) | 16.10.31303.231
Microsoft.VisualStudio.Component.VC.14.28.16.9.CLI.Support | v142 ビルド ツールの C++/CLI サポート (14.28-16.9) | 16.10.31303.231
Microsoft.VisualStudio.Component.VC.14.28.16.9.MFC | v142 ビルド ツール用 C++ v14.28 (16.9) MFC (x86 & x64) | 16.10.31303.231
Microsoft.VisualStudio.Component.VC.14.28.16.9.MFC.ARM | v142 ビルド ツール用 C++ v14.28 (16.9) MFC (ARM) | 16.10.31303.231
Microsoft.VisualStudio.Component.VC.14.28.16.9.MFC.ARM.Spectre | v142 ビルド ツール用 C++ v14.28 (16.9) MFC と Spectre 軽減策 (ARM) | 16.10.31303.231
Microsoft.VisualStudio.Component.VC.14.28.16.9.MFC.ARM64 | v142 ビルド ツール用 C++ v14.28 (16.9) MFC (ARM64) | 16.10.31303.231
Microsoft.VisualStudio.Component.VC.14.28.16.9.MFC.ARM64.Spectre | v142 ビルド ツール用 C++ v14.28 (16.9) MFC と Spectre 軽減策 (ARM64) | 16.10.31303.231
Microsoft.VisualStudio.Component.VC.14.28.16.9.MFC.Spectre | v142 ビルド ツール用 C++ v14.28 (16.9) MFC と Spectre 軽減策 (x86 & x64) | 16.10.31303.231
Microsoft.VisualStudio.Component.VC.14.28.16.9.x86.x64 | MSVC v142 - VS 2019 C++ x64/x86 ビルド ツール (v14.28-16.9) | 16.10.31303.231
Microsoft.VisualStudio.Component.VC.14.28.16.9.x86.x64.Spectre | MSVC v142 - VS 2019 C++ x64/x86 Spectre 軽減ライブラリ (v14.28-16.9) | 16.10.31303.231
Microsoft.VisualStudio.Component.VC.14.28.ARM | MSVC v142 - VS 2019 C++ ARM ビルド ツール (v14.28-16.8) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.28.ARM.Spectre | MSVC v142 - VS 2019 C++ ARM Spectre 軽減ライブラリ (v14.28-16.8) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.28.ARM64 | MSVC v142 - VS 2019 C++ ARM64 ビルド ツール (v14.28-16.8) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.28.ARM64.Spectre | MSVC v142 - VS 2019 C++ ARM64 Spectre 軽減ライブラリ (v14.28-16.8) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.28.ATL | v142 ビルド ツール用 C++ v14.28 (16.8) ATL (x86 & x64) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.28.ATL.ARM | v142 ビルド ツール用 C++ v14.28 (16.8) ATL (ARM) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.28.ATL.ARM.Spectre | v142 ビルド ツール用 C++ v14.28 (16.8) ATL と Spectre 軽減策 (ARM) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.28.ATL.ARM64 | v142 ビルド ツール用 C++ v14.28 (16.8) ATL (ARM64) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.28.ATL.ARM64.Spectre | v142 ビルド ツール用 C++ v14.28 (16.8) ATL と Spectre 軽減策 (ARM64) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.28.ATL.Spectre | v142 ビルド ツール用 C++ v14.28 (16.8) ATL と Spectre 軽減策 (x86 & x64) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.28.CLI.Support | v142 ビルド ツールの C++/CLI サポート (14.28-16.8) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.28.MFC | v142 ビルド ツール用 C++ v14.28 (16.8) MFC (x86 & x64) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.28.MFC.ARM | v142 ビルド ツール用 C++ v14.28 (16.8) MFC (ARM) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.28.MFC.ARM.Spectre | v142 ビルド ツール用 C++ v14.28 (16.8) MFC と Spectre 軽減策 (ARM) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.28.MFC.ARM64 | v142 ビルド ツール用 C++ v14.28 (16.8) MFC (ARM64) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.28.MFC.ARM64.Spectre | v142 ビルド ツール用 C++ v14.28 (16.8) MFC と Spectre 軽減策 (ARM64) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.28.MFC.Spectre | v142 ビルド ツール用 C++ v14.28 (16.8) MFC と Spectre 軽減策 (x86 & x64) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.28.x86.x64 | MSVC v142 - VS 2019 C++ x64/x86 ビルド ツール (v14.28-16.8) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.28.x86.x64.Spectre | MSVC v142 - VS 2019 C++ x64/x86 Spectre 軽減ライブラリ (v14.28-16.8) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.14.29.16.10.ARM | MSVC v142 - VS 2019 C++ ARM ビルド ツール (v14.29-16.10) | 16.10.31313.121
Microsoft.VisualStudio.Component.VC.14.29.16.10.ARM.Spectre | MSVC v142 - VS 2019 C++ ARM Spectre 軽減ライブラリ (v14.29-16.10) | 16.10.31313.121
Microsoft.VisualStudio.Component.VC.14.29.16.10.ARM64 | MSVC v142 - VS 2019 C++ ARM64 ビルド ツール (v14.29-16.10) | 16.10.31313.121
Microsoft.VisualStudio.Component.VC.14.29.16.10.ARM64.Spectre | MSVC v142 - VS 2019 C++ ARM64 Spectre 軽減ライブラリ (v14.29-16.10) | 16.10.31313.121
Microsoft.VisualStudio.Component.VC.14.29.16.10.ATL | v142 ビルド ツール用 C++ v14.29 (16.10) ATL (x86 & x64) | 16.10.31313.121
Microsoft.VisualStudio.Component.VC.14.29.16.10.ATL.ARM | v142 ビルド ツール用 C++ v14.29 (16.10) ATL (ARM) | 16.10.31313.121
Microsoft.VisualStudio.Component.VC.14.29.16.10.ATL.ARM.Spectre | v142 ビルド ツール用 C++ v14.29 (16.10) ATL と Spectre 軽減策 (ARM) | 16.10.31313.121
Microsoft.VisualStudio.Component.VC.14.29.16.10.ATL.ARM64 | v142 ビルド ツール用 C++ v14.29 (16.10) ATL (ARM64) | 16.10.31313.121
Microsoft.VisualStudio.Component.VC.14.29.16.10.ATL.ARM64.Spectre | v142 ビルド ツール用 C++ v14.29 (16.10) ATL と Spectre 軽減策 (ARM64) | 16.10.31313.121
Microsoft.VisualStudio.Component.VC.14.29.16.10.ATL.Spectre | v142 ビルド ツール用 C++ v14.29 (16.10) ATL と Spectre 軽減策 (x86 & x64) | 16.10.31313.121
Microsoft.VisualStudio.Component.VC.14.29.16.10.CLI.Support | v142 ビルド ツールの C++/CLI サポート (14.29-16.10) | 16.10.31313.121
Microsoft.VisualStudio.Component.VC.14.29.16.10.MFC | v142 ビルド ツール用 C++ v14.29 (16.10) MFC (x86 & x64) | 16.10.31313.121
Microsoft.VisualStudio.Component.VC.14.29.16.10.MFC.ARM | v142 ビルド ツール用 C++ v14.29 (16.10) MFC (ARM) | 16.10.31313.121
Microsoft.VisualStudio.Component.VC.14.29.16.10.MFC.ARM.Spectre | v142 ビルド ツール用 C++ v14.29 (16.10) MFC と Spectre 軽減策 (ARM) | 16.10.31313.121
Microsoft.VisualStudio.Component.VC.14.29.16.10.MFC.ARM64 | v142 ビルド ツール用 C++ v14.29 (16.10) MFC (ARM64) | 16.10.31313.121
Microsoft.VisualStudio.Component.VC.14.29.16.10.MFC.ARM64.Spectre | v142 ビルド ツール用 C++ v14.29 (16.10) MFC と Spectre 軽減策 (ARM64) | 16.10.31313.121
Microsoft.VisualStudio.Component.VC.14.29.16.10.MFC.Spectre | v142 ビルド ツール用 C++ v14.29 (16.10) MFC と Spectre 軽減策 (x86 & x64) | 16.10.31313.121
Microsoft.VisualStudio.Component.VC.14.29.16.10.x86.x64 | MSVC v142 - VS 2019 C++ x64/x86 ビルド ツール (v14.29-16.10) | 16.10.31313.121
Microsoft.VisualStudio.Component.VC.14.29.16.10.x86.x64.Spectre | MSVC v142 - VS 2019 C++ x64/x86 Spectre 軽減ライブラリ (v14.29-16.10) | 16.10.31313.121
Microsoft.VisualStudio.Component.VC.ATL.ARM | 最新 v142 ビルド ツールの C++ ATL (ARM) | 16.4.29313.120
Microsoft.VisualStudio.Component.VC.ATL.ARM.Spectre | 最新 v142 ビルド ツール用 C++ ATL と Spectre 軽減策 (ARM) | 16.5.29721.120
Microsoft.VisualStudio.Component.VC.ATL.ARM64 | 最新 v142 ビルド ツールの C++ ATL (ARM64) | 16.4.29313.120
Microsoft.VisualStudio.Component.VC.ATL.ARM64.Spectre | 最新 v142 ビルド ツール用 C++ ATL と Spectre 軽減策 (ARM64) | 16.5.29515.121
Microsoft.VisualStudio.Component.VC.ATL.ARM64EC | 最新の v142 ビルド ツール用 C++ ATL (ARM64EC - 試験段階) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.ATL.ARM64EC.Spectre | Spectre の軽減策を含む、最新の v142 ビルド ツール用 C++ ATL (ARM64EC - 試験段階) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.ATL.Spectre | 最新 v142 ビルド ツール用 C++ ATL と Spectre 軽減策 (x86 & x64) | 16.5.29515.121
Microsoft.VisualStudio.Component.VC.ATLMFC.Spectre | 最新 v142 ビルド ツール用 C++ MFC と Spectre 軽減策 (x86 & x64) | 16.5.29721.120
Microsoft.VisualStudio.Component.VC.MFC.ARM | 最新 v142 ビルド ツールの C++ MFC (ARM) | 16.4.29313.120
Microsoft.VisualStudio.Component.VC.MFC.ARM.Spectre | 最新 v142 ビルド ツール用 C++ MFC と Spectre 軽減策 (ARM) | 16.5.29721.120
Microsoft.VisualStudio.Component.VC.MFC.ARM64 | 最新 v142 ビルド ツールの C++ MFC (ARM64) | 16.4.29313.120
Microsoft.VisualStudio.Component.VC.MFC.ARM64.Spectre | 最新 v142 ビルド ツール用 C++ MFC と Spectre 軽減策 (ARM64) | 16.5.29721.120
Microsoft.VisualStudio.Component.VC.MFC.ARM64EC | 最新の v142 ビルド ツール用 C++ MFC (ARM64EC - 試験段階) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.MFC.ARM64EC.Spectre | Spectre の軽減策を含む、最新の v142 ビルド ツール用 C++ MFC (ARM64EC - 試験段階) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.Redist.MSM | C++ 2019 再頒布可能パッケージ MSM | 16.5.29515.121
Microsoft.VisualStudio.Component.VC.Runtimes.ARM.Spectre | MSVC v142 - VS 2019 C++ ARM Spectre 軽減ライブラリ (最新) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.Runtimes.ARM64.Spectre | MSVC v142 - VS 2019 C++ ARM64 Spectre 軽減ライブラリ (最新) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.Runtimes.ARM64EC.Spectre | MSVC v142 - VS 2019 C++ ARM64EC Spectre 軽減ライブラリ (最新 - 試験段階) | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.Runtimes.x86.x64.Spectre | MSVC v142 - VS 2019 C++ x64/x86 Spectre 軽減ライブラリ (最新)  | 16.10.31205.252
Microsoft.VisualStudio.Component.VC.v141.ARM.Spectre | MSVC v141 - VS 2017 C++ ARM Spectre 軽減ライブラリ (v14.16) | 16.5.29515.121
Microsoft.VisualStudio.Component.VC.v141.ARM64.Spectre | MSVC v141 - VS 2017 C++ ARM64 Spectre 軽減ライブラリ (v14.16) | 16.5.29515.121
Microsoft.VisualStudio.Component.VC.v141.ATL | v141 ビルド ツールの C++ ATL (x86 & x64) | 16.0.28625.61
Microsoft.VisualStudio.Component.VC.v141.ATL.ARM | v141 ビルド ツールの C++ ATL (ARM) | 16.0.28625.61
Microsoft.VisualStudio.Component.VC.v141.ATL.ARM.Spectre | v141 ビルド ツール用 C++ ATL と Spectre 軽減策 (ARM) | 16.5.29721.120
Microsoft.VisualStudio.Component.VC.v141.ATL.ARM64 | v141 ビルド ツールの C++ ATL (ARM64) | 16.0.28625.61
Microsoft.VisualStudio.Component.VC.v141.ATL.ARM64.Spectre | v141 ビルド ツール用 C++ ATL と Spectre 軽減策 (ARM64) | 16.0.28625.61
Microsoft.VisualStudio.Component.VC.v141.ATL.Spectre | v141 ビルド ツール用 C++ ATL と Spectre 軽減策 (x86 & x64) | 16.0.28625.61
Microsoft.VisualStudio.Component.VC.v141.CLI.Support | v141 ビルド ツールの C++/CLI サポート (14.16) | 16.3.29207.166
Microsoft.VisualStudio.Component.VC.v141.MFC | v141 ビルド ツールの C++ MFC (x86 & x64) | 16.0.28625.61
Microsoft.VisualStudio.Component.VC.v141.MFC.ARM | v141 ビルド ツールの C++ MFC (ARM) | 16.2.28915.88
Microsoft.VisualStudio.Component.VC.v141.MFC.ARM.Spectre | v141 ビルド ツール用 C++ MFC と Spectre 軽減策 (ARM) | 16.0.28625.61
Microsoft.VisualStudio.Component.VC.v141.MFC.ARM64 | v141 ビルド ツールの C++ MFC (ARM64) | 16.0.28625.61
Microsoft.VisualStudio.Component.VC.v141.MFC.ARM64.Spectre | v141 ビルド ツール用 C++ MFC と Spectre 軽減策 (ARM64) | 16.0.28625.61
Microsoft.VisualStudio.Component.VC.v141.MFC.Spectre | v141 ビルド ツール用 C++ MFC と Spectre 軽減策 (x86 & x64) | 16.0.28625.61
Microsoft.VisualStudio.Component.VC.v141.x86.x64.Spectre | MSVC v141 - VS 2017 C++ x64/x86 Spectre 軽減ライブラリ (v14.16) | 16.5.29515.121
Microsoft.VisualStudio.Component.VisualStudioData | データソースとサービス参照 | 16.0.28707.177
Microsoft.VisualStudio.Component.WinXP | VS 2017 (v141) ツールの C++ Windows XP サポート [非推奨] | 16.10.31205.252
Microsoft.VisualStudio.Web.Mvc4.ComponentGroup | ASP.NET MVC 4 | 16.10.31205.180
