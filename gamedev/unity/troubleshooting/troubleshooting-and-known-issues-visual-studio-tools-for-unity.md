---
title: トラブルシューティングと既知の問題 (VS Tools for Unity)
description: Visual Studio Tools for Unity でのトラブルシューティングについて確認します。 既知の問題の説明を確認し、それらの問題の解決策について説明します。
ms.custom: ''
ms.date: 04/15/2021
ms.technology: vs-unity-tools
ms.prod: visual-studio-dev16
ms.topic: troubleshooting
ms.assetid: 8f5db192-8d78-4627-bd07-dbbc803ac554
author: therealjohn
ms.author: johmil
manager: crdun
ms.workload:
- unity
ms.openlocfilehash: 37ee35fa66d37f9b85af01f5012e8ede76e877de
ms.sourcegitcommit: 3e1ff87fba290f9e60fb4049d011bb8661255d58
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2021
ms.locfileid: "107879370"
---
# <a name="troubleshooting-and-known-issues-visual-studio-tools-for-unity"></a>トラブルシューティングと既知の問題 (Visual Studio Tools for Unity)

このセクションには、Visual Studio Tools for Unity における一般的な問題の解決法、既知の問題についての説明、およびエラー報告によって Visual Studio Tools for Unity を改善する方法について記されています。

## <a name="troubleshooting-the-connection-between-unity-and-visual-studio"></a>Unity と Visual Studio の間の接続のトラブルシューティング

### <a name="confirm-editor-attaching-is-enabled-or-code-optimization-on-startup-is-set-to-debug"></a>`Editor Attaching` が有効になっているか、`Code Optimization On Startup` が `Debug` に設定されていることを確認する

Unity メニューで、`Edit / Preferences` を選択します。

使用されている Unity のバージョンに応じて、次のことを行います。
- `Code Optimization On Startup` が `Debug` に設定されていることを確認します。
- または、`External Tools` タブを選択します。`Editor Attaching` チェック ボックスが有効になっていることを確認します。 

詳しくは、[Unity Preferences のドキュメント](https://docs.unity3d.com/Manual/Preferences.html)をご覧ください。

### <a name="unable-to-attach"></a>アタッチできない

- ウイルス対策ソフトウェアを一時的に無効にするか、VS と Unity 両方に対する除外規則を作成してみてください。
- ファイアウォールを一時的に無効にするか、VS と Unity の間の TCP/UDP ネットワークを許可する規則を作成してみてください。
- Team Viewer などの一部のプログラムが、プロセスの検出を妨げている可能性があります。 余分なソフトウェアを一時的に停止して、何か変化があるかどうかを試すことができます。
- VSTU は "Unity.exe" プロセスを監視するだけなので、メインの Unity 実行可能ファイルの名前を変更しないでください。

## <a name="visual-studio-crashes"></a>Visual Studio がクラッシュする

この問題は、Visual Studio MEF キャッシュの破損が原因になっている可能性があります。

次のフォルダーを削除して、MEF キャッシュをリセットすることを試してください (これを行う前に、Visual Studio を終了してください)。

```batch
%localappdata%\Microsoft\VisualStudio\<version>\ComponentModelCache
```

これで問題は解決するはずです。 まだ問題が発生する場合は、管理者として Visual Studio の開発者コマンド プロンプトを実行し、次のコマンドを使います。

```batch
 devenv /setup
```

## <a name="visual-studio-stops-responding"></a>Visual Studio が応答しない

Parse、FMOD、UMP (Universal Media Player)、ZFBrowser、Embedded Browser などの複数の Unity プラグインは、ネイティブ スレッドを使っています。 これは、プラグインがランタイムへのネイティブ スレッドのアタッチを終了した後で OS への呼び出しをブロックしている問題です。 つまり、Unity はデバッガー (またはドメインの再読み込み) のためにスレッドを中断できずに応答しなくなります。

FMOD の場合は回避策があります。`FMOD_STUDIO_INIT_SYNCHRONOUS_UPDATE` 初期化[フラグ](https://www.fmod.com/resources/documentation-studio?version=2.0&page=https://fmod.com/resources/documentation-api?version=2.0&page=studio-api-system.html#fmod_studio_initflags)を渡して非同期処理を無効にし、メイン スレッドですべての処理を実行します。

## <a name="incompatible-project-in-visual-studio"></a>Visual Studio での互換性のないプロジェクト

非常に重要なことは、Visual Studio では "非互換" 状態がプロジェクトの設定に保存され、`Reload Project` を明示的に使用するまでは、プロジェクトの再読み込みが試行されないということです。 そのため、トラブルシューティングの各手順を実行したら、その都度ソリューションを再度開いて、互換性のないすべてのプロジェクトを右クリックし、`Reload Project` を選択するようにしてください。

1. `Edit / Preferences / External Tools` を使用して、Visual Studio が Unity の外部スクリプト エディターとして設定されていることを確認します。
2. Unity のバージョンに応じて、次のことを行います。
   - Visual Studio プラグインが Unity にインストールされていることを確認します。 `Help / About` の下部に、「Microsoft Visual Studio Tools for Unity が有効になっています」のようなメッセージが表示されるはずです。
   - Unity 2020.x+: `Window / Package Manager` で、最新の Visual Studio エディター パッケージを使用していることを確認します。
3. プロジェクト内のすべてのプロジェクトまたはソリューション ファイルと、`.vs` フォルダーを削除してみてください。
4. `Open C# Project` または `Edit / Preferences / External tools / Regenerate Project files` を使用して、プロジェクトまたはソリューションを再作成してみてください。
5. Visual Studio に、ゲームまたは Unity のワークロードがインストールされていることを確認します。
6. [こちら](#visual-studio-crashes)で説明されているように、MEF キャッシュをクリーンアップしてみてください。
7. Visual Studio を再インストールしてみてください (ゲームまたは Unity のワークロードのみを使用して開始してください)。
8. Unity 拡張機能に干渉する可能性がある場合は、`Tools / Extensions` でサードパーティ製の拡張機能を無効にしてみてください。

## <a name="extra-reloads-or-visual-studio-losing-all-open-windows"></a>余分な再読み込みが発生する、または Visual Studio で開いているウィンドウがすべて失われる

アセット プロセッサなどのツールから直接プロジェクト ファイルに触れないようにしてください。 プロジェクト ファイルをどうしても操作する必要がある場合は、弊社でそのための API を公開します。 「[アセンブリ参照の問題](#assembly-reference-or-project-property-issues)」セクションを確認してください。

余分な再読み込みが発生する場合、または Visual Studio で再読み込み時に開いているウィンドウがすべて失われる場合は、適切な .NET Targeting Pack がインストールされていることを確認してください。 詳細については、フレームワークに関する以下のセクションを確認してください。

## <a name="the-debugger-does-not-break-on-exceptions"></a>例外でデバッガーが中断しない

従来の Unity ランタイム (.NET 3.5 に相当) を使用しているときに、例外が処理されない (try/catch ブロックの外側にある) 場合、デバッガーは常に中断します。 例外が処理される場合、デバッガーは例外設定ウィンドウを使用して、中断が必要かどうかを判断します。

新しいランタイム (.NET 4.6 に相当) では、Unity でユーザー例外を管理するための新しい方法が導入されました。その結果、try/catch ブロックの外側にある場合でも、例外はすべて "ユーザーによる処理" と見なされます。 そのため、デバッガーを中断させる場合は、例外設定ウィンドウで明示的に確認する必要があります。

例外設定ウィンドウ ([デバッグ] > [ウィンドウ] > [例外設定]) で、例外のカテゴリのノード (たとえば、[共通言語ランタイム例外]、つまり、.NET に関する例外) を展開し、そのカテゴリ内のキャッチする特定の例外 (たとえば、System.NullReferenceException) のチェックボックスをオンにします。 例外のカテゴリ全体を選択することもできます。

## <a name="on-windows-visual-studio-asks-to-download-the-unity-target-framework"></a>Windows の場合に Unity ターゲット フレームワークをダウンロードするよう Visual Studio から求められる

レガシ Unity ランタイム (.NET 3.5 に相当) を使用している場合、Visual Studio Tools for Unity には .NET framework 3.5 が必要ですが、これは、Windows 8 または 10 では既定でインストールされません。 この問題を解決するには、.NET Framework 3.5 のダウンロードとインストールに関する手順に従ってください。

新しい Unity ランタイムを使用している場合、Unity のバージョンによっては、.NET Targeting Pack のバージョン 4.6 または 4.7.1 も必要になります。 Visual Studio インストーラーを使用すると、インストールをすばやく実行することができます (インストール、個々のコンポーネント、.NET カテゴリを変更して、4.x Targeting Pack をすべて選択します)。

## <a name="assembly-reference-or-project-property-issues"></a>アセンブリ参照またはプロジェクト プロパティの問題

プロジェクトの参照が複雑な場合、またはこの生成ステップをいっそう適切に制御したい場合は、[API](../extensibility/customize-project-files-created-by-vstu.md) を使って、生成されるプロジェクトまたはソリューションのコンテンツを操作できます。 また、Unity プロジェクトで[応答ファイル](https://docs.unity3d.com/Manual/PlatformDependentCompilation.html)を使って処理を任せることもできます。

Visual Studio と Unity の最近のバージョンでは、生成されたプロジェクトと共に、カスタムの `Directory.Build.props` ファイルを使用することをお勧めします。 これにより、生成プロセスに干渉することなく、プロジェクトの構造を強化できるようになります。 詳細情報は [こちら](https://docs.microsoft.com/visualstudio/msbuild/customize-your-build#directorybuildprops-and-directorybuildtargets)です。

## <a name="breakpoints-with-a-warning"></a>ブレークポイントでの警告

Visual Studio が特定のブレークポイントのソースの場所を見つけられない場合、ブレークポイントの周囲に警告が表示されます。 使っているスクリプトが現在の Unity シーンに正しく読み込まれて使われていることを確認してください。

## <a name="breakpoints-not-hit"></a>ブレークポイントがヒットない

使っているスクリプトが現在の Unity シーンに正しく読み込まれて使われていることを確認してください。 Visual Studio と Unity の両方を終了し、すべての生成されたファイル (\*.csproj、\*.sln)、`.vs` フォルダー、および Library フォルダー全体を削除します。 C# のデバッグについて詳しくは、Unity の [Web サイト](https://docs.unity3d.com/Manual/ManagedCodeDebugging.html)をご覧ください。

## <a name="unable-to-debug-android-players"></a>Android プレーヤーをデバッグできない

プレーヤーの検出にはマルチキャストが使われていますが (Unity で使われる既定のメカニズム)、その後で通常の TCP 接続を使ってデバッガーをアタッチします。 検出フェーズが Android デバイスの主な問題です。

Wi-Fi は高い汎用性を備えていますが、待機時間のため USB と比べると非常に低速です。 一部のルーターまたはデバイス (よく知られているのは Nexus シリーズ) では、マルチキャストが適切にサポートされていないことがわかっています。

USB はデバッグに関しては超高速です。Visual Studio Tools for Unity では USB デバイスを検出し、デバッグのために適切にポートを転送するよう adb サーバーに指示できるようになりました。

## <a name="issues-with-intellisense-or-code-coloration"></a>IntelliSense またはコード配色の問題

Visual Studio を最新バージョンにアップグレードしてみてください。 [互換性のないプロジェクト](#incompatible-project-in-visual-studio)の場合と同じトラブルシューティング手順を試してください。

## <a name="known-issues"></a>既知の問題

デバッガーが Unity の古いバージョンの C# コンパイラとやり取りする方法に起因する、Visual Studio Tools for Unity の既知の問題があります。 これらの問題を修正するために作業中ですが、修正されるまでは以下の問題が発生する可能性があります。

- デバッグ時に Unity がクラッシュすることがあります。

- デバッグ時に Unity がフリーズすることがあります。

- メソッドのステップインとステップアウトが正しく動作しないことがあります。特に、反復子または switch ステートメント内でこれが生じる可能性があります。

## <a name="report-errors"></a>レポート エラー

クラッシュ、フリーズ、またはその他のエラーが発生する場合、エラー レポートを送信することによって、Visual Studio Tools for Unity の品質向上にご協力ください。 Visual Studio Tools for Unity における問題の調査と解決に役立ちます。 ご協力に感謝いたします。

### <a name="how-to-report-an-error-when-visual-studio-freezes"></a>Visual Studio がフリーズする場合にエラーを報告する方法

Visual Studio Tools for Unity でデバッグすると Visual Studio がフリーズするという報告を受け取っていますが、問題を把握するためにさらにデータを必要としています。 次の手順を実行していただくと、調査に役立ちます。

##### <a name="to-report-that-visual-studio-freezes-while-debugging-with-visual-studio-tools-for-unity"></a>Visual Studio Tools for Unity でデバッグすると Visual Studio がフリーズすることを報告する方法

*Windows の場合:*

1. Visual Studio の新しいインスタンスを開きます。

1. [プロセスにアタッチ] ダイアログ ボックスを開きます。 Visual Studio の新しいインスタンスのメイン メニューで、 **[デバッグ]** 、 **[プロセスにアタッチ]** を選択します。

1. Visual Studio のフリーズしたインスタンスに、デバッガーをアタッチします。 **[プロセスにアタッチ]** ダイアログ ボックスで、 **[選択可能なプロセス]** テーブルからフリーズした Visual Studio インスタンスを選択し、 **[アタッチ]** ボタンを選択します。

1. デバッガーを一時停止します。 Visual Studio の新しいインスタンスのメイン メニューで **[デバッグ]** 、 **[すべて中断]** を選ぶか、単に **Ctrl + Alt + Break** キーを押します。

1. スレッド ダンプを作成します。 コマンド ウィンドウで、次のコマンドを入力して **Enter** キーを押します。

    ```powershell
    Debug.ListCallStack /AllThreads /ShowExternalCode
    ```

    最初に **[コマンド]** ウィンドウを表示しなければならない場合もあります。 Visual Studio のメイン メニューで、 **[ビュー]** 、 **[その他のウィンドウ]** 、 **[コマンド ウィンドウ]** の順に選択します。

*Mac の場合:*

1. ターミナルを開き、Visual Studio for Mac の PID を取得します。

    ```shell
    ps aux | grep "[V]isual Studio.app"
    ```

1. lldb デバッガーを起動します。

    ```shell
    lldb
    ```

1. PID を使って Visual Studio for Mac のインスタンスにアタッチします。

    ```shell
    process attach --pid THE_PID_OF_THE_VSFM_PROCESS
    ```

1. すべてのスレッドの StackTrace を取得します。

    ```shell
    bt all
    ```

最後に、Visual Studio がフリーズ状態になったときに実行していた作業内容に関する説明を添えて、スレッド ダンプを [vstusp@microsoft.com](mailto:vstusp@microsoft.com)に送信します。

## <a name="see-also"></a>関連項目

- [Visual Studio トラブルシューティング](/troubleshoot/visualstudio/welcome-visual-studio/)
