---
title: AsyncPackage を使用してバックグラウンドで VSPackage を読み込む
description: バックグラウンド スレッドでのパッケージの読み込みを有効にする AsyncPackage クラスの使用方法について説明します。これにより、ディスク I/O からの応答性の問題を防ぐことができます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: dedf0173-197e-4258-ae5a-807eb3abc952
author: leslierichardson95
ms.author: lerich
ms.workload:
- vssdk
ms.openlocfilehash: 516b6797d622a3f88ed1fcd37b87ecd117d4e8a8
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105074822"
---
# <a name="how-to-use-asyncpackage-to-load-vspackages-in-the-background"></a>方法: AsyncPackage を使用してバックグラウンドで VSPackage を読み込む
VS パッケージの読み込みと初期化では、ディスク I/O が発生する可能性があります。 このような I/O が UI スレッドで発生した場合、応答性の問題が発生する可能性があります。 これに対処するために、Visual Studio 2015 では、バックグラウンド スレッドでのパッケージの読み込みを可能にする <xref:Microsoft.VisualStudio.Shell.AsyncPackage> クラスが導入されました。

## <a name="create-an-asyncpackage"></a>AsyncPackage を作成する
 最初に、VSIX プロジェクトを作成し ( **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]**  >  **[Visual C#]**  >  **[機能拡張]**  >  **[VSIX プロジェクト]** )、プロジェクトに VSPackage を追加します (プロジェクトを右クリックし、 **[追加]**  >  **[新規項目]**  >  **[C# 項目]**  >  **[機能拡張]**  >  **[Visual Studio のパッケージ]** )。 その後、サービスを作成し、それらのサービスをパッケージに追加できます。

1. <xref:Microsoft.VisualStudio.Shell.AsyncPackage> からパッケージを派生させます。

2. クエリによってパッケージが読み込まれる可能性があるサービスを提供する場合:

    バックグラウンドの読み込みに対して、パッケージが安全であることを Visual Studio に示し、この動作を選択するには、<xref:Microsoft.VisualStudio.Shell.PackageRegistrationAttribute> で、属性コンストラクターの **Allowsbackgroundloading** プロパティを true に設定する必要があります。

   ```csharp
   [PackageRegistration(UseManagedResourcesOnly = true, AllowsBackgroundLoading = true)]

   ```

    バックグラウンド スレッドでサービスをインスタンス化しても安全であることを Visual Studio に示すには、<xref:Microsoft.VisualStudio.Shell.ProvideServiceAttributeBase.IsAsyncQueryable%2A> コンストラクターの <xref:Microsoft.VisualStudio.Shell.ProvideServiceAttribute> プロパティを true に設定する必要があります。

   ```csharp
   [ProvideService(typeof(SMyTestService), IsAsyncQueryable = true)]

   ```

3. UI コンテキスト経由で読み込んでいる場合は、<xref:Microsoft.VisualStudio.Shell.ProvideAutoLoadAttribute> に **PackageAutoLoadFlags.BackgroundLoad** を指定するか、またはパッケージの自動読み込みエントリの値として書き込まれるフラグに値 (0x2) を指定する必要があります。

   ```csharp
   [ProvideAutoLoad(UIContextGuid, PackageAutoLoadFlags.BackgroundLoad)]

   ```

4. 非同期の初期化作業がある場合は、<xref:Microsoft.VisualStudio.Shell.AsyncPackage.InitializeAsync%2A> をオーバーライドする必要があります。 VSIX テンプレートによって提供される `Initialize()` メソッドを削除します。 (**AsyncPackage** の `Initialize()` メソッドはシールされています)。 任意の <xref:Microsoft.VisualStudio.Shell.AsyncPackage.AddService%2A> メソッドを使用して、パッケージに非同期サービスを追加できます。

    注: `base.InitializeAsync()` を呼び出すには、ソース コードを次のように変更できます。

   ```csharp
   await base.InitializeAsync(cancellationToken, progress);
   ```

5. 非同期初期化コード (**InitializeAsync**) から RPC (リモート プロシージャ コール) を実行しないように注意する必要があります。 これらは、<xref:Microsoft.VisualStudio.Shell.Package.GetService%2A> を直接または間接的に呼び出すと発生する可能性があります。  同期読み込みが必要な場合、UI スレッドによって <xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory> の使用がブロックされます。 既定のブロッキング モデルでは、RPC が無効にされます。 このことは、非同期タスクから RPC を使用しようとしていて、UI スレッド自体がパッケージの読み込みを待機している場合にデッドロックが発生することを意味します。 一般的な代替方法は、**結合可能なタスク ファクトリ** の <xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory.SwitchToMainThreadAsync%2A> のようなものや、RPC を使用しないその他のメカニズムを使用して、必要に応じて、コードを UI スレッドにマーシャリングすることです。  **ThreadHelper.Generic.Invoke** を使用したり、一般的に UI スレッドへのアクセスを待機している呼び出しスレッドをブロックしたりしないでください。

    注: `InitializeAsync` メソッドでは **GetService** または **QueryService** を使用しないようにしてください。 それらを使用する必要がある場合は、最初に UI スレッドに切り替える必要があります。 代替方法は、**AsyncPackage** から <xref:Microsoft.VisualStudio.Shell.AsyncServiceProvider.GetServiceAsync%2A> を使用することです (それを <xref:Microsoft.VisualStudio.Shell.Interop.IAsyncServiceProvider> にキャストすることによって)。

   C#: AsyncPackage を作成します。

```csharp
[PackageRegistration(UseManagedResourcesOnly = true, AllowsBackgroundLoading = true)]
[ProvideService(typeof(SMyTestService), IsAsyncQueryable = true)]
public sealed class TestPackage : AsyncPackage
{
    protected override Task InitializeAsync(System.Threading.CancellationToken cancellationToken, IProgress<ServiceProgressData> progress)
    {
        this.AddService(typeof(SMyTestService), CreateService, true);
        return Task.FromResult<object>(null);
    }
}
```

## <a name="convert-an-existing-vspackage-to-asyncpackage"></a>既存の VSPackage を AsyncPackage に変換する
 作業の大部分は、新しい **Asyncpackage** の作成と同じです。 上の手順 1 から 5 に従います。 また、次の推奨事項に特別に注意する必要があります。

1. パッケージに指定していた `Initialize` オーバーライドを忘れずに削除してください。

2. デッドロックの回避: コードに非表示の RPC が存在する可能性があります。 これがバックグラウンド スレッドで行われるようになりました。 RPC (**GetService** など) を行う場合は、(1) メイン スレッドに切り替えるか、(2) API の非同期バージョン (**GetServiceAsync** など) がある場合は、それを使用する必要があります。

3. スレッド間で頻繁に切り替えないでください。 バックグラウンド スレッドで行われる可能性のある作業をローカライズして、読み込み時間を短縮してください。

## <a name="querying-services-from-asyncpackage"></a>AsyncPackage からのサービスのクエリ
 **AsyncPackage** では、呼び出し元に応じて非同期的に読み込む場合と読み込まない場合があります。 たとえば、

- 呼び出し元によって、**GetService** または **QueryService** (共に非同期 API) が呼び出された場合、または

- 呼び出し元によって、**IVsShell::LoadPackage** (または **IVsShell5::LoadPackageWithContext**) が呼び出された場合、または

- 読み込みは UI コンテキストによってトリガーされるが、UI コンテキスト メカニズムで非同期に読み込むことができるように指定しなかった場合

  パッケージは同期的に読み込まれます。

  パッケージにはまだ UI スレッドを離れて作業を行う機会 (非同期の初期化フェーズで) がありますが、UI スレッドは、その作業の完了までブロックされます。 呼び出し元が **IAsyncServiceProvider** を使用して、サービスに対して非同期的にクエリする場合、読み込みと初期化は、結果となるタスク オブジェクトですぐにブロックされないという前提で、非同期に行われます。

  C#: サービスを非同期でクエリする方法:

```csharp
using Microsoft.VisualStudio.Shell;
using Microsoft.VisualStudio.Shell.Interop;

IAsyncServiceProvider asyncServiceProvider = Package.GetService(typeof(SAsyncServiceProvider)) as IAsyncServiceProvider;
IMyTestService testService = await asyncServiceProvider.GetServiceAsync(typeof(SMyTestService)) as IMyTestService;
```
