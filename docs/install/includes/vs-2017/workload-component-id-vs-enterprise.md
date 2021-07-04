---
title: Visual Studio Enterprise 2017 のワークロードとコンポーネント ID
titleSuffix: ''
description: ワークロード ID とコンポーネント ID を使用して、コマンドラインを使用して Visual Studio をインストールするか、VSIX マニフェストで依存関係として指定します。
keywords: ''
author: j-martens
ms.author: jmartens
manager: jmartens
ms.date: 2/12/2019
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.topic: include
ms.openlocfilehash: 977c50d42a5c3b59a397714a656f6fd84d94de36
ms.sourcegitcommit: 6d88913a8b5a9e5eda01d3f95205b4d138f440f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/13/2021
ms.locfileid: "110449873"
---
## <a name="visual-studio-core-editor-included-with-visual-studio-enterprise-2017"></a>Visual Studio のコア エディター (Visual Studio Enterprise 2017 に付属)

**ID:** Microsoft.VisualStudio.Workload.CoreEditor

**説明:** 構文認識コード編集機能、ソース コード管理、作業項目管理などの Visual Studio の基本的なシェル エクスペリエンス。

### <a name="components-included-by-this-workload"></a>このワークロードに含まれるコンポーネント

コンポーネント ID | 名前 | バージョン | 依存関係の種類
--- | --- | --- | ---
Microsoft.VisualStudio.Component.CoreEditor | Visual Studio のコア エディター | 15.8.27729.1 | 必須
Microsoft.VisualStudio.Component.StartPageExperiment.Cpp | C++ ユーザー用 Visual Studio スタート ページ | 15.0.27128.1 | Optional

## <a name="azure-development"></a>Azure の開発

**ID:** Microsoft.VisualStudio.Workload.Azure

**説明:** クラウド アプリの開発、リソースの作成、Docker サポートを含むコンテナーのビルドのための Azure SDK、ツール、プロジェクト。

### <a name="components-included-by-this-workload"></a>このワークロードに含まれるコンポーネント

コンポーネント ID | 名前 | バージョン | 依存関係の種類
--- | --- | --- | ---
Component.Microsoft.VisualStudio.RazorExtension | Razor 言語サービス | 15.0.26720.2 | 必須
Component.Microsoft.VisualStudio.Web.AzureFunctions | Microsoft Azure WebJobs ツール | 15.7.27617.1 | 必須
Component.Microsoft.Web.LibraryManager | ライブラリ マネージャー | 15.8.27705.0 | 必須
Component.WebSocket | WebSocket4Net | 15.0.26606.0 | 必須
Microsoft.Component.ClickOnce | ClickOnce Publishing | 15.8.27825.0 | 必須
Microsoft.Component.MSBuild | MSBuild | 15.7.27520.0 | 必須
Microsoft.Component.NetFX.Core.Runtime | .NET Core ランタイム | 15.0.26208.0 | 必須
Microsoft.Net.Component.4.5.2.TargetingPack | .NET Framework 4.5.2 Targeting Pack | 15.6.27406.0 | 必須
Microsoft.Net.Component.4.5.TargetingPack | .NET Framework 4.5 Targeting Pack | 15.6.27406.0 | 必須
Microsoft.Net.Component.4.6.1.SDK | .NET Framework 4.6.1 SDK | 15.6.27406.0 | 必須
Microsoft.Net.Component.4.6.1.TargetingPack | .NET Framework 4.6.1 Targeting Pack | 15.6.27406.0 | 必須
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | .NET Framework 4.6.1 開発ツール | 15.8.27825.0 | 必須
Microsoft.Net.Core.Component.SDK.2.1 | .NET Core 2.1 開発ツール | 15.8.27924.0 | 必須
Microsoft.NetCore.ComponentGroup.DevelopmentTools.2.1 | .NET Core 2.1 開発ツール | 15.8.27924.0 | 必須
Microsoft.NetCore.ComponentGroup.Web.2.1 | .NET Core 2.1 開発ツール | 15.8.27924.0 | 必須
Microsoft.VisualStudio.Component.Azure.AuthoringTools | Azure Authoring Tools | 15.9.28307.421 | 必須
Microsoft.VisualStudio.Component.Azure.ClientLibs | .NET 用 Azure ライブラリ | 15.0.26208.0 | 必須
Microsoft.VisualStudio.Component.Azure.Compute.Emulator | Azure コンピューティング エミュレーター | 15.9.28307.421 | 必須
Microsoft.VisualStudio.Component.Azure.Storage.Emulator | Azure Storage エミュレーター | 15.9.28125.51 | 必須
Microsoft.VisualStudio.Component.CloudExplorer | Cloud Explorer | 15.9.28230.55 | 必須
Microsoft.VisualStudio.Component.Common.Azure.Tools | 接続および発行ツール | 15.9.28107.0 | 必須
Microsoft.VisualStudio.Component.DockerTools | コンテナー開発ツール | 15.8.27906.1 | 必須
Microsoft.VisualStudio.Component.DockerTools.BuildTools | コンテナーの開発ツール - Build Tools | 15.7.27617.1 | 必須
Microsoft.VisualStudio.Component.FSharp | F# 言語サポート | 15.8.27825.0 | 必須
Microsoft.VisualStudio.Component.FSharp.WebTemplates | Web プロジェクト用の F# 言語サポート | 15.9.28307.421 | 必須
Microsoft.VisualStudio.Component.IISExpress | IIS Express  | 15.0.26208.0 | 必須
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | JavaScript 診断 | 15.8.27729.1 | 必須
Microsoft.VisualStudio.Component.JavaScript.TypeScript | JavaScript および TypeScript の言語サポート | 15.9.28125.51 | 必須
Microsoft.VisualStudio.Component.ManagedDesktop.Core | Managed Desktop Workload コア | 15.8.27729.1 | 必須
Microsoft.VisualStudio.Component.NuGet | NuGet パッケージ マネージャー | 15.9.28016.0 | 必須
Microsoft.VisualStudio.Component.PortableLibrary | .NET ポータブル ライブラリ Targeting Pack | 15.6.27309.0 | 必須
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# および Visual Basic Roslyn コンパイラ | 15.6.27309.0 | 必須
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# および Visual Basic | 15.8.27729.1 | 必須
Microsoft.VisualStudio.Component.SQL.ADAL | SQL ADAL ランタイム | 15.6.27406.0 | 必須
Microsoft.VisualStudio.Component.SQL.CLR | SQL Server の CLR データ型 | 15.0.26208.0 | 必須
Microsoft.VisualStudio.Component.SQL.CMDUtils | SQL Server コマンド ライン ユーティリティ | 15.0.26208.0 | 必須
Microsoft.VisualStudio.Component.SQL.DataSources | SQL Server サポートのためのデータ ソース | 15.0.26621.2 | 必須
Microsoft.VisualStudio.Component.SQL.LocalDB.Runtime | SQL Server Express 2016 LocalDB | 15.7.27617.1 | 必須
Microsoft.VisualStudio.Component.SQL.NCLI | SQL Server Native Client | 15.0.26208.0 | 必須
Microsoft.VisualStudio.Component.SQL.SSDT | SQL Server Data Tools | 15.9.28107.0 | 必須
Microsoft.VisualStudio.Component.Static.Analysis.Tools | スタティック分析ツール | 15.0.26208.0 | 必須
Microsoft.VisualStudio.Component.TextTemplating | テキスト テンプレート変換 | 15.0.26208.0 | 必須
Microsoft.VisualStudio.Component.TypeScript.3.1 | TypeScript 3.1 SDK | 15.0.28218.60 | 必須
Microsoft.VisualStudio.Component.VisualStudioData | データソースとサービス参照 | 15.6.27406.0 | 必須
Microsoft.VisualStudio.Component.Web | ASP.NET と Web の開発ツール | 15.8.27825.0 | 必須
Microsoft.VisualStudio.ComponentGroup.Azure.Prerequisites | Azure 開発の前提条件 | 15.9.28107.0 | 必須
Microsoft.VisualStudio.ComponentGroup.AzureFunctions | Microsoft Azure WebJobs ツール | 15.7.27617.1 | 必須
Microsoft.VisualStudio.ComponentGroup.Web | ASP.NET と Web の開発ツールの前提条件 | 15.9.28219.51 | 必須
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | ASP.NET と Web 開発 | 15.8.27825.0 | 必須
Microsoft.Component.Azure.DataLake.Tools | Azure Data Lake と Stream Analytics ツール | 15.9.28107.0 | 推奨
Microsoft.Net.Component.4.5.1.TargetingPack | .NET Framework 4.5.1 Targeting Pack | 15.6.27406.0 | 推奨
Microsoft.Net.Component.4.6.TargetingPack | .NET Framework 4.6 Targeting Pack | 15.6.27406.0 | 推奨
Microsoft.Net.Component.4.TargetingPack | .NET Framework 4 Targeting Pack | 15.6.27406.0 | 推奨
Microsoft.Net.ComponentGroup.TargetingPacks.Common | .NET Framework 4 – 4.6 開発ツール | 15.6.27406.0 | 推奨
Microsoft.VisualStudio.Component.AspNet45 | 高度な ASP.NET 機能 | 15.7.27625.0 | 推奨
Microsoft.VisualStudio.Component.Azure.MobileAppsSdk | Azure Mobile Apps SDK | 15.7.27625.0 | 推奨
Microsoft.VisualStudio.Component.Azure.ResourceManager.Tools | Azure Resource Manager コア ツール | 15.9.28107.0 | 推奨
Microsoft.VisualStudio.Component.Azure.ServiceFabric.Tools | Service Fabric Tools | 15.8.27825.0 | 推奨
Microsoft.VisualStudio.Component.Azure.Waverton | Azure Cloud Services コア ツール | 15.9.28107.0 | 推奨
Microsoft.VisualStudio.Component.Azure.Waverton.BuildTools | Azure Cloud Services ビルド ツール | 15.7.27617.1 | 推奨
Microsoft.VisualStudio.Component.Debugger.Snapshot | スナップショット デバッガー | 15.8.28010.0 | 推奨
Microsoft.VisualStudio.Component.DiagnosticTools | .NET プロファイル ツール | 15.8.27729.1 | 推奨
Microsoft.VisualStudio.Component.IntelliTrace.FrontEnd | [IntelliTrace] | 15.8.27729.1 | 推奨
Microsoft.VisualStudio.Component.WebDeploy | Web 配置 | 15.8.27729.1 | 推奨
Microsoft.VisualStudio.ComponentGroup.Azure.CloudServices | Azure Cloud Services ツール | 15.0.26504.0 | 推奨
Microsoft.VisualStudio.ComponentGroup.Azure.ResourceManager.Tools | Azure Resource Manager ツール | 15.0.27005.2 | 推奨
Microsoft.Net.Component.4.6.2.SDK | .NET Framework 4.6.2 SDK | 15.6.27406.0 | Optional
Microsoft.Net.Component.4.6.2.TargetingPack | .NET Framework 4.6.2 Targeting Pack | 15.6.27406.0 | Optional
Microsoft.Net.Component.4.7.1.SDK | .NET Framework 4.7.1 SDK | 15.6.27406.0 | Optional
Microsoft.Net.Component.4.7.1.TargetingPack | .NET Framework 4.7.1 Targeting Pack | 15.6.27406.0 | Optional
Microsoft.Net.Component.4.7.2.SDK | .NET Framework 4.7.2 SDK | 15.8.27825.0 | Optional
Microsoft.Net.Component.4.7.2.TargetingPack | .NET Framework 4.7.2 Targeting Pack | 15.8.27825.0 | Optional
Microsoft.Net.Component.4.7.SDK | .NET Framework 4.7 SDK | 15.6.27406.0 | Optional
Microsoft.Net.Component.4.7.TargetingPack | .NET Framework 4.7 Targeting Pack | 15.6.27406.0 | Optional
Microsoft.Net.ComponentGroup.4.6.2.DeveloperTools | .NET Framework 4.6.2 開発ツール | 15.6.27406.0 | Optional
Microsoft.Net.ComponentGroup.4.7.1.DeveloperTools | .NET Framework 4.7.1 開発ツール | 15.6.27406.0 | Optional
Microsoft.Net.ComponentGroup.4.7.2.DeveloperTools | .NET Framework 4.7.2 開発ツール | 15.8.27825.0 | Optional
Microsoft.Net.ComponentGroup.4.7.DeveloperTools | .NET Framework 4.7 開発ツール | 15.6.27406.0 | Optional
Microsoft.Net.Core.Component.SDK | .NET Core 2.0 開発ツール | 15.6.27406.0 | Optional
Microsoft.Net.Core.Component.SDK.1x | .NET Core 1.0 - 1.1 開発ツール | 15.6.27406.0 | Optional
Microsoft.NetCore.1x.ComponentGroup.Web | .NET Core 1.0 - 1.1 Web 用開発ツール | 15.6.27406.0 | Optional
Microsoft.NetCore.ComponentGroup.DevelopmentTools | .NET Core 2.0 開発ツール | 15.8.27729.1 | Optional
Microsoft.NetCore.ComponentGroup.Web | .NET Core 2.0 開発ツール | 15.7.27625.0 | Optional
Microsoft.VisualStudio.Component.Azure.Storage.AzCopy | Azure Storage AzCopy | 15.0.26906.1 | Optional
Microsoft.VisualStudio.Component.Wcf.Tooling | Windows Communication Foundation | 15.8.27924.0 | Optional

## <a name="data-storage-and-processing"></a>データ ストレージとデータ処理

**ID:** Microsoft.VisualStudio.Workload.Data

**説明:** SQL Server、Azure Data Lake、Hadoop を使用してデータ ソリューションの接続、開発、テストを行います。

### <a name="components-included-by-this-workload"></a>このワークロードに含まれるコンポーネント

コンポーネント ID | 名前 | バージョン | 依存関係の種類
--- | --- | --- | ---
Component.Microsoft.VisualStudio.RazorExtension | Razor 言語サービス | 15.0.26720.2 | 推奨
Component.Microsoft.Web.LibraryManager | ライブラリ マネージャー | 15.8.27705.0 | 推奨
Component.Redgate.ReadyRoll | Redgate ReadyRoll Core | 1.17.18155.10346 | 推奨
Component.Redgate.SQLPrompt.VsPackage | Redgate SQL Prompt Core | 9.2.0.5601 | 推奨
Component.Redgate.SQLSearch.VSExtension | Redgate SQL Search | 3.1.7.2062 | 推奨
Component.WebSocket | WebSocket4Net | 15.0.26606.0 | 推奨
Microsoft.Component.Azure.DataLake.Tools | Azure Data Lake と Stream Analytics ツール | 15.9.28107.0 | 推奨
Microsoft.Component.ClickOnce | ClickOnce Publishing | 15.8.27825.0 | 推奨
Microsoft.Component.MSBuild | MSBuild | 15.7.27520.0 | 推奨
Microsoft.Net.Component.4.5.1.TargetingPack | .NET Framework 4.5.1 Targeting Pack | 15.6.27406.0 | 推奨
Microsoft.Net.Component.4.5.2.TargetingPack | .NET Framework 4.5.2 Targeting Pack | 15.6.27406.0 | 推奨
Microsoft.Net.Component.4.5.TargetingPack | .NET Framework 4.5 Targeting Pack | 15.6.27406.0 | 推奨
Microsoft.Net.Component.4.6.1.SDK | .NET Framework 4.6.1 SDK | 15.6.27406.0 | 推奨
Microsoft.Net.Component.4.6.1.TargetingPack | .NET Framework 4.6.1 Targeting Pack | 15.6.27406.0 | 推奨
Microsoft.Net.Component.4.6.TargetingPack | .NET Framework 4.6 Targeting Pack | 15.6.27406.0 | 推奨
Microsoft.Net.Component.4.TargetingPack | .NET Framework 4 Targeting Pack | 15.6.27406.0 | 推奨
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | .NET Framework 4.6.1 開発ツール | 15.8.27825.0 | 推奨
Microsoft.Net.ComponentGroup.TargetingPacks.Common | .NET Framework 4 – 4.6 開発ツール | 15.6.27406.0 | 推奨
Microsoft.Net.Core.Component.SDK.2.1 | .NET Core 2.1 開発ツール | 15.8.27924.0 | 推奨
Microsoft.VisualStudio.Component.Azure.AuthoringTools | Azure Authoring Tools | 15.9.28307.421 | 推奨
Microsoft.VisualStudio.Component.Azure.ClientLibs | .NET 用 Azure ライブラリ | 15.0.26208.0 | 推奨
Microsoft.VisualStudio.Component.Azure.Compute.Emulator | Azure コンピューティング エミュレーター | 15.9.28307.421 | 推奨
Microsoft.VisualStudio.Component.Azure.Storage.Emulator | Azure Storage エミュレーター | 15.9.28125.51 | 推奨
Microsoft.VisualStudio.Component.Azure.Waverton | Azure Cloud Services コア ツール | 15.9.28107.0 | 推奨
Microsoft.VisualStudio.Component.Azure.Waverton.BuildTools | Azure Cloud Services ビルド ツール | 15.7.27617.1 | 推奨
Microsoft.VisualStudio.Component.CloudExplorer | Cloud Explorer | 15.9.28230.55 | 推奨
Microsoft.VisualStudio.Component.Common.Azure.Tools | 接続および発行ツール | 15.9.28107.0 | 推奨
Microsoft.VisualStudio.Component.DockerTools | コンテナー開発ツール | 15.8.27906.1 | 推奨
Microsoft.VisualStudio.Component.DockerTools.BuildTools | コンテナーの開発ツール - Build Tools | 15.7.27617.1 | 推奨
Microsoft.VisualStudio.Component.IISExpress | IIS Express  | 15.0.26208.0 | 推奨
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | JavaScript 診断 | 15.8.27729.1 | 推奨
Microsoft.VisualStudio.Component.JavaScript.TypeScript | JavaScript および TypeScript の言語サポート | 15.9.28125.51 | 推奨
Microsoft.VisualStudio.Component.ManagedDesktop.Core | Managed Desktop Workload コア | 15.8.27729.1 | 推奨
Microsoft.VisualStudio.Component.NuGet | NuGet パッケージ マネージャー | 15.9.28016.0 | 推奨
Microsoft.VisualStudio.Component.PortableLibrary | .NET ポータブル ライブラリ Targeting Pack | 15.6.27309.0 | 推奨
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# および Visual Basic Roslyn コンパイラ | 15.6.27309.0 | 推奨
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# および Visual Basic | 15.8.27729.1 | 推奨
Microsoft.VisualStudio.Component.SQL.ADAL | SQL ADAL ランタイム | 15.6.27406.0 | 推奨
Microsoft.VisualStudio.Component.SQL.CLR | SQL Server の CLR データ型 | 15.0.26208.0 | 推奨
Microsoft.VisualStudio.Component.SQL.CMDUtils | SQL Server コマンド ライン ユーティリティ | 15.0.26208.0 | 推奨
Microsoft.VisualStudio.Component.SQL.DataSources | SQL Server サポートのためのデータ ソース | 15.0.26621.2 | 推奨
Microsoft.VisualStudio.Component.SQL.LocalDB.Runtime | SQL Server Express 2016 LocalDB | 15.7.27617.1 | 推奨
Microsoft.VisualStudio.Component.SQL.NCLI | SQL Server Native Client | 15.0.26208.0 | 推奨
Microsoft.VisualStudio.Component.SQL.SSDT | SQL Server Data Tools | 15.9.28107.0 | 推奨
Microsoft.VisualStudio.Component.Static.Analysis.Tools | スタティック分析ツール | 15.0.26208.0 | 推奨
Microsoft.VisualStudio.Component.TextTemplating | テキスト テンプレート変換 | 15.0.26208.0 | 推奨
Microsoft.VisualStudio.Component.TypeScript.3.1 | TypeScript 3.1 SDK | 15.0.28218.60 | 推奨
Microsoft.VisualStudio.Component.VisualStudioData | データソースとサービス参照 | 15.6.27406.0 | 推奨
Microsoft.VisualStudio.Component.Web | ASP.NET と Web の開発ツール | 15.8.27825.0 | 推奨
Microsoft.VisualStudio.ComponentGroup.Web | ASP.NET と Web の開発ツールの前提条件 | 15.9.28219.51 | 推奨
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | ASP.NET と Web 開発 | 15.8.27825.0 | 推奨
Microsoft.VisualStudio.Component.FSharp.Desktop | F# デスクトップ言語のサポート | 15.8.27825.0 | Optional

## <a name="data-science-and-analytical-applications"></a>データ サイエンスと分析のアプリケーション

**ID:** Microsoft.VisualStudio.Workload.DataScience

**説明:** Python、R、F# など、データ サイエンス アプリケーションを作成するための言語とツール。

### <a name="components-included-by-this-workload"></a>このワークロードに含まれるコンポーネント

コンポーネント ID | 名前 | バージョン | 依存関係の種類
--- | --- | --- | ---
Component.Anaconda3.x64 | Anaconda3 64 ビット (5.2.0) | 5.2.0 | 推奨
Microsoft.Component.CookiecutterTools | cookiecutter テンプレートのサポート | 15.0.26621.2 | 推奨
Microsoft.Component.PythonTools | Python 言語サポート | 15.0.26823.1 | 推奨
Microsoft.Component.PythonTools.Web | Python Web サポート | 15.9.28107.0 | 推奨
Microsoft.Net.Component.4.6.1.TargetingPack | .NET Framework 4.6.1 Targeting Pack | 15.6.27406.0 | 推奨
Microsoft.VisualStudio.Component.Common.Azure.Tools | 接続および発行ツール | 15.9.28107.0 | 推奨
Microsoft.VisualStudio.Component.FSharp.Desktop | F# デスクトップ言語のサポート | 15.8.27825.0 | 推奨
Microsoft.VisualStudio.Component.JavaScript.TypeScript | JavaScript および TypeScript の言語サポート | 15.9.28125.51 | 推奨
Microsoft.VisualStudio.Component.NuGet | NuGet パッケージ マネージャー | 15.9.28016.0 | 推奨
Microsoft.VisualStudio.Component.R.Open | Microsoft R クライアント (3.3.2) | 15.6.27406.0 | 推奨
Microsoft.VisualStudio.Component.RHost | R 開発ツールのランタイム サポート | 15.6.27406.0 | 推奨
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# および Visual Basic Roslyn コンパイラ | 15.6.27309.0 | 推奨
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# および Visual Basic | 15.8.27729.1 | 推奨
Microsoft.VisualStudio.Component.RTools | R 言語サポート | 15.0.26919.1 | 推奨
Microsoft.VisualStudio.Component.SQL.CLR | SQL Server の CLR データ型 | 15.0.26208.0 | 推奨
Microsoft.VisualStudio.Component.Static.Analysis.Tools | スタティック分析ツール | 15.0.26208.0 | 推奨
Microsoft.VisualStudio.Component.TypeScript.3.1 | TypeScript 3.1 SDK | 15.0.28218.60 | 推奨
Microsoft.VisualStudio.Component.VisualStudioData | データソースとサービス参照 | 15.6.27406.0 | 推奨
Microsoft.VisualStudio.Component.WebDeploy | Web 配置 | 15.8.27729.1 | 推奨
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | ASP.NET と Web 開発 | 15.8.27825.0 | 推奨
Component.Anaconda2.x64 | Anaconda2 64 ビット (5.2.0) | 5.2.0 | Optional
Component.Anaconda2.x86 | Anaconda2 32 ビット (5.2.0) | 5.2.0 | Optional
Component.Anaconda3.x86 | Anaconda3 32 ビット (5.2.0) | 5.2.0 | Optional
Microsoft.Component.VC.Runtime.UCRTSDK | Windows Universal CRT SDK | 15.6.27309.0 | Optional
Microsoft.ComponentGroup.PythonTools.NativeDevelopment | Python ネイティブ開発ツール | 15.9.28307.102 | Optional
Microsoft.VisualStudio.Component.Graphics.Tools | DirectX 用グラフィックス デバッガーおよび GPU プロファイラー | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Graphics.Win81 | グラフィックス ツール Windows 8.1 SDK | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.VC.140 | デスクトップ用 VC++ 2015.3 v14.00 (v140) ツールセット | 15.7.27617.1 | Optional
Microsoft.VisualStudio.Component.VC.CoreIde | Visual Studio C++ コア機能 | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.VC.DiagnosticTools | C++ のプロファイル ツール | 15.0.26823.1 | Optional
Microsoft.VisualStudio.Component.VC.Tools.x86.x64 | VC++ 2017 バージョン 15.9 v14.16 最新の v141 ツール | 15.9.28230.55 | Optional
Microsoft.VisualStudio.Component.Windows10SDK | Windows ユニバーサル C ランタイム | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.17763 | Windows 10 SDK (10.0.17763.0) | 15.9.28307.102 | Optional
Microsoft.VisualStudio.Component.Windows81SDK | Windows 8.1 SDK | 15.6.27406.0 | Optional

## <a name="net-desktop-development"></a>.NET デスクトップ開発

**ID:** Microsoft.VisualStudio.Workload.ManagedDesktop

**説明:** C#、Visual Basic、F# を使用して、WPF、Windows フォーム、コンソール アプリケーションをビルドします。

### <a name="components-included-by-this-workload"></a>このワークロードに含まれるコンポーネント

コンポーネント ID | 名前 | バージョン | 依存関係の種類
--- | --- | --- | ---
Microsoft.Component.ClickOnce | ClickOnce Publishing | 15.8.27825.0 | 必須
Microsoft.Component.MSBuild | MSBuild | 15.7.27520.0 | 必須
Microsoft.Net.Component.4.6.1.SDK | .NET Framework 4.6.1 SDK | 15.6.27406.0 | 必須
Microsoft.Net.Component.4.6.1.TargetingPack | .NET Framework 4.6.1 Targeting Pack | 15.6.27406.0 | 必須
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | .NET Framework 4.6.1 開発ツール | 15.8.27825.0 | 必須
Microsoft.VisualStudio.Component.ManagedDesktop.Core | Managed Desktop Workload コア | 15.8.27729.1 | 必須
Microsoft.VisualStudio.Component.ManagedDesktop.Prerequisites | .NET デスクトップ開発ツール | 15.7.27625.0 | 必須
Microsoft.VisualStudio.Component.PortableLibrary | .NET ポータブル ライブラリ Targeting Pack | 15.6.27309.0 | 必須
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# および Visual Basic Roslyn コンパイラ | 15.6.27309.0 | 必須
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# および Visual Basic | 15.8.27729.1 | 必須
Microsoft.VisualStudio.Component.SQL.CLR | SQL Server の CLR データ型 | 15.0.26208.0 | 必須
Microsoft.VisualStudio.Component.Static.Analysis.Tools | スタティック分析ツール | 15.0.26208.0 | 必須
Microsoft.VisualStudio.Component.TextTemplating | テキスト テンプレート変換 | 15.0.26208.0 | 必須
Microsoft.VisualStudio.Component.VisualStudioData | データソースとサービス参照 | 15.6.27406.0 | 必須
Microsoft.ComponentGroup.Blend | Blend for Visual Studio | 15.6.27406.0 | 推奨
Microsoft.Net.Component.4.5.1.TargetingPack | .NET Framework 4.5.1 Targeting Pack | 15.6.27406.0 | 推奨
Microsoft.Net.Component.4.5.2.TargetingPack | .NET Framework 4.5.2 Targeting Pack | 15.6.27406.0 | 推奨
Microsoft.Net.Component.4.5.TargetingPack | .NET Framework 4.5 Targeting Pack | 15.6.27406.0 | 推奨
Microsoft.Net.Component.4.6.TargetingPack | .NET Framework 4.6 Targeting Pack | 15.6.27406.0 | 推奨
Microsoft.Net.Component.4.TargetingPack | .NET Framework 4 Targeting Pack | 15.6.27406.0 | 推奨
Microsoft.Net.ComponentGroup.TargetingPacks.Common | .NET Framework 4 – 4.6 開発ツール | 15.6.27406.0 | 推奨
Microsoft.VisualStudio.Component.Debugger.JustInTime | Just-In-Time デバッガー | 15.0.27005.2 | 推奨
Microsoft.VisualStudio.Component.DiagnosticTools | .NET プロファイル ツール | 15.8.27729.1 | 推奨
Microsoft.VisualStudio.Component.EntityFramework | Entity Framework 6 Tools | 15.6.27406.0 | 推奨
Microsoft.VisualStudio.Component.IntelliTrace.FrontEnd | [IntelliTrace] | 15.8.27729.1 | 推奨
Microsoft.VisualStudio.Component.LiveUnitTesting | Live Unit Testing | 15.0.26720.2 | 推奨
Component.Dotfuscator | PreEmptive Protection - Dotfuscator | 15.0.26208.0 | Optional
Component.Microsoft.VisualStudio.RazorExtension | Razor 言語サービス | 15.0.26720.2 | Optional
Component.Microsoft.Web.LibraryManager | ライブラリ マネージャー | 15.8.27705.0 | オプション
Component.WebSocket | WebSocket4Net | 15.0.26606.0 | Optional
Microsoft.Net.Component.4.6.2.SDK | .NET Framework 4.6.2 SDK | 15.6.27406.0 | Optional
Microsoft.Net.Component.4.6.2.TargetingPack | .NET Framework 4.6.2 Targeting Pack | 15.6.27406.0 | Optional
Microsoft.Net.Component.4.7.1.SDK | .NET Framework 4.7.1 SDK | 15.6.27406.0 | Optional
Microsoft.Net.Component.4.7.1.TargetingPack | .NET Framework 4.7.1 Targeting Pack | 15.6.27406.0 | Optional
Microsoft.Net.Component.4.7.2.SDK | .NET Framework 4.7.2 SDK | 15.8.27825.0 | Optional
Microsoft.Net.Component.4.7.2.TargetingPack | .NET Framework 4.7.2 Targeting Pack | 15.8.27825.0 | Optional
Microsoft.Net.Component.4.7.SDK | .NET Framework 4.7 SDK | 15.6.27406.0 | Optional
Microsoft.Net.Component.4.7.TargetingPack | .NET Framework 4.7 Targeting Pack | 15.6.27406.0 | Optional
Microsoft.Net.ComponentGroup.4.6.2.DeveloperTools | .NET Framework 4.6.2 開発ツール | 15.6.27406.0 | Optional
Microsoft.Net.ComponentGroup.4.7.1.DeveloperTools | .NET Framework 4.7.1 開発ツール | 15.6.27406.0 | Optional
Microsoft.Net.ComponentGroup.4.7.2.DeveloperTools | .NET Framework 4.7.2 開発ツール | 15.8.27825.0 | Optional
Microsoft.Net.ComponentGroup.4.7.DeveloperTools | .NET Framework 4.7 開発ツール | 15.6.27406.0 | Optional
Microsoft.Net.Core.Component.SDK | .NET Core 2.0 開発ツール | 15.6.27406.0 | Optional
Microsoft.Net.Core.Component.SDK.1x | .NET Core 1.0 - 1.1 開発ツール | 15.6.27406.0 | Optional
Microsoft.Net.Core.Component.SDK.2.1 | .NET Core 2.1 開発ツール | 15.8.27924.0 | Optional
Microsoft.NetCore.ComponentGroup.DevelopmentTools | .NET Core 2.0 開発ツール | 15.8.27729.1 | Optional
Microsoft.NetCore.ComponentGroup.DevelopmentTools.2.1 | .NET Core 2.1 開発ツール | 15.8.27924.0 | Optional
Microsoft.VisualStudio.Component.CodeClone | コード クローン | 15.0.26208.0 | Optional
Microsoft.VisualStudio.Component.CodeMap | コード マップ | 15.0.26208.0 | Optional
Microsoft.VisualStudio.Component.Common.Azure.Tools | 接続および発行ツール | 15.9.28107.0 | Optional
Microsoft.VisualStudio.Component.DependencyValidation.Enterprise | ライブ依存関係検証 | 15.0.26208.0 | Optional
Microsoft.VisualStudio.Component.DockerTools | コンテナー開発ツール | 15.8.27906.1 | オプション
Microsoft.VisualStudio.Component.DockerTools.BuildTools | コンテナーの開発ツール - Build Tools | 15.7.27617.1 | Optional
Microsoft.VisualStudio.Component.FSharp | F# 言語サポート | 15.8.27825.0 | Optional
Microsoft.VisualStudio.Component.FSharp.Desktop | F# デスクトップ言語のサポート | 15.8.27825.0 | Optional
Microsoft.VisualStudio.Component.GraphDocument | DGML エディター | 15.0.27005.2 | Optional
Microsoft.VisualStudio.Component.IISExpress | IIS Express  | 15.0.26208.0 | Optional
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | JavaScript 診断 | 15.8.27729.1 | Optional
Microsoft.VisualStudio.Component.JavaScript.TypeScript | JavaScript および TypeScript の言語サポート | 15.9.28125.51 | Optional
Microsoft.VisualStudio.Component.NuGet | NuGet パッケージ マネージャー | 15.9.28016.0 | Optional
Microsoft.VisualStudio.Component.SQL.ADAL | SQL ADAL ランタイム | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.SQL.CMDUtils | SQL Server コマンド ライン ユーティリティ | 15.0.26208.0 | Optional
Microsoft.VisualStudio.Component.SQL.DataSources | SQL Server サポートのためのデータ ソース | 15.0.26621.2 | Optional
Microsoft.VisualStudio.Component.SQL.LocalDB.Runtime | SQL Server Express 2016 LocalDB | 15.7.27617.1 | Optional
Microsoft.VisualStudio.Component.SQL.NCLI | SQL Server Native Client | 15.0.26208.0 | Optional
Microsoft.VisualStudio.Component.SQL.SSDT | SQL Server Data Tools | 15.9.28107.0 | Optional
Microsoft.VisualStudio.Component.TypeScript.3.1 | TypeScript 3.1 SDK | 15.0.28218.60 | Optional
Microsoft.VisualStudio.Component.Wcf.Tooling | Windows Communication Foundation | 15.8.27924.0 | Optional
Microsoft.VisualStudio.Component.Web | ASP.NET と Web の開発ツール | 15.8.27825.0 | Optional
Microsoft.VisualStudio.ComponentGroup.ArchitectureTools.Managed | アーキテクチャおよび分析ツール | 15.0.26208.0 | Optional
Microsoft.VisualStudio.ComponentGroup.Web | ASP.NET と Web の開発ツールの前提条件 | 15.9.28219.51 | Optional
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | ASP.NET と Web 開発 | 15.8.27825.0 | Optional

## <a name="game-development-with-unity"></a>Unity でのゲーム開発

**ID:** Microsoft.VisualStudio.Workload.ManagedGame

**説明:** 強力なクロスプラットフォーム開発環境である Unity を使って、2D および 3D ゲームを作成します。

### <a name="components-included-by-this-workload"></a>このワークロードに含まれるコンポーネント

コンポーネント ID | 名前 | バージョン | 依存関係の種類
--- | --- | --- | ---
Microsoft.Net.Component.3.5.DeveloperTools | .NET Framework 3.5 開発ツール | 15.6.27406.0 | 必須
Microsoft.Net.Component.4.7.1.TargetingPack | .NET Framework 4.7.1 Targeting Pack | 15.6.27406.0 | 必須
Microsoft.VisualStudio.Component.NuGet | NuGet パッケージ マネージャー | 15.9.28016.0 | 必須
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# および Visual Basic Roslyn コンパイラ | 15.6.27309.0 | 必須
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# および Visual Basic | 15.8.27729.1 | 必須
Microsoft.VisualStudio.Component.Static.Analysis.Tools | スタティック分析ツール | 15.0.26208.0 | 必須
Microsoft.VisualStudio.Component.Unity | Visual Studio Tools for Unity | 15.7.27617.1 | 必須
Component.UnityEngine.x64 | Unity 2018.3 64 ビット エディター | 15.9.28307.271 | 推奨
Component.UnityEngine.x86 | Unity 5.6 32 ビット エディター | 15.6.27406.0 | 推奨

## <a name="linux-development-with-c"></a>C++ による Linux 開発

**ID:** Microsoft.VisualStudio.Workload.NativeCrossPlat

**説明:** Linux 環境で実行するアプリケーションを作成およびデバッグします。

### <a name="components-included-by-this-workload"></a>このワークロードに含まれるコンポーネント

コンポーネント ID | 名前 | バージョン | 依存関係の種類
--- | --- | --- | ---
Component.MDD.Linux | Visual C++ for Linux Development | 15.6.27406.0 | 必須
Microsoft.VisualStudio.Component.VC.CoreIde | Visual Studio C++ コア機能 | 15.6.27406.0 | 必須
Microsoft.VisualStudio.Component.Windows10SDK | Windows ユニバーサル C ランタイム | 15.6.27406.0 | 必須
Component.Linux.CMake | CMake および Linux 用 Visual C++ ツール | 15.9.28307.102 | 推奨
Microsoft.VisualStudio.Component.Static.Analysis.Tools | スタティック分析ツール | 15.0.26208.0 | 推奨
Microsoft.VisualStudio.Component.VC.Tools.x86.x64 | VC++ 2017 バージョン 15.9 v14.16 最新の v141 ツール | 15.9.28230.55 | 推奨
Microsoft.VisualStudio.Component.Windows10SDK.17763 | Windows 10 SDK (10.0.17763.0) | 15.9.28307.102 | 推奨
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | ASP.NET と Web 開発 | 15.8.27825.0 | 推奨
Component.MDD.Linux.GCC.arm | Embedded 開発と IoT 開発 | 15.6.27309.0 | Optional

## <a name="desktop-development-with-c"></a>C++ によるデスクトップ開発

**ID:** Microsoft.VisualStudio.Workload.NativeDesktop

**説明:** Microsoft C++ ツールセット、ATL、MFC を使用して Windows のデスクトップ アプリケーションをビルドします。

### <a name="components-included-by-this-workload"></a>このワークロードに含まれるコンポーネント

コンポーネント ID | 名前 | バージョン | 依存関係の種類
--- | --- | --- | ---
Microsoft.Component.MSBuild | MSBuild | 15.7.27520.0 | 必須
Microsoft.VisualStudio.Component.ClassDesigner | クラス デザイナー | 15.0.26208.0 | 必須
Microsoft.VisualStudio.Component.CodeMap | コード マップ | 15.0.26208.0 | 必須
Microsoft.VisualStudio.Component.GraphDocument | DGML エディター | 15.0.27005.2 | 必須
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# および Visual Basic Roslyn コンパイラ | 15.6.27309.0 | 必須
Microsoft.VisualStudio.Component.SQL.LocalDB.Runtime | SQL Server Express 2016 LocalDB | 15.7.27617.1 | 必須
Microsoft.VisualStudio.Component.SQL.NCLI | SQL Server Native Client | 15.0.26208.0 | 必須
Microsoft.VisualStudio.Component.TextTemplating | テキスト テンプレート変換 | 15.0.26208.0 | 必須
Microsoft.VisualStudio.Component.VC.CoreIde | Visual Studio C++ コア機能 | 15.6.27406.0 | 必須
Microsoft.VisualStudio.Component.VC.Redist.14.Latest | Visual C++ 2017 再頒布可能パッケージ Update | 15.6.27406.0 | 必須
Microsoft.VisualStudio.ComponentGroup.ArchitectureTools.Native | C++ 用のアーキテクチャ ツール | 15.0.26208.0 | 必須
Microsoft.VisualStudio.ComponentGroup.NativeDesktop.Core | Visual C++ コア デスクトップ機能 | 15.8.27729.1 | 必須
Microsoft.VisualStudio.Component.Debugger.JustInTime | Just-In-Time デバッガー | 15.0.27005.2 | 推奨
Microsoft.VisualStudio.Component.Graphics.Tools | DirectX 用グラフィックス デバッガーおよび GPU プロファイラー | 15.6.27406.0 | 推奨
Microsoft.VisualStudio.Component.Graphics.Win81 | グラフィックス ツール Windows 8.1 SDK | 15.6.27406.0 | 推奨
Microsoft.VisualStudio.Component.IntelliTrace.FrontEnd | [IntelliTrace] | 15.8.27729.1 | 推奨
Microsoft.VisualStudio.Component.NuGet | NuGet パッケージ マネージャー | 15.9.28016.0 | 推奨
Microsoft.VisualStudio.Component.Static.Analysis.Tools | スタティック分析ツール | 15.0.26208.0 | 推奨
Microsoft.VisualStudio.Component.VC.ATL | x86 用と x64 用の Visual C++ ATL | 15.7.27625.0 | 推奨
Microsoft.VisualStudio.Component.VC.CMake.Project | CMake の Visual C++ ツール | 15.9.28307.102 | 推奨
Microsoft.VisualStudio.Component.VC.DiagnosticTools | C++ のプロファイル ツール | 15.0.26823.1 | 推奨
Microsoft.VisualStudio.Component.VC.TestAdapterForBoostTest | Test Adapter for Boost.Test | 15.8.27906.1 | 推奨
Microsoft.VisualStudio.Component.VC.TestAdapterForGoogleTest | Test Adapter for Google Test | 15.8.27906.1 | 推奨
Microsoft.VisualStudio.Component.VC.Tools.x86.x64 | VC++ 2017 バージョン 15.9 v14.16 最新の v141 ツール | 15.9.28230.55 | 推奨
Microsoft.VisualStudio.Component.Windows10SDK.17763 | Windows 10 SDK (10.0.17763.0) | 15.9.28307.102 | 推奨
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | ASP.NET と Web 開発 | 15.8.27825.0 | 推奨
Component.Incredibuild | IncrediBuild - ビルド アクセラレーション | 15.7.27617.1 | Optional
Component.IncredibuildMenu | IncrediBuildMenu | 1.5.0.2 | Optional
Microsoft.Component.VC.Runtime.UCRTSDK | Windows Universal CRT SDK | 15.6.27309.0 | Optional
Microsoft.Net.Component.4.6.1.SDK | .NET Framework 4.6.1 SDK | 15.6.27406.0 | Optional
Microsoft.Net.Component.4.6.1.TargetingPack | .NET Framework 4.6.1 Targeting Pack | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.VC.140 | デスクトップ用 VC++ 2015.3 v14.00 (v140) ツールセット | 15.7.27617.1 | Optional
Microsoft.VisualStudio.Component.VC.ATLMFC | x86 用と x64 用の Visual C++ MFC | 15.7.27625.0 | Optional
Microsoft.VisualStudio.Component.VC.CLI.Support | C++/CLI サポート | 15.6.27309.0 | Optional
Microsoft.VisualStudio.Component.VC.Modules.x86.x64 | 標準ライブラリ用モジュール (試験段階) | 15.6.27309.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.10240 | Windows 10 SDK (10.0.10240.0) | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.10586 | Windows 10 SDK (10.0.10586.0) | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.14393 | Windows 10 SDK (10.0.14393.0) | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.15063.Desktop | デスクトップ用 Windows 10 SDK (10.0.15063.0) C++ [x86 および x64] | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.15063.UWP | UWP 用 Windows 10 SDK (10.0.15063.0): C#、VB、JS | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.15063.UWP.Native | UWP 用 Windows 10 SDK (10.0.15063.0): C++ | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.16299.Desktop | デスクトップ用 Windows 10 SDK (10.0.16299.0) C++ [x86 および x64] | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.16299.Desktop.arm | デスクトップ用 Windows 10 SDK (10.0.16299.0) C++ [ARM および ARM64] | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.16299.UWP | UWP 用 Windows 10 SDK (10.0.16299.0): C#、VB、JS | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.16299.UWP.Native | UWP 用 Windows 10 SDK (10.0.16299.0): C++ | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.17134 | Windows 10 SDK (10.0.17134.0) | 15.9.28307.102 | Optional
Microsoft.VisualStudio.Component.Windows81SDK | Windows 8.1 SDK | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.WinXP | C++ に関する Windows XP サポート | 15.8.27924.0 | Optional
Microsoft.VisualStudio.ComponentGroup.NativeDesktop.Win81 | Windows 8.1 SDK と UCRT SDK | 15.6.27406.0 | Optional
Microsoft.VisualStudio.ComponentGroup.NativeDesktop.WinXP | C++ に関する Windows XP サポート | 15.8.27705.0 | オプション
Microsoft.VisualStudio.ComponentGroup.Windows10SDK.15063 | Windows 10 SDK (10.0.15063.0) | 15.8.27825.0 | Optional
Microsoft.VisualStudio.ComponentGroup.Windows10SDK.16299 | Windows 10 SDK (10.0.16299.0) | 15.8.27825.0 | Optional

## <a name="game-development-with-c"></a>C++ によるゲーム開発

**ID:** Microsoft.VisualStudio.Workload.NativeGame

**説明:** C++ を最大限に活用して、DirectX、Unreal、Cocos2d を利用するプロフェッショナルなゲームを構築します。

### <a name="components-included-by-this-workload"></a>このワークロードに含まれるコンポーネント

コンポーネント ID | 名前 | バージョン | 依存関係の種類
--- | --- | --- | ---
Microsoft.VisualStudio.Component.Static.Analysis.Tools | スタティック分析ツール | 15.0.26208.0 | 必須
Microsoft.VisualStudio.Component.VC.CoreIde | Visual Studio C++ コア機能 | 15.6.27406.0 | 必須
Microsoft.VisualStudio.Component.VC.Redist.14.Latest | Visual C++ 2017 再頒布可能パッケージ Update | 15.6.27406.0 | 必須
Microsoft.VisualStudio.Component.VC.Tools.x86.x64 | VC++ 2017 バージョン 15.9 v14.16 最新の v141 ツール | 15.9.28230.55 | 必須
Microsoft.VisualStudio.Component.Windows10SDK | Windows ユニバーサル C ランタイム | 15.6.27406.0 | 必須
Microsoft.VisualStudio.Component.Graphics.Tools | DirectX 用グラフィックス デバッガーおよび GPU プロファイラー | 15.6.27406.0 | 推奨
Microsoft.VisualStudio.Component.Graphics.Win81 | グラフィックス ツール Windows 8.1 SDK | 15.6.27406.0 | 推奨
Microsoft.VisualStudio.Component.IntelliTrace.FrontEnd | [IntelliTrace] | 15.8.27729.1 | 推奨
Microsoft.VisualStudio.Component.VC.DiagnosticTools | C++ のプロファイル ツール | 15.0.26823.1 | 推奨
Microsoft.VisualStudio.Component.Windows10SDK.17763 | Windows 10 SDK (10.0.17763.0) | 15.9.28307.102 | 推奨
Component.Android.NDK.R12B | Android NDK (R12B) | 12.1.10 | オプション
Component.Android.SDK23.Private | Android SDK セットアップ (API レベル 23) (JavaScript/C++ を使用したモバイル開発のためにローカルにインストール) | 15.9.28016.0 | Optional
Component.Ant | Apache Ant (1.9.3) | 1.9.3.8 | Optional
Component.Cocos | Cocos | 15.0.26906.1 | Optional
Component.Incredibuild | IncrediBuild - ビルド アクセラレーション | 15.7.27617.1 | Optional
Component.IncredibuildMenu | IncrediBuildMenu | 1.5.0.2 | Optional
Component.MDD.Android | C++ Android 開発ツール | 15.0.26606.0 | Optional
Component.OpenJDK | Microsoft 配布の OpenJDK | 15.9.28125.51 | Optional
Component.Unreal | Unreal Engine のインストーラー | 15.8.27729.1 | Optional
Component.Unreal.Android | Unreal Engine 用の Visual Studio Android サポート | 15.9.28307.341 | Optional
Microsoft.Component.VC.Runtime.UCRTSDK | Windows Universal CRT SDK | 15.6.27309.0 | Optional
Microsoft.Net.Component.4.5.1.TargetingPack | .NET Framework 4.5.1 Targeting Pack | 15.6.27406.0 | Optional
Microsoft.Net.Component.4.5.2.TargetingPack | .NET Framework 4.5.2 Targeting Pack | 15.6.27406.0 | Optional
Microsoft.Net.Component.4.5.TargetingPack | .NET Framework 4.5 Targeting Pack | 15.6.27406.0 | Optional
Microsoft.Net.Component.4.6.1.SDK | .NET Framework 4.6.1 SDK | 15.6.27406.0 | Optional
Microsoft.Net.Component.4.6.1.TargetingPack | .NET Framework 4.6.1 Targeting Pack | 15.6.27406.0 | Optional
Microsoft.Net.Component.4.6.TargetingPack | .NET Framework 4.6 Targeting Pack | 15.6.27406.0 | Optional
Microsoft.Net.Component.4.TargetingPack | .NET Framework 4 Targeting Pack | 15.6.27406.0 | Optional
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | .NET Framework 4.6.1 開発ツール | 15.8.27825.0 | Optional
Microsoft.Net.ComponentGroup.TargetingPacks.Common | .NET Framework 4 – 4.6 開発ツール | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.NuGet.BuildTools | NuGet ターゲットとビルド タスク | 15.9.28016.0 | Optional
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# および Visual Basic Roslyn コンパイラ | 15.6.27309.0 | Optional
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# および Visual Basic | 15.8.27729.1 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.10240 | Windows 10 SDK (10.0.10240.0) | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.10586 | Windows 10 SDK (10.0.10586.0) | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.14393 | Windows 10 SDK (10.0.14393.0) | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.15063.Desktop | デスクトップ用 Windows 10 SDK (10.0.15063.0) C++ [x86 および x64] | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.15063.UWP | UWP 用 Windows 10 SDK (10.0.15063.0): C#、VB、JS | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.15063.UWP.Native | UWP 用 Windows 10 SDK (10.0.15063.0): C++ | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.16299.Desktop | デスクトップ用 Windows 10 SDK (10.0.16299.0) C++ [x86 および x64] | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.16299.Desktop.arm | デスクトップ用 Windows 10 SDK (10.0.16299.0) C++ [ARM および ARM64] | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.16299.UWP | UWP 用 Windows 10 SDK (10.0.16299.0): C#、VB、JS | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.16299.UWP.Native | UWP 用 Windows 10 SDK (10.0.16299.0): C++ | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.17134 | Windows 10 SDK (10.0.17134.0) | 15.9.28307.102 | Optional
Microsoft.VisualStudio.Component.Windows81SDK | Windows 8.1 SDK | 15.6.27406.0 | Optional
Microsoft.VisualStudio.ComponentGroup.NativeDesktop.Win81 | Windows 8.1 SDK と UCRT SDK | 15.6.27406.0 | Optional
Microsoft.VisualStudio.ComponentGroup.Windows10SDK.15063 | Windows 10 SDK (10.0.15063.0) | 15.8.27825.0 | Optional
Microsoft.VisualStudio.ComponentGroup.Windows10SDK.16299 | Windows 10 SDK (10.0.16299.0) | 15.8.27825.0 | Optional

## <a name="mobile-development-with-c"></a>C++ でのモバイル開発

**ID:** Microsoft.VisualStudio.Workload.NativeMobile

**説明:** iOS、Android、Windows 向けのクロスプラットフォーム アプリケーションを、C++ を使って構築します。

### <a name="components-included-by-this-workload"></a>このワークロードに含まれるコンポーネント

コンポーネント ID | 名前 | バージョン | 依存関係の種類
--- | --- | --- | ---
Component.Android.SDK19.Private | Android SDK セットアップ (API レベル 19) (Javascript/C++ を使用したモバイル開発のためにローカルにインストール) | 15.9.28107.0 | 必須
Component.Android.SDK21.Private | Android SDK セットアップ (API レベル 21) (Javascript/C++ を使用したモバイル開発のためにローカルにインストール) | 15.9.28016.0 | 必須
Component.Android.SDK22.Private | Android SDK セットアップ (API レベル 22) (Javascript/C++ を使用したモバイル開発のためにローカルにインストール) | 15.9.28016.0 | 必須
Component.Android.SDK23.Private | Android SDK セットアップ (API レベル 23) (JavaScript/C++ を使用したモバイル開発のためにローカルにインストール) | 15.9.28016.0 | 必須
Component.Android.SDK25.Private | Android SDK セットアップ (API レベル 25) (Javascript/C++ を使用したモバイル開発のためにローカルにインストール) | 15.9.28016.0 | 必須
Component.OpenJDK | Microsoft 配布の OpenJDK | 15.9.28125.51 | 必須
Microsoft.VisualStudio.Component.VC.CoreIde | Visual Studio C++ コア機能 | 15.6.27406.0 | 必須
Component.Android.NDK.R15C | Android NDK (R15C) | 15.2.1 | 推奨
Component.Ant | Apache Ant (1.9.3) | 1.9.3.8 | 推奨
Component.MDD.Android | C++ Android 開発ツール | 15.0.26606.0 | 推奨
Component.Android.NDK.R12B | Android NDK (R12B) | 12.1.10 | オプション
Component.Android.NDK.R12B_3264 | Android NDK (R12B) (32 ビット) | 12.1.11 | オプション
Component.Android.NDK.R13B | Android NDK (R13B) | 13.1.7 | オプション
Component.Android.NDK.R13B_3264 | Android NDK (R13B) (32 ビット) | 13.1.8 | オプション
Component.Android.NDK.R15C_3264 | Android NDK (R15C) (32 ビット) | 15.2.1 | オプション
Component.Google.Android.Emulator.API23.Private | Google Android Emulator (API レベル 23) (ローカル インストール) | 15.6.27413.0 | Optional
Component.HAXM.Private | Intel Hardware Accelerated Execution Manager (HAXM) (ローカル インストール) | 15.9.28307.421 | Optional
Component.Incredibuild | IncrediBuild - ビルド アクセラレーション | 15.7.27617.1 | Optional
Component.IncredibuildMenu | IncrediBuildMenu | 1.5.0.2 | Optional
Component.MDD.IOS | C++ iOS 開発ツール | 15.0.26621.2 | Optional

## <a name="net-core-cross-platform-development"></a>.NET Core クロスプラットフォームの開発

**ID:** Microsoft.VisualStudio.Workload.NetCoreTools

**説明:** .NET Core、ASP.NET Core、HTML/JavaScript、コンテナー (Docker サポートなど) を使用して、クロスプラットフォーム アプリケーションをビルドします。

### <a name="components-included-by-this-workload"></a>このワークロードに含まれるコンポーネント

コンポーネント ID | 名前 | バージョン | 依存関係の種類
--- | --- | --- | ---
Component.Microsoft.VisualStudio.RazorExtension | Razor 言語サービス | 15.0.26720.2 | 必須
Component.Microsoft.Web.LibraryManager | ライブラリ マネージャー | 15.8.27705.0 | 必須
Component.WebSocket | WebSocket4Net | 15.0.26606.0 | 必須
Microsoft.Component.ClickOnce | ClickOnce Publishing | 15.8.27825.0 | 必須
Microsoft.Component.MSBuild | MSBuild | 15.7.27520.0 | 必須
Microsoft.Net.Component.4.5.2.TargetingPack | .NET Framework 4.5.2 Targeting Pack | 15.6.27406.0 | 必須
Microsoft.Net.Component.4.5.TargetingPack | .NET Framework 4.5 Targeting Pack | 15.6.27406.0 | 必須
Microsoft.Net.Component.4.6.1.SDK | .NET Framework 4.6.1 SDK | 15.6.27406.0 | 必須
Microsoft.Net.Component.4.6.1.TargetingPack | .NET Framework 4.6.1 Targeting Pack | 15.6.27406.0 | 必須
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | .NET Framework 4.6.1 開発ツール | 15.8.27825.0 | 必須
Microsoft.Net.Core.Component.SDK.2.1 | .NET Core 2.1 開発ツール | 15.8.27924.0 | 必須
Microsoft.NetCore.ComponentGroup.DevelopmentTools.2.1 | .NET Core 2.1 開発ツール | 15.8.27924.0 | 必須
Microsoft.NetCore.ComponentGroup.Web.2.1 | .NET Core 2.1 開発ツール | 15.8.27924.0 | 必須
Microsoft.VisualStudio.Component.Common.Azure.Tools | 接続および発行ツール | 15.9.28107.0 | 必須
Microsoft.VisualStudio.Component.DockerTools | コンテナー開発ツール | 15.8.27906.1 | 必須
Microsoft.VisualStudio.Component.DockerTools.BuildTools | コンテナーの開発ツール - Build Tools | 15.7.27617.1 | 必須
Microsoft.VisualStudio.Component.FSharp | F# 言語サポート | 15.8.27825.0 | 必須
Microsoft.VisualStudio.Component.FSharp.WebTemplates | Web プロジェクト用の F# 言語サポート | 15.9.28307.421 | 必須
Microsoft.VisualStudio.Component.IISExpress | IIS Express  | 15.0.26208.0 | 必須
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | JavaScript 診断 | 15.8.27729.1 | 必須
Microsoft.VisualStudio.Component.JavaScript.TypeScript | JavaScript および TypeScript の言語サポート | 15.9.28125.51 | 必須
Microsoft.VisualStudio.Component.ManagedDesktop.Core | Managed Desktop Workload コア | 15.8.27729.1 | 必須
Microsoft.VisualStudio.Component.NuGet | NuGet パッケージ マネージャー | 15.9.28016.0 | 必須
Microsoft.VisualStudio.Component.PortableLibrary | .NET ポータブル ライブラリ Targeting Pack | 15.6.27309.0 | 必須
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# および Visual Basic Roslyn コンパイラ | 15.6.27309.0 | 必須
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# および Visual Basic | 15.8.27729.1 | 必須
Microsoft.VisualStudio.Component.SQL.ADAL | SQL ADAL ランタイム | 15.6.27406.0 | 必須
Microsoft.VisualStudio.Component.SQL.CLR | SQL Server の CLR データ型 | 15.0.26208.0 | 必須
Microsoft.VisualStudio.Component.SQL.CMDUtils | SQL Server コマンド ライン ユーティリティ | 15.0.26208.0 | 必須
Microsoft.VisualStudio.Component.SQL.DataSources | SQL Server サポートのためのデータ ソース | 15.0.26621.2 | 必須
Microsoft.VisualStudio.Component.SQL.LocalDB.Runtime | SQL Server Express 2016 LocalDB | 15.7.27617.1 | 必須
Microsoft.VisualStudio.Component.SQL.NCLI | SQL Server Native Client | 15.0.26208.0 | 必須
Microsoft.VisualStudio.Component.SQL.SSDT | SQL Server Data Tools | 15.9.28107.0 | 必須
Microsoft.VisualStudio.Component.Static.Analysis.Tools | スタティック分析ツール | 15.0.26208.0 | 必須
Microsoft.VisualStudio.Component.TextTemplating | テキスト テンプレート変換 | 15.0.26208.0 | 必須
Microsoft.VisualStudio.Component.TypeScript.3.1 | TypeScript 3.1 SDK | 15.0.28218.60 | 必須
Microsoft.VisualStudio.Component.VisualStudioData | データソースとサービス参照 | 15.6.27406.0 | 必須
Microsoft.VisualStudio.ComponentGroup.Web | ASP.NET と Web の開発ツールの前提条件 | 15.9.28219.51 | 必須
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | ASP.NET と Web 開発 | 15.8.27825.0 | 必須
Component.Microsoft.VisualStudio.Web.AzureFunctions | Microsoft Azure WebJobs ツール | 15.7.27617.1 | 推奨
Microsoft.VisualStudio.Component.AppInsights.Tools | Developer Analytics Tools | 15.8.27825.0 | 推奨
Microsoft.VisualStudio.Component.Azure.AuthoringTools | Azure Authoring Tools | 15.9.28307.421 | 推奨
Microsoft.VisualStudio.Component.Azure.ClientLibs | .NET 用 Azure ライブラリ | 15.0.26208.0 | 推奨
Microsoft.VisualStudio.Component.Azure.Compute.Emulator | Azure コンピューティング エミュレーター | 15.9.28307.421 | 推奨
Microsoft.VisualStudio.Component.Azure.Storage.Emulator | Azure Storage エミュレーター | 15.9.28125.51 | 推奨
Microsoft.VisualStudio.Component.CloudExplorer | Cloud Explorer | 15.9.28230.55 | 推奨
Microsoft.VisualStudio.Component.Debugger.Snapshot | スナップショット デバッガー | 15.8.28010.0 | 推奨
Microsoft.VisualStudio.Component.DiagnosticTools | .NET プロファイル ツール | 15.8.27729.1 | 推奨
Microsoft.VisualStudio.Component.IntelliTrace.FrontEnd | [IntelliTrace] | 15.8.27729.1 | 推奨
Microsoft.VisualStudio.Component.LiveUnitTesting | Live Unit Testing | 15.0.26720.2 | 推奨
Microsoft.VisualStudio.Component.Web | ASP.NET と Web の開発ツール | 15.8.27825.0 | 推奨
Microsoft.VisualStudio.Component.WebDeploy | Web 配置 | 15.8.27729.1 | 推奨
Microsoft.VisualStudio.ComponentGroup.AzureFunctions | Microsoft Azure WebJobs ツール | 15.7.27617.1 | 推奨
Microsoft.VisualStudio.ComponentGroup.Web.CloudTools | Web 開発用クラウド ツール | 15.8.27729.1 | 推奨
Microsoft.Net.Core.Component.SDK | .NET Core 2.0 開発ツール | 15.6.27406.0 | Optional
Microsoft.Net.Core.Component.SDK.1x | .NET Core 1.0 - 1.1 開発ツール | 15.6.27406.0 | Optional
Microsoft.NetCore.1x.ComponentGroup.Web | .NET Core 1.0 - 1.1 Web 用開発ツール | 15.6.27406.0 | Optional
Microsoft.NetCore.ComponentGroup.DevelopmentTools | .NET Core 2.0 開発ツール | 15.8.27729.1 | Optional
Microsoft.NetCore.ComponentGroup.Web | .NET Core 2.0 開発ツール | 15.7.27625.0 | Optional
Microsoft.VisualStudio.ComponentGroup.IISDevelopment | 開発時の IIS サポート | 15.9.28219.51 | Optional

## <a name="mobile-development-with-net"></a>.NET によるモバイル開発

**ID:** Microsoft.VisualStudio.Workload.NetCrossPlat

**説明:** iOS、Android、Windows 向けのクロスプラットフォーム アプリケーションを、Xamarin を使って構築します。

### <a name="components-included-by-this-workload"></a>このワークロードに含まれるコンポーネント

コンポーネント ID | 名前 | バージョン | 依存関係の種類
--- | --- | --- | ---
Component.Xamarin | Xamarin | 15.8.27906.1 | 必須
Component.Xamarin.RemotedSimulator | Xamarin Remoted Simulator | 15.6.27323.2 | 必須
Microsoft.Component.MSBuild | MSBuild | 15.7.27520.0 | 必須
Microsoft.Net.Component.4.6.1.SDK | .NET Framework 4.6.1 SDK | 15.6.27406.0 | 必須
Microsoft.Net.Component.4.6.1.TargetingPack | .NET Framework 4.6.1 Targeting Pack | 15.6.27406.0 | 必須
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | .NET Framework 4.6.1 開発ツール | 15.8.27825.0 | 必須
Microsoft.Net.Core.Component.SDK | .NET Core 2.0 開発ツール | 15.6.27406.0 | 必須
Microsoft.NetCore.ComponentGroup.DevelopmentTools | .NET Core 2.0 開発ツール | 15.8.27729.1 | 必須
Microsoft.VisualStudio.Component.FSharp | F# 言語サポート | 15.8.27825.0 | 必須
Microsoft.VisualStudio.Component.Merq | Xamarin の一般的な内部ツール | 15.8.27924.0 | 必須
Microsoft.VisualStudio.Component.MonoDebugger | Mono デバッガー | 15.0.26720.2 | 必須
Microsoft.VisualStudio.Component.NuGet | NuGet パッケージ マネージャー | 15.9.28016.0 | 必須
Microsoft.VisualStudio.Component.PortableLibrary | .NET ポータブル ライブラリ Targeting Pack | 15.6.27309.0 | 必須
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# および Visual Basic Roslyn コンパイラ | 15.6.27309.0 | 必須
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# および Visual Basic | 15.8.27729.1 | 必須
Microsoft.VisualStudio.Component.Static.Analysis.Tools | スタティック分析ツール | 15.0.26208.0 | 必須
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions.TemplateEngine | ASP.NET テンプレート エンジン | 15.8.27729.1 | 必須
Component.Android.SDK27 | Android SDK セットアップ (API レベル 27) | 15.9.28016.0 | 推奨
Component.Google.Android.Emulator.API27 | Google Android Emulator (API レベル 27) | 15.9.28307.421 | 推奨
Component.HAXM | Intel Hardware Accelerated Execution Manager (HAXM) (グローバル インストール) | 15.9.28307.421 | 推奨
Component.OpenJDK | Microsoft 配布の OpenJDK | 15.9.28125.51 | 推奨
Component.Xamarin.Profiler | Xamarin Profiler | 15.0.27005.2 | 推奨
Component.Xamarin.Inspector | Xamarin Workbooks | 15.0.26606.0 | Optional
Microsoft.Component.ClickOnce | ClickOnce Publishing | 15.8.27825.0 | Optional
Microsoft.Component.NetFX.Native | .NET Native | 15.0.26208.0 | Optional
Microsoft.VisualStudio.Component.AppInsights.Tools | Developer Analytics Tools | 15.8.27825.0 | Optional
Microsoft.VisualStudio.Component.CodeClone | コード クローン | 15.0.26208.0 | Optional
Microsoft.VisualStudio.Component.CodeMap | コード マップ | 15.0.26208.0 | Optional
Microsoft.VisualStudio.Component.DependencyValidation.Enterprise | ライブ依存関係検証 | 15.0.26208.0 | Optional
Microsoft.VisualStudio.Component.DiagnosticTools | .NET プロファイル ツール | 15.8.27729.1 | Optional
Microsoft.VisualStudio.Component.GraphDocument | DGML エディター | 15.0.27005.2 | Optional
Microsoft.VisualStudio.Component.Graphics | イメージ エディターと 3D モデル エディター | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.SQL.CLR | SQL Server の CLR データ型 | 15.0.26208.0 | Optional
Microsoft.VisualStudio.Component.SQL.LocalDB.Runtime | SQL Server Express 2016 LocalDB | 15.7.27617.1 | Optional
Microsoft.VisualStudio.Component.SQL.NCLI | SQL Server Native Client | 15.0.26208.0 | Optional
Microsoft.VisualStudio.Component.VisualStudioData | データソースとサービス参照 | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.17763 | Windows 10 SDK (10.0.17763.0) | 15.9.28307.102 | Optional
Microsoft.VisualStudio.ComponentGroup.ArchitectureTools.Managed | アーキテクチャおよび分析ツール | 15.0.26208.0 | Optional
Microsoft.VisualStudio.ComponentGroup.UWP.Xamarin | Xamarin 用ユニバーサル Windows プラットフォーム ツール | 15.9.28307.102 | Optional

## <a name="aspnet-and-web-development"></a>ASP.NET と Web 開発

**ID:** Microsoft.VisualStudio.Workload.NetWeb

**説明:** ASP.NET、ASP.NET Core、HTML/JavaScript、Containers (Docker サポートを含む) を使用して、Web アプリケーションをビルドします。

### <a name="components-included-by-this-workload"></a>このワークロードに含まれるコンポーネント

コンポーネント ID | 名前 | バージョン | 依存関係の種類
--- | --- | --- | ---
Component.Microsoft.VisualStudio.RazorExtension | Razor 言語サービス | 15.0.26720.2 | 必須
Component.Microsoft.Web.LibraryManager | ライブラリ マネージャー | 15.8.27705.0 | 必須
Component.WebSocket | WebSocket4Net | 15.0.26606.0 | 必須
Microsoft.Component.ClickOnce | ClickOnce Publishing | 15.8.27825.0 | 必須
Microsoft.Component.MSBuild | MSBuild | 15.7.27520.0 | 必須
Microsoft.Net.Component.4.5.2.TargetingPack | .NET Framework 4.5.2 Targeting Pack | 15.6.27406.0 | 必須
Microsoft.Net.Component.4.5.TargetingPack | .NET Framework 4.5 Targeting Pack | 15.6.27406.0 | 必須
Microsoft.Net.Component.4.6.1.SDK | .NET Framework 4.6.1 SDK | 15.6.27406.0 | 必須
Microsoft.Net.Component.4.6.1.TargetingPack | .NET Framework 4.6.1 Targeting Pack | 15.6.27406.0 | 必須
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | .NET Framework 4.6.1 開発ツール | 15.8.27825.0 | 必須
Microsoft.Net.Core.Component.SDK.2.1 | .NET Core 2.1 開発ツール | 15.8.27924.0 | 必須
Microsoft.NetCore.ComponentGroup.DevelopmentTools.2.1 | .NET Core 2.1 開発ツール | 15.8.27924.0 | 必須
Microsoft.NetCore.ComponentGroup.Web.2.1 | .NET Core 2.1 開発ツール | 15.8.27924.0 | 必須
Microsoft.VisualStudio.Component.Common.Azure.Tools | 接続および発行ツール | 15.9.28107.0 | 必須
Microsoft.VisualStudio.Component.DockerTools | コンテナー開発ツール | 15.8.27906.1 | 必須
Microsoft.VisualStudio.Component.DockerTools.BuildTools | コンテナーの開発ツール - Build Tools | 15.7.27617.1 | 必須
Microsoft.VisualStudio.Component.FSharp | F# 言語サポート | 15.8.27825.0 | 必須
Microsoft.VisualStudio.Component.FSharp.WebTemplates | Web プロジェクト用の F# 言語サポート | 15.9.28307.421 | 必須
Microsoft.VisualStudio.Component.IISExpress | IIS Express  | 15.0.26208.0 | 必須
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | JavaScript 診断 | 15.8.27729.1 | 必須
Microsoft.VisualStudio.Component.JavaScript.TypeScript | JavaScript および TypeScript の言語サポート | 15.9.28125.51 | 必須
Microsoft.VisualStudio.Component.ManagedDesktop.Core | Managed Desktop Workload コア | 15.8.27729.1 | 必須
Microsoft.VisualStudio.Component.NuGet | NuGet パッケージ マネージャー | 15.9.28016.0 | 必須
Microsoft.VisualStudio.Component.PortableLibrary | .NET ポータブル ライブラリ Targeting Pack | 15.6.27309.0 | 必須
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# および Visual Basic Roslyn コンパイラ | 15.6.27309.0 | 必須
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# および Visual Basic | 15.8.27729.1 | 必須
Microsoft.VisualStudio.Component.SQL.ADAL | SQL ADAL ランタイム | 15.6.27406.0 | 必須
Microsoft.VisualStudio.Component.SQL.CLR | SQL Server の CLR データ型 | 15.0.26208.0 | 必須
Microsoft.VisualStudio.Component.SQL.CMDUtils | SQL Server コマンド ライン ユーティリティ | 15.0.26208.0 | 必須
Microsoft.VisualStudio.Component.SQL.DataSources | SQL Server サポートのためのデータ ソース | 15.0.26621.2 | 必須
Microsoft.VisualStudio.Component.SQL.LocalDB.Runtime | SQL Server Express 2016 LocalDB | 15.7.27617.1 | 必須
Microsoft.VisualStudio.Component.SQL.NCLI | SQL Server Native Client | 15.0.26208.0 | 必須
Microsoft.VisualStudio.Component.SQL.SSDT | SQL Server Data Tools | 15.9.28107.0 | 必須
Microsoft.VisualStudio.Component.Static.Analysis.Tools | スタティック分析ツール | 15.0.26208.0 | 必須
Microsoft.VisualStudio.Component.TextTemplating | テキスト テンプレート変換 | 15.0.26208.0 | 必須
Microsoft.VisualStudio.Component.TypeScript.3.1 | TypeScript 3.1 SDK | 15.0.28218.60 | 必須
Microsoft.VisualStudio.Component.VisualStudioData | データソースとサービス参照 | 15.6.27406.0 | 必須
Microsoft.VisualStudio.Component.Web | ASP.NET と Web の開発ツール | 15.8.27825.0 | 必須
Microsoft.VisualStudio.ComponentGroup.Web | ASP.NET と Web の開発ツールの前提条件 | 15.9.28219.51 | 必須
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | ASP.NET と Web 開発 | 15.8.27825.0 | 必須
Component.Microsoft.VisualStudio.Web.AzureFunctions | Microsoft Azure WebJobs ツール | 15.7.27617.1 | 推奨
Microsoft.Net.Component.4.5.1.TargetingPack | .NET Framework 4.5.1 Targeting Pack | 15.6.27406.0 | 推奨
Microsoft.Net.Component.4.6.TargetingPack | .NET Framework 4.6 Targeting Pack | 15.6.27406.0 | 推奨
Microsoft.Net.Component.4.TargetingPack | .NET Framework 4 Targeting Pack | 15.6.27406.0 | 推奨
Microsoft.Net.ComponentGroup.TargetingPacks.Common | .NET Framework 4 – 4.6 開発ツール | 15.6.27406.0 | 推奨
Microsoft.VisualStudio.Component.AppInsights.Tools | Developer Analytics Tools | 15.8.27825.0 | 推奨
Microsoft.VisualStudio.Component.AspNet45 | 高度な ASP.NET 機能 | 15.7.27625.0 | 推奨
Microsoft.VisualStudio.Component.Azure.AuthoringTools | Azure Authoring Tools | 15.9.28307.421 | 推奨
Microsoft.VisualStudio.Component.Azure.ClientLibs | .NET 用 Azure ライブラリ | 15.0.26208.0 | 推奨
Microsoft.VisualStudio.Component.Azure.Compute.Emulator | Azure コンピューティング エミュレーター | 15.9.28307.421 | 推奨
Microsoft.VisualStudio.Component.Azure.Storage.Emulator | Azure Storage エミュレーター | 15.9.28125.51 | 推奨
Microsoft.VisualStudio.Component.CloudExplorer | Cloud Explorer | 15.9.28230.55 | 推奨
Microsoft.VisualStudio.Component.Debugger.Snapshot | スナップショット デバッガー | 15.8.28010.0 | 推奨
Microsoft.VisualStudio.Component.DiagnosticTools | .NET プロファイル ツール | 15.8.27729.1 | 推奨
Microsoft.VisualStudio.Component.EntityFramework | Entity Framework 6 Tools | 15.6.27406.0 | 推奨
Microsoft.VisualStudio.Component.IntelliTrace.FrontEnd | [IntelliTrace] | 15.8.27729.1 | 推奨
Microsoft.VisualStudio.Component.LiveUnitTesting | Live Unit Testing | 15.0.26720.2 | 推奨
Microsoft.VisualStudio.Component.Wcf.Tooling | Windows Communication Foundation | 15.8.27924.0 | 推奨
Microsoft.VisualStudio.Component.WebDeploy | Web 配置 | 15.8.27729.1 | 推奨
Microsoft.VisualStudio.ComponentGroup.AzureFunctions | Microsoft Azure WebJobs ツール | 15.7.27617.1 | 推奨
Microsoft.VisualStudio.ComponentGroup.Web.CloudTools | Web 開発用クラウド ツール | 15.8.27729.1 | 推奨
Microsoft.Net.Component.4.6.2.SDK | .NET Framework 4.6.2 SDK | 15.6.27406.0 | Optional
Microsoft.Net.Component.4.6.2.TargetingPack | .NET Framework 4.6.2 Targeting Pack | 15.6.27406.0 | Optional
Microsoft.Net.Component.4.7.1.SDK | .NET Framework 4.7.1 SDK | 15.6.27406.0 | Optional
Microsoft.Net.Component.4.7.1.TargetingPack | .NET Framework 4.7.1 Targeting Pack | 15.6.27406.0 | Optional
Microsoft.Net.Component.4.7.2.SDK | .NET Framework 4.7.2 SDK | 15.8.27825.0 | Optional
Microsoft.Net.Component.4.7.2.TargetingPack | .NET Framework 4.7.2 Targeting Pack | 15.8.27825.0 | Optional
Microsoft.Net.Component.4.7.SDK | .NET Framework 4.7 SDK | 15.6.27406.0 | Optional
Microsoft.Net.Component.4.7.TargetingPack | .NET Framework 4.7 Targeting Pack | 15.6.27406.0 | Optional
Microsoft.Net.ComponentGroup.4.6.2.DeveloperTools | .NET Framework 4.6.2 開発ツール | 15.6.27406.0 | Optional
Microsoft.Net.ComponentGroup.4.7.1.DeveloperTools | .NET Framework 4.7.1 開発ツール | 15.6.27406.0 | Optional
Microsoft.Net.ComponentGroup.4.7.2.DeveloperTools | .NET Framework 4.7.2 開発ツール | 15.8.27825.0 | Optional
Microsoft.Net.ComponentGroup.4.7.DeveloperTools | .NET Framework 4.7 開発ツール | 15.6.27406.0 | Optional
Microsoft.Net.Core.Component.SDK | .NET Core 2.0 開発ツール | 15.6.27406.0 | Optional
Microsoft.Net.Core.Component.SDK.1x | .NET Core 1.0 - 1.1 開発ツール | 15.6.27406.0 | Optional
Microsoft.NetCore.1x.ComponentGroup.Web | .NET Core 1.0 - 1.1 Web 用開発ツール | 15.6.27406.0 | Optional
Microsoft.NetCore.ComponentGroup.DevelopmentTools | .NET Core 2.0 開発ツール | 15.8.27729.1 | Optional
Microsoft.NetCore.ComponentGroup.Web | .NET Core 2.0 開発ツール | 15.7.27625.0 | Optional
Microsoft.VisualStudio.Component.CodeClone | コード クローン | 15.0.26208.0 | Optional
Microsoft.VisualStudio.Component.CodeMap | コード マップ | 15.0.26208.0 | Optional
Microsoft.VisualStudio.Component.DependencyValidation.Enterprise | ライブ依存関係検証 | 15.0.26208.0 | Optional
Microsoft.VisualStudio.Component.GraphDocument | DGML エディター | 15.0.27005.2 | Optional
Microsoft.VisualStudio.Component.TestTools.WebLoadTest | Web パフォーマンスとロード テスト ツール | 15.8.27729.1 | Optional
Microsoft.VisualStudio.ComponentGroup.ArchitectureTools.Managed | アーキテクチャおよび分析ツール | 15.0.26208.0 | Optional
Microsoft.VisualStudio.ComponentGroup.IISDevelopment | 開発時の IIS サポート | 15.9.28219.51 | Optional
Microsoft.VisualStudio.Web.Mvc4.ComponentGroup | ASP.NET MVC 4 | 15.6.27406.0 | Optional

## <a name="nodejs-development"></a>Node.js 開発

**ID:** Microsoft.VisualStudio.Workload.Node

**説明:** Node.js (非同期、イベント ドリブン JavaScript ランタイム) を使用してスケーラブルなネットワーク アプリケーションをビルドします。 

### <a name="components-included-by-this-workload"></a>このワークロードに含まれるコンポーネント

コンポーネント ID | 名前 | バージョン | 依存関係の種類
--- | --- | --- | ---
Component.WebSocket | WebSocket4Net | 15.0.26606.0 | 必須
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | JavaScript 診断 | 15.8.27729.1 | 必須
Microsoft.VisualStudio.Component.JavaScript.TypeScript | JavaScript および TypeScript の言語サポート | 15.9.28125.51 | 必須
Microsoft.VisualStudio.Component.Node.Build | Node.js MSBuild サポート | 15.8.27825.0 | 必須
Microsoft.VisualStudio.Component.Node.Tools | Node.js 開発サポート | 15.8.27825.0 | 必須
Microsoft.VisualStudio.Component.NuGet | NuGet パッケージ マネージャー | 15.9.28016.0 | 必須
Microsoft.VisualStudio.Component.TestTools.Core | テスト ツールのコア機能 | 15.7.27520.0 | 必須
Microsoft.VisualStudio.Component.TypeScript.3.1 | TypeScript 3.1 SDK | 15.0.28218.60 | 必須
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | ASP.NET と Web 開発 | 15.8.27825.0 | 必須
Microsoft.VisualStudio.Component.WebDeploy | Web 配置 | 15.8.27729.1 | 推奨
Microsoft.VisualStudio.Component.AppInsights.Tools | Developer Analytics Tools | 15.8.27825.0 | Optional
Microsoft.VisualStudio.Component.Common.Azure.Tools | 接続および発行ツール | 15.9.28107.0 | Optional
Microsoft.VisualStudio.Component.Static.Analysis.Tools | スタティック分析ツール | 15.0.26208.0 | Optional
Microsoft.VisualStudio.Component.VC.CoreIde | Visual Studio C++ コア機能 | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.VC.Tools.x86.x64 | VC++ 2017 バージョン 15.9 v14.16 最新の v141 ツール | 15.9.28230.55 | Optional

## <a name="officesharepoint-development"></a>Office/SharePoint 開発

**ID:** Microsoft.VisualStudio.Workload.Office

**説明:** C#、VB、JavaScript を使用して、Office アドイン、SharePoint アドイン、SharePoint ソリューション、VSTO アドインを作成します。

### <a name="components-included-by-this-workload"></a>このワークロードに含まれるコンポーネント

コンポーネント ID | 名前 | バージョン | 依存関係の種類
--- | --- | --- | ---
Component.Microsoft.VisualStudio.RazorExtension | Razor 言語サービス | 15.0.26720.2 | 必須
Component.Microsoft.Web.LibraryManager | ライブラリ マネージャー | 15.8.27705.0 | 必須
Component.WebSocket | WebSocket4Net | 15.0.26606.0 | 必須
Microsoft.Component.ClickOnce | ClickOnce Publishing | 15.8.27825.0 | 必須
Microsoft.Component.MSBuild | MSBuild | 15.7.27520.0 | 必須
Microsoft.Net.Component.4.5.2.TargetingPack | .NET Framework 4.5.2 Targeting Pack | 15.6.27406.0 | 必須
Microsoft.Net.Component.4.5.TargetingPack | .NET Framework 4.5 Targeting Pack | 15.6.27406.0 | 必須
Microsoft.Net.Component.4.6.1.SDK | .NET Framework 4.6.1 SDK | 15.6.27406.0 | 必須
Microsoft.Net.Component.4.6.1.TargetingPack | .NET Framework 4.6.1 Targeting Pack | 15.6.27406.0 | 必須
Microsoft.Net.Component.4.TargetingPack | .NET Framework 4 Targeting Pack | 15.6.27406.0 | 必須
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | .NET Framework 4.6.1 開発ツール | 15.8.27825.0 | 必須
Microsoft.Net.Core.Component.SDK.2.1 | .NET Core 2.1 開発ツール | 15.8.27924.0 | 必須
Microsoft.VisualStudio.Component.AppInsights.Tools | Developer Analytics Tools | 15.8.27825.0 | 必須
Microsoft.VisualStudio.Component.Common.Azure.Tools | 接続および発行ツール | 15.9.28107.0 | 必須
Microsoft.VisualStudio.Component.DockerTools | コンテナー開発ツール | 15.8.27906.1 | 必須
Microsoft.VisualStudio.Component.DockerTools.BuildTools | コンテナーの開発ツール - Build Tools | 15.7.27617.1 | 必須
Microsoft.VisualStudio.Component.IISExpress | IIS Express  | 15.0.26208.0 | 必須
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | JavaScript 診断 | 15.8.27729.1 | 必須
Microsoft.VisualStudio.Component.JavaScript.TypeScript | JavaScript および TypeScript の言語サポート | 15.9.28125.51 | 必須
Microsoft.VisualStudio.Component.ManagedDesktop.Core | Managed Desktop Workload コア | 15.8.27729.1 | 必須
Microsoft.VisualStudio.Component.ManagedDesktop.Prerequisites | .NET デスクトップ開発ツール | 15.7.27625.0 | 必須
Microsoft.VisualStudio.Component.NuGet | NuGet パッケージ マネージャー | 15.9.28016.0 | 必須
Microsoft.VisualStudio.Component.PortableLibrary | .NET ポータブル ライブラリ Targeting Pack | 15.6.27309.0 | 必須
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# および Visual Basic Roslyn コンパイラ | 15.6.27309.0 | 必須
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# および Visual Basic | 15.8.27729.1 | 必須
Microsoft.VisualStudio.Component.Sharepoint.Tools | Office Developer Tools for Visual Studio | 15.8.27924.0 | 必須
Microsoft.VisualStudio.Component.SQL.ADAL | SQL ADAL ランタイム | 15.6.27406.0 | 必須
Microsoft.VisualStudio.Component.SQL.CLR | SQL Server の CLR データ型 | 15.0.26208.0 | 必須
Microsoft.VisualStudio.Component.SQL.CMDUtils | SQL Server コマンド ライン ユーティリティ | 15.0.26208.0 | 必須
Microsoft.VisualStudio.Component.SQL.DataSources | SQL Server サポートのためのデータ ソース | 15.0.26621.2 | 必須
Microsoft.VisualStudio.Component.SQL.LocalDB.Runtime | SQL Server Express 2016 LocalDB | 15.7.27617.1 | 必須
Microsoft.VisualStudio.Component.SQL.NCLI | SQL Server Native Client | 15.0.26208.0 | 必須
Microsoft.VisualStudio.Component.SQL.SSDT | SQL Server Data Tools | 15.9.28107.0 | 必須
Microsoft.VisualStudio.Component.Static.Analysis.Tools | スタティック分析ツール | 15.0.26208.0 | 必須
Microsoft.VisualStudio.Component.TextTemplating | テキスト テンプレート変換 | 15.0.26208.0 | 必須
Microsoft.VisualStudio.Component.TypeScript.3.1 | TypeScript 3.1 SDK | 15.0.28218.60 | 必須
Microsoft.VisualStudio.Component.VisualStudioData | データソースとサービス参照 | 15.6.27406.0 | 必須
Microsoft.VisualStudio.Component.Wcf.Tooling | Windows Communication Foundation | 15.8.27924.0 | 必須
Microsoft.VisualStudio.Component.Web | ASP.NET と Web の開発ツール | 15.8.27825.0 | 必須
Microsoft.VisualStudio.Component.Workflow | Windows Workflow Foundation | 15.8.27825.0 | 必須
Microsoft.VisualStudio.ComponentGroup.Web | ASP.NET と Web の開発ツールの前提条件 | 15.9.28219.51 | 必須
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | ASP.NET と Web 開発 | 15.8.27825.0 | 必須
Microsoft.VisualStudio.Component.TeamOffice | Visual Studio Tools for Office (VSTO) | 15.7.27625.0 | 推奨
Microsoft.VisualStudio.Component.WebDeploy | Web 配置 | 15.8.27729.1 | 推奨
Microsoft.Net.Component.4.6.2.SDK | .NET Framework 4.6.2 SDK | 15.6.27406.0 | Optional
Microsoft.Net.Component.4.6.2.TargetingPack | .NET Framework 4.6.2 Targeting Pack | 15.6.27406.0 | Optional
Microsoft.Net.Component.4.7.1.SDK | .NET Framework 4.7.1 SDK | 15.6.27406.0 | Optional
Microsoft.Net.Component.4.7.1.TargetingPack | .NET Framework 4.7.1 Targeting Pack | 15.6.27406.0 | Optional
Microsoft.Net.Component.4.7.2.SDK | .NET Framework 4.7.2 SDK | 15.8.27825.0 | Optional
Microsoft.Net.Component.4.7.2.TargetingPack | .NET Framework 4.7.2 Targeting Pack | 15.8.27825.0 | Optional
Microsoft.Net.Component.4.7.SDK | .NET Framework 4.7 SDK | 15.6.27406.0 | Optional
Microsoft.Net.Component.4.7.TargetingPack | .NET Framework 4.7 Targeting Pack | 15.6.27406.0 | Optional
Microsoft.Net.ComponentGroup.4.6.2.DeveloperTools | .NET Framework 4.6.2 開発ツール | 15.6.27406.0 | Optional
Microsoft.Net.ComponentGroup.4.7.1.DeveloperTools | .NET Framework 4.7.1 開発ツール | 15.6.27406.0 | Optional
Microsoft.Net.ComponentGroup.4.7.2.DeveloperTools | .NET Framework 4.7.2 開発ツール | 15.8.27825.0 | Optional
Microsoft.Net.ComponentGroup.4.7.DeveloperTools | .NET Framework 4.7 開発ツール | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.IntelliTrace.FrontEnd | [IntelliTrace] | 15.8.27729.1 | Optional

## <a name="python-development"></a>Python 開発

**ID:** Microsoft.VisualStudio.Workload.Python

**説明:** Python の編集、デバッグ、対話型開発、ソース管理。

### <a name="components-included-by-this-workload"></a>このワークロードに含まれるコンポーネント

コンポーネント ID | 名前 | バージョン | 依存関係の種類
--- | --- | --- | ---
Microsoft.Component.PythonTools | Python 言語サポート | 15.0.26823.1 | 必須
Component.CPython3.x64 | Python 3 64 ビット (3.6.6) | 3.6.6 | 推奨
Microsoft.Component.CookiecutterTools | cookiecutter テンプレートのサポート | 15.0.26621.2 | 推奨
Microsoft.Component.PythonTools.Web | Python Web サポート | 15.9.28107.0 | 推奨
Microsoft.VisualStudio.Component.Common.Azure.Tools | 接続および発行ツール | 15.9.28107.0 | 推奨
Microsoft.VisualStudio.Component.JavaScript.TypeScript | JavaScript および TypeScript の言語サポート | 15.9.28125.51 | 推奨
Microsoft.VisualStudio.Component.SQL.CLR | SQL Server の CLR データ型 | 15.0.26208.0 | 推奨
Microsoft.VisualStudio.Component.TypeScript.3.1 | TypeScript 3.1 SDK | 15.0.28218.60 | 推奨
Microsoft.VisualStudio.Component.VisualStudioData | データソースとサービス参照 | 15.6.27406.0 | 推奨
Microsoft.VisualStudio.Component.WebDeploy | Web 配置 | 15.8.27729.1 | 推奨
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | ASP.NET と Web 開発 | 15.8.27825.0 | 推奨
Component.Anaconda2.x64 | Anaconda2 64 ビット (5.2.0) | 5.2.0 | Optional
Component.Anaconda2.x86 | Anaconda2 32 ビット (5.2.0) | 5.2.0 | Optional
Component.Anaconda3.x64 | Anaconda3 64 ビット (5.2.0) | 5.2.0 | Optional
Component.Anaconda3.x86 | Anaconda3 32 ビット (5.2.0) | 5.2.0 | Optional
Component.CPython2.x64 | Python 2 64 ビット (2.7.14) | 2.7.14 | Optional
Component.CPython2.x86 | Python 2 32 ビット (2.7.14) | 2.7.14 | Optional
Component.CPython3.x86 | Python 3 32 ビット (3.6.6) | 3.6.6 | Optional
Component.Microsoft.VisualStudio.RazorExtension | Razor 言語サービス | 15.0.26720.2 | Optional
Component.Microsoft.Web.LibraryManager | ライブラリ マネージャー | 15.8.27705.0 | オプション
Component.WebSocket | WebSocket4Net | 15.0.26606.0 | Optional
Microsoft.Component.ClickOnce | ClickOnce Publishing | 15.8.27825.0 | Optional
Microsoft.Component.MSBuild | MSBuild | 15.7.27520.0 | オプション
Microsoft.Component.NetFX.Native | .NET Native | 15.0.26208.0 | Optional
Microsoft.Component.PythonTools.UWP | Python IoT サポート | 15.0.26606.0 | Optional
Microsoft.Component.VC.Runtime.UCRTSDK | Windows Universal CRT SDK | 15.6.27309.0 | Optional
Microsoft.ComponentGroup.PythonTools.NativeDevelopment | Python ネイティブ開発ツール | 15.9.28307.102 | Optional
Microsoft.Net.Component.4.5.2.TargetingPack | .NET Framework 4.5.2 Targeting Pack | 15.6.27406.0 | Optional
Microsoft.Net.Component.4.5.TargetingPack | .NET Framework 4.5 Targeting Pack | 15.6.27406.0 | Optional
Microsoft.Net.Component.4.6.1.SDK | .NET Framework 4.6.1 SDK | 15.6.27406.0 | Optional
Microsoft.Net.Component.4.6.1.TargetingPack | .NET Framework 4.6.1 Targeting Pack | 15.6.27406.0 | Optional
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | .NET Framework 4.6.1 開発ツール | 15.8.27825.0 | Optional
Microsoft.Net.Core.Component.SDK.2.1 | .NET Core 2.1 開発ツール | 15.8.27924.0 | Optional
Microsoft.VisualStudio.Component.AppInsights.Tools | Developer Analytics Tools | 15.8.27825.0 | Optional
Microsoft.VisualStudio.Component.Azure.AuthoringTools | Azure Authoring Tools | 15.9.28307.421 | Optional
Microsoft.VisualStudio.Component.Azure.ClientLibs | .NET 用 Azure ライブラリ | 15.0.26208.0 | Optional
Microsoft.VisualStudio.Component.Azure.Compute.Emulator | Azure コンピューティング エミュレーター | 15.9.28307.421 | Optional
Microsoft.VisualStudio.Component.Azure.Storage.Emulator | Azure Storage エミュレーター | 15.9.28125.51 | Optional
Microsoft.VisualStudio.Component.Azure.Waverton | Azure Cloud Services コア ツール | 15.9.28107.0 | Optional
Microsoft.VisualStudio.Component.Azure.Waverton.BuildTools | Azure Cloud Services ビルド ツール | 15.7.27617.1 | Optional
Microsoft.VisualStudio.Component.ClassDesigner | クラス デザイナー | 15.0.26208.0 | Optional
Microsoft.VisualStudio.Component.CodeClone | コード クローン | 15.0.26208.0 | Optional
Microsoft.VisualStudio.Component.CodeMap | コード マップ | 15.0.26208.0 | Optional
Microsoft.VisualStudio.Component.DiagnosticTools | .NET プロファイル ツール | 15.8.27729.1 | Optional
Microsoft.VisualStudio.Component.DockerTools | コンテナー開発ツール | 15.8.27906.1 | オプション
Microsoft.VisualStudio.Component.DockerTools.BuildTools | コンテナーの開発ツール - Build Tools | 15.7.27617.1 | Optional
Microsoft.VisualStudio.Component.GraphDocument | DGML エディター | 15.0.27005.2 | Optional
Microsoft.VisualStudio.Component.Graphics | イメージ エディターと 3D モデル エディター | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Graphics.Tools | DirectX 用グラフィックス デバッガーおよび GPU プロファイラー | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Graphics.Win81 | グラフィックス ツール Windows 8.1 SDK | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.IISExpress | IIS Express  | 15.0.26208.0 | Optional
Microsoft.VisualStudio.Component.IntelliTrace.FrontEnd | [IntelliTrace] | 15.8.27729.1 | Optional
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | JavaScript 診断 | 15.8.27729.1 | Optional
Microsoft.VisualStudio.Component.ManagedDesktop.Core | Managed Desktop Workload コア | 15.8.27729.1 | Optional
Microsoft.VisualStudio.Component.NuGet | NuGet パッケージ マネージャー | 15.9.28016.0 | Optional
Microsoft.VisualStudio.Component.PortableLibrary | .NET ポータブル ライブラリ Targeting Pack | 15.6.27309.0 | Optional
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# および Visual Basic Roslyn コンパイラ | 15.6.27309.0 | Optional
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# および Visual Basic | 15.8.27729.1 | Optional
Microsoft.VisualStudio.Component.SQL.ADAL | SQL ADAL ランタイム | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.SQL.CMDUtils | SQL Server コマンド ライン ユーティリティ | 15.0.26208.0 | Optional
Microsoft.VisualStudio.Component.SQL.DataSources | SQL Server サポートのためのデータ ソース | 15.0.26621.2 | Optional
Microsoft.VisualStudio.Component.SQL.LocalDB.Runtime | SQL Server Express 2016 LocalDB | 15.7.27617.1 | Optional
Microsoft.VisualStudio.Component.SQL.NCLI | SQL Server Native Client | 15.0.26208.0 | Optional
Microsoft.VisualStudio.Component.SQL.SSDT | SQL Server Data Tools | 15.9.28107.0 | Optional
Microsoft.VisualStudio.Component.Static.Analysis.Tools | スタティック分析ツール | 15.0.26208.0 | Optional
Microsoft.VisualStudio.Component.TextTemplating | テキスト テンプレート変換 | 15.0.26208.0 | Optional
Microsoft.VisualStudio.Component.VC.140 | デスクトップ用 VC++ 2015.3 v14.00 (v140) ツールセット | 15.7.27617.1 | Optional
Microsoft.VisualStudio.Component.VC.CoreIde | Visual Studio C++ コア機能 | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.VC.DiagnosticTools | C++ のプロファイル ツール | 15.0.26823.1 | Optional
Microsoft.VisualStudio.Component.VC.Tools.x86.x64 | VC++ 2017 バージョン 15.9 v14.16 最新の v141 ツール | 15.9.28230.55 | Optional
Microsoft.VisualStudio.Component.Web | ASP.NET と Web の開発ツール | 15.8.27825.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK | Windows ユニバーサル C ランタイム | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.10586 | Windows 10 SDK (10.0.10586.0) | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.17763 | Windows 10 SDK (10.0.17763.0) | 15.9.28307.102 | Optional
Microsoft.VisualStudio.Component.Windows81SDK | Windows 8.1 SDK | 15.6.27406.0 | Optional
Microsoft.VisualStudio.ComponentGroup.Web | ASP.NET と Web の開発ツールの前提条件 | 15.9.28219.51 | Optional

## <a name="universal-windows-platform-development"></a>ユニバーサル Windows プラットフォーム開発

**ID:** Microsoft.VisualStudio.Workload.Universal

**説明:** C#、VB、JavaScript、または C++ (オプション) を使ってユニバーサル Windows プラットフォームのアプリケーションを作成します。

### <a name="components-included-by-this-workload"></a>このワークロードに含まれるコンポーネント

コンポーネント ID | 名前 | バージョン | 依存関係の種類
--- | --- | --- | ---
Component.WebSocket | WebSocket4Net | 15.0.26606.0 | 必須
Microsoft.Component.ClickOnce | ClickOnce Publishing | 15.8.27825.0 | 必須
Microsoft.Component.NetFX.Native | .NET Native | 15.0.26208.0 | 必須
Microsoft.ComponentGroup.Blend | Blend for Visual Studio | 15.6.27406.0 | 必須
Microsoft.Net.Component.4.5.TargetingPack | .NET Framework 4.5 Targeting Pack | 15.6.27406.0 | 必須
Microsoft.Net.Component.4.6.1.SDK | .NET Framework 4.6.1 SDK | 15.6.27406.0 | 必須
Microsoft.Net.Core.Component.SDK.2.1 | .NET Core 2.1 開発ツール | 15.8.27924.0 | 必須
Microsoft.VisualStudio.Component.AppInsights.Tools | Developer Analytics Tools | 15.8.27825.0 | 必須
Microsoft.VisualStudio.Component.DiagnosticTools | .NET プロファイル ツール | 15.8.27729.1 | 必須
Microsoft.VisualStudio.Component.Graphics | イメージ エディターと 3D モデル エディター | 15.6.27406.0 | 必須
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | JavaScript 診断 | 15.8.27729.1 | 必須
Microsoft.VisualStudio.Component.JavaScript.TypeScript | JavaScript および TypeScript の言語サポート | 15.9.28125.51 | 必須
Microsoft.VisualStudio.Component.NuGet | NuGet パッケージ マネージャー | 15.9.28016.0 | 必須
Microsoft.VisualStudio.Component.PortableLibrary | .NET ポータブル ライブラリ Targeting Pack | 15.6.27309.0 | 必須
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# および Visual Basic Roslyn コンパイラ | 15.6.27309.0 | 必須
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# および Visual Basic | 15.8.27729.1 | 必須
Microsoft.VisualStudio.Component.SQL.CLR | SQL Server の CLR データ型 | 15.0.26208.0 | 必須
Microsoft.VisualStudio.Component.Static.Analysis.Tools | スタティック分析ツール | 15.0.26208.0 | 必須
Microsoft.VisualStudio.Component.TypeScript.3.1 | TypeScript 3.1 SDK | 15.0.28218.60 | 必須
Microsoft.VisualStudio.Component.UWP.Support | ユニバーサル Windows プラットフォーム ツール | 15.9.28119.51 | 必須
Microsoft.VisualStudio.Component.VisualStudioData | データソースとサービス参照 | 15.6.27406.0 | 必須
Microsoft.VisualStudio.Component.Windows10SDK.17763 | Windows 10 SDK (10.0.17763.0) | 15.9.28307.102 | 必須
Microsoft.VisualStudio.ComponentGroup.UWP.Cordova | Cordova 用ユニバーサル Windows プラットフォーム ツール | 15.9.28307.102 | 必須
Microsoft.VisualStudio.ComponentGroup.UWP.NetCoreAndStandard | .NET ネイティブと .NET Standard | 15.8.27906.1 | 必須
Microsoft.VisualStudio.ComponentGroup.UWP.Xamarin | Xamarin 用ユニバーサル Windows プラットフォーム ツール | 15.9.28307.102 | 必須
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | ASP.NET と Web 開発 | 15.8.27825.0 | 必須
Microsoft.VisualStudio.Component.IntelliTrace.FrontEnd | [IntelliTrace] | 15.8.27729.1 | 推奨
Microsoft.Component.VC.Runtime.OSSupport | UWP 用の Visual C++ ランタイム | 15.6.27406.0 | Optional
Microsoft.Net.Component.4.7.2.SDK | .NET Framework 4.7.2 SDK | 15.8.27825.0 | Optional
Microsoft.VisualStudio.Component.CodeClone | コード クローン | 15.0.26208.0 | Optional
Microsoft.VisualStudio.Component.CodeMap | コード マップ | 15.0.26208.0 | Optional
Microsoft.VisualStudio.Component.DependencyValidation.Enterprise | ライブ依存関係検証 | 15.0.26208.0 | Optional
Microsoft.VisualStudio.Component.GraphDocument | DGML エディター | 15.0.27005.2 | Optional
Microsoft.VisualStudio.Component.Graphics.Tools | DirectX 用グラフィックス デバッガーおよび GPU プロファイラー | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Graphics.Win81 | グラフィックス ツール Windows 8.1 SDK | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Phone.Emulator.15254 | Windows 10 Mobile エミュレーター (Fall Creators Update) | 15.0.27406.0 | Optional
Microsoft.VisualStudio.Component.SQL.LocalDB.Runtime | SQL Server Express 2016 LocalDB | 15.7.27617.1 | Optional
Microsoft.VisualStudio.Component.SQL.NCLI | SQL Server Native Client | 15.0.26208.0 | Optional
Microsoft.VisualStudio.Component.UWP.VC.ARM64 | ARM64 用 C++ ユニバーサル Windows プラットフォーム ツール | 15.0.28125.51 | Optional
Microsoft.VisualStudio.Component.VC.CoreIde | Visual Studio C++ コア機能 | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.VC.Tools.ARM | ARM 用 Visual C++ コンパイラとライブラリ | 15.8.27825.0 | Optional
Microsoft.VisualStudio.Component.VC.Tools.ARM64 | ARM64 用 Visual C++ コンパイラとライブラリ | 15.9.28230.55 | Optional
Microsoft.VisualStudio.Component.VC.Tools.x86.x64 | VC++ 2017 バージョン 15.9 v14.16 最新の v141 ツール | 15.9.28230.55 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.10240 | Windows 10 SDK (10.0.10240.0) | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.10586 | Windows 10 SDK (10.0.10586.0) | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.14393 | Windows 10 SDK (10.0.14393.0) | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.15063.Desktop | デスクトップ用 Windows 10 SDK (10.0.15063.0) C++ [x86 および x64] | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.15063.UWP | UWP 用 Windows 10 SDK (10.0.15063.0): C#、VB、JS | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.15063.UWP.Native | UWP 用 Windows 10 SDK (10.0.15063.0): C++ | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.16299.Desktop | デスクトップ用 Windows 10 SDK (10.0.16299.0) C++ [x86 および x64] | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.16299.Desktop.arm | デスクトップ用 Windows 10 SDK (10.0.16299.0) C++ [ARM および ARM64] | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.16299.UWP | UWP 用 Windows 10 SDK (10.0.16299.0): C#、VB、JS | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.16299.UWP.Native | UWP 用 Windows 10 SDK (10.0.16299.0): C++ | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.17134 | Windows 10 SDK (10.0.17134.0) | 15.9.28307.102 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.IpOverUsb | USB デバイスの接続 | 15.9.28307.102 | Optional
Microsoft.VisualStudio.ComponentGroup.ArchitectureTools.Managed | アーキテクチャおよび分析ツール | 15.0.26208.0 | Optional
Microsoft.VisualStudio.ComponentGroup.UWP.VC | C++ ユニバーサル Windows プラットフォーム ツール | 15.9.28307.102 | Optional
Microsoft.VisualStudio.ComponentGroup.Windows10SDK.15063 | Windows 10 SDK (10.0.15063.0) | 15.8.27825.0 | Optional
Microsoft.VisualStudio.ComponentGroup.Windows10SDK.16299 | Windows 10 SDK (10.0.16299.0) | 15.8.27825.0 | Optional

## <a name="visual-studio-extension-development"></a>Visual Studio 拡張機能の開発

**ID:** Microsoft.VisualStudio.Workload.VisualStudioExtension

**説明:** Visual Studio 用のアドオンや拡張機能 (新しいコマンド、コード アナライザー、ツール ウィンドウを含みます) を作成します。

### <a name="components-included-by-this-workload"></a>このワークロードに含まれるコンポーネント

コンポーネント ID | 名前 | バージョン | 依存関係の種類
--- | --- | --- | ---
Microsoft.Component.ClickOnce | ClickOnce Publishing | 15.8.27825.0 | 必須
Microsoft.Component.MSBuild | MSBuild | 15.7.27520.0 | 必須
Microsoft.Net.Component.4.6.1.SDK | .NET Framework 4.6.1 SDK | 15.6.27406.0 | 必須
Microsoft.Net.Component.4.6.1.TargetingPack | .NET Framework 4.6.1 Targeting Pack | 15.6.27406.0 | 必須
Microsoft.Net.Component.4.6.TargetingPack | .NET Framework 4.6 Targeting Pack | 15.6.27406.0 | 必須
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | .NET Framework 4.6.1 開発ツール | 15.8.27825.0 | 必須
Microsoft.VisualStudio.Component.NuGet | NuGet パッケージ マネージャー | 15.9.28016.0 | 必須
Microsoft.VisualStudio.Component.PortableLibrary | .NET ポータブル ライブラリ Targeting Pack | 15.6.27309.0 | 必須
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# および Visual Basic Roslyn コンパイラ | 15.6.27309.0 | 必須
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# および Visual Basic | 15.8.27729.1 | 必須
Microsoft.VisualStudio.Component.Static.Analysis.Tools | スタティック分析ツール | 15.0.26208.0 | 必須
Microsoft.VisualStudio.Component.VSSDK | Visual Studio SDK | 15.8.27729.1 | 必須
Microsoft.VisualStudio.ComponentGroup.VisualStudioExtension.Prerequisites | Visual Studio 拡張機能の開発の前提条件 | 15.7.27625.0 | 必須
Microsoft.VisualStudio.Component.DiagnosticTools | .NET プロファイル ツール | 15.8.27729.1 | 推奨
Microsoft.VisualStudio.Component.IntelliTrace.FrontEnd | [IntelliTrace] | 15.8.27729.1 | 推奨
Microsoft.VisualStudio.Component.TextTemplating | テキスト テンプレート変換 | 15.0.26208.0 | 推奨
Component.Dotfuscator | PreEmptive Protection - Dotfuscator | 15.0.26208.0 | Optional
Microsoft.Component.CodeAnalysis.SDK | .NET Compiler Platform SDK | 15.0.27729.1 | Optional
Microsoft.Component.VC.Runtime.OSSupport | UWP 用の Visual C++ ランタイム | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.AppInsights.Tools | Developer Analytics Tools | 15.8.27825.0 | Optional
Microsoft.VisualStudio.Component.ClassDesigner | クラス デザイナー | 15.0.26208.0 | Optional
Microsoft.VisualStudio.Component.CodeClone | コード クローン | 15.0.26208.0 | Optional
Microsoft.VisualStudio.Component.CodeMap | コード マップ | 15.0.26208.0 | Optional
Microsoft.VisualStudio.Component.DependencyValidation.Enterprise | ライブ依存関係検証 | 15.0.26208.0 | Optional
Microsoft.VisualStudio.Component.DslTools | Modeling SDK | 15.0.27005.2 | Optional
Microsoft.VisualStudio.Component.GraphDocument | DGML エディター | 15.0.27005.2 | Optional
Microsoft.VisualStudio.Component.SQL.LocalDB.Runtime | SQL Server Express 2016 LocalDB | 15.7.27617.1 | Optional
Microsoft.VisualStudio.Component.SQL.NCLI | SQL Server Native Client | 15.0.26208.0 | Optional
Microsoft.VisualStudio.Component.VC.ATL | x86 用と x64 用の Visual C++ ATL | 15.7.27625.0 | Optional
Microsoft.VisualStudio.Component.VC.ATLMFC | x86 用と x64 用の Visual C++ MFC | 15.7.27625.0 | Optional
Microsoft.VisualStudio.Component.VC.CoreIde | Visual Studio C++ コア機能 | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.VC.Tools.x86.x64 | VC++ 2017 バージョン 15.9 v14.16 最新の v141 ツール | 15.9.28230.55 | Optional
Microsoft.VisualStudio.ComponentGroup.ArchitectureTools.Managed | アーキテクチャおよび分析ツール | 15.0.26208.0 | Optional

## <a name="mobile-development-with-javascript"></a>JavaScript でのモバイル開発

**ID:** Microsoft.VisualStudio.Workload.WebCrossPlat

**説明:** Tools for Apache Cordova を使用して Android、iOS、UWP 向けのアプリをビルドします。

### <a name="components-included-by-this-workload"></a>このワークロードに含まれるコンポーネント

コンポーネント ID | 名前 | バージョン | 依存関係の種類
--- | --- | --- | ---
Component.CordovaToolset.6.3.1 | Cordova 6.3.1 ツールセット | 15.7.27625.0 | 必須
Component.WebSocket | WebSocket4Net | 15.0.26606.0 | 必須
Microsoft.VisualStudio.Component.Cordova | JavaScript でのモバイル開発のコア機能 | 15.0.26606.0 | 必須
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | JavaScript 診断 | 15.8.27729.1 | 必須
Microsoft.VisualStudio.Component.JavaScript.ProjectSystem | JavaScript ProjectSystem と共有ツール | 15.0.26606.0 | 必須
Microsoft.VisualStudio.Component.JavaScript.TypeScript | JavaScript および TypeScript の言語サポート | 15.9.28125.51 | 必須
Microsoft.VisualStudio.Component.TypeScript.2.3 | TypeScript 2.3 SDK | 15.8.27729.1 | 必須
Microsoft.VisualStudio.Component.TypeScript.3.1 | TypeScript 3.1 SDK | 15.0.28218.60 | 必須
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | ASP.NET と Web 開発 | 15.8.27825.0 | 必須
Component.Android.SDK23.Private | Android SDK セットアップ (API レベル 23) (JavaScript/C++ を使用したモバイル開発のためにローカルにインストール) | 15.9.28016.0 | Optional
Component.Google.Android.Emulator.API23.Private | Google Android Emulator (API レベル 23) (ローカル インストール) | 15.6.27413.0 | Optional
Component.HAXM.Private | Intel Hardware Accelerated Execution Manager (HAXM) (ローカル インストール) | 15.9.28307.421 | Optional
Component.OpenJDK | Microsoft 配布の OpenJDK | 15.9.28125.51 | Optional
Microsoft.Component.ClickOnce | ClickOnce Publishing | 15.8.27825.0 | Optional
Microsoft.Component.NetFX.Native | .NET Native | 15.0.26208.0 | Optional
Microsoft.VisualStudio.Component.AppInsights.Tools | Developer Analytics Tools | 15.8.27825.0 | Optional
Microsoft.VisualStudio.Component.DiagnosticTools | .NET プロファイル ツール | 15.8.27729.1 | Optional
Microsoft.VisualStudio.Component.Git | Git for Windows | 15.0.26208.0 | Optional
Microsoft.VisualStudio.Component.Graphics | イメージ エディターと 3D モデル エディター | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Phone.Emulator.15254 | Windows 10 Mobile エミュレーター (Fall Creators Update) | 15.0.27406.0 | Optional
Microsoft.VisualStudio.Component.SQL.CLR | SQL Server の CLR データ型 | 15.0.26208.0 | Optional
Microsoft.VisualStudio.Component.VisualStudioData | データソースとサービス参照 | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.17763 | Windows 10 SDK (10.0.17763.0) | 15.9.28307.102 | Optional
Microsoft.VisualStudio.ComponentGroup.UWP.Cordova | Cordova 用ユニバーサル Windows プラットフォーム ツール | 15.9.28307.102 | Optional

## <a name="unaffiliated-components"></a>関連付けられていないコンポーネント

以下のコンポーネントはどのワークロードにも含まれていませんが、個別のコンポーネントとして選択できます。

コンポーネント ID | 名前 | バージョン
--- | --- | ---
Component.Android.Emulator | Visual Studio Emulator for Android | 15.6.27413.0
Component.Android.NDK.R11C | Android NDK (R11C) | 11.3.14
Component.Android.NDK.R11C_3264 | Android NDK (R11C) (32 ビット) | 11.3.16
Component.Android.SDK23 | Android SDK セットアップ (API レベル 23) (グローバル インストール) | 15.9.28107.0
Component.Android.SDK25 | Android SDK セットアップ (API レベル 25) | 15.9.28107.0
Component.GitHub.VisualStudio | Visual Studio 用の GitHub 拡張機能 | 2.5.2.2500
Component.Google.Android.Emulator.API23.V2 | Google Android Emulator (API レベル 23) (グローバル インストール) | 15.6.27413.0
Component.Google.Android.Emulator.API25 | Google Android Emulator (API レベル 25) | 15.7.27604.0
Microsoft.Component.Blend.SDK.WPF | Blend for Visual Studio SDK for .NET | 15.6.27406.0
Microsoft.Component.HelpViewer | ヘルプ ビューアー | 15.9.28307.421
Microsoft.VisualStudio.Component.LinqToSql | LINQ to SQL ツール | 15.6.27406.0
Microsoft.VisualStudio.Component.Phone.Emulator | Windows 10 Mobile エミュレーター (Anniversary Edition) | 15.6.27406.0
Microsoft.VisualStudio.Component.Phone.Emulator.15063 | Windows 10 Mobile エミュレーター (Creators Update) | 15.6.27406.0
Microsoft.VisualStudio.Component.Runtime.Node.x86.6.4.0 | Node.js v6.4.0 (x86) ベースのコンポーネント用ランタイム | 15.7.27617.1
Microsoft.VisualStudio.Component.Runtime.Node.x86.7.4.0 | Node.js v7.4.0 (x86) ベースのコンポーネント用ランタイム | 15.7.27617.1
Microsoft.VisualStudio.Component.TestTools.CodedUITest | コード化された UI テスト | 15.0.26606.0
Microsoft.VisualStudio.Component.TestTools.FeedbackClient | Microsoft Feedback Client | 15.6.27406.0
Microsoft.VisualStudio.Component.TestTools.MicrosoftTestManager | Microsoft Test Manager | 15.6.27406.0
Microsoft.VisualStudio.Component.TypeScript.2.0 | TypeScript 2.0 SDK | 15.8.27729.1
Microsoft.VisualStudio.Component.TypeScript.2.1 | TypeScript 2.1 SDK | 15.8.27729.1
Microsoft.VisualStudio.Component.TypeScript.2.2 | TypeScript 2.2 SDK | 15.8.27729.1
Microsoft.VisualStudio.Component.TypeScript.2.5 | TypeScript 2.5 SDK | 15.6.27406.0
Microsoft.VisualStudio.Component.TypeScript.2.6 | TypeScript 2.6 SDK | 15.0.27729.1
Microsoft.VisualStudio.Component.TypeScript.2.7 | TypeScript 2.7 SDK | 15.0.27729.1
Microsoft.VisualStudio.Component.TypeScript.2.8 | TypeScript 2.8 SDK | 15.0.27729.1
Microsoft.VisualStudio.Component.TypeScript.2.9 | TypeScript 2.9 SDK | 15.0.27924.0
Microsoft.VisualStudio.Component.TypeScript.3.0 | TypeScript 3.0 SDK | 15.0.27924.0
Microsoft.VisualStudio.Component.VC.ATL.ARM | ARM 用 Visual C++ ATL | 15.7.27625.0
Microsoft.VisualStudio.Component.VC.ATL.ARM.Spectre | Spectre の軽減策を含む ARM 用 Visual C++ ATL | 15.7.27625.0
Microsoft.VisualStudio.Component.VC.ATL.ARM64 | ARM64 用 Visual C++ ATL | 15.7.27625.0
Microsoft.VisualStudio.Component.VC.ATL.ARM64.Spectre | Spectre の軽減策を含む ARM64 用 Visual C++ ATL | 15.7.27625.0
Microsoft.VisualStudio.Component.VC.ATL.Spectre | Spectre の軽減策を含む Visual C++ ATL (x86 または x64) | 15.7.27625.0
Microsoft.VisualStudio.Component.VC.ATLMFC.Spectre | Spectre の軽減策を含む x86 または x64 用 Visual C++ MFC | 15.7.27625.0
Microsoft.VisualStudio.Component.VC.ClangC2 | Clang/C2 (試験的) | 15.7.27520.0
Microsoft.VisualStudio.Component.VC.MFC.ARM | ARM 用 Visual C++ MFC | 15.7.27625.0
Microsoft.VisualStudio.Component.VC.MFC.ARM.Spectre | Spectre の軽減策を含む ARM 用 Visual C++ MFC | 15.7.27625.0
Microsoft.VisualStudio.Component.VC.MFC.ARM64 | ARM64 用 Visual C++ MFC | 15.7.27625.0
Microsoft.VisualStudio.Component.VC.MFC.ARM64.Spectre | Spectre の軽減策を含む ARM64 用 Visual C++ MFC サポート | 15.7.27625.0
Microsoft.VisualStudio.Component.VC.Runtimes.ARM.Spectre | VC++ 2017 バージョン 15.9 v14.16 Spectre 用ライブラリ (ARM) | 15.9.28230.55
Microsoft.VisualStudio.Component.VC.Runtimes.ARM64.Spectre | VC++ 2017 バージョン 15.9 v14.16 Spectre 用ライブラリ (ARM64) | 15.9.28230.55
Microsoft.VisualStudio.Component.VC.Runtimes.x86.x64.Spectre | VC++ 2017 バージョン 15.9 v14.16 Spectre 用ライブラリ (x86 および x64) | 15.9.28230.55
Microsoft.VisualStudio.Component.VC.Tools.14.11 | VC++ 2017 バージョン 15.4 v14.11 ツールセット | 15.0.27924.0
Microsoft.VisualStudio.Component.VC.Tools.14.12 | VC++ 2017 バージョン 15.5 v14.12 ツールセット | 15.0.27924.0
Microsoft.VisualStudio.Component.VC.Tools.14.13 | VC++ 2017 バージョン 15.6 v14.13 ツールセット | 15.0.27924.0
Microsoft.VisualStudio.Component.VC.Tools.14.14 | VC++ 2017 バージョン 15.7 v14.14 ツールセット | 15.0.27924.0
Microsoft.VisualStudio.Component.VC.Tools.14.15 | VC++ 2017 バージョン 15.8 v14.15 ツールセット | 15.0.28230.55
