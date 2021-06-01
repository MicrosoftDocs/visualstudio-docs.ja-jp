---
title: 機能拡張プロジェクトを Visual Studio 2017 に移行する
titleSuffix: ''
description: 機能拡張プロジェクトを Visual Studio 2017 にアップグレードする方法と、拡張機能マニフェスト バージョン 2 からバージョン 3 VSIX マニフェストにアップグレードする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/09/2016
ms.topic: how-to
ms.assetid: 8ca07b00-a3ff-40ab-b647-c0a93b55e86a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
monikerRange: vs-2017
ms.openlocfilehash: d50624dc4c0d96c20323afb3c7d065121a4baacb
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105069973"
---
# <a name="how-to-migrate-extensibility-projects-to-visual-studio-2017"></a>方法: 機能拡張プロジェクトを Visual Studio 2017 に移行する

このドキュメントでは、機能拡張プロジェクトを Visual Studio 2017 にアップグレードする方法について説明します。 プロジェクト ファイルを更新する方法について説明するだけでなく、拡張機能マニフェスト バージョン 2 (VSIX v2) から新しいバージョン 3 VSIX マニフェスト形式 (VSIX v3) にアップグレードする方法についても説明します。

## <a name="install-visual-studio-2017-with-required-workloads"></a>必要なワークロードを含む Visual Studio 2017 をインストールする

インストールに次のワークロードが含まれていることを確認します。

* .NET デスクトップ開発
* Visual Studio 拡張機能の開発

## <a name="open-vsix-solution-in-visual-studio-2017"></a>Visual Studio 2017 で VSIX ソリューションを開く

すべての VSIX プロジェクトは、Visual Studio 2017 への一方向のメジャー バージョン アップグレードが必要になります。

プロジェクト ファイル (たとえば、* *.csproj* ) は次のように更新されます。

* MinimumVisualStudioVersion - 15.0 に設定されます
* OldToolsVersion (既に存在する場合) - 14.0 に設定されます

## <a name="update-the-microsoftvssdkbuildtools-nuget-package"></a>Microsoft.VSSDK.BuildTools NuGet パッケージを更新する

> [!Note]
> ソリューションから Microsoft.VSSDK.BuildTools NuGet パッケージを参照していない場合は、この手順をスキップできます。

拡張機能を新しい VSIX v3 (バージョン 3) 形式でビルドするには、新しい VSSDK ビルド ツールを使用してソリューションをビルドする必要があります。 これは Visual Studio 2017 と共にインストールされますが、NuGet を介して以前のバージョンへの参照が VSIX v2 拡張機能に保持されている可能性があります。 その場合は、ソリューションの Microsoft.VSSDK.BuildTools NuGet パッケージの更新プログラムを手動でインストールする必要があります。

Microsoft.VSSDK.BuildTools への NuGet 参照を更新するには:

* ソリューションを右クリックし、 **[ソリューションの NuGet パッケージの管理]** を選択します。
* **[更新プログラム]** タブに移動します。
* **Microsoft.VSSDK.BuildTools (最新バージョン)** を選択します。
* **[更新]** を押します。

![VSSDK ビルド ツール](media/vssdk-build-tools.png)

## <a name="make-changes-to-the-vsix-extension-manifest"></a>VSIX 拡張機能マニフェストに変更を加える

Visual Studio のユーザーのインストールに、拡張機能の実行に必要なすべてのアセンブリを確実に含めるには、拡張機能マニフェスト ファイルにすべての必須コンポーネントまたはパッケージを指定します。 ユーザーが拡張機能をインストールしようとすると、VSIXInstaller により、すべての必須コンポーネントがインストールされているかどうかが確認されます。 一部が不足している場合、ユーザーは、拡張機能のインストール プロセスの一部として不足しているコンポーネントをインストールするように求められます。

> [!Note]
> 少なくとも、すべての拡張機能に必須コンポーネントとして Visual Studio コア エディター コンポーネントを指定する必要があります。

* 拡張機能マニフェスト ファイル (通常は *source.extension.vsixmanifest* と呼ばれます) を編集します。
* `InstallationTarget` に必ず 15.0 を含めます。
* 必要なインストールの必須コンポーネントを追加します (次の例を参照してください)。
  * インストールの必須コンポーネントには、コンポーネント ID のみを指定することをお勧めします。
  * [コンポーネント ID の識別に関する手順](#find-component-ids)については、このドキュメントの最後にあるセクションを参照してください。

例:

```xml
<PackageManifest>
 ...
    <Prerequisites>
        <Prerequisite Id="Microsoft.VisualStudio.Component.CoreEditor" Version="[15.0,16.0)" />
        <Prerequisite Id="Microsoft.VisualStudio.Component.DiagnosticTools" Version="[15.0.25814.0,16.0)" />
        <Prerequisite Id="Microsoft.VisualStudio.Shell.12.0" Version="[12.0]" />
    </Prerequisites>
 ...
</PackageManifest>
```

### <a name="option-use-the-designer-to-make-changes-to-the-vsix-extension-manifest"></a>省略可能: デザイナーを使用して、VSIX 拡張機能マニフェストに変更を加える

マニフェスト XML を直接編集する代わりに、マニフェスト デザイナーの新しい **[必須コンポーネント]** タブを使用して必須コンポーネントを選択すると、XML が更新されます。

> [!Note]
> マニフェスト デザイナーでは、現在の Visual Studio インスタンスにインストールされている (ワークロードやパッケージではなく) コンポーネントのみを選択できます。 現在インストールされていないワークロード、パッケージ、またはコンポーネントの必須コンポーネントを追加する必要がある場合は、マニフェストの XML を直接編集します。

* *source.extension.vsixmanifest [Design]* ファイルを開きます。
* **[必須コンポーネント]** タブを選択し、 **[新規]** ボタンを押します。

   ![VSIX マニフェスト デザイナー](media/vsix-manifest-designer.png)

* **[新しい前提条件の追加]** ウィンドウが開きます。

   ![vsix の必須コンポーネントを追加する](media/add-vsix-prerequisite.png)

* **[名前]** のドロップダウンをクリックして、目的の必須コンポーネントを選択します。
* 必要に応じてバージョンを更新します。

   > [!Note]
   > バージョン フィールドには、現在インストールされているコンポーネントのバージョンがあらかじめ設定されています。範囲は、そのコンポーネントの次のメジャー バージョンの前までです。

   ![roslyn の必須コンポーネントを追加する](media/add-roslyn-prerequisite.png)

* **[OK]** を押します。

## <a name="update-debug-settings-for-the-project"></a>プロジェクトの [デバッグ設定] を更新する

Visual Studio の実験用インスタンスで拡張機能をデバッグする場合は、 **[デバッグ]**  >  **[開始アクション]** のプロジェクト設定で、 **[外部プログラムの開始]** 値を Visual Studio 2017 インストールの *devenv.exe* ファイルに設定します。

これは *C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise\Common7\IDE\devenv.exe* のようになります

![外部プログラムの開始](media/start-external-program.png)

> [!Note]
> 通常、デバッグの開始アクションは *.csproj.user* ファイルに格納されています。 一般的に、このファイルは *.gitignore* ファイルに含まれているため、ソース管理にコミットするときに他のプロジェクト ファイルと共に保存されることは通常はありません。 そのため、ソース管理からソリューションを新たにプルした場合、プロジェクトの開始アクションに値が設定されていない可能性があります。 Visual Studio 2017 を使用して作成された新しい VSIX プロジェクトには、現在の Visual Studio インストール ディレクトリを指す既定値を使用して作成された *.csproj.user* ファイルが含まれます。 ただし、VSIX v2 拡張機能を移行する場合は、 *.csproj.user* ファイルに以前の Visual Studio バージョンのインストール ディレクトリへの参照が含まれる可能性があります。 **[デバッグ]**  >  **[開始アクション]** の値を設定すると、拡張機能をデバッグしようとしたときに、正しい Visual Studio 実験用インスタンスを起動することができます。

## <a name="check-that-the-extension-builds-correctly-as-a-vsix-v3"></a>拡張機能が (VSIX v3 として) 正しくビルドされることを確認する

* VSIX プロジェクトをビルドします。
* 生成された VSIX を展開します。
  * 既定で、VSIX ファイルは *bin/Debug* または *bin/Release* 内に *[YourCustomExtension].vsix* という名前で存在します。
  * 内容を簡単に確認できるように、 *.vsix* の名前を *.zip* に変更します。
* 次の 3 つのファイルが存在することを確認します。
  * *extension.vsixmanifest*
  * *manifest.json*
  * *catalog.json*

## <a name="check-when-all-required-prerequisites-are-installed"></a>必須コンポーネントがすべてインストールされていることを確認する

必要なすべての必須コンポーネントがインストールされているマシンに、VSIX が正常にインストールされていることをテストします。

> [!Note]
> 拡張機能をインストールする前に、Visual Studio のすべてのインスタンスをシャットダウンしてください。

次の拡張機能のインストールを試みます。

* Visual Studio 2017 の場合

![Visual Studio 2017 上の VSIX インストーラー](media/vsixinstaller-vs-2017.png)

* 省略可能: 以前のバージョンの Visual Studio を確認します。
  * 下位互換性を証明する。
  * Visual Studio 2012、Visual Studio 2013、Visual Studio 2015 上で動作する必要がある。
* 省略可能:VSIX インストーラー バージョン チェッカーにバージョンの選択肢が表示されていることを確認します。
  * 以前のバージョンの Visual Studio が含まれている (インストールされている場合)。
  * Visual Studio 2017 が含まれている。

Visual Studio を最近開いた場合は、次のようなダイアログ ボックスが表示されることがあります。

![vs の実行中のプロセス](media/vs-running-processes.png)

プロセスがシャットダウンするのを待つか、手動でタスクを終了します。 表示されている名前、またはかっこ内に表示されている PID を使用してプロセスを見つけることができます。

> [!Note]
> Visual Studio のインスタンスの実行中に、これらのプロセスによって自動的にシャットダウンされることはありません。 マシン上の Visual Studio のすべてのインスタンス (他のユーザーによるものを含む) をシャットダウンしたことを確認してから、再試行を続けます。

## <a name="check-when-missing-the-required-prerequisites"></a>必須コンポーネントが不足している場合を確認する

* (前述の) 「必須コンポーネント」に定義されているすべてのコンポーネントを "含まない"、Visual Studio 2017 がインストールされたマシンに拡張機能をインストールしてみてください。
* インストールによって、不足しているコンポーネントが特定され、VSIXInstaller の必須コンポーネントとして表示されることを確認します。
* 注: 拡張機能と共に必須コンポーネントをインストールする必要がある場合は、昇格が必要になります。

![vsixinstaller の不足している必須コンポーネント](media/vsixinstaller-missing-prerequisite.png)

## <a name="decide-on-components"></a>コンポーネントについて決定する

依存関係を調べると、1 つの依存関係が複数のコンポーネントにマップされる可能性があることがわかります。 必須コンポーネントとして指定する必要がある依存関係を決定するには、拡張機能と同様の機能を持つコンポーネントを選択し、ユーザーと、どのようなコンポーネントをインストールしているか、またはインストールしても構わないかを考慮することも必要です。 また、必要なコンポーネントは、拡張機能が動作するために必要な最小限のものだけを満たし、追加機能については、特定のコンポーネントが検出されない場合は休止するような方法で拡張機能を構築することをお勧めします。

さらにガイダンスを提供するために、いくつかの一般的な拡張機能の種類とそれらの推奨される必須コンポーネントを特定しました。

拡張機能の種類 | 表示名 | id
--- | --- | ---
エディター | Visual Studio のコア エディター | Microsoft.VisualStudio.Component.CoreEditor
Roslyn | C# および Visual Basic | Microsoft.VisualStudio.Component.Roslyn.LanguageServices
WPF | Managed Desktop Workload コア | Microsoft.VisualStudio.Component.ManagedDesktop.Core
デバッガー | Just-In-Time デバッガー | Microsoft.VisualStudio.Component.Debugger.JustInTime

## <a name="find-component-ids"></a>コンポーネント ID を検索する

Visual Studio 製品で並べ替えられたコンポーネントの一覧については、[Visual Studio 2017 のワークロードとコンポーネント ID](../install/workload-and-component-ids.md?view=vs-2019&preserve-view=true) に関するページを参照してください。 マニフェストの必須コンポーネント ID には、これらのコンポーネント ID を使用します。

特定のバイナリが含まれているコンポーネントがわからない場合は、[コンポーネント -> バイナリのマッピング スプレッドシート](https://aka.ms/vs2017componentid-binaries)をダウンロードします。

### <a name="vs2017-componentbinarymappingxlsx"></a>vs2017-ComponentBinaryMapping.xlsx

この Excel シートには、**Component Name**、**ComponentId**、**Version**、および **Binary / File Names** という 4 つの列があります。  フィルターを使用して、特定のコンポーネントとバイナリを検索して見つけることができます。

すべての参照について、まずコア エディター (Microsoft.VisualStudio.Component.CoreEditor) コンポーネント内にあるものを特定します。  少なくとも、すべての拡張機能の必須コンポーネントとしてコア エディター コンポーネントを指定する必要があります。 コア エディターにない残りの参照のうち、**Binaries / Files Names** セクションにフィルターを追加し、それらの参照のサブセットのいずれかを持つコンポーネントを検索します。

例 :

* デバッガーの拡張機能があり、プロジェクトに *VSDebugEng.dll* および *VSDebug.dll* への参照があることがわかっている場合は、**Binaries / Files Names** ヘッダーのフィルター ボタンをクリックします。  「VSDebugEng.dll」を検索し、 *[OK]* を選択します。  次に、**Binaries / Files Names** ヘッダーのフィルター ボタンをもう一度クリックして、「VSDebug.dll」を検索します。  **[Add current selection to filter]\(現在の選択項目をフィルターに追加する\)** チェックボックスをオンにして、 **[OK]** を選択します。  次に、 **[コンポーネント名]** を調べて、拡張機能の種類に最も関係のあるコンポーネントを見つけます。 この例では、Just-In-Time デバッガーを選択し、それを vsixmanifest に追加します。
* プロジェクトでデバッガー要素が処理されることがわかっている場合は、フィルター検索ボックスで「debugger」について検索し、名前に debugger が含まれているコンポーネントを確認できます。

## <a name="specify-a-visual-studio-2017-release"></a>Visual Studio 2017 リリースを指定する

拡張機能に特定のバージョンの Visual Studio 2017 が必要な場合、たとえば、15.3 でリリースされた機能に依存している場合は、VSIX **InstallationTarget** でビルド番号を指定する必要があります。 たとえば、リリース 15.3 のビルド番号は '15.0.26730.3' です。 [ここで](../install/visual-studio-build-numbers-and-release-dates.md)、リリースからビルド番号へのマッピングを確認できます。 リリース番号 '15.3' を使用しても適切に機能しません。

拡張機能に 15.3 以降が必要な場合は、**InstallationTarget Version** を次のように [15.0.26730.3, 16.0) として宣言します。

```xml
<Installation>
  <InstallationTarget Id="Microsoft.VisualStudio.Community" Version="[15.0.26730.3, 16.0)" />
</Installation>
```