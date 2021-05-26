---
title: '方法: Visual Studio の非同期サービスを提供する | Microsoft Docs'
description: Visual Studio の非同期サービスを提供する方法について説明します。 このアプローチにより、UI スレッドをブロックせずにサービスを取得できます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 0448274c-d3d2-4e12-9d11-8aca78a1f3f5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: f9973bb86296442f4b936ddb54ff645d74d7ab74
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105074939"
---
# <a name="how-to-provide-an-asynchronous-visual-studio-service"></a>方法: Visual Studio の非同期サービスを提供する
UI スレッドをブロックせずにサービスを取得する場合は、非同期サービスを作成し、バックグラウンド スレッドでパッケージを読み込む必要があります。 この目的で、<xref:Microsoft.VisualStudio.Shell.Package> ではなく <xref:Microsoft.VisualStudio.Shell.AsyncPackage> を使用して、非同期パッケージの特別な非同期メソッドを使用してサービスを追加できます。

 Visual Studio の同期サービスの提供の詳細については、「[方法: サービスを提供する](../extensibility/how-to-provide-a-service.md)」を参照してください。

## <a name="implement-an-asynchronous-service"></a>非同期サービスを実装する

1. VSIX プロジェクトを作成します ( **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]**  >  **[Visual C#]**  >  **[機能拡張]**  >  **[VSIX プロジェクト]** )。 プロジェクトに **TestAsync**  という名前を付けます。

2. VSPackage をプロジェクトに追加します。 **ソリューション エクスプローラー** でプロジェクト ノードを選択し、 **[追加]**  >  **[新しい項目]**  >  **[Visual C# アイテム]**  >  **[機能拡張]**  >  **[Visual Studio パッケージ]** の順にクリックします。 このファイルに *TestAsyncPackage.cs* という名前を指定します。

3. *TestAsyncPackage.cs* で、パッケージを `Package` ではなく `AsyncPackage` から継承するように変更します。

    ```csharp
    public sealed class TestAsyncPackage : AsyncPackage
    ```

4. サービスを実装するには、次の 3 種類を作成する必要があります。

    - サービスを識別するインターフェイス。 これらのインターフェイスの多くは空です。つまり、サービスのクエリ専用に使用されるため、メソッドはありません。

    - サービス インターフェイスを記述するインターフェイス。 このインターフェイスには、実装するメソッドが含まれています。

    - サービスとサービス インターフェイスの両方を実装するクラス。

5. 次の例に、3 つの種類のきわめて基本的な実装を示します。 サービス クラスのコンストラクターでは、サービス プロバイダーを設定する必要があります。 この例では、パッケージ コード ファイルにサービスを追加するだけです。

6. パッケージ ファイルに次の using ディレクティブを追加します。

    ```csharp
    using System.Threading;
    using System.Threading.Tasks;
    using System.Runtime.CompilerServices;
    using System.IO;
    using Microsoft.VisualStudio.Threading;
    using IAsyncServiceProvider = Microsoft.VisualStudio.Shell.IAsyncServiceProvider;
    using Task = System.Threading.Tasks.Task;
    ```

7. 非同期サービスの実装を次に示します。 コンストラクターに、同期サービス プロバイダーではなく、非同期サービス プロバイダーを設定する必要があることに注意してください。

    ```csharp
    public class TextWriterService : STextWriterService, ITextWriterService
    {
        private IAsyncServiceProvider asyncServiceProvider;

        public TextWriterService(IAsyncServiceProvider provider)
        {
            // constructor should only be used for simple initialization
            // any usage of Visual Studio service, expensive background operations should happen in the
            // asynchronous InitializeAsync method for best performance
            asyncServiceProvider = provider;
        }

        public async Task InitializeAsync(CancellationToken cancellationToken)
        {
            await TaskScheduler.Default;
            // do background operations that involve IO or other async methods

            await ThreadHelper.JoinableTaskFactory.SwitchToMainThreadAsync(cancellationToken);
            // query Visual Studio services on main thread unless they are documented as free threaded explicitly.
            // The reason for this is the final cast to service interface (such as IVsShell) may involve COM operations to add/release references.

            IVsShell vsShell = this.asyncServiceProvider.GetServiceAsync(typeof(SVsShell)) as IVsShell;
            // use Visual Studio services to continue initialization
        }

        public async Task WriteLineAsync(string path, string line)
        {
            StreamWriter writer = new StreamWriter(path);
            await writer.WriteLineAsync(line);
            writer.Close();
        }
    }

    public interface STextWriterService
    {
    }

    public interface ITextWriterService
    {
        System.Threading.Tasks.Task WriteLineAsync(string path, string line);
    }
    ```

## <a name="register-a-service"></a>サービスを登録する
 サービスを登録するには、サービスを提供するパッケージに <xref:Microsoft.VisualStudio.Shell.ProvideServiceAttribute> を追加します。 同期サービスの登録と異なり、パッケージとサービスの両方で非同期読み込みがサポートされていることを確認する必要があります。

- **AllowsBackgroundLoading = true** フィールドを <xref:Microsoft.VisualStudio.Shell.PackageRegistrationAttribute> に追加して、パッケージを非同期に初期化できるようにする必要があります。PackageRegistrationAttribute の詳細については、「[VSPackage の登録と登録解除](../extensibility/registering-and-unregistering-vspackages.md)」を参照してください。

- サービス インスタンスを非同期に初期化できるようにするために、**IsAsyncQueryable = true** フィールドを <xref:Microsoft.VisualStudio.Shell.ProvideServiceAttribute> に追加する必要があります。

  非同期サービスを登録した `AsyncPackage` の例を次に示します。

```csharp
[ProvideService((typeof(STextWriterService)), IsAsyncQueryable = true)]
[ProvideAutoLoad(UIContextGuids80.SolutionExists, PackageAutoLoadFlags.BackgroundLoad)]
[PackageRegistration(UseManagedResourcesOnly = true, AllowsBackgroundLoading = true)]
[Guid(TestAsyncPackage.PackageGuidString)]
public sealed class TestAsyncPackage : AsyncPackage
{. . . }
```

## <a name="add-a-service"></a>サービスの追加

1. *TestAsyncPackage.cs* で、`Initialize()` メソッドを削除し、`InitializeAsync()` メソッドをオーバーライドします。 サービスを追加し、コールバック メソッドを追加してサービスを作成します。 サービスを追加する非同期初期化子の例を次に示します。

    ```csharp
    protected override async Task InitializeAsync(CancellationToken cancellationToken, IProgress<ServiceProgressData> progress)
    {
        await base.InitializeAsync(cancellationToken, progress);
        this.AddService(typeof(STextWriterService), CreateTextWriterService);
    }

    ```
    このサービスがこのパッケージの外部で表示されるようにするには、最後のパラメーターとして、promote フラグの値を *true* に設定します。`this.AddService(typeof(STextWriterService), CreateTextWriterService, true);`

2. *Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll* に参照を追加します。

3. サービスを作成して返す非同期メソッドとしてコールバック メソッドを実装します。

    ```csharp
    public async Task<object> CreateTextWriterService(IAsyncServiceContainer container, CancellationToken cancellationToken, Type serviceType)
    {
        TextWriterService service = new TextWriterService(this);
        await service.InitializeAsync(cancellationToken);
        return service;
    }

    ```

## <a name="use-a-service"></a>サービスを使用する
 サービスを取得し、そのメソッドを使用できるようになりました。

1. これを初期化子で示しますが、サービスを使用する任意の場所でサービスを取得できます。

    ```csharp
    protected override async System.Threading.Tasks.Task InitializeAsync(CancellationToken cancellationToken, IProgress<ServiceProgressData> progress)
    {
        await base.InitializeAsync(cancellationToken, progress);
        this.AddService(typeof(STextWriterService), CreateTextWriterService);

        ITextWriterService textService = await this.GetServiceAsync(typeof(STextWriterService)) as ITextWriterService;
        string userpath = @"C:\MyDir\MyFile.txt";
        await textService.WriteLineAsync(userpath, "this is a test");
    }

    ```

     `userpath` をコンピューター上のわかりやすいファイル名とパスに変更してください。

2. コードをビルドし、実行します。 Visual Studio の実験用インスタンスが表示されたら、ソリューションを開きます。 これにより、`AsyncPackage` が自動読み込みされます。 初期化子が実行されたら、指定した場所にファイルが見つかるはずです。

## <a name="use-an-asynchronous-service-in-a-command-handler"></a>コマンドハンドラーで非同期サービスを使用する
 メニュー コマンドで非同期サービスを使用する方法の例を次に示します。 他の非同期メソッドでサービスを使用するには、次に示す手順を使用できます。

1. プロジェクトにメニュー コマンドを追加します。 (**ソリューション エクスプローラー** で、プロジェクト ノードを選択して右クリックし、 **[追加]**  >  **[新しい項目]**  >  **[機能拡張]**  >  **[カスタム コマンド]** を選択します)。コマンド ファイルに *TestAsyncCommand.cs* という名前を付けます。

2. カスタム コマンド テンプレートにより、コマンドを初期化するために、`Initialize()` メソッドが *TestAsyncPackage.cs* ファイルに再追加されます。 `Initialize()` メソッドで、コマンドを初期化する行をコピーします。 内容は次のようになります。

    ```csharp
    TestAsyncCommand.Initialize(this);
    ```

     この行を *AsyncPackageForService.cs* ファイル内の `InitializeAsync()` メソッドに移動します。 これは非同期の初期化であるため、<xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory.SwitchToMainThreadAsync%2A> を使用してコマンドを初期化する前に、メイン スレッドに切り替える必要があります。 その結果、次のようになります。

    ```csharp

    protected override async System.Threading.Tasks.Task InitializeAsync(CancellationToken cancellationToken, IProgress<ServiceProgressData> progress)
    {
        await base.InitializeAsync(cancellationToken, progress);
        this.AddService(typeof(STextWriterService), CreateTextWriterService);

        ITextWriterService textService =
           await this.GetServiceAsync(typeof(STextWriterService)) as ITextWriterService;
        
        string userpath = @"C:\MyDir\MyFile.txt";
        await textService.WriteLineAsync(userpath, "this is a test");

        await this.JoinableTaskFactory.SwitchToMainThreadAsync(cancellationToken);
        TestAsyncCommand.Initialize(this);
    }

    ```

3. `Initialize()` メソッドを削除します。

4. *TestAsyncCommand.cs* ファイルで、`MenuItemCallback()` メソッドを見つけます。 メソッドの本体を削除します。

5. using ディレクティブを追加します。

    ```csharp
    using System.IO;
    ```

6. `UseTextWriterAsync()` という名前の非同期メソッドを追加します。これにより、サービスを取得し、そのメソッドを使用します。

    ```csharp
    private async System.Threading.Tasks.Task UseTextWriterAsync()
    {
        // Query text writer service asynchronously to avoid a blocking call.
        ITextWriterService textService =
           await AsyncServiceProvider.GlobalProvider.GetServiceAsync(typeof(STextWriterService))
              as ITextWriterService;

        string userpath = @"C:\MyDir\MyFile.txt";
        await textService.WriteLineAsync(userpath, "this is a test");
       }

    ```

7. `MenuItemCallback()` メソッドからこのメソッドを呼び出します。

    ```csharp
    private void MenuItemCallback(object sender, EventArgs e)
    {
        UseTextWriterAsync();
    }

    ```

8. ソリューションをビルドし、デバッグを開始します。 Visual Studio の実験用インスタンスが表示されたら、 **[ツール]** メニューに移動し、 **[TestAsyncCommand の呼び出し]** メニュー項目を探します。 これをクリックすると、TextWriterService によって、指定したファイルに書き込まれます。 (コマンドを呼び出すとパッケージも読み込まれるため、ソリューションを開く必要はありません)。

## <a name="see-also"></a>関連項目
- [サービスを使用および提供する](../extensibility/using-and-providing-services.md)
