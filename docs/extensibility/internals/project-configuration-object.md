---
title: プロジェクト構成オブジェクト | Microsoft Docs
description: プロジェクト構成オブジェクトで UI への構成情報の表示を管理する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- project configurations, object
- objects, project configuration
ms.assetid: 877756c9-4261-43d9-9f32-51bf06b4219f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 15a999f78d017c76ee021f86d81cb611310d079d
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112899863"
---
# <a name="project-configuration-object"></a>プロジェクト構成オブジェクト
プロジェクト構成オブジェクトでは、UI への構成情報の表示を管理します。

 ![Visual Studio プロジェクト構成](../../extensibility/internals/media/vsprojectcfg.gif "vsProjectCfg")プロジェクト構成プロパティ ページ

 プロジェクト構成プロバイダーでは、プロジェクト構成を管理します。 プロジェクトの構成に関する情報にアクセスして取得するために、環境およびその他のパッケージにより、プロジェクト構成プロバイダー オブジェクトにアタッチされているインターフェイスが呼び出されます。

> [!NOTE]
> プログラムで、ソリューション構成ファイルを作成または編集することはできません。 `DTE.SolutionBuilder` を使用する必要があります。 詳細については、「[ソリューション構成](../../extensibility/internals/solution-configuration.md)」を参照してください。

 構成 UI で使用する表示名を発行するには、プロジェクトで <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfg.get_DisplayName%2A> を実装する必要があります。 環境により <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2.GetCfgs%2A> が呼び出され、これにより、環境の UI に一覧表示される構成およびプラットフォーム情報の表示名を取得するために使用できる `IVsCfg` ポインターの一覧が返されます。 アクティブな構成とプラットフォームは、アクティブなソリューション構成に格納されているプロジェクトの構成によって決まります。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionBuildManager.FindActiveProjectCfg%2A> メソッドを使用すると、アクティブなプロジェクトの構成を取得できます。

 必要に応じて、<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfgProvider> オブジェクトを <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProviderEventsHelper> オブジェクトと共に <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2> オブジェクトに実装して、正規のプロジェクト構成名に基づいて `IVsProjectCfg2` オブジェクトを取得できます。

 環境や他のプロジェクトでプロジェクト構成にアクセスできるようにするもう 1 つの方法は、プロジェクトで `IVsCfgProvider2::GetCfgs` メソッドを実装して、1 つ以上の構成オブジェクトを返すというものです。 プロジェクトでは、構成固有の情報を提供するために、`IVsProjectCfg` から継承され、したがって `IVsCfg` からも継承される <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg2> を実装することもできます。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2> では、プロジェクト構成を追加、削除、名前変更するためのプラットフォームと機能がサポートされています。

> [!NOTE]
> Visual Studio は 2 種類の構成に制限されなくなったため、構成を処理するコードを、構成の数を想定して記述する必要も、1 つだけの構成を持つプロジェクが必ずデバッグかリテールのどちらかであるという想定で記述する必要もありません。 これにより、<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfg.get_IsReleaseOnly%2A> と <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfg.get_IsDebugOnly%2A> の使用が廃止されます。

 `IVsGetCfgProvider::GetCfgProvider` から返されたオブジェクトに対して `QueryInterface` を呼び出すと、`IVsCfgProvider2` が取得されます。 `IVsProject3` プロジェクト オブジェクトで `QueryInterface` を呼び出しても `IVsGetCfgProvider` が見つからない場合は、`IVsHierarchy::GetProperty(VSITEM_ROOT, VSHPROPID_BrowseObject)` に対して返されたオブジェクトについて階層ルート ブラウザー オブジェクトで `QueryInterface` を呼び出すか、`IVsHierarchy::GetProperty(VSITEM_ROOT, VSHPROPID_ConfigurationProvider)` に対して返された構成ブラウザーへのポインターを通じて、構成プロバイダー オブジェクトにアクセスできます。

 `IVsProjectCfg2` を使用すると、主にビルド、デバッグ、デプロイ管理オブジェクトにアクセスでき、プロジェクトで出力を自由にグループ化できるようになります。 `IVsProjectCfg` と `IVsProjectCfg2` のメソッドを使用すると、<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildableProjectCfg> を実装して、ビルド プロセスと、構成の出力グループへの <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputGroup> ポインターを管理できます。

 グループ内に含まれる出力の数が構成ごとに異なる場合でも、プロジェクトでは、サポートする構成ごとに同じ数のグループを返す必要があります。 また、グループには、プロジェクト内のそれぞれの構成で同じ識別子情報 (正規名、表示名、グループ情報) が保有されている必要もあります。 詳細については、「[出力のためのプロジェクト構成](../../extensibility/internals/project-configuration-for-output.md)」を参照してください。

 デバッグを有効にするには、構成で <xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg> を実装する必要があります。 `IVsDebuggableProjectCfg` は、デバッガーで構成を起動できるようにするためにプロジェクトによって実装される省略可能なインターフェイスであり、`IVsCfg` と `IVsProjectCfg` を使用して構成オブジェクト上に実装されます。 ユーザーが F5 キーを押してデバッガーの起動を選択したときに、環境によってこれが呼び出されます。

 `ISpecifyPropertyPages` と `IDispatch` は、プロパティ ページと組み合わせて使用され、構成に依存する情報を取得してユーザーに表示します。 詳細については、「[プロパティ ページ](../../extensibility/internals/property-pages.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [構成オプションの管理](../../extensibility/internals/managing-configuration-options.md)
- [ビルドのためのプロジェクト構成](../../extensibility/internals/project-configuration-for-building.md)
- [出力のためのプロジェクト構成](../../extensibility/internals/project-configuration-for-output.md)
- [[プロパティ ページ]](../../extensibility/internals/property-pages.md)
- [ソリューション構成](../../extensibility/internals/solution-configuration.md)
