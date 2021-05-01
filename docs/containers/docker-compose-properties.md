---
title: Docker Compose のビルド設定
author: ghogen
description: Visual Studio による Docker Compose アプリケーションのビルドおよび実行方法をカスタマイズする目的で Docker Compose のビルド プロパティを編集する方法について説明します。
ms.custom: SEO-VS-2020
ms.author: ghogen
ms.date: 04/06/2021
ms.technology: vs-azure
ms.topic: reference
ms.openlocfilehash: ed4b2a0dc1dc7a0520bf8e83ab1968a3815196e0
ms.sourcegitcommit: e12d6cdaeb37564f05361965db2ec8ad0d4f21ad
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/27/2021
ms.locfileid: "108025866"
---
# <a name="docker-compose-build-properties"></a>Docker Compose のビルド プロパティ

「[コンテナー ツールのビルド プロパティ](container-msbuild-properties.md)」で説明している、個々の Docker プロジェクトを制御するプロパティに加え、ソリューション構築のために MSBuild で使用される Docker Compose プロパティを設定することで、Visual Studio による Docker Compose プロジェクトのビルド方法をカスタマイズすることもできます。 Docker Compose 構成ファイルでファイル ラベルを設定することで、Visual Studio デバッガーによる Docker Compose アプリの実行方法を制御することもできます。

## <a name="how-to-set-the-msbuild-properties"></a>MSBuild プロパティの設定方法

プロパティの値を設定するには、プロジェクト ファイルを編集します。 Docker Compose プロパティの場合、このプロジェクトファイルは、次のセクションの表で特に指定されていない限り、拡張子が .dcproj のプロジェクト ファイルです。 たとえば、デバッグを開始するときにブラウザーを起動するように指定するとします。 次のように、.dcproj プロジェクト ファイル内で `DockerLaunchAction` プロパティを設定できます。

```xml
<PropertyGroup>
   <DockerLaunchAction>LaunchBrowser</DockerLaunchAction>
</PropertyGroup>
```

プロパティ設定を既存の `PropertyGroup` 要素に追加できます。存在しない場合は、新しい `PropertyGroup` 要素を作成できます。

## <a name="docker-compose-msbuild-properties"></a>Docker Compose MSBuild のプロパティ

次の表は、Docker Compose プロジェクトで使用できる MSBuild プロパティを示しています。

| プロパティ名 | 場所 | 説明 | 既定値  |
|---------------|----------|-------------|----------------|
|AdditionalComposeFilePaths|dcproj|すべてのコマンドで docker-compose.exe に追加の Compose ファイルがセミコロンで区切られたリストで送信されるように指定します。 docker-compose プロジェクト ファイル (dcproj) からの相対パスが許可されます。|-|
|DockerComposeBaseFilePath|dcproj|docker-compose ファイルのファイル名の最初の部分を *.yml* 拡張子なしで指定します。 次に例を示します。 <br>1. DockerComposeBaseFilePath = null または未定義: 基本ファイル パス *docker-compose* を使用し、ファイル名は *docker-compose.yml* と *docker-compose.override.yml* になります。<br>2. DockerComposeBaseFilePath = *mydockercompose*: ファイル名は *mydockercompose.yml* と *mydockercompose.override.yml* になります。<br> 3. DockerComposeBaseFilePath = *..\mydockercompose*: ファイルは 1 レベル上になります。 |docker-compose|
|DockerComposeBuildArguments|dcproj|`docker-compose build` コマンドに渡す追加のパラメーターを指定します。 たとえば、「 `--parallel --pull` 」のように入力します。 |
|DockerComposeDownArguments|dcproj|`docker-compose down` コマンドに渡す追加のパラメーターを指定します。 たとえば、「 `--timeout 500` 」のように入力します。|-|  
|DockerComposeProjectName| dcproj | 指定した場合、docker-compose プロジェクトのプロジェクト名がオーバーライドされます。 | "dockercompose" + 自動生成されたハッシュ |
|DockerComposeProjectPath|csproj または vbproj|docker-compose プロジェクト (dcproj) ファイルの相対パス。 docker-compose.yml ファイルに格納されている関連イメージ ビルド設定を見つける目的で、サービス プロジェクトの公開時にこのプロパティを設定します。|-|
|DockerComposeProjectsToIgnore|dcproj| プロジェクトがデバッグ中に docker-compose ツールによって無視されるように指定します。 このプロパティは、任意のプロジェクトに使用できます。 ファイル パスは、次の 2 つの方法のどちらかで指定できます。 <br> 1. dcproj を基準として。 たとえば、「 `<DockerComposeProjectsToIgnore>path\to\AngularProject1.csproj</DockerComposeProjectsToIgnore>` 」のように入力します。 <br> 2. 絶対パス。<br> **注**: これらのパスは、区切り文字 `;` で区切る必要があります。|-|
|DockerComposeUpArguments|dcproj|`docker-compose up` コマンドに渡す追加のパラメーターを指定します。 たとえば、「 `--timeout 500` 」のように入力します。|-|
|DockerDevelopmentMode| dcproj | ユーザー プロジェクトをコンテナーにビルドするかどうかを制御します。 **Fast** または **Regular** の許可される値によって、Dockerfile で[どのステージがビルドされるか](https://aka.ms/containerfastmode)が制御されます。 デバッグ構成は、既定では Fast モードであり、それ以外の場合は Regular モードです。 | Fast |
|DockerLaunchAction| dcproj | F5 または Ctrl + F5 キーで実行する起動アクションを指定します。  指定できる値には、None、LaunchBrowser、LaunchWCFTestClient があります。 | None |
|DockerLaunchBrowser| dcproj | ブラウザーを起動するかどうかを示します。 DockerLaunchAction が指定されている場合は無視されます。 | False |
|DockerServiceName| dcproj| DockerLaunchAction または DockerLaunchBrowser が指定されている場合、DockerServiceName では、docker-compose ファイルで参照されているどのサービスが起動されるかを指定します。|-|
|DockerServiceUrl| dcproj | ブラウザーを起動するときに使用される URL。  有効な置換トークンには、"{ServiceIPAddress}"、"{ServicePort}"、"{Scheme}" があります。  例: {Scheme}://{ServiceIPAddress}:{ServicePort}|-|
|DockerTargetOS| dcproj | Docker イメージをビルドするときに使用されるターゲット OS。|-|

## <a name="example"></a>例

`DockerComposeBaseFilePath` を相対パスに設定することによって、Docker Compose ファイルの場所を変更する場合は、ソリューション フォルダーを参照するように、ビルド コンテキストが変更されていることを確認することも必要です。 たとえば、ご利用の Docker Compose ファイルが *DockerComposeFiles* という名前のフォルダーである場合、Docker Compose ファイルでは、ソリューション フォルダーに対するそれの位置に応じて、ビルド コンテキストが ".." または "../.." に設定される必要があります。

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project ToolsVersion="15.0" Sdk="Microsoft.Docker.Sdk">
  <PropertyGroup Label="Globals">
    <ProjectVersion>2.1</ProjectVersion>
    <DockerTargetOS>Windows</DockerTargetOS>
    <ProjectGuid>154022c1-8014-4e9d-bd78-6ff46670ffa4</ProjectGuid>
    <DockerLaunchAction>LaunchBrowser</DockerLaunchAction>
    <DockerServiceUrl>{Scheme}://{ServiceIPAddress}{ServicePort}</DockerServiceUrl>
    <DockerServiceName>webapplication1</DockerServiceName>
    <DockerComposeBaseFilePath>DockerComposeFiles\mydockercompose</DockerComposeBaseFilePath>
    <AdditionalComposeFilePaths>AdditionalComposeFiles\myadditionalcompose.yml</AdditionalComposeFilePaths>
  </PropertyGroup>
  <ItemGroup>
    <None Include="DockerComposeFiles\mydockercompose.override.yml">
      <DependentUpon>DockerComposeFiles\mydockercompose.yml</DependentUpon>
    </None>
    <None Include="DockerComposeFiles\mydockercompose.yml" />
    <None Include=".dockerignore" />
  </ItemGroup>
</Project>
```

ビルド コンテキストがソリューション フォルダーの相対パスに設定された状態 (この場合は `..`) では、*mydockercompose* ファイルは次のようになります。

```yml
version: '3.4'

services:
  webapplication1:
    image: ${DOCKER_REGISTRY-}webapplication1
    build:
      context: ..
      dockerfile: WebApplication1\Dockerfile
```

> [!NOTE]
> Visual Studio 2019 バージョン 16.3 では、DockerComposeBuildArguments、DockerComposeDownArguments、DockerComposeUpArguments が新しく追加されています。

## <a name="overriding-visual-studios-docker-compose-configuration"></a>Visual Studio の Docker Compose 構成のオーバーライド

*docker-compose.yml* ファイルと同じディレクトリ内に *docker-compose.vs.debug.yml* (**Fast** モードの場合) または *docker-compose.vs.release.yml* (**Regular** モードの場合) という名前のファイルを置くことによって、特定の設定をオーバーライドできます。 

>[!TIP] 
>これらのいずれかの設定の既定値を見つけるには、*docker-compose.vs.debug.g.yml* または *docker-compose.vs.release.g.yml* 内を調べてください。

### <a name="docker-compose-file-labels"></a>Docker Compose ファイル ラベル

 *docker-compose.vs.debug.yml* または *docker-compose.vs.release.yml* で、オーバーライド固有のラベルを次のように定義できます。

```yml
services:
  webapplication1:
    labels:
      com.microsoft.visualstudio.debuggee.workingdirectory: "C:\\my_app_folder"
```

前の例のように値を二重引用符で囲み、パスでバックスラッシュのエスケープ文字としてバックスラッシュを使用します。

|ラベル名|説明|
|----------|-----------|
|com.microsoft.visualstudio.debuggee.arguments|デバッグの開始時にプログラムに渡される引数。 .NET Core アプリの場合、通常、これらの引数は NuGet パッケージの追加検索パスであり、これにプロジェクトの出力アセンブリのパスが続きます。|
|com.microsoft.visualstudio.debuggee.program|デバッグの開始時に起動するプログラム。 .NET Core アプリの場合、この設定は通常、**dotnet** です。|
|com.microsoft.visualstudio.debuggee.workingdirectory|デバッグの開始時に開始ディレクトリとして使用されるディレクトリ。 この設定は通常、Linux コンテナーの場合は */app*、Windows コンテナーの場合は *C:\app* になります。|
|com.microsoft.visualstudio.debuggee.killprogram|このコマンドは、(必要なときに) コンテナー内で実行されているデバッグ対象プログラムを停止する目的で使用されます。|

### <a name="customize-the-docker-build-process"></a>Docker ビルド プロセスをカスタマイズする

`build` プロパティの `target` 設定を使用して、Dockerfile でどのステージをビルドするかを宣言できます。 このオーバーライドは、*docker-compose.vs.debug.yml* または *docker-compose.vs.release.yml* でのみ使用できます。 

```yml
services:
  webapplication1:
    build:
      target: customStage
    labels:
      ...
```

### <a name="customize-the-app-startup-process"></a>アプリのスタートアップ プロセスをカスタマイズする

`entrypoint` 設定を使用し、それを `DockerDevelopmentMode` に依存させることによって、アプリの起動前にコマンドまたはカスタム スクリプトを実行できます。 たとえば、`update-ca-certificates` を実行することによって (**Regular** モードではなく) **Fast** モードでのみ証明書を設定する必要がある場合は、次のコードを *docker-compose.vs.debug.yml* に **のみ** 追加することができます。

```yml
services:
  webapplication1:
    entrypoint: "sh -c 'update-ca-certificates && tail -f /dev/null'"
    labels:
      ...
```

## <a name="next-steps"></a>次の手順

MSBuild プロパティの一般情報については、[MSBuild プロパティ](../msbuild/msbuild-properties.md)を参照してください。

## <a name="see-also"></a>関連項目

[コンテナー ツールのビルド プロパティ](container-msbuild-properties.md)

[コンテナー ツールの起動設定](container-launch-settings.md)

[MSBuild の予約済みおよび既知のプロパティ](../msbuild/msbuild-reserved-and-well-known-properties.md)
