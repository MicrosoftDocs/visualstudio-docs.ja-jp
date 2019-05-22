---
title: Visual Studio Professional 2019 のワークロード ID とコンポーネント ID
titleSuffix: ''
description: ワークロード ID とコンポーネント ID を使用して、コマンドラインを使用して Visual Studio をインストールするか、VSIX マニフェストで依存関係として指定します。
keywords: ''
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.date: 04/02/2019
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.topic: include
ms.openlocfilehash: 23cbd90b81bcc05fef34040b4934c7152f79ae41
ms.sourcegitcommit: 2ee11676af4f3fc5729934d52541e9871fb43ee9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/17/2019
ms.locfileid: "65848901"
---
## <a name="visual-studio-core-editor-included-with-visual-studio-professional-2019"></a>Visual Studio のコア エディター (Visual Studio Professional 2019 に付属)

**ID:** Microsoft.VisualStudio.Workload.CoreEditor

**説明:** 構文認識コード編集機能、ソース コード管理、作業項目管理などの Visual Studio の基本的なシェル エクスペリエンス。

### <a name="components-included-by-this-workload"></a>このワークロードに含まれるコンポーネント

コンポーネント ID | name | Version | 依存関係の種類
--- | --- | --- | ---
Microsoft.VisualStudio.Component.CoreEditor | Visual Studio のコア エディター | 16.0.28315.86 | 必須
Microsoft.VisualStudio.Component.StartPageExperiment.Cpp | C++ ユーザー用 Visual Studio スタート ページ | 16.0.28315.86 | Optional

## <a name="azure-development"></a>Azure の開発

**ID:** Microsoft.VisualStudio.Workload.Azure

**説明:** クラウド アプリの開発、リソースの作成、Docker サポートを含むコンテナーのビルドのための Azure SDK、ツール、プロジェクト。

### <a name="components-included-by-this-workload"></a>このワークロードに含まれるコンポーネント

コンポーネント ID | name | Version | 依存関係の種類
--- | --- | --- | ---
Component.Microsoft.VisualStudio.RazorExtension | Razor 言語サービス | 16.0.28714.129 | 必須
Component.Microsoft.VisualStudio.Web.AzureFunctions | Azure WebJobs ツール | 16.0.28714.129 | 必須
Component.Microsoft.Web.LibraryManager | ライブラリ マネージャー | 16.0.28315.86 | 必須
Microsoft.Component.MSBuild | MSBuild | 16.0.28517.75 | 必須
Microsoft.Net.Component.4.5.2.TargetingPack | .NET Framework 4.5.2 Targeting Pack | 16.0.28517.75 | 必須
Microsoft.Net.Component.4.5.TargetingPack | .NET Framework 4.5 Targeting Pack | 16.0.28517.75 | 必須
Microsoft.Net.Component.4.6.1.TargetingPack | .NET Framework 4.6.1 Targeting Pack | 16.0.28517.75 | 必須
Microsoft.Net.Component.4.7.2.SDK | .NET Framework 4.7.2 SDK | 16.0.28517.75 | 必須
Microsoft.Net.Component.4.7.2.TargetingPack | .NET Framework 4.7.2 Targeting Pack | 16.0.28517.75 | 必須
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | .NET Framework 4.7.2 開発ツール | 16.0.28516.191 | 必須
Microsoft.Net.Core.Component.SDK.2.1 | .NET Core 2.1 開発ツール | 16.0.28621.142 | 必須
Microsoft.NetCore.ComponentGroup.DevelopmentTools.2.1 | .NET Core 2.1 開発ツール | 16.0.28516.191 | 必須
Microsoft.NetCore.ComponentGroup.Web.2.1 | .NET Core 2.1 開発ツール | 16.0.28621.142 | 必須
Microsoft.VisualStudio.Component.Azure.AuthoringTools | Azure Authoring Tools | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.Azure.ClientLibs | .NET 用 Azure ライブラリ | 16.0.28315.86 | 必須
Microsoft.VisualStudio.Component.Azure.Compute.Emulator | Azure コンピューティング エミュレーター | 16.0.28720.110 | 必須
Microsoft.VisualStudio.Component.Azure.Storage.Emulator | Azure Storage エミュレーター | 16.0.28517.75 | 必須
Microsoft.VisualStudio.Component.CloudExplorer | Cloud Explorer | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.Common.Azure.Tools | 接続および発行ツール | 16.0.28315.86 | 必須
Microsoft.VisualStudio.Component.DockerTools | コンテナー開発ツール | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.FSharp | F# 言語サポート | 16.0.28315.86 | 必須
Microsoft.VisualStudio.Component.FSharp.WebTemplates | Web プロジェクト用の F# 言語サポート | 16.0.28517.75 | 必須
Microsoft.VisualStudio.Component.IISExpress | IIS Express  | 16.0.28315.86 | 必須
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | JavaScript 診断 | 16.0.28517.75 | 必須
Microsoft.VisualStudio.Component.JavaScript.TypeScript | JavaScript および TypeScript の言語サポート | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.ManagedDesktop.Core | Managed Desktop Workload コア | 16.0.28621.142 | 必須
Microsoft.VisualStudio.Component.MSODBC.SQL | SQL Server ODBC Driver | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.MSSQL.CMDLnUtils | SQL Server コマンド ライン ユーティリティ | 16.0.28707.177 | 必須
Microsoft.VisualStudio.Component.NuGet | NuGet パッケージ マネージャー | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# および Visual Basic Roslyn コンパイラ | 16.0.28714.129 | 必須
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# および Visual Basic | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.SQL.ADAL | SQL ADAL ランタイム | 16.0.28517.75 | 必須
Microsoft.VisualStudio.Component.SQL.CLR | SQL Server の CLR データ型 | 16.0.28315.86 | 必須
Microsoft.VisualStudio.Component.SQL.DataSources | SQL Server サポートのためのデータ ソース | 16.0.28315.86 | 必須
Microsoft.VisualStudio.Component.SQL.LocalDB.Runtime | SQL Server Express 2016 LocalDB | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.SQL.SSDT | SQL Server Data Tools | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.TextTemplating | テキスト テンプレート変換 | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.TypeScript.3.3 | TypeScript 3.3 SDK | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.Web | ASP.NET と Web の開発ツール | 16.0.28517.75 | 必須
Microsoft.VisualStudio.ComponentGroup.Azure.Prerequisites | Azure 開発の前提条件 | 16.0.28625.61 | 必須
Microsoft.VisualStudio.ComponentGroup.AzureFunctions | Azure WebJobs ツール | 16.0.28621.142 | 必須
Microsoft.VisualStudio.ComponentGroup.Web | ASP.NET と Web の開発ツールの前提条件 | 16.0.28621.142 | 必須
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | ASP.NET と Web 開発 | 16.0.28621.142 | 必須
Microsoft.Component.Azure.DataLake.Tools | Azure Data Lake と Stream Analytics ツール | 16.0.28720.110 | 推奨
Microsoft.Net.Component.4.5.1.TargetingPack | .NET Framework 4.5.1 Targeting Pack | 16.0.28517.75 | 推奨
Microsoft.Net.Component.4.6.TargetingPack | .NET Framework 4.6 Targeting Pack | 16.0.28517.75 | 推奨
Microsoft.Net.Component.4.TargetingPack | .NET Framework 4 Targeting Pack | 16.0.28517.75 | 推奨
Microsoft.Net.ComponentGroup.TargetingPacks.Common | .NET Framework 4 – 4.6 開発ツール | 16.0.28516.191 | 推奨
Microsoft.VisualStudio.Component.AspNet45 | 高度な ASP.NET 機能 | 16.0.28315.86 | 推奨
Microsoft.VisualStudio.Component.Azure.Kubernetes.Tools | Visual Studio Tools for Kubernetes | 16.0.28625.61 | 推奨
Microsoft.VisualStudio.Component.Azure.ResourceManager.Tools | Azure Resource Manager コア ツール | 16.0.28517.75 | 推奨
Microsoft.VisualStudio.Component.Azure.ServiceFabric.Tools | Service Fabric Tools | 16.0.28517.75 | 推奨
Microsoft.VisualStudio.Component.Azure.Waverton | Azure Cloud Services コア ツール | 16.0.28625.61 | 推奨
Microsoft.VisualStudio.Component.Azure.Waverton.BuildTools | Azure Cloud Services ビルド ツール | 16.0.28625.61 | 推奨
Microsoft.VisualStudio.Component.DiagnosticTools | .NET プロファイル ツール | 16.0.28625.61 | 推奨
Microsoft.VisualStudio.Component.WebDeploy | Web 配置 | 16.0.28517.75 | 推奨
Microsoft.VisualStudio.ComponentGroup.Azure.CloudServices | Azure Cloud Services ツール | 16.0.28315.86 | 推奨
Microsoft.VisualStudio.ComponentGroup.Azure.ResourceManager.Tools | Azure Resource Manager ツール | 16.0.28528.71 | 推奨
Microsoft.Net.Component.4.6.1.SDK | .NET Framework 4.6.1 SDK | 16.0.28517.75 | Optional
Microsoft.Net.Component.4.6.2.SDK | .NET Framework 4.6.2 SDK | 16.0.28517.75 | Optional
Microsoft.Net.Component.4.6.2.TargetingPack | .NET Framework 4.6.2 Targeting Pack | 16.0.28517.75 | Optional
Microsoft.Net.Component.4.7.1.SDK | .NET Framework 4.7.1 SDK | 16.0.28517.75 | Optional
Microsoft.Net.Component.4.7.1.TargetingPack | .NET Framework 4.7.1 Targeting Pack | 16.0.28517.75 | Optional
Microsoft.Net.Component.4.7.SDK | .NET Framework 4.7 SDK | 16.0.28517.75 | Optional
Microsoft.Net.Component.4.7.TargetingPack | .NET Framework 4.7 Targeting Pack | 16.0.28517.75 | Optional
Microsoft.Net.ComponentGroup.4.6.1.DeveloperTools | .NET Framework 4.6.1 開発ツール | 16.0.28621.142 | Optional
Microsoft.Net.ComponentGroup.4.6.2.DeveloperTools | .NET Framework 4.6.2 開発ツール | 16.0.28516.191 | Optional
Microsoft.Net.ComponentGroup.4.7.1.DeveloperTools | .NET Framework 4.7.1 開発ツール | 16.0.28516.191 | Optional
Microsoft.Net.ComponentGroup.4.7.DeveloperTools | .NET Framework 4.7 開発ツール | 16.0.28516.191 | Optional
Microsoft.Net.Core.Component.SDK.2.2 | .NET Core 2.2 開発ツール | 16.0.28621.142 | Optional
Microsoft.NetCore.ComponentGroup.DevelopmentTools.2.2 | .NET Core 2.2 開発ツール | 16.0.28516.191 | Optional
Microsoft.NetCore.ComponentGroup.Web.2.2 | .NET Core 2.2 開発ツール | 16.0.28621.142 | Optional
Microsoft.VisualStudio.Component.Azure.Storage.AzCopy | Azure Storage AzCopy | 16.0.28517.75 | Optional
Microsoft.VisualStudio.Component.Wcf.Tooling | Windows Communication Foundation | 16.0.28625.61 | Optional

## <a name="data-storage-and-processing"></a>データ ストレージとデータ処理

**ID:** Microsoft.VisualStudio.Workload.Data

**説明:** SQL Server、Azure Data Lake、Hadoop を使用してデータ ソリューションの接続、開発、テストを行います。

### <a name="components-included-by-this-workload"></a>このワークロードに含まれるコンポーネント

コンポーネント ID | name | Version | 依存関係の種類
--- | --- | --- | ---
Component.Microsoft.VisualStudio.RazorExtension | Razor 言語サービス | 16.0.28714.129 | 推奨
Component.Microsoft.Web.LibraryManager | ライブラリ マネージャー | 16.0.28315.86 | 推奨
Microsoft.Component.Azure.DataLake.Tools | Azure Data Lake と Stream Analytics ツール | 16.0.28720.110 | 推奨
Microsoft.Component.MSBuild | MSBuild | 16.0.28517.75 | 推奨
Microsoft.Net.Component.4.5.1.TargetingPack | .NET Framework 4.5.1 Targeting Pack | 16.0.28517.75 | 推奨
Microsoft.Net.Component.4.5.2.TargetingPack | .NET Framework 4.5.2 Targeting Pack | 16.0.28517.75 | 推奨
Microsoft.Net.Component.4.5.TargetingPack | .NET Framework 4.5 Targeting Pack | 16.0.28517.75 | 推奨
Microsoft.Net.Component.4.6.TargetingPack | .NET Framework 4.6 Targeting Pack | 16.0.28517.75 | 推奨
Microsoft.Net.Component.4.7.2.SDK | .NET Framework 4.7.2 SDK | 16.0.28517.75 | 推奨
Microsoft.Net.Component.4.7.2.TargetingPack | .NET Framework 4.7.2 Targeting Pack | 16.0.28517.75 | 推奨
Microsoft.Net.Component.4.TargetingPack | .NET Framework 4 Targeting Pack | 16.0.28517.75 | 推奨
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | .NET Framework 4.7.2 開発ツール | 16.0.28516.191 | 推奨
Microsoft.Net.ComponentGroup.TargetingPacks.Common | .NET Framework 4 – 4.6 開発ツール | 16.0.28516.191 | 推奨
Microsoft.Net.Core.Component.SDK.2.1 | .NET Core 2.1 開発ツール | 16.0.28621.142 | 推奨
Microsoft.VisualStudio.Component.Azure.AuthoringTools | Azure Authoring Tools | 16.0.28625.61 | 推奨
Microsoft.VisualStudio.Component.Azure.ClientLibs | .NET 用 Azure ライブラリ | 16.0.28315.86 | 推奨
Microsoft.VisualStudio.Component.Azure.Compute.Emulator | Azure コンピューティング エミュレーター | 16.0.28720.110 | 推奨
Microsoft.VisualStudio.Component.Azure.Storage.Emulator | Azure Storage エミュレーター | 16.0.28517.75 | 推奨
Microsoft.VisualStudio.Component.Azure.Waverton | Azure Cloud Services コア ツール | 16.0.28625.61 | 推奨
Microsoft.VisualStudio.Component.Azure.Waverton.BuildTools | Azure Cloud Services ビルド ツール | 16.0.28625.61 | 推奨
Microsoft.VisualStudio.Component.CloudExplorer | Cloud Explorer | 16.0.28625.61 | 推奨
Microsoft.VisualStudio.Component.Common.Azure.Tools | 接続および発行ツール | 16.0.28315.86 | 推奨
Microsoft.VisualStudio.Component.DockerTools | コンテナー開発ツール | 16.0.28625.61 | 推奨
Microsoft.VisualStudio.Component.IISExpress | IIS Express  | 16.0.28315.86 | 推奨
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | JavaScript 診断 | 16.0.28517.75 | 推奨
Microsoft.VisualStudio.Component.JavaScript.TypeScript | JavaScript および TypeScript の言語サポート | 16.0.28625.61 | 推奨
Microsoft.VisualStudio.Component.ManagedDesktop.Core | Managed Desktop Workload コア | 16.0.28621.142 | 推奨
Microsoft.VisualStudio.Component.MSODBC.SQL | SQL Server ODBC Driver | 16.0.28625.61 | 推奨
Microsoft.VisualStudio.Component.MSSQL.CMDLnUtils | SQL Server コマンド ライン ユーティリティ | 16.0.28707.177 | 推奨
Microsoft.VisualStudio.Component.NuGet | NuGet パッケージ マネージャー | 16.0.28625.61 | 推奨
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# および Visual Basic Roslyn コンパイラ | 16.0.28714.129 | 推奨
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# および Visual Basic | 16.0.28625.61 | 推奨
Microsoft.VisualStudio.Component.SQL.ADAL | SQL ADAL ランタイム | 16.0.28517.75 | 推奨
Microsoft.VisualStudio.Component.SQL.CLR | SQL Server の CLR データ型 | 16.0.28315.86 | 推奨
Microsoft.VisualStudio.Component.SQL.DataSources | SQL Server サポートのためのデータ ソース | 16.0.28315.86 | 推奨
Microsoft.VisualStudio.Component.SQL.LocalDB.Runtime | SQL Server Express 2016 LocalDB | 16.0.28625.61 | 推奨
Microsoft.VisualStudio.Component.SQL.SSDT | SQL Server Data Tools | 16.0.28625.61 | 推奨
Microsoft.VisualStudio.Component.TextTemplating | テキスト テンプレート変換 | 16.0.28625.61 | 推奨
Microsoft.VisualStudio.Component.TypeScript.3.3 | TypeScript 3.3 SDK | 16.0.28625.61 | 推奨
Microsoft.VisualStudio.Component.Web | ASP.NET と Web の開発ツール | 16.0.28517.75 | 推奨
Microsoft.VisualStudio.ComponentGroup.Web | ASP.NET と Web の開発ツールの前提条件 | 16.0.28621.142 | 推奨
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | ASP.NET と Web 開発 | 16.0.28621.142 | 推奨
Microsoft.Net.Component.4.6.1.TargetingPack | .NET Framework 4.6.1 Targeting Pack | 16.0.28517.75 | Optional
Microsoft.VisualStudio.Component.FSharp.Desktop | F# デスクトップ言語のサポート | 16.0.28315.86 | Optional

## <a name="data-science-and-analytical-applications"></a>データ サイエンスと分析のアプリケーション

**ID:** Microsoft.VisualStudio.Workload.DataScience

**説明:** データ サイエンス アプリケーションを作成するための言語とツール (Python と F# が含まれます)。

### <a name="components-included-by-this-workload"></a>このワークロードに含まれるコンポーネント

コンポーネント ID | name | Version | 依存関係の種類
--- | --- | --- | ---
Microsoft.Component.PythonTools | Python 言語サポート | 16.0.28625.61 | 推奨
Microsoft.Component.PythonTools.Minicondax64 | Python miniconda | 16.0.28625.61 | 推奨
Microsoft.Component.PythonTools.Web | Python Web サポート | 16.0.28517.75 | 推奨
Microsoft.Net.Component.4.6.1.TargetingPack | .NET Framework 4.6.1 Targeting Pack | 16.0.28517.75 | 推奨
Microsoft.VisualStudio.Component.Common.Azure.Tools | 接続および発行ツール | 16.0.28315.86 | 推奨
Microsoft.VisualStudio.Component.FSharp.Desktop | F# デスクトップ言語のサポート | 16.0.28315.86 | 推奨
Microsoft.VisualStudio.Component.JavaScript.TypeScript | JavaScript および TypeScript の言語サポート | 16.0.28625.61 | 推奨
Microsoft.VisualStudio.Component.NuGet | NuGet パッケージ マネージャー | 16.0.28625.61 | 推奨
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# および Visual Basic Roslyn コンパイラ | 16.0.28714.129 | 推奨
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# および Visual Basic | 16.0.28625.61 | 推奨
Microsoft.VisualStudio.Component.TypeScript.3.3 | TypeScript 3.3 SDK | 16.0.28625.61 | 推奨
Microsoft.VisualStudio.Component.WebDeploy | Web 配置 | 16.0.28517.75 | 推奨
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | ASP.NET と Web 開発 | 16.0.28621.142 | 推奨
Microsoft.Component.VC.Runtime.UCRTSDK | Windows Universal CRT SDK | 16.0.28625.61 | Optional
Microsoft.ComponentGroup.PythonTools.NativeDevelopment | Python ネイティブ開発ツール | 16.0.28621.142 | Optional
Microsoft.VisualStudio.Component.Graphics.Tools | DirectX 用グラフィックス デバッガーおよび GPU プロファイラー | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.VC.140 | MSVC v140 - VS 2015 C++ ビルド ツール (v14.00) | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.VC.CoreIde | C++ コア機能 | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.VC.DiagnosticTools | C++ のプロファイル ツール | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.VC.Tools.x86.x64 | MSVC v142 – VS 2019 C++ x64/x86 ビルド ツール (v14.20) | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.Windows10SDK | Windows ユニバーサル C ランタイム | 16.0.28315.86 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.17763 | Windows 10 SDK (10.0.17763.0) | 16.0.28517.75 | Optional

## <a name="net-desktop-development"></a>.NET デスクトップ開発

**ID:** Microsoft.VisualStudio.Workload.ManagedDesktop

**説明:** C#、Visual Basic、F# を使用して、WPF、Windows フォーム、コンソール アプリケーションをビルドします。

### <a name="components-included-by-this-workload"></a>このワークロードに含まれるコンポーネント

コンポーネント ID | name | Version | 依存関係の種類
--- | --- | --- | ---
Microsoft.Component.MSBuild | MSBuild | 16.0.28517.75 | 必須
Microsoft.Net.Component.4.7.2.SDK | .NET Framework 4.7.2 SDK | 16.0.28517.75 | 必須
Microsoft.Net.Component.4.7.2.TargetingPack | .NET Framework 4.7.2 Targeting Pack | 16.0.28517.75 | 必須
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | .NET Framework 4.7.2 開発ツール | 16.0.28516.191 | 必須
Microsoft.Net.Core.Component.SDK.2.1 | .NET Core 2.1 開発ツール | 16.0.28621.142 | 必須
Microsoft.VisualStudio.Component.ManagedDesktop.Core | Managed Desktop Workload コア | 16.0.28621.142 | 必須
Microsoft.VisualStudio.Component.ManagedDesktop.Prerequisites | .NET デスクトップ開発ツール | 16.0.28621.142 | 必須
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# および Visual Basic Roslyn コンパイラ | 16.0.28714.129 | 必須
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# および Visual Basic | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.SQL.CLR | SQL Server の CLR データ型 | 16.0.28315.86 | 必須
Microsoft.VisualStudio.Component.TextTemplating | テキスト テンプレート変換 | 16.0.28625.61 | 必須
Component.Microsoft.VisualStudio.LiveShare | Live Share | 1.0.12 | 推奨
Microsoft.ComponentGroup.Blend | Blend for Visual Studio | 16.0.28315.86 | 推奨
Microsoft.Net.Component.4.5.1.TargetingPack | .NET Framework 4.5.1 Targeting Pack | 16.0.28517.75 | 推奨
Microsoft.Net.Component.4.5.2.TargetingPack | .NET Framework 4.5.2 Targeting Pack | 16.0.28517.75 | 推奨
Microsoft.Net.Component.4.5.TargetingPack | .NET Framework 4.5 Targeting Pack | 16.0.28517.75 | 推奨
Microsoft.Net.Component.4.6.TargetingPack | .NET Framework 4.6 Targeting Pack | 16.0.28517.75 | 推奨
Microsoft.Net.Component.4.TargetingPack | .NET Framework 4 Targeting Pack | 16.0.28517.75 | 推奨
Microsoft.Net.ComponentGroup.TargetingPacks.Common | .NET Framework 4 – 4.6 開発ツール | 16.0.28516.191 | 推奨
Microsoft.VisualStudio.Component.Debugger.JustInTime | Just-In-Time デバッガー | 16.0.28517.75 | 推奨
Microsoft.VisualStudio.Component.EntityFramework | Entity Framework 6 Tools | 16.0.28315.86 | 推奨
Component.Dotfuscator | PreEmptive Protection - Dotfuscator | 16.0.28528.71 | Optional
Component.Microsoft.VisualStudio.RazorExtension | Razor 言語サービス | 16.0.28714.129 | Optional
Component.Microsoft.Web.LibraryManager | ライブラリ マネージャー | 16.0.28315.86 | Optional
Microsoft.Net.Component.4.6.1.SDK | .NET Framework 4.6.1 SDK | 16.0.28517.75 | Optional
Microsoft.Net.Component.4.6.1.TargetingPack | .NET Framework 4.6.1 Targeting Pack | 16.0.28517.75 | Optional
Microsoft.Net.Component.4.6.2.SDK | .NET Framework 4.6.2 SDK | 16.0.28517.75 | Optional
Microsoft.Net.Component.4.6.2.TargetingPack | .NET Framework 4.6.2 Targeting Pack | 16.0.28517.75 | Optional
Microsoft.Net.Component.4.7.1.SDK | .NET Framework 4.7.1 SDK | 16.0.28517.75 | Optional
Microsoft.Net.Component.4.7.1.TargetingPack | .NET Framework 4.7.1 Targeting Pack | 16.0.28517.75 | Optional
Microsoft.Net.Component.4.7.SDK | .NET Framework 4.7 SDK | 16.0.28517.75 | Optional
Microsoft.Net.Component.4.7.TargetingPack | .NET Framework 4.7 Targeting Pack | 16.0.28517.75 | Optional
Microsoft.Net.ComponentGroup.4.6.1.DeveloperTools | .NET Framework 4.6.1 開発ツール | 16.0.28621.142 | Optional
Microsoft.Net.ComponentGroup.4.6.2.DeveloperTools | .NET Framework 4.6.2 開発ツール | 16.0.28516.191 | Optional
Microsoft.Net.ComponentGroup.4.7.1.DeveloperTools | .NET Framework 4.7.1 開発ツール | 16.0.28516.191 | Optional
Microsoft.Net.ComponentGroup.4.7.DeveloperTools | .NET Framework 4.7 開発ツール | 16.0.28516.191 | Optional
Microsoft.Net.Core.Component.SDK.2.2 | .NET Core 2.2 開発ツール | 16.0.28621.142 | Optional
Microsoft.NetCore.ComponentGroup.DevelopmentTools.2.1 | .NET Core 2.1 開発ツール | 16.0.28516.191 | Optional
Microsoft.NetCore.ComponentGroup.DevelopmentTools.2.2 | .NET Core 2.2 開発ツール | 16.0.28516.191 | Optional
Microsoft.VisualStudio.Component.Common.Azure.Tools | 接続および発行ツール | 16.0.28315.86 | Optional
Microsoft.VisualStudio.Component.DockerTools | コンテナー開発ツール | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.FSharp | F# 言語サポート | 16.0.28315.86 | Optional
Microsoft.VisualStudio.Component.FSharp.Desktop | F# デスクトップ言語のサポート | 16.0.28315.86 | Optional
Microsoft.VisualStudio.Component.IISExpress | IIS Express  | 16.0.28315.86 | Optional
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | JavaScript 診断 | 16.0.28517.75 | Optional
Microsoft.VisualStudio.Component.JavaScript.TypeScript | JavaScript および TypeScript の言語サポート | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.MSODBC.SQL | SQL Server ODBC Driver | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.MSSQL.CMDLnUtils | SQL Server コマンド ライン ユーティリティ | 16.0.28707.177 | Optional
Microsoft.VisualStudio.Component.NuGet | NuGet パッケージ マネージャー | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.PortableLibrary | .NET ポータブル ライブラリ Targeting Pack | 16.0.28517.75 | Optional
Microsoft.VisualStudio.Component.SQL.ADAL | SQL ADAL ランタイム | 16.0.28517.75 | Optional
Microsoft.VisualStudio.Component.SQL.DataSources | SQL Server サポートのためのデータ ソース | 16.0.28315.86 | Optional
Microsoft.VisualStudio.Component.SQL.LocalDB.Runtime | SQL Server Express 2016 LocalDB | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.SQL.SSDT | SQL Server Data Tools | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.TypeScript.3.3 | TypeScript 3.3 SDK | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.Wcf.Tooling | Windows Communication Foundation | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.Web | ASP.NET と Web の開発ツール | 16.0.28517.75 | Optional
Microsoft.VisualStudio.ComponentGroup.Web | ASP.NET と Web の開発ツールの前提条件 | 16.0.28621.142 | Optional
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | ASP.NET と Web 開発 | 16.0.28621.142 | Optional

## <a name="game-development-with-unity"></a>Unity でのゲーム開発

**ID:** Microsoft.VisualStudio.Workload.ManagedGame

**説明:** 強力なクロスプラットフォーム開発環境である Unity を使って、2D および 3D ゲームを作成します。

### <a name="components-included-by-this-workload"></a>このワークロードに含まれるコンポーネント

コンポーネント ID | name | Version | 依存関係の種類
--- | --- | --- | ---
Microsoft.Net.Component.3.5.DeveloperTools | .NET Framework 3.5 開発ツール | 16.0.28517.75 | 必須
Microsoft.Net.Component.4.7.1.TargetingPack | .NET Framework 4.7.1 Targeting Pack | 16.0.28517.75 | 必須
Microsoft.VisualStudio.Component.NuGet | NuGet パッケージ マネージャー | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# および Visual Basic Roslyn コンパイラ | 16.0.28714.129 | 必須
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# および Visual Basic | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.Unity | Visual Studio Tools for Unity | 16.0.28315.86 | 必須
Component.UnityEngine.x64 | Unity 2018.3 64 ビット エディター | 16.0.28707.178 | 推奨
Component.UnityEngine.x86 | Unity 5.6 32 ビット エディター | 16.0.28707.178 | 推奨

## <a name="linux-development-with-c"></a>C++ による Linux 開発

**ID:** Microsoft.VisualStudio.Workload.NativeCrossPlat

**説明:** Linux 環境で実行するアプリケーションを作成およびデバッグします。

### <a name="components-included-by-this-workload"></a>このワークロードに含まれるコンポーネント

コンポーネント ID | name | Version | 依存関係の種類
--- | --- | --- | ---
Component.MDD.Linux | Linux 開発用 C++ | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.VC.CoreIde | C++ コア機能 | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.Windows10SDK | Windows ユニバーサル C ランタイム | 16.0.28315.86 | 必須
Component.Linux.CMake | Linux 用の C++ CMake ツール | 16.0.28625.61 | 推奨
Microsoft.VisualStudio.Component.VC.Tools.x86.x64 | MSVC v142 – VS 2019 C++ x64/x86 ビルド ツール (v14.20) | 16.0.28625.61 | 推奨
Microsoft.VisualStudio.Component.Windows10SDK.17763 | Windows 10 SDK (10.0.17763.0) | 16.0.28517.75 | 推奨
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | ASP.NET と Web 開発 | 16.0.28621.142 | 推奨
Component.MDD.Linux.GCC.arm | 埋め込み開発ツールと IoT 開発ツール | 16.0.28625.61 | Optional

## <a name="desktop-development-with-c"></a>C++ によるデスクトップ開発

**ID:** Microsoft.VisualStudio.Workload.NativeDesktop

**説明:** Microsoft C++ ツールセット、ATL、MFC を使用して Windows のデスクトップ アプリケーションをビルドします。

### <a name="components-included-by-this-workload"></a>このワークロードに含まれるコンポーネント

コンポーネント ID | name | Version | 依存関係の種類
--- | --- | --- | ---
Microsoft.Component.MSBuild | MSBuild | 16.0.28517.75 | 必須
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# および Visual Basic Roslyn コンパイラ | 16.0.28714.129 | 必須
Microsoft.VisualStudio.Component.TextTemplating | テキスト テンプレート変換 | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.VC.CoreIde | C++ コア機能 | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.VC.Redist.14.Latest | C++ 2019 再頒布可能パッケージの更新プログラム | 16.0.28625.61 | 必須
Microsoft.VisualStudio.ComponentGroup.NativeDesktop.Core | Visual C++ コア デスクトップ機能 | 16.0.28315.86 | 必須
Component.Microsoft.VisualStudio.LiveShare | Live Share | 1.0.12 | 推奨
Microsoft.VisualStudio.Component.Debugger.JustInTime | Just-In-Time デバッガー | 16.0.28517.75 | 推奨
Microsoft.VisualStudio.Component.Graphics.Tools | DirectX 用グラフィックス デバッガーおよび GPU プロファイラー | 16.0.28625.61 | 推奨
Microsoft.VisualStudio.Component.NuGet | NuGet パッケージ マネージャー | 16.0.28625.61 | 推奨
Microsoft.VisualStudio.Component.VC.ATL | v142 ビルド ツールの C++ ATL (x86 & x64) | 16.0.28625.61 | 推奨
Microsoft.VisualStudio.Component.VC.CMake.Project | Windows 用 C++ CMake ツール | 16.0.28625.61 | 推奨
Microsoft.VisualStudio.Component.VC.DiagnosticTools | C++ のプロファイル ツール | 16.0.28625.61 | 推奨
Microsoft.VisualStudio.Component.VC.TestAdapterForBoostTest | Test Adapter for Boost.Test | 16.0.28517.75 | 推奨
Microsoft.VisualStudio.Component.VC.TestAdapterForGoogleTest | Test Adapter for Google Test | 16.0.28517.75 | 推奨
Microsoft.VisualStudio.Component.VC.Tools.x86.x64 | MSVC v142 – VS 2019 C++ x64/x86 ビルド ツール (v14.20) | 16.0.28625.61 | 推奨
Microsoft.VisualStudio.Component.Windows10SDK.17763 | Windows 10 SDK (10.0.17763.0) | 16.0.28517.75 | 推奨
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | ASP.NET と Web 開発 | 16.0.28621.142 | 推奨
Component.Incredibuild | IncrediBuild - ビルド アクセラレーション | 16.0.28528.71 | Optional
Component.IncredibuildMenu | IncrediBuildMenu | 1.5.0.3 | Optional
Microsoft.Component.VC.Runtime.UCRTSDK | Windows Universal CRT SDK | 16.0.28625.61 | Optional
Microsoft.Net.Component.4.6.1.SDK | .NET Framework 4.6.1 SDK | 16.0.28517.75 | Optional
Microsoft.Net.Component.4.6.1.TargetingPack | .NET Framework 4.6.1 Targeting Pack | 16.0.28517.75 | Optional
Microsoft.VisualStudio.Component.VC.140 | MSVC v140 - VS 2015 C++ ビルド ツール (v14.00) | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.VC.ATLMFC | v142 ビルド ツールの C++ MFC (x86 & x64) | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.VC.CLI.Support | v142 ビルド ツールの C++/CLI サポート | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.VC.Modules.x86.x64 | v142 ビルド ツール用の C++ モジュール (x64/x86 – 実験) | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.VC.v141.x86.x64 | MSVC v141 – VS 2017 C++ x64/x86 ビルド ツール (v14.16) | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.16299 | Windows 10 SDK (10.0.16299.0) | 16.0.28517.75 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.17134 | Windows 10 SDK (10.0.17134.0) | 16.0.28517.75 | Optional

## <a name="game-development-with-c"></a>C++ によるゲーム開発

**ID:** Microsoft.VisualStudio.Workload.NativeGame

**説明:** C++ を最大限に活用して、DirectX、Unreal、Cocos2d を利用するプロフェッショナルなゲームを構築します。

### <a name="components-included-by-this-workload"></a>このワークロードに含まれるコンポーネント

コンポーネント ID | name | Version | 依存関係の種類
--- | --- | --- | ---
Microsoft.VisualStudio.Component.VC.CoreIde | C++ コア機能 | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.VC.Redist.14.Latest | C++ 2019 再頒布可能パッケージの更新プログラム | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.VC.Tools.x86.x64 | MSVC v142 – VS 2019 C++ x64/x86 ビルド ツール (v14.20) | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.Windows10SDK | Windows ユニバーサル C ランタイム | 16.0.28315.86 | 必須
Microsoft.VisualStudio.Component.Graphics.Tools | DirectX 用グラフィックス デバッガーおよび GPU プロファイラー | 16.0.28625.61 | 推奨
Microsoft.VisualStudio.Component.VC.DiagnosticTools | C++ のプロファイル ツール | 16.0.28625.61 | 推奨
Microsoft.VisualStudio.Component.Windows10SDK.17763 | Windows 10 SDK (10.0.17763.0) | 16.0.28517.75 | 推奨
Component.Android.NDK.R16B | Android NDK (R16B) | 16.0.28728.38 | Optional
Component.Android.SDK25.Private | Android SDK セットアップ (API レベル 25) (C++ を使用したモバイル開発のためにローカルにインストール) | 16.0.28625.61 | Optional
Component.Ant | Apache Ant (1.9.3) | 1.9.3.8 | Optional
Component.Cocos | Cocos | 16.0.28315.86 | Optional
Component.Incredibuild | IncrediBuild - ビルド アクセラレーション | 16.0.28528.71 | Optional
Component.IncredibuildMenu | IncrediBuildMenu | 1.5.0.3 | Optional
Component.MDD.Android | C++ Android 開発ツール | 16.0.28517.75 | Optional
Component.OpenJDK | OpenJDK (Microsoft ディストリビューション) | 16.0.28625.61 | Optional
Component.Unreal | Unreal Engine のインストーラー | 16.0.28625.61 | Optional
Component.Unreal.Android | Unreal Engine 用の Android IDE サポート | 16.0.28625.61 | Optional
Microsoft.Net.Component.4.5.1.TargetingPack | .NET Framework 4.5.1 Targeting Pack | 16.0.28517.75 | Optional
Microsoft.Net.Component.4.5.2.TargetingPack | .NET Framework 4.5.2 Targeting Pack | 16.0.28517.75 | Optional
Microsoft.Net.Component.4.5.TargetingPack | .NET Framework 4.5 Targeting Pack | 16.0.28517.75 | Optional
Microsoft.Net.Component.4.6.2.TargetingPack | .NET Framework 4.6.2 Targeting Pack | 16.0.28517.75 | Optional
Microsoft.Net.Component.4.6.TargetingPack | .NET Framework 4.6 Targeting Pack | 16.0.28517.75 | Optional
Microsoft.Net.Component.4.7.2.SDK | .NET Framework 4.7.2 SDK | 16.0.28517.75 | Optional
Microsoft.Net.Component.4.7.2.TargetingPack | .NET Framework 4.7.2 Targeting Pack | 16.0.28517.75 | Optional
Microsoft.Net.Component.4.TargetingPack | .NET Framework 4 Targeting Pack | 16.0.28517.75 | Optional
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | .NET Framework 4.7.2 開発ツール | 16.0.28516.191 | Optional
Microsoft.Net.ComponentGroup.TargetingPacks.Common | .NET Framework 4 – 4.6 開発ツール | 16.0.28516.191 | Optional
Microsoft.VisualStudio.Component.NuGet.BuildTools | NuGet ターゲットとビルド タスク | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# および Visual Basic Roslyn コンパイラ | 16.0.28714.129 | Optional
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# および Visual Basic | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.16299 | Windows 10 SDK (10.0.16299.0) | 16.0.28517.75 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.17134 | Windows 10 SDK (10.0.17134.0) | 16.0.28517.75 | Optional

## <a name="mobile-development-with-c"></a>C++ でのモバイル開発

**ID:** Microsoft.VisualStudio.Workload.NativeMobile

**説明:** iOS、Android、Windows 向けのクロスプラットフォーム アプリケーションを、C++ を使って構築します。

### <a name="components-included-by-this-workload"></a>このワークロードに含まれるコンポーネント

コンポーネント ID | name | Version | 依存関係の種類
--- | --- | --- | ---
Component.Android.SDK25.Private | Android SDK セットアップ (API レベル 25) (C++ を使用したモバイル開発のためにローカルにインストール) | 16.0.28625.61 | 必須
Component.OpenJDK | OpenJDK (Microsoft ディストリビューション) | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.VC.CoreIde | C++ コア機能 | 16.0.28625.61 | 必須
Component.Android.NDK.R16B | Android NDK (R16B) | 16.0.28728.38 | 推奨
Component.Ant | Apache Ant (1.9.3) | 1.9.3.8 | 推奨
Component.MDD.Android | C++ Android 開発ツール | 16.0.28517.75 | 推奨
Component.Android.NDK.R16B_3264 | Android NDK (R16B) (32 ビット) | 16.0.28728.38 | Optional
Component.Google.Android.Emulator.API25.Private | Google Android Emulator (API レベル 25) (ローカル インストール) | 16.0.28625.61 | Optional
Component.HAXM.Private | Intel Hardware Accelerated Execution Manager (HAXM) (ローカル インストール) | 16.0.28528.71 | Optional
Component.Incredibuild | IncrediBuild - ビルド アクセラレーション | 16.0.28528.71 | Optional
Component.IncredibuildMenu | IncrediBuildMenu | 1.5.0.3 | Optional
Component.MDD.IOS | C++ iOS 開発ツール | 16.0.28517.75 | Optional

## <a name="net-core-cross-platform-development"></a>.NET Core クロスプラットフォームの開発

**ID:** Microsoft.VisualStudio.Workload.NetCoreTools

**説明:**.NET Core、ASP.NET Core、HTML/JavaScript、コンテナー (Docker サポートなど) を使用して、クロスプラットフォーム アプリケーションをビルドします。

### <a name="components-included-by-this-workload"></a>このワークロードに含まれるコンポーネント

コンポーネント ID | name | Version | 依存関係の種類
--- | --- | --- | ---
Component.Microsoft.VisualStudio.RazorExtension | Razor 言語サービス | 16.0.28714.129 | 必須
Component.Microsoft.Web.LibraryManager | ライブラリ マネージャー | 16.0.28315.86 | 必須
Microsoft.Component.MSBuild | MSBuild | 16.0.28517.75 | 必須
Microsoft.Net.Component.4.5.2.TargetingPack | .NET Framework 4.5.2 Targeting Pack | 16.0.28517.75 | 必須
Microsoft.Net.Component.4.5.TargetingPack | .NET Framework 4.5 Targeting Pack | 16.0.28517.75 | 必須
Microsoft.Net.Component.4.6.1.TargetingPack | .NET Framework 4.6.1 Targeting Pack | 16.0.28517.75 | 必須
Microsoft.Net.Component.4.7.2.SDK | .NET Framework 4.7.2 SDK | 16.0.28517.75 | 必須
Microsoft.Net.Component.4.7.2.TargetingPack | .NET Framework 4.7.2 Targeting Pack | 16.0.28517.75 | 必須
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | .NET Framework 4.7.2 開発ツール | 16.0.28516.191 | 必須
Microsoft.Net.Core.Component.SDK.2.1 | .NET Core 2.1 開発ツール | 16.0.28621.142 | 必須
Microsoft.NetCore.ComponentGroup.DevelopmentTools.2.1 | .NET Core 2.1 開発ツール | 16.0.28516.191 | 必須
Microsoft.NetCore.ComponentGroup.Web.2.1 | .NET Core 2.1 開発ツール | 16.0.28621.142 | 必須
Microsoft.VisualStudio.Component.Common.Azure.Tools | 接続および発行ツール | 16.0.28315.86 | 必須
Microsoft.VisualStudio.Component.DockerTools | コンテナー開発ツール | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.FSharp | F# 言語サポート | 16.0.28315.86 | 必須
Microsoft.VisualStudio.Component.FSharp.WebTemplates | Web プロジェクト用の F# 言語サポート | 16.0.28517.75 | 必須
Microsoft.VisualStudio.Component.IISExpress | IIS Express  | 16.0.28315.86 | 必須
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | JavaScript 診断 | 16.0.28517.75 | 必須
Microsoft.VisualStudio.Component.JavaScript.TypeScript | JavaScript および TypeScript の言語サポート | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.ManagedDesktop.Core | Managed Desktop Workload コア | 16.0.28621.142 | 必須
Microsoft.VisualStudio.Component.MSODBC.SQL | SQL Server ODBC Driver | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.MSSQL.CMDLnUtils | SQL Server コマンド ライン ユーティリティ | 16.0.28707.177 | 必須
Microsoft.VisualStudio.Component.NuGet | NuGet パッケージ マネージャー | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# および Visual Basic Roslyn コンパイラ | 16.0.28714.129 | 必須
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# および Visual Basic | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.SQL.ADAL | SQL ADAL ランタイム | 16.0.28517.75 | 必須
Microsoft.VisualStudio.Component.SQL.CLR | SQL Server の CLR データ型 | 16.0.28315.86 | 必須
Microsoft.VisualStudio.Component.SQL.DataSources | SQL Server サポートのためのデータ ソース | 16.0.28315.86 | 必須
Microsoft.VisualStudio.Component.SQL.LocalDB.Runtime | SQL Server Express 2016 LocalDB | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.SQL.SSDT | SQL Server Data Tools | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.TextTemplating | テキスト テンプレート変換 | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.TypeScript.3.3 | TypeScript 3.3 SDK | 16.0.28625.61 | 必須
Microsoft.VisualStudio.ComponentGroup.Web | ASP.NET と Web の開発ツールの前提条件 | 16.0.28621.142 | 必須
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | ASP.NET と Web 開発 | 16.0.28621.142 | 必須
Component.Microsoft.VisualStudio.LiveShare | Live Share | 1.0.12 | 推奨
Component.Microsoft.VisualStudio.Web.AzureFunctions | Azure WebJobs ツール | 16.0.28714.129 | 推奨
Microsoft.VisualStudio.Component.AppInsights.Tools | Developer Analytics Tools | 16.0.28625.61 | 推奨
Microsoft.VisualStudio.Component.Azure.AuthoringTools | Azure Authoring Tools | 16.0.28625.61 | 推奨
Microsoft.VisualStudio.Component.Azure.ClientLibs | .NET 用 Azure ライブラリ | 16.0.28315.86 | 推奨
Microsoft.VisualStudio.Component.Azure.Compute.Emulator | Azure コンピューティング エミュレーター | 16.0.28720.110 | 推奨
Microsoft.VisualStudio.Component.Azure.Storage.Emulator | Azure Storage エミュレーター | 16.0.28517.75 | 推奨
Microsoft.VisualStudio.Component.CloudExplorer | Cloud Explorer | 16.0.28625.61 | 推奨
Microsoft.VisualStudio.Component.DiagnosticTools | .NET プロファイル ツール | 16.0.28625.61 | 推奨
Microsoft.VisualStudio.Component.Web | ASP.NET と Web の開発ツール | 16.0.28517.75 | 推奨
Microsoft.VisualStudio.Component.WebDeploy | Web 配置 | 16.0.28517.75 | 推奨
Microsoft.VisualStudio.ComponentGroup.AzureFunctions | Azure WebJobs ツール | 16.0.28621.142 | 推奨
Microsoft.VisualStudio.ComponentGroup.Web.CloudTools | Web 開発用クラウド ツール | 16.0.28621.142 | 推奨
Microsoft.Net.Core.Component.SDK.2.2 | .NET Core 2.2 開発ツール | 16.0.28621.142 | Optional
Microsoft.NetCore.ComponentGroup.DevelopmentTools.2.2 | .NET Core 2.2 開発ツール | 16.0.28516.191 | Optional
Microsoft.NetCore.ComponentGroup.Web.2.2 | .NET Core 2.2 開発ツール | 16.0.28621.142 | Optional
Microsoft.VisualStudio.ComponentGroup.IISDevelopment | 開発時の IIS サポート | 16.0.28315.86 | Optional

## <a name="mobile-development-with-net"></a>.NET によるモバイル開発

**ID:** Microsoft.VisualStudio.Workload.NetCrossPlat

**説明:** iOS、Android、Windows 向けのクロスプラットフォーム アプリケーションを、Xamarin を使って構築します。

### <a name="components-included-by-this-workload"></a>このワークロードに含まれるコンポーネント

コンポーネント ID | name | Version | 依存関係の種類
--- | --- | --- | ---
Component.Xamarin | Xamarin | 16.0.28625.61 | 必須
Component.Xamarin.RemotedSimulator | Xamarin Remoted Simulator | 16.0.28315.86 | 必須
Microsoft.Component.MSBuild | MSBuild | 16.0.28517.75 | 必須
Microsoft.Net.Component.4.6.1.TargetingPack | .NET Framework 4.6.1 Targeting Pack | 16.0.28517.75 | 必須
Microsoft.Net.Component.4.7.2.SDK | .NET Framework 4.7.2 SDK | 16.0.28517.75 | 必須
Microsoft.Net.Component.4.7.2.TargetingPack | .NET Framework 4.7.2 Targeting Pack | 16.0.28517.75 | 必須
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | .NET Framework 4.7.2 開発ツール | 16.0.28516.191 | 必須
Microsoft.Net.Core.Component.SDK.2.1 | .NET Core 2.1 開発ツール | 16.0.28621.142 | 必須
Microsoft.NetCore.ComponentGroup.DevelopmentTools.2.1 | .NET Core 2.1 開発ツール | 16.0.28516.191 | 必須
Microsoft.VisualStudio.Component.FSharp | F# 言語サポート | 16.0.28315.86 | 必須
Microsoft.VisualStudio.Component.Merq | Xamarin の一般的な内部ツール | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.MonoDebugger | Mono デバッガー | 16.0.28517.75 | 必須
Microsoft.VisualStudio.Component.NuGet | NuGet パッケージ マネージャー | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# および Visual Basic Roslyn コンパイラ | 16.0.28714.129 | 必須
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# および Visual Basic | 16.0.28625.61 | 必須
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions.TemplateEngine | ASP.NET テンプレート エンジン | 16.0.28315.86 | 必須
Component.Android.SDK27 | Android SDK セットアップ (API レベル 27) | 16.0.28517.75 | 推奨
Component.OpenJDK | OpenJDK (Microsoft ディストリビューション) | 16.0.28625.61 | 推奨

## <a name="aspnet-and-web-development"></a>ASP.NET と Web 開発

**ID:** Microsoft.VisualStudio.Workload.NetWeb

**説明:** ASP.NET、ASP.NET Core、HTML/JavaScript、コンテナー (Docker サポートなど) を使用して、Web アプリケーションをビルドします。

### <a name="components-included-by-this-workload"></a>このワークロードに含まれるコンポーネント

コンポーネント ID | name | Version | 依存関係の種類
--- | --- | --- | ---
Component.Microsoft.VisualStudio.RazorExtension | Razor 言語サービス | 16.0.28714.129 | 必須
Component.Microsoft.Web.LibraryManager | ライブラリ マネージャー | 16.0.28315.86 | 必須
Microsoft.Component.MSBuild | MSBuild | 16.0.28517.75 | 必須
Microsoft.Net.Component.4.5.2.TargetingPack | .NET Framework 4.5.2 Targeting Pack | 16.0.28517.75 | 必須
Microsoft.Net.Component.4.5.TargetingPack | .NET Framework 4.5 Targeting Pack | 16.0.28517.75 | 必須
Microsoft.Net.Component.4.6.1.TargetingPack | .NET Framework 4.6.1 Targeting Pack | 16.0.28517.75 | 必須
Microsoft.Net.Component.4.7.2.SDK | .NET Framework 4.7.2 SDK | 16.0.28517.75 | 必須
Microsoft.Net.Component.4.7.2.TargetingPack | .NET Framework 4.7.2 Targeting Pack | 16.0.28517.75 | 必須
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | .NET Framework 4.7.2 開発ツール | 16.0.28516.191 | 必須
Microsoft.Net.Core.Component.SDK.2.1 | .NET Core 2.1 開発ツール | 16.0.28621.142 | 必須
Microsoft.NetCore.ComponentGroup.DevelopmentTools.2.1 | .NET Core 2.1 開発ツール | 16.0.28516.191 | 必須
Microsoft.NetCore.ComponentGroup.Web.2.1 | .NET Core 2.1 開発ツール | 16.0.28621.142 | 必須
Microsoft.VisualStudio.Component.Common.Azure.Tools | 接続および発行ツール | 16.0.28315.86 | 必須
Microsoft.VisualStudio.Component.DockerTools | コンテナー開発ツール | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.FSharp | F# 言語サポート | 16.0.28315.86 | 必須
Microsoft.VisualStudio.Component.FSharp.WebTemplates | Web プロジェクト用の F# 言語サポート | 16.0.28517.75 | 必須
Microsoft.VisualStudio.Component.IISExpress | IIS Express  | 16.0.28315.86 | 必須
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | JavaScript 診断 | 16.0.28517.75 | 必須
Microsoft.VisualStudio.Component.JavaScript.TypeScript | JavaScript および TypeScript の言語サポート | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.ManagedDesktop.Core | Managed Desktop Workload コア | 16.0.28621.142 | 必須
Microsoft.VisualStudio.Component.MSODBC.SQL | SQL Server ODBC Driver | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.MSSQL.CMDLnUtils | SQL Server コマンド ライン ユーティリティ | 16.0.28707.177 | 必須
Microsoft.VisualStudio.Component.NuGet | NuGet パッケージ マネージャー | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# および Visual Basic Roslyn コンパイラ | 16.0.28714.129 | 必須
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# および Visual Basic | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.SQL.ADAL | SQL ADAL ランタイム | 16.0.28517.75 | 必須
Microsoft.VisualStudio.Component.SQL.CLR | SQL Server の CLR データ型 | 16.0.28315.86 | 必須
Microsoft.VisualStudio.Component.SQL.DataSources | SQL Server サポートのためのデータ ソース | 16.0.28315.86 | 必須
Microsoft.VisualStudio.Component.SQL.LocalDB.Runtime | SQL Server Express 2016 LocalDB | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.SQL.SSDT | SQL Server Data Tools | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.TextTemplating | テキスト テンプレート変換 | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.TypeScript.3.3 | TypeScript 3.3 SDK | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.Web | ASP.NET と Web の開発ツール | 16.0.28517.75 | 必須
Microsoft.VisualStudio.ComponentGroup.Web | ASP.NET と Web の開発ツールの前提条件 | 16.0.28621.142 | 必須
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | ASP.NET と Web 開発 | 16.0.28621.142 | 必須
Component.Microsoft.VisualStudio.LiveShare | Live Share | 1.0.12 | 推奨
Component.Microsoft.VisualStudio.Web.AzureFunctions | Azure WebJobs ツール | 16.0.28714.129 | 推奨
Microsoft.Net.Component.4.5.1.TargetingPack | .NET Framework 4.5.1 Targeting Pack | 16.0.28517.75 | 推奨
Microsoft.Net.Component.4.6.TargetingPack | .NET Framework 4.6 Targeting Pack | 16.0.28517.75 | 推奨
Microsoft.Net.Component.4.TargetingPack | .NET Framework 4 Targeting Pack | 16.0.28517.75 | 推奨
Microsoft.Net.ComponentGroup.TargetingPacks.Common | .NET Framework 4 – 4.6 開発ツール | 16.0.28516.191 | 推奨
Microsoft.VisualStudio.Component.AppInsights.Tools | Developer Analytics Tools | 16.0.28625.61 | 推奨
Microsoft.VisualStudio.Component.AspNet45 | 高度な ASP.NET 機能 | 16.0.28315.86 | 推奨
Microsoft.VisualStudio.Component.Azure.AuthoringTools | Azure Authoring Tools | 16.0.28625.61 | 推奨
Microsoft.VisualStudio.Component.Azure.ClientLibs | .NET 用 Azure ライブラリ | 16.0.28315.86 | 推奨
Microsoft.VisualStudio.Component.Azure.Compute.Emulator | Azure コンピューティング エミュレーター | 16.0.28720.110 | 推奨
Microsoft.VisualStudio.Component.Azure.Storage.Emulator | Azure Storage エミュレーター | 16.0.28517.75 | 推奨
Microsoft.VisualStudio.Component.CloudExplorer | Cloud Explorer | 16.0.28625.61 | 推奨
Microsoft.VisualStudio.Component.DiagnosticTools | .NET プロファイル ツール | 16.0.28625.61 | 推奨
Microsoft.VisualStudio.Component.EntityFramework | Entity Framework 6 Tools | 16.0.28315.86 | 推奨
Microsoft.VisualStudio.Component.WebDeploy | Web 配置 | 16.0.28517.75 | 推奨
Microsoft.VisualStudio.ComponentGroup.AzureFunctions | Azure WebJobs ツール | 16.0.28621.142 | 推奨
Microsoft.VisualStudio.ComponentGroup.Web.CloudTools | Web 開発用クラウド ツール | 16.0.28621.142 | 推奨
Microsoft.Net.Component.4.6.1.SDK | .NET Framework 4.6.1 SDK | 16.0.28517.75 | Optional
Microsoft.Net.Component.4.6.2.SDK | .NET Framework 4.6.2 SDK | 16.0.28517.75 | Optional
Microsoft.Net.Component.4.6.2.TargetingPack | .NET Framework 4.6.2 Targeting Pack | 16.0.28517.75 | Optional
Microsoft.Net.Component.4.7.1.SDK | .NET Framework 4.7.1 SDK | 16.0.28517.75 | Optional
Microsoft.Net.Component.4.7.1.TargetingPack | .NET Framework 4.7.1 Targeting Pack | 16.0.28517.75 | Optional
Microsoft.Net.Component.4.7.SDK | .NET Framework 4.7 SDK | 16.0.28517.75 | Optional
Microsoft.Net.Component.4.7.TargetingPack | .NET Framework 4.7 Targeting Pack | 16.0.28517.75 | Optional
Microsoft.Net.ComponentGroup.4.6.1.DeveloperTools | .NET Framework 4.6.1 開発ツール | 16.0.28621.142 | Optional
Microsoft.Net.ComponentGroup.4.6.2.DeveloperTools | .NET Framework 4.6.2 開発ツール | 16.0.28516.191 | Optional
Microsoft.Net.ComponentGroup.4.7.1.DeveloperTools | .NET Framework 4.7.1 開発ツール | 16.0.28516.191 | Optional
Microsoft.Net.ComponentGroup.4.7.DeveloperTools | .NET Framework 4.7 開発ツール | 16.0.28516.191 | Optional
Microsoft.Net.Core.Component.SDK.2.2 | .NET Core 2.2 開発ツール | 16.0.28621.142 | Optional
Microsoft.NetCore.ComponentGroup.DevelopmentTools.2.2 | .NET Core 2.2 開発ツール | 16.0.28516.191 | Optional
Microsoft.NetCore.ComponentGroup.Web.2.2 | .NET Core 2.2 開発ツール | 16.0.28621.142 | Optional
Microsoft.VisualStudio.Component.Wcf.Tooling | Windows Communication Foundation | 16.0.28625.61 | Optional
Microsoft.VisualStudio.ComponentGroup.AdditionalWebProjectTemplates | 追加のプロジェクト テンプレート (以前のバージョン) | 16.0.28621.142 | Optional
Microsoft.VisualStudio.ComponentGroup.IISDevelopment | 開発時の IIS サポート | 16.0.28315.86 | Optional

## <a name="nodejs-development"></a>Node.js 開発

**ID:** Microsoft.VisualStudio.Workload.Node

**説明:** Node.js (非同期、イベント ドリブン JavaScript ランタイム) を使用してスケーラブルなネットワーク アプリケーションをビルドします。 

### <a name="components-included-by-this-workload"></a>このワークロードに含まれるコンポーネント

コンポーネント ID | name | Version | 依存関係の種類
--- | --- | --- | ---
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | JavaScript 診断 | 16.0.28517.75 | 必須
Microsoft.VisualStudio.Component.JavaScript.TypeScript | JavaScript および TypeScript の言語サポート | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.Node.Tools | Node.js 開発ツール | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.TypeScript.3.3 | TypeScript 3.3 SDK | 16.0.28625.61 | 必須
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | ASP.NET と Web 開発 | 16.0.28621.142 | 必須
Component.Microsoft.VisualStudio.LiveShare | Live Share | 1.0.12 | 推奨
Microsoft.VisualStudio.Component.WebDeploy | Web 配置 | 16.0.28517.75 | 推奨
Microsoft.VisualStudio.Component.AppInsights.Tools | Developer Analytics Tools | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.Common.Azure.Tools | 接続および発行ツール | 16.0.28315.86 | Optional
Microsoft.VisualStudio.Component.VC.CoreIde | C++ コア機能 | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.VC.Tools.x86.x64 | MSVC v142 – VS 2019 C++ x64/x86 ビルド ツール (v14.20) | 16.0.28625.61 | Optional

## <a name="officesharepoint-development"></a>Office/SharePoint 開発

**ID:** Microsoft.VisualStudio.Workload.Office

**説明:** C#、VB、JavaScript を使用して、Office アドイン、SharePoint アドイン、SharePoint ソリューション、VSTO アドインを作成します。

### <a name="components-included-by-this-workload"></a>このワークロードに含まれるコンポーネント

コンポーネント ID | name | Version | 依存関係の種類
--- | --- | --- | ---
Component.Microsoft.VisualStudio.RazorExtension | Razor 言語サービス | 16.0.28714.129 | 必須
Component.Microsoft.Web.LibraryManager | ライブラリ マネージャー | 16.0.28315.86 | 必須
Microsoft.Component.MSBuild | MSBuild | 16.0.28517.75 | 必須
Microsoft.Net.Component.4.5.2.TargetingPack | .NET Framework 4.5.2 Targeting Pack | 16.0.28517.75 | 必須
Microsoft.Net.Component.4.5.TargetingPack | .NET Framework 4.5 Targeting Pack | 16.0.28517.75 | 必須
Microsoft.Net.Component.4.6.1.TargetingPack | .NET Framework 4.6.1 Targeting Pack | 16.0.28517.75 | 必須
Microsoft.Net.Component.4.7.2.SDK | .NET Framework 4.7.2 SDK | 16.0.28517.75 | 必須
Microsoft.Net.Component.4.7.2.TargetingPack | .NET Framework 4.7.2 Targeting Pack | 16.0.28517.75 | 必須
Microsoft.Net.Component.4.TargetingPack | .NET Framework 4 Targeting Pack | 16.0.28517.75 | 必須
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | .NET Framework 4.7.2 開発ツール | 16.0.28516.191 | 必須
Microsoft.Net.Core.Component.SDK.2.1 | .NET Core 2.1 開発ツール | 16.0.28621.142 | 必須
Microsoft.VisualStudio.Component.AppInsights.Tools | Developer Analytics Tools | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.Common.Azure.Tools | 接続および発行ツール | 16.0.28315.86 | 必須
Microsoft.VisualStudio.Component.DockerTools | コンテナー開発ツール | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.IISExpress | IIS Express  | 16.0.28315.86 | 必須
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | JavaScript 診断 | 16.0.28517.75 | 必須
Microsoft.VisualStudio.Component.JavaScript.TypeScript | JavaScript および TypeScript の言語サポート | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.ManagedDesktop.Core | Managed Desktop Workload コア | 16.0.28621.142 | 必須
Microsoft.VisualStudio.Component.ManagedDesktop.Prerequisites | .NET デスクトップ開発ツール | 16.0.28621.142 | 必須
Microsoft.VisualStudio.Component.MSODBC.SQL | SQL Server ODBC Driver | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.MSSQL.CMDLnUtils | SQL Server コマンド ライン ユーティリティ | 16.0.28707.177 | 必須
Microsoft.VisualStudio.Component.NuGet | NuGet パッケージ マネージャー | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# および Visual Basic Roslyn コンパイラ | 16.0.28714.129 | 必須
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# および Visual Basic | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.Sharepoint.Tools | Office Developer Tools for Visual Studio | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.SQL.ADAL | SQL ADAL ランタイム | 16.0.28517.75 | 必須
Microsoft.VisualStudio.Component.SQL.CLR | SQL Server の CLR データ型 | 16.0.28315.86 | 必須
Microsoft.VisualStudio.Component.SQL.DataSources | SQL Server サポートのためのデータ ソース | 16.0.28315.86 | 必須
Microsoft.VisualStudio.Component.SQL.LocalDB.Runtime | SQL Server Express 2016 LocalDB | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.SQL.SSDT | SQL Server Data Tools | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.TextTemplating | テキスト テンプレート変換 | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.TypeScript.3.3 | TypeScript 3.3 SDK | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.Wcf.Tooling | Windows Communication Foundation | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.Web | ASP.NET と Web の開発ツール | 16.0.28517.75 | 必須
Microsoft.VisualStudio.Component.Workflow | Windows Workflow Foundation | 16.0.28315.86 | 必須
Microsoft.VisualStudio.ComponentGroup.Web | ASP.NET と Web の開発ツールの前提条件 | 16.0.28621.142 | 必須
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | ASP.NET と Web 開発 | 16.0.28621.142 | 必須
Microsoft.VisualStudio.Component.TeamOffice | Visual Studio Tools for Office (VSTO) | 16.0.28625.61 | 推奨
Microsoft.VisualStudio.Component.WebDeploy | Web 配置 | 16.0.28517.75 | 推奨
Microsoft.Net.Component.4.6.1.SDK | .NET Framework 4.6.1 SDK | 16.0.28517.75 | Optional
Microsoft.Net.Component.4.6.2.SDK | .NET Framework 4.6.2 SDK | 16.0.28517.75 | Optional
Microsoft.Net.Component.4.6.2.TargetingPack | .NET Framework 4.6.2 Targeting Pack | 16.0.28517.75 | Optional
Microsoft.Net.Component.4.7.1.SDK | .NET Framework 4.7.1 SDK | 16.0.28517.75 | Optional
Microsoft.Net.Component.4.7.1.TargetingPack | .NET Framework 4.7.1 Targeting Pack | 16.0.28517.75 | Optional
Microsoft.Net.Component.4.7.SDK | .NET Framework 4.7 SDK | 16.0.28517.75 | Optional
Microsoft.Net.Component.4.7.TargetingPack | .NET Framework 4.7 Targeting Pack | 16.0.28517.75 | Optional
Microsoft.Net.ComponentGroup.4.6.1.DeveloperTools | .NET Framework 4.6.1 開発ツール | 16.0.28621.142 | Optional
Microsoft.Net.ComponentGroup.4.6.2.DeveloperTools | .NET Framework 4.6.2 開発ツール | 16.0.28516.191 | Optional
Microsoft.Net.ComponentGroup.4.7.1.DeveloperTools | .NET Framework 4.7.1 開発ツール | 16.0.28516.191 | Optional
Microsoft.Net.ComponentGroup.4.7.DeveloperTools | .NET Framework 4.7 開発ツール | 16.0.28516.191 | Optional
Microsoft.VisualStudio.ComponentGroup.Sharepoint.WIF | Windows Identity Foundation 3.5 | 16.0.28621.142 | Optional

## <a name="python-development"></a>Python 開発

**ID:** Microsoft.VisualStudio.Workload.Python

**説明:** Python の編集、デバッグ、対話型開発、ソース管理。

### <a name="components-included-by-this-workload"></a>このワークロードに含まれるコンポーネント

コンポーネント ID | name | Version | 依存関係の種類
--- | --- | --- | ---
Microsoft.Component.PythonTools | Python 言語サポート | 16.0.28625.61 | 必須
Component.CPython3.x64 | Python 3 64 ビット (3.7.2) | 3.7.2 | 推奨
Component.Microsoft.VisualStudio.LiveShare | Live Share | 1.0.12 | 推奨
Microsoft.Component.PythonTools.Minicondax64 | Python miniconda | 16.0.28625.61 | 推奨
Microsoft.Component.PythonTools.Web | Python Web サポート | 16.0.28517.75 | 推奨
Microsoft.VisualStudio.Component.Common.Azure.Tools | 接続および発行ツール | 16.0.28315.86 | 推奨
Microsoft.VisualStudio.Component.JavaScript.TypeScript | JavaScript および TypeScript の言語サポート | 16.0.28625.61 | 推奨
Microsoft.VisualStudio.Component.TypeScript.3.3 | TypeScript 3.3 SDK | 16.0.28625.61 | 推奨
Microsoft.VisualStudio.Component.WebDeploy | Web 配置 | 16.0.28517.75 | 推奨
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | ASP.NET と Web 開発 | 16.0.28621.142 | 推奨
Component.CPython2.x64 | Python 2 64 ビット (2.7.15) | 2.7.15 | Optional
Component.CPython2.x86 | Python 2 32 ビット (2.7.15) | 2.7.15 | Optional
Component.CPython3.x86 | Python 3 32 ビット (3.7.2) | 3.7.2 | Optional
Component.Microsoft.VisualStudio.RazorExtension | Razor 言語サービス | 16.0.28714.129 | Optional
Component.Microsoft.Web.LibraryManager | ライブラリ マネージャー | 16.0.28315.86 | Optional
Microsoft.Component.MSBuild | MSBuild | 16.0.28517.75 | Optional
Microsoft.Component.VC.Runtime.UCRTSDK | Windows Universal CRT SDK | 16.0.28625.61 | Optional
Microsoft.ComponentGroup.PythonTools.NativeDevelopment | Python ネイティブ開発ツール | 16.0.28621.142 | Optional
Microsoft.Net.Component.4.5.2.TargetingPack | .NET Framework 4.5.2 Targeting Pack | 16.0.28517.75 | Optional
Microsoft.Net.Component.4.5.TargetingPack | .NET Framework 4.5 Targeting Pack | 16.0.28517.75 | Optional
Microsoft.Net.Component.4.7.2.SDK | .NET Framework 4.7.2 SDK | 16.0.28517.75 | Optional
Microsoft.Net.Component.4.7.2.TargetingPack | .NET Framework 4.7.2 Targeting Pack | 16.0.28517.75 | Optional
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | .NET Framework 4.7.2 開発ツール | 16.0.28516.191 | Optional
Microsoft.Net.Core.Component.SDK.2.1 | .NET Core 2.1 開発ツール | 16.0.28621.142 | Optional
Microsoft.VisualStudio.Component.Azure.AuthoringTools | Azure Authoring Tools | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.Azure.ClientLibs | .NET 用 Azure ライブラリ | 16.0.28315.86 | Optional
Microsoft.VisualStudio.Component.Azure.Compute.Emulator | Azure コンピューティング エミュレーター | 16.0.28720.110 | Optional
Microsoft.VisualStudio.Component.Azure.Storage.Emulator | Azure Storage エミュレーター | 16.0.28517.75 | Optional
Microsoft.VisualStudio.Component.Azure.Waverton | Azure Cloud Services コア ツール | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.Azure.Waverton.BuildTools | Azure Cloud Services ビルド ツール | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.DockerTools | コンテナー開発ツール | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.Graphics.Tools | DirectX 用グラフィックス デバッガーおよび GPU プロファイラー | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.IISExpress | IIS Express  | 16.0.28315.86 | Optional
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | JavaScript 診断 | 16.0.28517.75 | Optional
Microsoft.VisualStudio.Component.ManagedDesktop.Core | Managed Desktop Workload コア | 16.0.28621.142 | Optional
Microsoft.VisualStudio.Component.MSODBC.SQL | SQL Server ODBC Driver | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.MSSQL.CMDLnUtils | SQL Server コマンド ライン ユーティリティ | 16.0.28707.177 | Optional
Microsoft.VisualStudio.Component.NuGet | NuGet パッケージ マネージャー | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# および Visual Basic Roslyn コンパイラ | 16.0.28714.129 | Optional
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# および Visual Basic | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.SQL.ADAL | SQL ADAL ランタイム | 16.0.28517.75 | Optional
Microsoft.VisualStudio.Component.SQL.CLR | SQL Server の CLR データ型 | 16.0.28315.86 | Optional
Microsoft.VisualStudio.Component.SQL.DataSources | SQL Server サポートのためのデータ ソース | 16.0.28315.86 | Optional
Microsoft.VisualStudio.Component.SQL.LocalDB.Runtime | SQL Server Express 2016 LocalDB | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.SQL.SSDT | SQL Server Data Tools | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.TextTemplating | テキスト テンプレート変換 | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.VC.140 | MSVC v140 - VS 2015 C++ ビルド ツール (v14.00) | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.VC.CoreIde | C++ コア機能 | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.VC.DiagnosticTools | C++ のプロファイル ツール | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.VC.Tools.x86.x64 | MSVC v142 – VS 2019 C++ x64/x86 ビルド ツール (v14.20) | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.Web | ASP.NET と Web の開発ツール | 16.0.28517.75 | Optional
Microsoft.VisualStudio.Component.Windows10SDK | Windows ユニバーサル C ランタイム | 16.0.28315.86 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.17763 | Windows 10 SDK (10.0.17763.0) | 16.0.28517.75 | Optional
Microsoft.VisualStudio.ComponentGroup.Web | ASP.NET と Web の開発ツールの前提条件 | 16.0.28621.142 | Optional

## <a name="universal-windows-platform-development"></a>ユニバーサル Windows プラットフォーム開発

**ID:** Microsoft.VisualStudio.Workload.Universal

**説明:** C#、VB、または C++ (オプション) を使ってユニバーサル Windows プラットフォームのアプリケーションを作成します。

### <a name="components-included-by-this-workload"></a>このワークロードに含まれるコンポーネント

コンポーネント ID | name | Version | 依存関係の種類
--- | --- | --- | ---
Microsoft.Component.NetFX.Native | .NET Native | 16.0.28315.86 | 必須
Microsoft.ComponentGroup.Blend | Blend for Visual Studio | 16.0.28315.86 | 必須
Microsoft.Net.Component.4.5.TargetingPack | .NET Framework 4.5 Targeting Pack | 16.0.28517.75 | 必須
Microsoft.Net.Component.4.6.1.SDK | .NET Framework 4.6.1 SDK | 16.0.28517.75 | 必須
Microsoft.Net.Core.Component.SDK.2.1 | .NET Core 2.1 開発ツール | 16.0.28621.142 | 必須
Microsoft.VisualStudio.Component.AppInsights.Tools | Developer Analytics Tools | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.DiagnosticTools | .NET プロファイル ツール | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.Graphics | イメージ エディターと 3D モデル エディター | 16.0.28517.75 | 必須
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | JavaScript 診断 | 16.0.28517.75 | 必須
Microsoft.VisualStudio.Component.JavaScript.TypeScript | JavaScript および TypeScript の言語サポート | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.NuGet | NuGet パッケージ マネージャー | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# および Visual Basic Roslyn コンパイラ | 16.0.28714.129 | 必須
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# および Visual Basic | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.SQL.CLR | SQL Server の CLR データ型 | 16.0.28315.86 | 必須
Microsoft.VisualStudio.Component.TypeScript.3.3 | TypeScript 3.3 SDK | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.Windows10SDK.17763 | Windows 10 SDK (10.0.17763.0) | 16.0.28517.75 | 必須
Microsoft.VisualStudio.ComponentGroup.UWP.NetCoreAndStandard | .NET ネイティブと .NET Standard | 16.0.28516.191 | 必須
Microsoft.VisualStudio.ComponentGroup.UWP.Support | ユニバーサル Windows プラットフォーム ツール | 16.0.28621.142 | 必須
Microsoft.VisualStudio.ComponentGroup.UWP.Xamarin | Xamarin 用ユニバーサル Windows プラットフォーム ツール | 16.0.28621.142 | 必須
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | ASP.NET と Web 開発 | 16.0.28621.142 | 必須
Microsoft.Component.MSBuild | MSBuild | 16.0.28517.75 | Optional
Microsoft.Component.VC.Runtime.OSSupport | v142 ビルド ツールの C++ ユニバーサル Windows プラットフォーム ランタイム | 16.0.28625.61 | Optional
Microsoft.Net.Component.4.7.2.SDK | .NET Framework 4.7.2 SDK | 16.0.28517.75 | Optional
Microsoft.VisualStudio.Component.Graphics.Tools | DirectX 用グラフィックス デバッガーおよび GPU プロファイラー | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.TextTemplating | テキスト テンプレート変換 | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.UWP.VC.ARM64 | v142 ビルド ツールの C++ ユニバーサル Windows プラットフォーム サポート (ARM64) | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.VC.CoreIde | C++ コア機能 | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.VC.Redist.14.Latest | C++ 2019 再頒布可能パッケージの更新プログラム | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.VC.Tools.ARM | MSVC v142 – VS 2019 C++ ARM ビルド ツール (v14.20) | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.VC.Tools.ARM64 | MSVC v142 – VS 2019 C++ ARM64 ビルド ツール (v14.20) | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.VC.Tools.x86.x64 | MSVC v142 – VS 2019 C++ x64/x86 ビルド ツール (v14.20) | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.VC.v141.ARM | MSVC v141 – VS 2017 C++ ARM ビルド ツール (v14.16) | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.VC.v141.ARM64 | MSVC v141 – VS 2017 C++ ARM64 ビルド ツール (v14.16) | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.VC.v141.x86.x64 | MSVC v141 – VS 2017 C++ x64/x86 ビルド ツール (v14.16) | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.16299 | Windows 10 SDK (10.0.16299.0) | 16.0.28517.75 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.17134 | Windows 10 SDK (10.0.17134.0) | 16.0.28517.75 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.IpOverUsb | USB デバイスの接続 | 16.0.28320.51 | Optional
Microsoft.VisualStudio.ComponentGroup.NativeDesktop.Core | Visual C++ コア デスクトップ機能 | 16.0.28315.86 | Optional
Microsoft.VisualStudio.ComponentGroup.UWP.VC | C++ (v142) ユニバーサル Windows プラットフォーム ツール | 16.0.28621.142 | Optional
Microsoft.VisualStudio.ComponentGroup.UWP.VC.v141 | C++ (v141) ユニバーサル Windows プラットフォーム ツール | 16.0.28621.142 | Optional

## <a name="visual-studio-extension-development"></a>Visual Studio 拡張機能の開発

**ID:** Microsoft.VisualStudio.Workload.VisualStudioExtension

**説明:** Visual Studio 用のアドオンや拡張機能 (新しいコマンド、コード アナライザー、ツール ウィンドウを含みます) を作成します。

### <a name="components-included-by-this-workload"></a>このワークロードに含まれるコンポーネント

コンポーネント ID | name | Version | 依存関係の種類
--- | --- | --- | ---
Microsoft.Component.MSBuild | MSBuild | 16.0.28517.75 | 必須
Microsoft.Net.Component.4.6.TargetingPack | .NET Framework 4.6 Targeting Pack | 16.0.28517.75 | 必須
Microsoft.Net.Component.4.7.2.SDK | .NET Framework 4.7.2 SDK | 16.0.28517.75 | 必須
Microsoft.Net.Component.4.7.2.TargetingPack | .NET Framework 4.7.2 Targeting Pack | 16.0.28517.75 | 必須
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | .NET Framework 4.7.2 開発ツール | 16.0.28516.191 | 必須
Microsoft.VisualStudio.Component.NuGet | NuGet パッケージ マネージャー | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# および Visual Basic Roslyn コンパイラ | 16.0.28714.129 | 必須
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# および Visual Basic | 16.0.28625.61 | 必須
Microsoft.VisualStudio.Component.VSSDK | Visual Studio SDK | 16.0.28315.86 | 必須
Microsoft.VisualStudio.ComponentGroup.VisualStudioExtension.Prerequisites | Visual Studio 拡張機能の開発の前提条件 | 16.0.28621.142 | 必須
Microsoft.VisualStudio.Component.DiagnosticTools | .NET プロファイル ツール | 16.0.28625.61 | 推奨
Microsoft.VisualStudio.Component.TextTemplating | テキスト テンプレート変換 | 16.0.28625.61 | 推奨
Component.Dotfuscator | PreEmptive Protection - Dotfuscator | 16.0.28528.71 | Optional
Microsoft.Component.CodeAnalysis.SDK | .NET Compiler Platform SDK | 16.0.28625.61 | Optional
Microsoft.Component.VC.Runtime.OSSupport | v142 ビルド ツールの C++ ユニバーサル Windows プラットフォーム ランタイム | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.AppInsights.Tools | Developer Analytics Tools | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.ClassDesigner | クラス デザイナー | 16.0.28528.71 | Optional
Microsoft.VisualStudio.Component.DslTools | Modeling SDK | 16.0.28315.86 | Optional
Microsoft.VisualStudio.Component.VC.ATL | v142 ビルド ツールの C++ ATL (x86 & x64) | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.VC.ATLMFC | v142 ビルド ツールの C++ MFC (x86 & x64) | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.VC.CoreIde | C++ コア機能 | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.VC.Tools.x86.x64 | MSVC v142 – VS 2019 C++ x64/x86 ビルド ツール (v14.20) | 16.0.28625.61 | Optional

## <a name="unaffiliated-components"></a>関連付けられていないコンポーネント

以下のコンポーネントはどのワークロードにも含まれていませんが、個別のコンポーネントとして選択できます。

コンポーネント ID | name | Version
--- | --- | ---
Component.GitHub.VisualStudio | Visual Studio 用の GitHub 拡張機能 | 2.5.9.5485
Component.Xamarin.Inspector | Xamarin Inspector | 16.0.28315.86
Component.Xamarin.Profiler | Xamarin Profiler | 16.0.28315.86
Component.Xamarin.Workbooks | Xamarin Workbooks | 16.0.28315.86
Microsoft.Component.ClickOnce | ClickOnce Publishing | 16.0.28707.177
Microsoft.Component.HelpViewer | ヘルプ ビューアー | 16.0.28625.61
Microsoft.NetCore.1x.ComponentGroup.Web | .NET Core 1.0 - 1.1 Web 用開発ツール | 16.0.28621.142
Microsoft.VisualStudio.Component.AzureDevOps.OfficeIntegration | Azure DevOps Office Integration | 16.0.28625.61
Microsoft.VisualStudio.Component.DependencyValidation.Community | 依存関係検証 | 16.0.28517.75
Microsoft.VisualStudio.Component.Git | Git for Windows | 16.0.28625.61
Microsoft.VisualStudio.Component.GraphDocument | DGML エディター | 16.0.28625.61
Microsoft.VisualStudio.Component.LinqToSql | LINQ to SQL ツール | 16.0.28625.61
Microsoft.VisualStudio.Component.VC.ATL.ARM | v142 ビルド ツールの C++ ATL (ARM) | 16.0.28625.61
Microsoft.VisualStudio.Component.VC.ATL.ARM.Spectre | v142 ビルド ツール用 C++ ATL と Spectre 軽減策 (ARM) | 16.0.28625.61
Microsoft.VisualStudio.Component.VC.ATL.ARM64 | v142 ビルド ツールの C++ ATL (ARM64) | 16.0.28625.61
Microsoft.VisualStudio.Component.VC.ATL.ARM64.Spectre | v142 ビルド ツール用 C++ ATL と Spectre 軽減策 (ARM64) | 16.0.28625.61
Microsoft.VisualStudio.Component.VC.ATL.Spectre | v142 ビルド ツール用 C++ ATL と Spectre 軽減策 (x86 & x64) | 16.0.28625.61
Microsoft.VisualStudio.Component.VC.ATLMFC.Spectre | v142 ビルド ツール用 C++ MFC と Spectre 軽減策 (x86 & x64) | 16.0.28625.61
Microsoft.VisualStudio.Component.VC.MFC.ARM | v142 ビルド ツール用 C++ MFC (ARM) | 16.0.28625.61
Microsoft.VisualStudio.Component.VC.MFC.ARM.Spectre | v142 ビルド ツール用 C++ MFC と Spectre 軽減策 (ARM) | 16.0.28625.61
Microsoft.VisualStudio.Component.VC.MFC.ARM64 | v142 ビルド ツール用 C++ MFC (ARM64) | 16.0.28625.61
Microsoft.VisualStudio.Component.VC.MFC.ARM64.Spectre | v142 ビルド ツール用 C++ MFC と Spectre 軽減策 (ARM64) | 16.0.28625.61
Microsoft.VisualStudio.Component.VC.Redist.MSM | C++ 2019 再頒布可能パッケージ MSM | 16.0.28625.61
Microsoft.VisualStudio.Component.VC.Runtimes.ARM.Spectre | MSVC v142 – VS 2019 C++ ARM Spectre 軽減ライブラリ (v14.20) | 16.0.28625.61
Microsoft.VisualStudio.Component.VC.Runtimes.ARM64.Spectre | MSVC v142 – VS 2019 C++ ARM64 Spectre 軽減ライブラリ (v14.20) | 16.0.28625.61
Microsoft.VisualStudio.Component.VC.Runtimes.x86.x64.Spectre | MSVC v142 – VS 2019 C++ x64/x86 Spectre 軽減ライブラリ (v14.20)  | 16.0.28625.61
Microsoft.VisualStudio.Component.VC.v141.ARM.Spectre | MSVC v141 – VS 2017 C++ ARM Spectre 軽減ライブラリ (v14.16) | 16.0.28625.61
Microsoft.VisualStudio.Component.VC.v141.ARM64.Spectre | MSVC v141 – VS 2017 C++ ARM64 Spectre 軽減ライブラリ (v14.16) | 16.0.28625.61
Microsoft.VisualStudio.Component.VC.v141.ATL | v141 ビルド ツールの C++ ATL (x86 & x64) | 16.0.28625.61
Microsoft.VisualStudio.Component.VC.v141.ATL.ARM | v141 ビルド ツールの C++ ATL (ARM) | 16.0.28625.61
Microsoft.VisualStudio.Component.VC.v141.ATL.ARM.Spectre | v141 ビルド ツール用 C++ ATL と Spectre 軽減策 (ARM) | 16.0.28625.61
Microsoft.VisualStudio.Component.VC.v141.ATL.ARM64 | v141 ビルド ツールの C++ ATL (ARM64) | 16.0.28625.61
Microsoft.VisualStudio.Component.VC.v141.ATL.ARM64.Spectre | v141 ビルド ツール用 C++ ATL と Spectre 軽減策 (ARM64) | 16.0.28625.61
Microsoft.VisualStudio.Component.VC.v141.ATL.Spectre | v141 ビルド ツール用 C++ ATL と Spectre 軽減策 (x86 & x64) | 16.0.28625.61
Microsoft.VisualStudio.Component.VC.v141.CLI.Support | v141 ビルド ツールの C++/CLI サポート | 16.0.28625.61
Microsoft.VisualStudio.Component.VC.v141.MFC | v141 ビルド ツールの C++ MFC (x86 & x64) | 16.0.28625.61
Microsoft.VisualStudio.Component.VC.v141.MFC.ARM | v141 ビルド ツールの C++ MFC (ARM) | 16.0.28625.61
Microsoft.VisualStudio.Component.VC.v141.MFC.ARM.Spectre | v141 ビルド ツール用 C++ MFC と Spectre 軽減策 (ARM) | 16.0.28625.61
Microsoft.VisualStudio.Component.VC.v141.MFC.ARM64 | v141 ビルド ツールの C++ MFC (ARM64) | 16.0.28625.61
Microsoft.VisualStudio.Component.VC.v141.MFC.ARM64.Spectre | v141 ビルド ツール用 C++ MFC と Spectre 軽減策 (ARM64) | 16.0.28625.61
Microsoft.VisualStudio.Component.VC.v141.MFC.Spectre | v141 ビルド ツール用 C++ MFC と Spectre 軽減策 (x86 & x64) | 16.0.28625.61
Microsoft.VisualStudio.Component.VC.v141.x86.x64.Spectre | MSVC v141 – VS 2017 C++ x64/x86 Spectre 軽減ライブラリ (v14.16) | 16.0.28625.61
Microsoft.VisualStudio.Component.VisualStudioData | データソースとサービス参照 | 16.0.28707.177
Microsoft.VisualStudio.Component.WinXP | VS 2017 (v141) ツールの C++ Windows XP サポート [非推奨] | 16.0.28625.61
Microsoft.VisualStudio.Web.Mvc4.ComponentGroup | ASP.NET MVC 4 | 16.0.28621.142
