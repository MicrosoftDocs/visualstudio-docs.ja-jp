---
title: Visual Studio コンテナー ツールの起動設定
author: ghogen
description: コンテナー化されたアプリの Visual Studio による処理方法に関連する、コンテナー ツールの起動設定について説明します。
ms.author: ghogen
ms.date: 08/15/2019
ms.technology: vs-azure
ms.topic: reference
ms.openlocfilehash: e50935145913bcd1f3c4457f4704376a0ac0f6ef
ms.sourcegitcommit: 162be102d2c22a1c4ad2c447685abd28e0e85d15
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "109973240"
---
# <a name="container-tools-launch-settings"></a>コンテナー ツールの起動設定

ASP.NET Core プロジェクト内の "*プロパティ*" フォルダーでは、開発用コンピューター上で Web アプリを起動させる方法を制御する設定が含まれる launchSettings.json ファイルを検索できます。 ASP.NET 開発でのこのファイルの使用方法についての詳細は、「[ASP.NET Core で複数の環境を使用する](/aspnet/core/fundamentals/environments?view=aspnetcore-2.2&preserve-view=true)」を参照してください。 *launchSettings.json* では、**Docker** セクションの設定は、Visual Studio でのコンテナー化されたアプリの処理方法に関連しています。

::: moniker range="vs-2017"

```json
    "Docker": {
      "commandName": "Docker",
      "launchBrowser": true,
      "launchUrl": "{Scheme}://{ServiceHost}:{ServicePort}"
    }
```

::: moniker-end
::: moniker range=">=vs-2019"

```json
    "Docker": {
      "commandName": "Docker",
      "launchBrowser": true,
      "launchUrl": "{Scheme}://{ServiceHost}:{ServicePort}",
      "environmentVariables": {
        "ASPNETCORE_URLS": "https://+:443;http://+:80",
        "ASPNETCORE_HTTPS_PORT": "44360"
      },
      "httpPort": 51803,
      "useSSL": true,
      "sslPort": 44360
    }
```

::: moniker-end

commandName 設定は、このセクションがコンテナー ツールに適用されることを示しています。 このセクションで設定できるプロパティを次の表に示します。

::: moniker range="vs-2017"

|設定の名前|バージョン|例|説明|
|------------|-------|-------|---------------|
|launchBrowser|Visual Studio 2017|"launchBrowser": true|プロジェクトを正常に起動した後にブラウザーを起動するかどうかを示します。|
|launchUrl|Visual Studio 2017|"launchUrl": "{Scheme}://{ServiceHost}:{ServicePort}"|この URL は、ブラウザーを起動するときに使用されます。  この文字列に対してサポートされている置換トークンは次のとおりです。<br>   {Scheme} - SSL が使用されているかどうかに応じて、"http" または "https" に置き換えられます。<br>   {ServiceHost} - 通常は "localhost" に置き換えられます。 ただし、windows 10 RS3 以前の Windows コンテナーを対象とする場合は、コンテナーの IP に置き換えられます。<br>   {ServicePort} - SSL が使用されているかどうかに応じて、通常は sslPort または httpPort に置き換えられます。  ただし、windows 10 RS3 以前の Windows コンテナーを対象とする場合、SSL が使用されているかどうかに応じて、"443" または "80" に置き換えられます。|

::: moniker-end

::: moniker range=">=vs-2019"

| 設定の名前         | 例                                               | 説明                                                                                                             |
| -------------------- | ----------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| commandLineArgs      | "commandLineArgs": "--mysetting myvalue"              | これらのコマンドライン引数は、コンテナー内のプロジェクトを起動するときにアプリを起動するために使用されます。                                     |
| environmentVariables | "environmentVariables": {                             | これらの環境変数の値は、プロセスがコンテナーで起動されるときに、プロセスに渡されます。                       |
|                      | "ASPNETCORE_URLS": "https://+:443; http://+:80"、       |                                                                                                                         |
|                      | "ASPNETCORE_HTTPS_PORT":"44381"                      |                                                                                                                         |
|                      | }                                                     |                                                                                                                         |
| httpPort             | "httpPort":24051                                     | コンテナーを起動すると、ホスト上にあるこのポートが、コンテナーのポート 80 にマップされます。                                |
|                      |                                                       | 指定されていない場合、値は iisSettings 値から取得されます。                                                          |
| launchBrowser        | "launchBrowser": true                                 | プロジェクトを正常に起動した後にブラウザーを起動するかどうかを示します。                                       |
| launchUrl            | "launchUrl": "{Scheme}://{ServiceHost}:{ServicePort}" | この URL は、ブラウザーを起動するときに使用されます。 この文字列に対してサポートされている置換トークンは次のとおりです。                          |
|                      |                                                       | - {Scheme} - SSL が使用されているかどうかに応じて、"http" または "https" に置き換えられます。                                   |
|                      |                                                       | - {ServiceHost} - 通常は "localhost" に置き換えられます。                                                                    |
|                      |                                                       | ただし、windows 10 RS3 以前の Windows コンテナーを対象とする場合は、コンテナーの IP に置き換えられます。           |
|                      |                                                       | - {ServicePort} - SSL が使用されているかどうかに応じて、通常は sslPort または httpPort に置き換えられます。                   |
|                      |                                                       | ただし、windows 10 RS3 以前の Windows コンテナーを対象とする場合は、"443" または "80" に置き換えられます         |
|                      |                                                       | (SSL が使用されているかどうかによって異なります)。                                                                                       |
| sslPort              | "sslPort":44381                                      | コンテナーを起動すると、ホスト上にあるこのポートが、コンテナーのポート 443 にマップされます。                               |
|                      |                                                       | 指定されていない場合、値は iisSettings 値から取得されます。                                                          |
| useSSL               | "useSSL": true                                        | プロジェクトを起動するときに SSL を使用するかどうかを示します。 useSSL が指定されていない場合は、sslPort > 0 のときに SSL が使用されます。 |

::: moniker-end

## <a name="next-steps"></a>次の手順

[コンテナー ツールのビルド プロパティ](container-msbuild-properties.md)を設定することで、プロジェクトを構成します。

## <a name="see-also"></a>関連項目

- [Docker Compose のビルド プロパティ](docker-compose-properties.md)
- [Docker Compose の起動プロファイルを管理する](launch-profiles.md)
