---
title: Just-In-Time デバッガーを使用してデバッグする | Microsoft Docs
description: Visual Studio で Just-In-Time デバッガーを使用してデバッグします。 Just-In-Time デバッグを使用すると、アプリでエラーまたはクラッシュが発生したときに、Visual Studio を自動的に起動できます。
ms.custom: SEO-VS-2020
ms.date: 09/24/2018
ms.topic: how-to
helpviewer_keywords:
- debugging [Visual Studio], Just-In-Time
- Just-In-Time debugging
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 3bdd35056706491ace6e5e6b2f7c3f6a45464d2e
ms.sourcegitcommit: a0f5e7188838c5989c9cc78d99fb29bb2813501e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/11/2021
ms.locfileid: "109729248"
---
# <a name="debug-using-the-just-in-time-debugger-in-visual-studio"></a>Visual Studio で Just-In-Time デバッガーを使用してデバッグする

Just-In-Time デバッグは、Visual Studio の外部で実行中のアプリでエラーまたはクラッシュが発生したときに、Visual Studio を自動的に起動できます。 Just-In-Time デバッグを使用すると、Visual Studio の外部でアプリをテストでき、問題が発生したときに Visual Studio を開いてデバッグを開始できます。

Just-In-Time デバッグは、Windows デスクトップ アプリで使用できます。 ユニバーサル Windows アプリ、またはビジュアライザーなどのネイティブ アプリケーションでホストされるマネージド コードには使用できません。

> [!TIP]
> [Just-In-Time デバッガー] ダイアログ ボックスの表示を停止したいとき、Visual Studio がインストールされていない場合は、「[Just-In-Time デバッガーを無効にする](../debugger/just-in-time-debugging-in-visual-studio.md)」を参照してください。 Visual Studio がインストールされていた場合は、[Windows レジストリで Just-In-Time デバッグを無効にする](#disable-just-in-time-debugging-from-the-windows-registry)必要があります。

## <a name="enable-or-disable-just-in-time-debugging-in-visual-studio"></a><a name="BKMK_Enabling"></a> Visual Studio で Just-In-Time デバッグを有効または無効にする

>[!NOTE]
>Just-In-Time デバッグを有効または無効にするには、Visual Studio を管理者として実行している必要があります。 Just-In-Time デバッグを有効または無効にするとレジストリ キーが設定され、そのキーを変更するには管理者特権が必要になります。 管理者として Visual Studio を開くには、Visual Studio アプリを右クリックし、 **[管理者として実行]** を選択します。

Just-In-Time デバッグは、Visual Studio の **[ツール]**  >  **[オプション]** (または **[デバッグ]**  >  **[オプション]** ) ダイアログ ボックスで構成できます。

**Just-In-Time デバッグの有効/無効を切り替えるには:**

1. **[ツール]** または **[デバッグ]** メニューで、 **[オプション]**  >  **[デバッグ]**  >  **[Just-In-Time]** を選択します。

   ![JIT デバッグの有効化または無効化](../debugger/media/dbg-jit-enable-or-disable.png "JIT デバッグの有効化または無効化")

1. **[このコードの種類の Just-In-Time デバッグを有効にする]** ボックスで、Just-In-Time デバッグでデバッグするコードの種類を選択します。 **[マネージド]** 、 **[ネイティブ]** 、または **[スクリプト]** 。

1. **[OK]** を選択します。

Just-In-Time デバッガーを有効にしたが、アプリのクラッシュやエラーの際に開かない場合は、「[Just-In-Time デバッグのトラブルシューティング](#jit_errors)」を参照してください。

## <a name="disable-just-in-time-debugging-from-the-windows-registry"></a>Windows レジストリで Just-In-Time デバッグを無効にする

Visual Studio がコンピューターからアンインストールされた後でも、Just-In-Time デバッグが有効になっている場合があります。 Visual Studio がもうインストールされていない場合は、Windows レジストリを編集して Just-In-Time デバッグを無効にできます。

**レジストリを編集して Just-In-Time デバッグを無効にするには:**

1. Windows の **[スタート]** メニューで、**レジストリ エディター** (*regedit.exe*) を実行します。

2. **[レジストリ エディター]** ウィンドウで、次のレジストリ エントリを探して削除します。

    - **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\\.NETFramework\DbgManagedDebugger**

    - **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AeDebug\Debugger**

    ![JIT レジストリ キー](../debugger/media/dbg-jit-registry.png "JIT レジストリ キー")

3. コンピューターで 64 ビット オペレーティング システムを実行している場合は、次のレジストリ エントリも削除します。

    - **HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\\.NETFramework\DbgManagedDebugger**

    - **HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows NT\CurrentVersion\AeDebug\Debugger**

    他のレジストリ キーを削除または変更しないようにしてください。

5. **[レジストリ エディター]** ウィンドウを閉じます。

## <a name="enable-just-in-time-debugging-of-a-windows-form"></a>Windows フォームの Just-In-Time デバッグを有効化する

Windows フォーム アプリには既定で最高レベルの例外ハンドラーがあり、回復可能であればアプリは実行し続けることができます。 Windows フォーム アプリが、ハンドルされない例外をスローすると、次のダイアログが表示されます。

![Windows フォームのハンドルされない例外](../debugger/media/windowsformsunhandledexception.png "Windows フォームのハンドルされない例外")

標準の Windows フォーム エラー処理の代わりに Just-In-Time デバッグを有効にするには、次の設定を追加します。

- *machine.config* または *\<app name>.exe.config* ファイルの `system.windows.forms` セクションで、`jitDebugging` 値を `true` に設定します。

    ```xml
    <configuration>
        <system.windows.forms jitDebugging="true" />
    </configuration>
    ```

- さらに、C++ Windows フォーム アプリケーションでは、 *.config* ファイルまたはコード内で `DebuggableAttribute` を `true`に設定することも必要です。 [/Zi](/cpp/build/reference/z7-zi-zi-debug-information-format) を使用し、[/Og](/cpp/build/reference/og-global-optimizations) は使用しないでコンパイルすると、コンパイラによってこの属性が設定されます。 ただし、最適化されていないリリース ビルドをデバッグする場合は、アプリの *AssemblyInfo* ファイルに次の行を追加して、`DebuggableAttribute` を設定する必要があります。

   ```cpp
   [assembly:System::Diagnostics::DebuggableAttribute(true, true)];
   ```

   詳細については、「<xref:System.Diagnostics.DebuggableAttribute>」を参照してください。

## <a name="use-just-in-time-debugging"></a><a name="BKMK_Using_JIT"></a>Just-In-Time デバッグを使用する
この例では、アプリがエラーをスローした場合の Just-In-Time デバッグについて説明します。

- これらのステップを実行するには、Visual Studio をインストールする必要があります。 Visual Studio をインストールしていない場合は、無料の [Visual Studio Community エディション](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=Community&rel=15)をダウンロードできます。

- **[ツール]**  >  **[オプション]**  >  **[デバッグ]**  >  **[Just-In-Time]** で、Just-In-Time デバッグが [有効](#BKMK_Enabling)になっていることを確認します。

この例では、[NullReferenceException](/dotnet/api/system.nullreferenceexception) をスローする C# コンソール アプリを Visual Studio で作成します。

1. Visual Studio で、*ThrowsNullException* という名前の C# コンソール アプリを作成します ( **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]**  >  **[Visual C#]**  >  **[コンソール アプリケーション]** )。 Visual Studio でのプロジェクトの作成の詳細については、[シンプルなアプリケーションを作成するチュートリアル](../get-started/csharp/tutorial-wpf.md)のページを参照してください。

1. プロジェクトが Visual Studio で開いたら、*Program.cs* ファイルを開きます。 Main() メソッドを次のコードで置き換えます。これは、行をコンソールに出力して、NullReferenceException をスローします。

   ```csharp
   static void Main(string[] args)
   {
       Console.WriteLine("we will now throw a NullReferenceException");
       throw new NullReferenceException("this is the exception thrown by the console app");
   }
   ```

1. ソリューションをビルドするには、 **[デバッグ]** (既定) または **[リリース]** 構成を選択してから、 **[ビルド]**  >  **[ソリューションのリビルド]** を選択します。

   > [!NOTE]
   > - 完全なデバッグ エクスペリエンスのためには、 **[デバッグ]** 構成を選択します。
   > - [[リリース]](../debugger/how-to-set-debug-and-release-configurations.md) 構成を選択する場合、この手順を行うためには [[マイ コードのみ]](../debugger/just-my-code.md) をオフにする必要があります。 **[ツール]**  >  **[オプション]**  >  **[デバッグ]** で、 **[マイ コードのみを有効にする]** を選択解除します。

   ビルド構成の詳細については、「[ビルド構成について](../ide/understanding-build-configurations.md)」を参照してください。

1. C# プロジェクト フォルダー ( *...\ThrowsNullException\ThrowsNullException\bin\Debug* または *...\ThrowsNullException\ThrowsNullException\bin\Release*) にある、ビルドされたアプリ *ThrowsNullException.exe* を開きます。

   次のコマンド ウィンドウが表示されます。

   ![未処理の null 参照例外 (System.NullReferenceException) をスローする ThrowsNullException.exe のコンソールのスクリーンショット。](../debugger/media/throwsnullexceptionconsole.png)

1. **[Just-In-Time デバッガーを選択する]** ダイアログが開きます。

   ![ThrowsNullException.exe コンソール ウィンドウに例外が表示された後に表示される、[Just-In-Time デバッガーを選択する] ダイアログ ボックスのスクリーンショット。](../debugger/media/justintimedialog.png)

   **[Available Debuggers]\(使用可能なデバッガー\)** の下で、まだ選択されていない場合は **[\<your preferred Visual Studio version/edition> の新しいインスタンス]** を選択します。

1. **[OK]** を選択します。

   ThrowsNullException プロジェクトが、Visual Studio の新しいインスタンスで開きます。例外をスローした行で実行が停止しています。

   ![Visual Studio の ThrowsNullException プロジェクトのスクリーンショット。例外をスローしたソース コードの行が強調表示されています。](../debugger/media/nullreferencesecondinstance.png)

この時点でデバッグを開始できます。 実際のアプリをデバッグしている場合は、コードが例外をスローする理由を確認する必要があります。

> [!CAUTION]
> アプリに信頼できないコードが含まれている場合は、[セキュリティ警告] ダイアログ ボックスが表示され、デバッグを続行するかどうかを決定できます。 デバッグを開始する前に、コードを信頼できるかどうかを判断します。 このコードは、自分で作成したコードですか。 アプリケーションをリモート コンピューター上で実行している場合、プロセスの名前を識別できますか。 アプリがローカルで実行している場合は、悪意のあるコードがコンピューター上で実行されている可能性も考慮してください。 コードが信頼できると判断した場合は、 **[OK]** を選択します。 それ以外の場合、 **[キャンセル]** を選択します。

## <a name="troubleshoot-just-in-time-debugging"></a><a name="jit_errors"></a>Just-In-Time デバッグのトラブルシューティング

Visual Studio で有効にしていても、アプリがクラッシュしたときに Just-In-Time デバッグが開始しない場合:

- Windows エラー報告が、コンピューター上でエラー処理を引き継いだ可能性があります。

  この問題を解決するには、レジストリ エディターを使用し、次のレジストリ キーに **[無効]** の **[DWORD 値]** を **[値のデータ]** を **1** として追加します。

  - **HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\Windows Error Reporting**

  - (64 ビットコンピューター):**HKEY_LOCAL_MACHINE\Software\WOW6432Node\Microsoft\Windows\Windows Error Reporting**

  詳細については、「[WER 設定](/windows/desktop/wer/wer-settings)」を参照してください。

- Windows の既知の問題により、Just-In-Time デバッガーが失敗する可能性があります。

  解決するには、次のレジストリ キーに **[自動]** の **[DWORD 値]** を **[値のデータ]** を **1** として追加します。

  - **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AeDebug**

  - (64 ビットコンピューター):**HKEY_LOCAL_MACHINE\Software\WOW6432Node\Microsoft\Windows NT\CurrentVersion\AeDebug**

Just-In-Time デバッグの際に次のエラー メッセージが表示されることがあります。

- **クラッシュ プロセスにアタッチできません。指定されたプログラムは、Windows または MS-DOS プログラムではありません。**

    デバッガーが、別のユーザーで実行されているプロセスにアタッチしようとしました。

    この問題を回避するには、Visual Studio で **[デバッグ]**  >  **[プロセスにアタッチ]** を開き (または、**Ctrl** + **Alt** + **P** を押して)、 **[選択可能なプロセス]** の一覧でデバッグするプロセスを見つけます。 プロセスの名前がわからない場合は、 **[Visual Studio Just-In-Time デバッガー]** ダイアログで、プロセス ID を確認します。 そのプロセスを **[選択可能なプロセス]** の一覧から選択し、 **[アタッチ]** を選択します。 **[いいえ]** を選択して、[Just-In-Time デバッガー] ダイアログを閉じます。

- **ログオンしているユーザーがいないため、デバッガーを開始できませんでした。**

    コンソールにログオンしているユーザーがいないため、[Just-In-Time デバッグ] ダイアログを表示するユーザー セッションがありません。

    この問題を解決するには、コンピューターにログオンします。

- **クラスは登録されていません。**

    おそらくインストールの問題が原因で登録されていない COM クラスをデバッガーが作成しようとしました。

    この問題を解決するには、Visual Studio インストーラーを使って Visual Studio を再インストールするか、既存のインストールを修復します。

## <a name="see-also"></a>関連項目

- [デバッガーのセキュリティ](../debugger/debugger-security.md)
- [デバッガーでのはじめに](../debugger/debugger-feature-tour.md)
- [[オプション]、[デバッグ]、[Just-In-Time] ダイアログ ボックス](../debugger/just-in-time-debugging-options-dialog-box.md)
- [セキュリティ警告: 信頼されていないユーザーが所有するプロセスにアタッチするには危険が伴います。以下の情報に関して疑わしい点がある場合や、不明な場合は、このプロセスにアタッチしないでください。](../debugger/security-warning-attaching-to-a-process-owned-by-an-untrusted-user.md)
