---
title: エラー :Kerberos 認証に失敗しました |Microsoft Docs
ms.date: 11/04/2016
ms.topic: troubleshooting
f1_keywords:
- vs.debug.error.callback_kerberos_auth_failed
dev_langs:
- CSharp
- VB
- FSharp
- C++
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 76a62a821a9b110be2ffd8e25cbdf6721f12bc08
ms.sourcegitcommit: 1fc6ee928733e61a1f42782f832ead9f7946d00c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "60087567"
---
# <a name="error-kerberos-authentication-failed"></a>エラー :Kerberos 認証に失敗しました
リモート デバッグを実行するときに、次のエラー メッセージが表示されることがあります。

```cmd
Error: The Visual Studio Remote Debugger on the target computer cannot connect back to this computer. Kerberos authentication failed.
```

 このエラーは、Visual Studio リモート デバッグ モニターがローカル システム アカウントまたはネットワーク サービス アカウントで実行されている場合に発生します。 これらのアカウントでは、リモート デバッガーが Visual Studio デバッガー ホスト コンピューターに接続するときに Kerberos 認証接続を確立する必要があります。

 Kerberos 認証は、以下の場合には使用できません。

- ターゲット コンピューターまたはデバッガー ホスト コンピューターがドメインではなくワークグループに属している

   \- または -

- ドメイン コントローラーで Kerberos が無効になっている。

  Kerberos 認証が使用できない場合は、Visual Studio リモート デバッグ モニターの実行に使用するアカウントを変更してください。 手順については、次を参照してください。[エラー。ターゲット コンピューターに Visual Studio リモート デバッガー サービスは、このコンピューターに接続できない](../debugger/error-the-visual-studio-remote-debugger-service-on-the-target-computer-cannot-connect-back-to-this-computer.md)します。

  両方のコンピューターが同じドメインに接続しているにもかかわらず、このメッセージが表示される場合は、ターゲット コンピューターの DNS がデバッガー ホスト コンピューターの名前を正しく解決していることを確認してください。 以降の手順を参照してください。

### <a name="to-verify-that-dns-on-the-target-computer-is-correctly-resolving-the-debugger-host-computer-name"></a>ターゲット コンピューターの DNS がデバッガー ホスト コンピューター名を正しく解決していることを確認するには

1. ターゲット コンピューターで **[スタート]** メニューを開き、**[アクセサリ]** をポイントして **[コマンド プロンプト]** をクリックします。

2. **[コマンド プロンプト]** ウィンドウに次のように入力します。

    ```cmd
    ping <debugger_host_computer_name>
    ```

3. `ping` の応答の 1 行目には、DNS が返した完全なコンピューター名と IP アドレスが表示されます。

4. デバッガー ホスト コンピューターで **[コマンド プロンプト]** を開き、`ipconfig` を実行します。

5. IP アドレス値を比較します。

## <a name="see-also"></a>関連項目
- [リモート デバッグ エラーとトラブルシューティング](../debugger/remote-debugging-errors-and-troubleshooting.md)
- [Remote Debugging](../debugger/remote-debugging.md)
