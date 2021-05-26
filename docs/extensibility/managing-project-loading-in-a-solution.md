---
title: ソリューションでのプロジェクトの読み込みの管理 | Microsoft Docs
description: 開発者がソリューション ロード マネージャーを作成することで、ソリューションの読み込み時間を短縮し、プロジェクトの読み込み動作を管理する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- solutions, managing project loading
ms.assetid: 097c89d0-f76a-4aaf-ada9-9a778bd179a0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 425f610e8a473460cb7d9170138521e2e7bee08a
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105073093"
---
# <a name="manage-project-loading-in-a-solution"></a>ソリューションでのプロジェクトの読み込みを管理する
Visual Studio ソリューションには、多数のプロジェクトを含めることができます。 Visual Studio の既定の動作では、ソリューションを開いたときにソリューション内のすべてのプロジェクトが読み込まれます。また、すべてのプロジェクトの読み込みが完了するまで、ユーザーはどのプロジェクトにもアクセスできません。 プロジェクトの読み込みプロセスが 2 分以上続く場合、読み込まれたプロジェクトの数とプロジェクトの合計数を示す進行状況バーが表示されます。 ユーザーは、複数のプロジェクトを含むソリューションで作業しているときにプロジェクトをアンロードできますが、この手順にはいくつかの欠点があります。つまり、アンロードされたプロジェクトは、ソリューションのリビルド コマンドの一部としてビルドされず、閉じられたプロジェクトの型とメンバーの IntelliSense 記述は表示されません。

 開発者はソリューション ロード マネージャーを作成することで、ソリューションの読み込み時間を短縮し、プロジェクトの読み込み動作を管理できます。 ソリューション ロード マネージャーでは、バックグラウンド ビルドを開始する前にプロジェクトが読み込まれるようにしたり、他のバックグラウンド タスクが完了するまでバックグラウンド読み込みを遅らせたり、その他のプロジェクトの読み込み管理タスクを実行したりすることができます。

## <a name="create-a-solution-load-manager"></a>ソリューション ロード マネージャーを作成する
 開発者は、<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadManager> を実装し、ソリューション ロード マネージャーがアクティブであることを Visual Studio に通知することで、ソリューション ロード マネージャーを作成できます。

### <a name="activate-a-solution-load-manager"></a>ソリューション ロード マネージャーをアクティブにする
 Visual Studio では一度に 1 つのソリューション ロード マネージャーのみが使用できるため、ソリューション ロード マネージャーをアクティブにする場合は、Visual Studio に通知する必要があります。 2 つ目のソリューション ロード マネージャーが後でアクティブになると、使用中のソリューション ロード マネージャーは切断されます。

 <xref:Microsoft.VisualStudio.Shell.Interop.SVsSolution> サービスを取得し、[__VSPROPID4.VSPROPID_ActiveSolutionLoadManager](<xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID4.VSPROPID_ActiveSolutionLoadManager>) プロパティを設定する必要があります。

```csharp
IVsSolution pSolution = GetService(typeof(SVsSolution)) as IVsSolution;
object objLoadMgr = this;   //the class that implements IVsSolutionManager
pSolution.SetProperty((int)__VSPROPID4.VSPROPID_ActiveSolutionLoadManager, objLoadMgr);
```

 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadManager.OnDisconnect%2A> メソッドは、Visual Studio がシャットダウンされるとき、または [__VSPROPID4.VSPROPID_ActiveSolutionLoadManager](<xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID4.VSPROPID_ActiveSolutionLoadManager>) プロパティを使用して <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.SetProperty%2A> を呼び出すことによって、アクティブなソリューション ロード マネージャーとして別のパッケージに引き継がれたときに呼び出されます。

#### <a name="strategies-for-different-kinds-of-solution-load-manager"></a>さまざまな種類のソリューション ロード マネージャーのための方法
 ソリューション ロード マネージャーは、管理対象のソリューションの種類に応じてさまざまな方法で実装できます。

 ソリューション ロード マネージャーがソリューションの読み込み全般を管理するものである場合、VSPackage の一部として実装できます。 VSPackage に値 <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionOpening_guid> で <xref:Microsoft.VisualStudio.Shell.ProvideAutoLoadAttribute> を追加することによって、パッケージを自動読み込みに設定する必要があります。 ソリューション ロード マネージャーは、その後 <xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A> メソッドでアクティブ化できます。

> [!NOTE]
> パッケージの自動読み込みの詳細については、「[VSPackages の読み込み](../extensibility/loading-vspackages.md)」を参照してください。

 Visual Studio では、最後にアクティブ化されるソリューション ロード マネージャーのみが認識されるため、一般的なソリューション ロード マネージャーでは、自身をアクティブ化する前に、既存のロード マネージャーがあるかどうかを常に検出する必要があります。 [__VSPROPID4.VSPROPID_ActiveSolutionLoadManager](<xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID4.VSPROPID_ActiveSolutionLoadManager>) のソリューション サービスで `GetProperty()` を呼び出したときに `null` が返された場合、アクティブなソリューション ロード マネージャーは存在しません。 Null が返されない場合は、オブジェクトが使用中のソリューション ロード マネージャーと同じであるかどうかを確認します。

 ソリューション ロード マネージャーが数種類のソリューションのみを管理するように設計されている場合、VSPackage では (<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.AdviseSolutionEvents%2A> を呼び出すことによって) ソリューション読み込みイベントをサブスクライブし、<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnBeforeOpenSolution%2A> のイベント ハンドラーを使用してソリューション ロード マネージャーをアクティブ化できます。

 ソリューション ロード マネージャーが特定のソリューションのみを管理するように設計されている場合、ソリューションの前のセクションで <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.WriteSolutionProps%2A> を呼び出すことによって、アクティブ化情報をソリューション ファイルの一部として永続化することができます。

 特定のソリューション ロード マネージャーは、他のソリューション ロード マネージャーと競合しないようにするために、<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents.OnAfterCloseSolution%2A> イベント ハンドラーで自身を非アクティブ化する必要があります。

 ソリューション ロード マネージャーがグローバル プロジェクト読み込みプロパティ ([オプション] ページで設定されたプロパティなど) を永続化するためだけに必要な場合、ソリューション ロード マネージャーを <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterOpenProject%2A> イベント ハンドラーでアクティブ化し、ソリューション プロパティの設定を永続化してから、ソリューション ロード マネージャーを非アクティブ化することができます。

## <a name="handle-solution-load-events"></a>ソリューションの読み込みイベントを処理する
 ソリューション読み込みイベントをサブスクライブするには、ソリューション ロード マネージャーをアクティブ化するときに <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.AdviseSolutionEvents%2A> を呼び出します。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents> を実装すると、さまざまなプロジェクトの読み込みプロパティに関連するイベントに応答できます。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnBeforeOpenSolution%2A>: このイベントは、ソリューションが開かれる前に発生します。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnBeforeBackgroundSolutionLoadBegins%2A>: このイベントは、ソリューションが完全に読み込まれた後、バックグラウンド プロジェクトの読み込みが開始される前に発生します。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnAfterBackgroundSolutionLoadComplete%2A>: このイベントは、ソリューション ロード マネージャーがあるかどうかにかかわらず、ソリューションが最初に完全に読み込まれた後に発生します。 また、ソリューションが完全に読み込まれたときに、バックグラウンド読み込みまたは要求読み込みの後にも発生します。 同時に、<xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionExistsAndFullyLoaded_guid> が再アクティブ化されます。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnQueryBackgroundLoadProjectBatch%2A>: このイベントは、1 つまたは複数のプロジェクトが読み込まれる前に発生します。 プロジェクトが読み込まれる前に他のバックグラウンド プロセスが完了するようにするには、`pfShouldDelayLoadToNextIdle` を **true** に設定します。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnBeforeLoadProjectBatch%2A>: このイベントは、プロジェクトのバッチが読み込まれようとしているときに発生します。 `fIsBackgroundIdleBatch` が true の場合、プロジェクトはバックグラウンドで読み込まれます。`fIsBackgroundIdleBatch` が false の場合、プロジェクトは (ユーザーがソリューション エクスプローラーで保留中のプロジェクトを展開する場合など) ユーザー要求の結果として同期的に読み込まれます。 このイベントを処理することで、そうでない場合に <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterOpenProject%2A> で実行する必要があるコストのかかる作業を行うことができます。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnAfterLoadProjectBatch%2A>: このイベントは、プロジェクトのバッチが読み込まれた後に発生します。

## <a name="detect-and-manage-solution-and-project-loading"></a>ソリューションとプロジェクトの読み込みを検出して管理する
 プロジェクトとソリューションの読み込み状態を検出するには、次の値を指定して <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.GetProperty%2A> を呼び出します。

- [__VSPROPID4.VSPROPID_IsSolutionFullyLoaded](<xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID4.VSPROPID_IsSolutionFullyLoaded>): ソリューションとそのすべてのプロジェクトが読み込まれている場合、`var` は `true` を返します。それ以外の場合は `false` を返します。

- [__VSPROPID4.VSPROPID_IsInBackgroundIdleLoadProjectBatch](<xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID4.VSPROPID_IsInBackgroundIdleLoadProjectBatch>): プロジェクトのバッチが現在バックグラウンドで読み込まれている場合、`var` は `true` を返します。それ以外の場合は `false` を返します。

- [__VSPROPID4.VSPROPID_IsInSyncDemandLoadProjectBatch](<xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID4.VSPROPID_IsInSyncDemandLoadProjectBatch>): ユーザー コマンドまたはその他の明示的な読み込みの結果として、プロジェクトのバッチが現在同期的に読み込まれている場合、`var` は `true` を返します。それ以外の場合は `false` を返します。

- [__VSPROPID2.VSPROPID_IsSolutionClosing](<xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID2.VSPROPID_IsSolutionClosing>): ソリューションが現在閉じられている場合、`var` は `true` を返します。それ以外の場合は `false` を返します。

- [__VSPROPID.VSPROPID_IsSolutionOpening](<xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID.VSPROPID_IsSolutionOpening>): ソリューションが現在開かれている場合、`var` は `true` を返します。それ以外の場合は `false` を返します。

次のいずれかのメソッドを呼び出すことによって、プロジェクトとソリューションが読み込まれるようにすることもできます。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution4.EnsureSolutionIsLoaded%2A>: このメソッドを呼び出すと、メソッドが返される前に、ソリューション内のプロジェクトが強制的に読み込まれます。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution4.EnsureProjectIsLoaded%2A>: このメソッドを呼び出すと、メソッドが返される前に、`guidProject` 内のプロジェクトが強制的に読み込まれます。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution4.EnsureProjectsAreLoaded%2A>: このメソッドを呼び出すと、メソッドが返される前に、`guidProjectID` 内のプロジェクトが強制的に読み込まれます。
