---
title: Visual Studio 2022 Preview で削除された API
description: 拡張機能の作成者が拡張機能を Visual Studio 2022 Preview で動作するように更新できるように、Visual Studio 2022 Preview で削除された VS SDK API について説明します。
ms.date: 06/08/2021
ms.topic: reference
author: leslierichardson95
ms.author: lerich
manager: jmartens
monikerRange: vs-2022
ms.workload:
- vssdk
ms.openlocfilehash: bed8d0a261f70acb5e842ebeaf0059faae3fc478
ms.sourcegitcommit: 5fb4a67a8208707e79dc09601e8db70b16ba7192
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2021
ms.locfileid: "112309221"
---
# <a name="visual-studio-2022-sdk-removed-apis"></a>Visual Studio 2022 SDK で削除された API

[!INCLUDE [preview-note](../includes/preview-note.md)]

以下の API は Visual Studio SDK から削除されているため、使用できなくなりました。コードの更新方法の詳細については、各セクションを参照してください。

* [`IVsImageService`](#ivsimageservice)
* [`IBlockContextProvider`](#iblockcontextprovider)
* [`IToolTipProvider`](#itooltipprovider)
* [`IVsTextScanner` と `IVsFullTextScanner`](#ivstextscanner-and-ivsfulltextscanner)
* [非同期ソリューション ロードとライトウェイト ソリューション ロード](#asynchronous-solution-load-and-lightweight-solution-load)
* [`IVsDummy`](#ivsdummy)
* [`Microsoft.VisualStudio.Shell.Task`](#microsoftvisualstudioshelltask)
* [ソース セーフから開く](#open-from-source-safe)
* [.NET Framework 向けの新しい WPF XAML デザイナー](#new-wpf-xaml-designer-for-net-framework)

## <a name="ivsimageservice"></a>IVsImageService

`IVsImageService` は Visual Studio 2022 で削除されています。 `IVsImageService` のすべてのユーザーが、代わりに `IVsImageService2` に移動する必要があります。

### <a name="recommended-updates"></a>推奨される更新プログラム

`IVsImageService` を使用する場合は、そのメソッドの呼び出しを、`IVsImageService2` に対する同等のメソッドの呼び出しに置き換えます。

| **IVsImageService メソッド** | **同等の IVsImageService2 メソッド** |
|----------------------------|----------------------------------------|
| 追加                        | AddCustomImage                         |
| 取得                        | GetImage                               |
| GetIconForFile             | GetImageMonikerForFile                 |
| GetIconForFileEx           | GetImageMonikerForFile                 |

`IVsImageService` の Add および Get メソッドは、モニカーではなく名前 (文字列) でカスタム イメージを参照しました。  カスタム イメージの参照にモニカーだけを使用するようにコードを切り替えることをお勧めしますが、これが現実的でない場合は、`IVsImageService2` に、名前とモニカーを関連付けられるメソッドがいくつかあります。

* `TryAssociateNameWithMoniker`
* `GetImageMonikerForName`

この 2 つの方法を使用すると、イメージを名前で参照し続けることができます。

## <a name="iblockcontextprovider"></a>IBlockContextProvider

`IBlockContextProvider` および関連する型は Visual Studio 2022 で削除されています。 `IBlockContextProvider` のすべてのユーザーが、代わりに `IStructureContextSourceProvider` に移動する必要があります。

### <a name="recommended-updates"></a>推奨される更新プログラム

`IBlockContextProvider` のユーザーが、代わりに `IStructureContextSourceProvider` を使用する必要があります ([ドキュメント](/dotnet/api/microsoft.visualstudio.text.adornments.istructurecontextsourceprovider))。

## <a name="itooltipprovider"></a>IToolTipProvider

`IToolTipProvider` および関連する型は Visual Studio 2022 で削除されています。 `IToolTipProvider` のすべてのユーザーが、代わりに `IToolTipService` に移動する必要があります。

### <a name="recommended-updates"></a>推奨される更新プログラム

`IToolTipProvider` のユーザーが、代わりに `IToolTipService` を使用する必要があります ([ドキュメント](/dotnet/api/microsoft.visualstudio.text.adornments.itooltipservice))。

## <a name="ivstextscanner-and-ivsfulltextscanner"></a>IVsTextScanner と IVsFullTextScanner

`IVsTextScanner` と `IVsFullTextScanner` は Visual Studio 2022 で削除されています。 `IVsTextScanner` または `IVsFullTextScanner` のすべてのユーザーが、代わりに `IVsTextLines` に移動する必要があります。

### <a name="recommended-updates"></a>推奨される更新プログラム

`IVsTextScanner` または `IVsFullTextScanner` のユーザーが、代わりに `IVsTextLines` を使用する必要があります ([ドキュメント](/dotnet/apimicrosoft.visualstudio.textmanager.interop.ivstextlines.getlinetext))。

## <a name="asynchronous-solution-load-and-lightweight-solution-load"></a>非同期ソリューション ロードとライトウェイト ソリューション ロード

非同期ソリューションロード (ASL) とライトウェイト ソリューション ロード (LSL) 機能は Visual Studio 2022 で削除されているため、次のメソッドも削除されています。

### <a name="interfaces"></a>インターフェイス

* `IVsSolution4` - メソッド: `IsBackgroundSolutionLoadEnabled`、`EnsureProjectsAreLoaded`、`EnsureProjectIsLoaded`、`EnsureSolutionIsLoaded`
* `IVsSolutionLoadEvents` - メソッド: `OnBeforeBackgroundSolutionLoadBegins`、`OnQueryBackgroundLoadProjectBatch`、`OnBeforeLoadProjectBatch`、`OnAfterLoadProjectBatch`
* `IVsSolutionLoadManagerSupport` - インターフェイス全体
* `IVsSolutionLoadManager` - インターフェイス全体
* `IVsSccManager3` - インターフェイス全体
* `IVsAsynchronousProjectCreate` - インターフェイス全体
* `IVsAsynchronousProjectCreateUI` - インターフェイス全体

### <a name="enums-properties-and-ui-contexts"></a>列挙型、プロパティ、および UI コンテキスト

* `VSHPROPID_ProjectUnloadStatus` - 列挙型: `UNLOADSTATUS_LoadPendingIfNeeded`
* `VSHPROPID_DemandLoadDependencies`
* `VSHPROPID_IsProjectProvisioned`
* `VSPROPID_IsInBackgroundIdleLoadProjectBatch`
* `VSPROPID_IsInSyncDemandLoadProjectBatch`
* `VSPROPID_ActiveSolutionLoadManager`
* `UICONTEXT_BackgroundProjectLoad`

### <a name="recommended-updates"></a>推奨される更新プログラム

[なし] :

## <a name="ivsdummy"></a>IVsDummy

`IVsDummy` は Visual Studio 2022 で削除されているため、置き換えられません。 

### <a name="recommended-updates"></a>推奨される更新プログラム

[なし] : しかし、API が何もしないため、影響はありません。

## <a name="microsoftvisualstudioshelltask"></a>Microsoft.VisualStudio.Shell.Task

`Microsoft.VisualStudio.Shell.Task` クラスは、非常に一般的な `System.Threading.Tasks.Task` クラスと競合しないように、名前が `Microsoft.VisualStudio.Shell.TaskListItem` に変更されました。

## <a name="open-from-source-safe"></a>ソース セーフから開く

ソース セーフからソリューションを開くためのサポートが削除されているため、次のメソッド、イベント、定数も削除されています。

## <a name="interfaces"></a>インターフェイス

* `IVsSCCProvider3` - インターフェイス全体

### <a name="recommended-updates"></a>推奨される更新プログラム

[なし] :

## <a name="new-wpf-xaml-designer-for-net-framework"></a>.NET Framework 向けの新しい WPF XAML デザイナー

現在の .NET Framework 向け WPF XAML デザイナーは非推奨とされたため、新しい .NET Framework 向け WPF XAML デザイナーに置き換えられます。これは、.NET (.NET Core) 向け WPF XAML デザイナーに使用されているものと同じアーキテクチャに基づいています。 これは、WPF .NET Framework が .design.dll に基づく拡張モデルを制御し、Microsoft.Windows.Design.Extensibility がサポートされなくなったことも意味します。 .NET Framework 向けの新しい WPF XAML デザイナーには、.NET (.NET Core) の WPF XAML デザイナーと同じ機能拡張モデルが提供されます。 .NET (.NET Core) 向けの .designtools.dll 拡張機能を既に作成している場合は、その同じ拡張機能が新しい .NET Framework 向け WPF XAML デザイナーでも機能します。 今後の WPF プラットフォーム (.NET Framework および .NET Core) と UWP プラットフォームの新しい機能拡張モデルに移行する方法の詳細については、以下の移行リンクを参照してください。 

### <a name="recommended-updates"></a>推奨される更新プログラム

「[XAML デザイナーの拡張性の移行](https://github.com/microsoft/xaml-designer-extensibility/blob/main/documents/xaml-designer-extensibility-migration.md)」を参照してください。
