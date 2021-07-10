---
title: Docker Compose プロジェクトの起動プロファイルを管理する
description: Docker Compose 起動プロファイルの使い方と、Visual Studio で Docker Compose を使用するときに起動するサービスの制御方法について説明します。
author: ghogen
manager: jmartens
ms.technology: vs-azure
ms.devlang: dotnet
ms.topic: how-to
ms.date: 05/10/2021
ms.author: ghogen
monikerRange: '>=vs-2019'
ms.openlocfilehash: e740ea3b7950c14bf11522c4e438a105b09eb7f6
ms.sourcegitcommit: ab5735d64a6ad7aecabf5d6df159888e3246bff5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2021
ms.locfileid: "111433702"
---
# <a name="manage-launch-profiles-for-docker-compose"></a>Docker Compose の起動プロファイルを管理する

複数のサービスで構成され、Docker Compose を使用するアプリケーションがある場合は、Docker Compose 起動設定で既存の起動プロファイルを作成または編集することで、実行およびデバッグするサービスを構成できます。 起動プロファイルを使用すると、現在のシナリオに関係するサービスのみを動的に実行できます。 デバッグ エクスペリエンスをカスタマイズし、`Browser Launch URL` などの特定の起動アクションを設定するための起動プロファイルを作成したり選択したりできます。 また、各サービスを個別に選択するか、Docker Compose プロファイルを選択することもできます。この場合、実行するサービスのグループを決定するために Compose ファイルも参照されます。

Docker Compose プロファイルの詳細については、「[Using profiles with Compose](https://docs.docker.com/compose/profiles/)」(Compose でのプロファイルの使用) を参照してください。
 
## <a name="prerequisites"></a>前提条件

- [Visual Studio 2019 バージョン 16.10](https://visualstudio.microsoft.com/vs/) 以降
- [Docker Compose によるコンテナーオーケストレーション](tutorial-multicontainer.md)を使用したソリューション

## <a name="manage-launch-settings"></a>起動設定を管理する

*docker-compose.yml* に 5 つのサービスと 3 つの Compose プロファイル (web、web1、web2) が含まれる次の Docker Compose プロジェクトについて考えてみてください。

```yml
version: '3.9'

services:
  webapplication1:
    image: ${DOCKER_REGISTRY-}webapplication1
    profiles: [web, web1]
    build:
      context: .
      dockerfile: WebApplication1/Dockerfile

  webapplication2:
    image: ${DOCKER_REGISTRY-}webapplication2
    profiles: [web, web2]
    build:
      context: .
      dockerfile: WebApplication2/Dockerfile

  webapplication3:
    image: ${DOCKER_REGISTRY-}webapplication3
    profiles: [web]
    build:
      context: .
      dockerfile: WebApplication3/Dockerfile

  external1:
    image: redis

  external2:
    image: redis

```

Docker Compose 起動設定のダイアログを開くには、次のようなオプションがあります。
- Visual Studio で、 **[デバッグ]**  >  **[Docker Compose 起動設定の管理]** を選択します。

    ![デバッグから Compose 設定の管理のメニュー項目のスクリーンショット](media/launch-settings/debug-dropdown-manage-compose.png)

- Visual Studio `docker-compose` プロジェクトを右クリックし、 **[Docker Compose 起動設定の管理]** を選択します

    ![コンテキスト メニュー項目のスクリーンショット](media/launch-settings/launch-settings-context-menu.png)

- クイック起動 (**Ctrl**+**Q**) を使用して **[Docker Compose]** を検索し、前述のコマンドを見つけます。

次の例では、`web1` Compose プロファイルが選択されています。 **[サービス]** 一覧が、このプロファイルに含まれる 5 つのうち 3 つにフィルターされます。

!["起動設定ダイアログ ボックスのスクリーンショット"](media/launch-settings/launch-settings-create-profile.png)

Docker Compose プロファイルのセクションは *docker-compose.yml* ファイルで定義されているプロファイルがある場合にのみ表示されます。

次の例は、Compose プロファイルでサービスをフィルターするのではなく、個々のサービス間で選択する方法を示しています。 ここでは、5 つのサービスのうちデバッグありの `webapplication1` とデバッグなしの `webapplication2` という 2 つのみを起動する `test2` という名前の新しい起動プロファイルを作成した場合のダイアログの外観を示します。  また、この起動プロファイルによって、アプリケーションの起動時にブラウザーが起動し、`webapplication1` のホーム ページが開きます。 

![一部のサービスが選択解除されている起動設定ダイアログのスクリーンショット](media/launch-settings/launch-settings-selected.png)

次に示すように、この情報は *launchSettings.json* に保存されます

```json
{
    "profiles": {
      "test2": {
        "commandName": "DockerCompose",
        "composeLaunchServiceName": "webapplication1",
        "serviceActions": {
          "external1": "DoNotStart",
          "external2": "DoNotStart",
          "webapplication1": "StartDebugging",
          "webapplication2": "StartWithoutDebugging",
          "webapplication3": "DoNotStart"
        },
        "composeLaunchAction": "LaunchBrowser",
        "commandVersion": "1.0",
        "composeLaunchUrl": "{Scheme}://localhost:{ServicePort}"
      }
   }
}
```

## <a name="create-a-launch-profile-that-uses-a-docker-compose-profile"></a>Docker Compose プロファイルを使用する起動プロファイルを作成する

Compose プロファイルを使用する Visual Studio 起動プロファイルを作成して、起動動作をさらにカスタマイズすることもできます。

Compose プロファイルを使用する別のプロファイルを作成するには、 **[Docker Compose プロファイルを使用]** を選択して `web1` を選択します。 起動プロファイルに、3 つのサービス `webapplication1` (`web` と `web1` の両方の Compose プロファイルに属する)、`external1`、`external2` が含まれるようになりました。 既定では、`external1` や `external2` などのソース コードのないサービスには、 **[デバッグなしで開始]** の既定のアクションがあります。 ソース コードを含む .NET アプリケーションでは、既定で **[デバッグ開始]** が設定されます。

> [!IMPORTANT]
> Compose プロファイルが指定されないサービスは、すべての Compose プロファイルに暗黙的に含まれます。

![別のプロファイルが作成されている起動設定ダイアログのスクリーンショット](media/launch-settings/launch-settings-create-profile.png)

この情報は、次のコードのように保存されます。 既定のアクションを変更しない限り、サービスとその既定のアクションの構成は保存されません。

```json
{
  "profiles": {
    "test1": {
      "commandName": "DockerCompose",
      "composeProfile": {
         "includes": [
            "web1"
         ]
      },
      "commandVersion": "1.0"
    }
  }
}
```

webapplication1 のアクションを **[デバッグなしで開始]** に変更することもできます。 これで、*launchSettings.json* の設定は次のコードのようになります。

```json
{
  "profiles": {
    "test1": {
        "commandName": "DockerCompose",
        "composeProfile": {
          "includes": [
              "web1"
              ],
          "serviceActions": {
              "webapplication1": "StartWithoutDebugging"
          }
        },
    "commandVersion": "1.0"
    }
  }
}
```

## <a name="properties"></a>Properties

次に、*launchSettings.json* の各プロパティの説明を示します。

|プロパティ| 説明|
| - | - |
|commandName| コマンドの名前。 既定値は "DockerCompose" です|
|commandVersion| DockerCompose 起動プロファイルのスキーマを管理するために使用されるバージョン番号。|
|composeProfile| 起動プロファイル定義を定義する親プロパティ。 その子プロパティは `includes` と `serviceActions` です|
|composeProfile - includes | 起動プロファイルを構成する Compose プロファイル名の一覧。|
|composeProfile - serviceActions | 選択した Compose プロファイル、サービス、および各サービスの起動アクションを一覧表示します|
|serviceActions | 選択したサービスと起動アクションを一覧表示します。|
|composeLaunchServiceName| DockerLaunchAction または DockerLaunchBrowser が指定されている場合、DockerServiceName は、起動する必要があるサービスの名前です。 このプロパティを使用して、Docker Compose ファイル内で起動するサービスが決定されます。|
|composeLaunchAction| **F5** または **Ctrl**+**F5** で実行する起動アクションを指定します。 指定できる値には、None、LaunchBrowser、LaunchWCFTestClient があります。|
|composeLaunchUrl| ブラウザーを起動するときに使用される URL。 有効な置換トークンには、"{ServiceIPAddress}"、"{ServicePort}"、"{Scheme}" があります。 例: {Scheme}://{ServiceIPAddress}:{ServicePort}|

## <a name="next-steps"></a>次のステップ

コンテナー ツールの動作の詳細については、[Visual Studio コンテナー ツールのビルドとデバッグの概要](container-build.md)に関する記事を参照してください。

## <a name="see-also"></a>関連項目

- [Visual Studio コンテナー ツールの起動設定](container-launch-settings.md)

- [Docker Compose のビルド設定](docker-compose-properties.md)
