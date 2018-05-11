---
title: '方法: Visual Studio の拡張機能をラウンドトリップする| Microsoft Docs'
ms.custom: ''
ms.date: 06/25/2017
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
ms.assetid: 2d6cf53c-011e-4c9e-9935-417edca8c486
author: willbrown
ms.author: willbrown
manager: justinclareburt
ms.workload:
- willbrown
ms.openlocfilehash: 9d8d0dc2e5c8c95b5f2502ef5a48e6f97c26e289
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/16/2018
---
# <a name="how-to-make-extensions-compatible-with-visual-studio-2017-and-visual-studio-2015"></a>方法: 拡張機能を Visual Studio 2017 と Visual Studio 2015 に対応させる

このドキュメントでは、拡張機能プロジェクトを Visual Studio 2015 と Visual Studio 2017 間でラウンドトリップさせる方法について説明します。 このアップグレードを完了すると、Visual Studio 2015 と Visual Studio 2017 の両方でプロジェクトを開いてビルド、インストール、および実行できるようになります。  参考として、[ここ](https://github.com/Microsoft/VSSDK-Extensibility-Samples)に示された Microsoft の拡張機能の例に、Visual Studio 2015 と Visual Studio 2017 間でラウンドトリップできるいくつかの拡張機能が含まれています。

Visual Studio 2017 でのみビルドするが、Visual Studio 2015 と Visual Studio 2017 の両方で VSIX を出力したい場合は、[拡張機能の移行に関するドキュメント](how-to-migrate-extensibility-projects-to-visual-studio-2017.md)をご覧ください。

>**注:** Visual Studio のバージョン間での変更が原因で、あるバージョンで利用できた機能が別のバージョンでは利用できないことがあります。 アクセスしようとしている機能が、両方のバージョンで利用可能であることを確認してください。この確認を行わない場合、拡張機能で予期しない結果が発生します。

VSIX をラウンドトリップするためにこのドキュメントで実行する手順の概要を以下に示します。

1. 適切な NuGet パッケージをインポートします。
2. 拡張機能マニフェストを更新します。
    * インストールの対象
    * 必須コンポーネント
3. CSProj を更新します。
    * `<MinimumVisualStudioVersion>` を更新します。
    * `<VsixType>` プロパティを追加します。
    * デバッグ プロパティ `($DevEnvDir)` を 3 回追加します。
    * ビルド ツールをインポートするための条件と対象を追加します。

4. ビルドとテストを行います。

## <a name="environment-setup"></a>環境の設定

このドキュメントは、コンピューターに以下をインストール済みであることを前提としています。

* VS SDK がインストールされた Visual Studio 2015
* 拡張機能ワークロードがインストールされた Visual Studio 2017

## <a name="recommended-approach"></a>推奨されるアプローチ

このアップグレードは、Visual Studio 2017 ではなく、Visual Studio 2015 で開始することを強くお勧めします。 Visual Studio 2015 で開発を行う主な利点は、Visual Studio 2015 で利用できないアセンブリの参照を確実に排除できるという点です。 Visual Studio 2017 で開発を行うと、Visual Studio 2017 にのみ存在するアセンブリへの依存関係を導入してしまうリスクがあります。

## <a name="ensure-there-is-no-reference-to-projectjson"></a>project.json への参照を確実に排除する

このドキュメントの後半で、*.csproj ファイルに条件付きインポート ステートメントを挿入します。  これは、project.json に NuGet 参照が格納されていると機能しません。 そのため、すべての NuGet 参照を packages.config ファイルに移動することをお勧めします。
プロジェクトに project.json ファイルが含まれている場合は、次の手順に従います。

* project.json に含まれる参照をメモします。
* ソリューション エクスプローラーで、プロジェクトから project.json ファイルを削除します。
    * これにより project.json ファイルが削除され、プロジェクトから除去されます。
* プロジェクトに NuGet 参照を再度追加します。
    * ソリューションを右クリックし、**[ソリューションの NuGet パッケージの管理...]** を選択します。
    * Visual Studio によって packages.config ファイルが自動的に作成されます。

>**注:** プロジェクトに EnvDTE パッケージが含まれていた場合、**[参照]** を右クリックして **[参照の追加]** を選択し、適切な参照を追加して、このパッケージを追加することが必要な場合があります。  NuGet パッケージを使用すると、プロジェクトのビルドを試みたときにエラーが発生する可能性があります。

## <a name="adding-appropriate-build-tools"></a>適切なビルド ツールを追加する

ビルドとデバッグを正しく実行できるビルド ツールを確実に追加する必要があります。 そのために、Microsoft は Microsoft.VisualStudio.Sdk.BuildTasks というアセンブリを作成しました。

Visual Studio 2015 と 2017 の両方で VSIXv3 をビルドして展開するには、次の NuGet パッケージが必要となります。

Version | ビルド ツール
--- | ---
Visual Studio 2015 | Microsoft.VisualStudio.Sdk.BuildTasks.14.0
Visual Studio 2017 | Microsoft.VSSDK.BuildTool

次の手順に従います。

* NuGet パッケージ Microsoft.VisualStudio.Sdk.BuildTasks.14.0 をプロジェクトに追加します。
* プロジェクトに Microsoft.VSSDK.BuildTools が含まれていない場合は、追加します。
* Microsoft.VSSDK.BuildTools のバージョンが 15.x 以上であることを確認します。

## <a name="update-extension-manifest"></a>拡張機能マニフェストを更新する

### <a name="1-installation-targets"></a>1.インストールの対象

VSIX をビルドする対象のバージョンを Visual Studio に指示する必要があります。  通常、これらの参照は、バージョン 14.0 (Visual Studio 2015) またはバージョン 15.0 (Visual Studio 2017) への参照です。  ここでは、両方に対応する拡張機能をインストールする VSIX をビルドしたいので、両方のバージョンを対象にする必要があります。  14.0 より前のバージョンで VSIX をビルドおよびインストールしたい場合は、前のバージョン番号を設定すれば可能です。ただし、10.0 以前のバージョンはサポートされていません。

* Visual Studio で source.extension.vsixmanifest ファイルを開きます。
* **[Install Targets]\(インストールの対象)\** タブを開きます。
* **[バージョン範囲]** を [14.0, 16.0) 変更します。  '[' は、14.0 とそれより前のすべてのバージョンを含めるよう Visual Studio に指示します。  ')' は、15.0 までのすべてのバージョンを含めるが、バージョン 16.0 は含めないように Visual Studio に指示します。
* すべての変更を保存し、Visual Studio のすべてのインスタンスを閉じます。

![インストールの対象の画像](media/visual-studio-installation-targets-example.png)

### <a name="2-adding-prerequisites-to-the-extensionvsixmanifest-file"></a>2.extension.vsixmanifest ファイルに必須コンポーネントを追加する

必須コンポーネントは、Visual Studio 2017 からの新しい機能です。  ここでは、必須コンポーネントとして Visual Studio のコア エディターが必要です。 Visual Studio 2015 の VSIX デザイナーでは新しい `Prerequisites` セクションを処理しないため、XML コードでこの部分を 手動で編集する必要があります。  または、Visual Studio 2017 を開き、更新されたマニフェスト デザイナーを使用して必須コンポーネントを挿入することもできます。

この操作を手動で行うには、次の手順に従います。

* エクスプローラーでプロジェクト ディレクトリに移動します。
* テキスト エディターで `extension.vsixmanifest` ファイルを開きます。
* 次のタグを追加します。

```xml
<Prerequisites>
    <Prerequisite Id="Microsoft.VisualStudio.Component.CoreEditor" Version="[15.0,16.0)" DisplayName="Visual Studio core editor" />
</Prerequisites>
```

* ファイルを保存して閉じます。

>**注:** Visual Studio 2017 の VSIX デザイナーを使用してこの操作を行う場合は、必須コンポーネントのバージョンを手動で編集して、Visual Studio 2017 のすべてのバージョンに対応させる必要があります。  なぜならば、デザイナーは最小バージョンをVisual Studio の現在のバージョンとして挿入するからです (例: 15.0.26208.0)。  しかし、他のユーザーがそれより前のバージョンを使用している可能性があるため、これを 15.0 に編集する必要があります。

この時点で、マニフェスト ファイルは次のようになります。

![必須コンポーネントの例](media/visual-studio-prerequisites-example.png)

## <a name="modify-the-project-file-myprojectcsproj"></a>プロジェクト ファイル (myproject.csproj) を変更する

この手順を実行する間、変更した .csproj への参照を開いておくことを強くお勧めします。  [ここ](https://github.com/Microsoft/VSSDK-Extensibility-Samples)でいくつかの例を入手できます。  拡張機能のサンプルを選択し、参照の .csproj ファイルを見つけて次の手順を実行します。

* エクスプローラーでプロジェクト ディレクトリに移動します。
* テキスト エディターで myproject.csproj ファイルを開きます。

### <a name="1-update-the-minimumvisualstudioversion"></a>1.MinimumVisualStudioVersion を更新する

* Visual Studio の最小バージョンを `$(VisualStudioVersion)` に設定し、その条件付きステートメントを追加します。  以下のタグが存在しない場合は、追加します。  タグが次のように設定されていることを確認してください。

```xml
<VisualStudioVersion Condition="'$(VisualStudioVersion)' == ''">14.0</VisualStudioVersion>
<MinimumVisualStudioVersion>$(VisualStudioVersion)</MinimumVisualStudioVersion>
```

### <a name="2-add-the-vsixtype-property"></a>2.VsixType プロパティを追加する

* プロパティ グループに次のタグ `<VsixType>v3</VsixType>` を追加します。

>**注:** これは `<OutputType></OutputType>` タグの下に追加することをお勧めします。

### <a name="3-add-the-debugging-properties"></a>3.デバッグ プロパティを追加する

* 次のプロパティ グループを追加します。

```xml
<PropertyGroup>
    <StartAction>Program</StartAction>
    <StartPrograms>$(DevEnvDir)devenv.exe</StartPrograms>
    <StartArguments>/rootsuffix Exp</StartArguments>
</PropertyGroup>
```

* .csproj ファイルおよび .csproj.ユーザー ファイルから、次のすべてのインスタンスを削除します。

```xml
<StartAction>Program</StartAction>
<StartPrograms>$(ProgramFiles)\Microsoft Visual Studio 14.0\Common7\IDE\devenv.exe</StartPrograms>
<StartArguments>/rootsuffix Exp</StartArguments>
```

### <a name="4-add-conditions-to-the-build-tools-imports"></a>4.ビルド ツールのインポートに条件を追加する

* Microsoft.VSSDK.BuildTools 参照を含んでいる `<import>` タグに、その他の条件付きステートメントを追加します。  これを行うには、条件付きステートメントの前に `'$(VisualStudioVersion)' != '14.0' And` を挿入します。  これらのステートメントは、csproj ファイルのヘッダーとフッターに表示されます。

例えば:

```xml
<Import Project="packages\Microsoft.VSSDK.BuildTools.15.0.26201…" Condition="'$(VisualStudioVersion)' != '14.0' And Exists(…" />
```

* Microsoft.VisualStudio.Sdk.BuildTasks.14.0 を含んでいる `<import>` タグに、その他の条件付きステートメントを追加します。  これを行うには、条件付きステートメントの前に `'$(VisualStudioVersion)' == '14.0' And` を挿入します。 これらのステートメントは、csproj ファイルのヘッダーとフッターに表示されます。

例えば:

```xml
<Import Project="packages\Microsoft.VisualStudio.Sdk.BuildTasks.14.0.14.0…" Condition="'$(VisualStudioVersion)' == '14.0' And Exists(…" />
```

* Microsoft.VSSDK.BuildTools 参照を含んでいる `<Error>` タグに、その他の条件付きステートメントを追加します。  これを行うには、条件付きステートメントの前に `'$(VisualStudioVersion)' != '14.0' And` を挿入します。 これらのステートメントは、csproj ファイルのフッターに表示されます。

例えば:

```xml
<Error Condition="'$(VisualStudioVersion)' != '14.0' And Exists('packages\Microsoft.VSSDK.BuildTools.15.0.26201…" />
```

* Microsoft.VisualStudio.Sdk.BuildTasks.14.0 を含んでいる `<Error>` タグに、その他の条件付きステートメントを追加します。  これを行うには、条件付きステートメントの前に `'$(VisualStudioVersion)' == '14.0' And` を挿入します。 これらのステートメントは、csproj ファイルのフッターに表示されます。

例えば:

```xml
<Error Condition="'$(VisualStudioVersion)' == '14.0' And Exists('packages\Microsoft.VisualStudio.Sdk.BuildTasks.14.0.14.0…" />
```

* csproj ファイルを保存して閉じます。

## <a name="test-the-extension-installs-in-visual-studio-2015-and-visual-studio-2017"></a>Visual Studio 2015 と Visual Studio 2017 で拡張機能のインストールをテストする

この時点で、プロジェクトは Visual Studio 2015 と Visual Studio 2017 の両方にインストール可能な VSIXv3 をビルドできる状態になっているはずです。

* Visual Studio 2015 でプロジェクトを開きます。
* プロジェクトをビルドし、出力で VSIX が正しくビルドされていることを確認します。
* プロジェクトのディレクトリに移動します。
* [bin] -> [デバッグ] フォルダーを開きます。
* VSIX ファイルをダブルクリックし、Visual Studio 2015 と Visual Studio 2017 に拡張機能をインストールします。
* [ツール] -> [拡張機能と更新プログラム] の [インストール済み] セクションで、拡張機能が表示されていることを確認します。
* 拡張機能の実行/使用を試みて、機能することを確認します。

![VSIX の検索](media/finding-a-VSIX-example.png)

>**注:** "ファイルを開いています" というメッセージを表示してプロジェクトが停止した場合は、Visual Studio を強制的にシャットダウンしてプロジェクト ディレクトリに移動し、非表示のフォルダーを表示して、.vs フォルダーを削除します。
