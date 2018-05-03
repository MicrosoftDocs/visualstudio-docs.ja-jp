---
title: Visual Studio のテスト コントローラーとテスト エージェントのタイムアウト期限
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- agents, configuring
- agetns, timeouts
- controllers, configuring
- controllers, timeouts
ms.assetid: 777d0db5-0073-458a-a2a3-58b1c1f24c60
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.openlocfilehash: 444c4e7214d55aad270a88325ee9e694e84987c6
ms.sourcegitcommit: e13e61ddea6032a8282abe16131d9e136a927984
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
---
# <a name="how-to-specify-timeout-periods-for-test-controllers-and-test-agents"></a>方法: テスト コントローラーおよびテスト エージェントのタイムアウト期限を指定する

テスト コントローラーもテスト エージェントも、相互の応答またはデータ ソースからの応答をどのくらいの時間待機するかを指定するいくつかのタイムアウト設定を持っています。この時間を超えると、失敗としてエラーになります。 特定の状況下では、トポロジや他の環境の問題の要件に合わせてタイムアウト値を編集しなければならない場合があります。 タイムアウト値を編集するには、以下の手順で説明されているように、テスト コントローラーまたはテスト エージェントと関連付けられている XML 構成ファイルを編集します。

 テスト コントローラーまたはテスト エージェントのさまざまなタイムアウト設定を編集するには、以下の構成ファイルを表のキー名と値を使用して変更します。

-   テスト コントローラー: QTController.exe.config

    |キー名|説明|[値]|
    |--------------|-----------------|-----------|
    |AgentConnectionTimeoutInSeconds|エージェントの ping 要求を待機する秒数。これを超えると、接続が失われたと判断されます。|"n" 秒。|
    |AgentSyncTimeoutInSeconds|同期テストの実行を開始するときに、すべてのエージェントの同期を待機する秒数。これを超えると、実行が中止されます。|"n" 秒。|
    |AgentInitializeTimeout|テストの実行開始時に、すべてのエージェントとそのデータ コレクターの初期化を待機する秒数。それを超えると、テストの実行が中止されます。 この値は、データ コレクターを使用する場合は、適度に大きくする必要があります。|"n" 秒。 既定値: "120" (2 分)。|
    |AgentCleanupTimeout|すべてのエージェントとそのデータ コレクターのクリーンアップを待機する秒数。それを超えると、テストの実行が完了します。 この値は、データ コレクターを使用する場合は、適度に大きくする必要があります。|"n" 秒。 既定値: "120" (2 分)。|

-   テスト エージェント: QTAgentService.exe.config

    |キー名|説明|[値]|
    |--------------|-----------------|-----------|
    |ControllerConnectionPeriodInSeconds|コントローラーへの接続を試行する間隔の秒数。|"n" 秒。 既定値: "30" (30 秒)。|
    |RemotingTimeoutSeconds|リモート処理呼び出しを継続できる時間の最大秒数。|"n" 秒。 既定値: "600" (10 分)。|
    |StopTestRunCallTimeoutInSeconds|テストの実行を停止する呼び出しを待機する秒数。|"n" 秒。 既定値: "120" (2 分)。|
    |GetCollectorDataTimeout|データ コレクターを待機する秒数。|"n" 秒。 既定値: "300" (5 分)。|

## <a name="to-specify-agent-timeout-options-for-a-test-controller"></a>テスト コントローラーのエージェント タイムアウト オプションを指定するには

1. %ProgramFiles(x86)%\Microsoft Visual Studio\2017\Enterprise\Common7\IDE にある QTCcontroller.exe.config XML 構成ファイルを開きます。

2. `<appSettings>` タグを探します。

    ```xml
    <appSettings>
      <add key="LogSizeLimitInMegs" value="20"/>
      <add key="AgentConnectionTimeoutInSeconds" value="120"/>
      <add key="AgentSyncTimeoutInSeconds" value="300"/>
      <add key="ControllerServicePort" value="6901"/>
      <add key="ControllerUsersGroup" value="TeamTestControllerUsers"/>
      <add key="ControllerAdminsGroup" value="TeamTestControllerAdmins"/>
      <add key="CreateTraceListener" value="no"/>
    </appSettings>
    ```

3. テスト コントローラーのいずれかのタイムアウト キーで、既存の値を編集します。 たとえば、次のようにして、キー `AgentConnectionTimeoutInSeconds` の既定値を 2 分から 3 分に変更できます。

    ```xml
    <add key="AgentConnectionTimeoutInSeconds" value="180"/>
    ```

    - または -

    キーを追加して、タイムアウト値を指定します。 たとえば、次のように、`AgentInitializeTimeout` キーを `<appSettings>` セクションに追加して、値を 5 分に指定します。

    ```xml
    <appSettings>
            <add key="AgentInitializeTimeout" value="300"/>
    </appSettings>
    ```

## <a name="to-specify-agent-timeout-options-for-a-test-agent"></a>テスト エージェントのエージェント タイムアウト オプションを指定するには

1. %ProgramFiles(x86)%\Microsoft Visual Studio\2017\Enterprise\Common7\IDE にある QTAgentService.exe.config XML 構成ファイルを開きます。

2. `<appSettings>` タグを探します。

    ```xml
    <appSettings>
      <appSettings>
      <add key="LogSizeLimitInMegs" value="20"/>
      <add key="AgentServicePort" value="6910"/>
      <add key="ControllerConnectionPeriodInSeconds" value="30"/>
      <add key="StopTestRunCallTimeoutInSeconds" value="120"/>
      <add key="CreateTraceListener" value="no"/>
      <add key="GetCollectorDataTimeout" value="300"/>
    </appSettings>  </appSettings>
    ```

3. テスト エージェントのいずれかのタイムアウト キーで、既存の値を編集します。 たとえば、次のようにして、キー `ControllerConnectionPeriodInSeconds` の既定値を 30 秒から 1 分に変更できます。

    ```xml
    <add key="ControllerConnectionPeriodInSeconds" value="60"/>
    ```

    - または -

    キーを追加して、タイムアウト値を指定します。 たとえば、次のように、`RemotingTimeoutSeconds` キーを `<appSettings>` セクションに追加して、値を 15 分に指定します。

    ```xml
    <appSettings>
            <add key=" RemotingTimeoutSeconds " value="900"/>
    </appSettings>
    ```

## <a name="see-also"></a>関連項目

- [テスト エージェントをインストールして構成する](../test/lab-management/install-configure-test-agents.md)
- [ロード テストのログ設定の変更](../test/modify-load-test-logging-settings.md)
- [Test Controller および Test Agent 用のポートの構成](../test/configure-ports-for-test-controllers-and-test-agents.md)
- [方法: ログ ファイルの最大サイズを指定する](../test/how-to-specify-the-maximum-size-for-the-log-file.md)
- [方法: ネットワーク アダプターに Test Controller または Test Agent をバインドする](../test/how-to-bind-a-test-controller-or-test-agent-to-a-network-adapter.md)