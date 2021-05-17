---
title: ClickOnce 信頼プロンプトの動作を構成する | Microsoft Docs
description: Clickonce 信頼プロンプトを構成して、ClickOnce アプリケーションをインストールするオプションをエンド ユーザーに付与するかどうかを制御する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, install without prompting
- deploying applications [ClickOnce], trust prompt
- ClickOnce applications, install without prompting
- ClickOnce applications, trust prompt
- ClickOnce deployment, trust prompt
ms.assetid: cc04fa75-012b-47c9-9347-f4216be23cf2
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 8cb23eeee53990113d779e241adb8dcf1ab0cf16
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99890306"
---
# <a name="how-to-configure-the-clickonce-trust-prompt-behavior"></a>方法: ClickOnce 信頼プロンプトの動作を構成する
ClickOnce 信頼プロンプトを構成して、Windows フォーム アプリケーション、Windows Presentation Foundation アプリケーション、コンソール アプリケーション、WPF ブラウザー アプリケーション、Office ソリューションなどの ClickOnce アプリケーションをインストールするオプションを、エンド ユーザーに付与するかどうかを制御できます。 信頼プロンプトは、各エンド ユーザーのコンピューターでレジストリ キーを設定することによって構成します。

 次の表は、5 つのゾーン (Internet、UntrustedSites、MyComputer、LocalIntranet、TrustedSites) のそれぞれに適用できる構成オプションを示しています。

|オプション|レジストリ設定値|説明|
|------------|----------------------------|-----------------|
|信頼プロンプトを有効にします。|`Enabled`|エンド ユーザーが ClickOnce アプリケーションに信頼を付与できるように ClickOnce 信頼プロンプトが表示されます。|
|信頼プロンプトを制限します。|`AuthenticodeRequired`|ClickOnce 信頼プロンプトは、ClickOnce アプリケーションが、発行元を識別する証明書で署名されている場合にのみ表示されます。|
|信頼プロンプトを無効にします。|`Disabled`|明示的に信頼された証明書で署名されていない ClickOnce アプリケーションに対して、ClickOnce 信頼プロンプトは表示されません。|

 次の表に、各ゾーンでの既定の動作を示します。 [アプリケーション] 列は、Windows フォーム アプリケーション、Windows Presentation Foundation アプリケーション、WPF ブラウザー アプリケーション、コンソール アプリケーションを指しています。

|ゾーン|アプリケーション|Office ソリューション|
|----------|------------------|----------------------|
|`MyComputer`|`Enabled`|`Enabled`|
|`LocalIntranet`|`Enabled`|`Enabled`|
|`TrustedSites`|`Enabled`|`Enabled`|
|`Internet`|`Enabled`|`AuthenticodeRequired`|
|`UntrustedSites`|`Disabled`|`Disabled`|

 これらの設定は、ClickOnce 信頼プロンプトを有効にする、制限する、または無効にすることでオーバーライドできます。

## <a name="enable-the-clickonce-trust-prompt"></a>ClickOnce 信頼プロンプトを有効にする
 そのゾーンから取得する ClickOnce アプリケーションをインストールして実行するオプションをエンド ユーザーに表示する場合は、ゾーンの信頼プロンプトを有効にします。

#### <a name="to-enable-the-clickonce-trust-prompt-by-using-the-registry-editor"></a>レジストリ エディターを使用して ClickOnce 信頼プロンプトを有効にするには

1. レジストリ エディターを開きます。

    1. **[スタート]** ボタンをクリックし、 **[ファイル名を指定して実行]** をクリックします。

    2. **[名前]** ボックスに「`regedit`」と入力し、 **[OK]** をクリックします。

2. 次のレジストリ キーを見つけます。

     **\HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\\.NETFramework\Security\TrustManager\PromptingLevel**

     このキーが存在しない場合は作成します。

3. 以下のサブキーがまだ存在しない場合は、それらを **文字列値** として追加します。次の表に、関連付けられている値を示します。

    |文字列値のサブキー|値|
    |-------------------------|-----------|
    |`Internet`|`Enabled`|
    |`UntrustedSites`|`Disabled`|
    |`MyComputer`|`Enabled`|
    |`LocalIntranet`|`Enabled`|
    |`TrustedSites`|`Enabled`|

     Office ソリューションの場合、`Internet` には既定値 `AuthenticodeRequired` があり、`UntrustedSites` の値は `Disabled` となります。 その他の場合、`Internet` の既定値は `Enabled` です。

#### <a name="to-enable-the-clickonce-trust-prompt-programmatically"></a>ClickOnce 信頼プロンプトをプログラムから有効にするには

1. Visual Studio で、Visual Basic または Visual C# コンソール アプリケーションを作成します。

2. 編集のために *Program.vb* または *Program.cs* ファイルを開き、次のコードを追加します。

    ```vb
    Dim key As Microsoft.Win32.RegistryKey
    key = Microsoft.Win32.Registry.LocalMachine.CreateSubKey("SOFTWARE\MICROSOFT\.NETFramework\Security\TrustManager\PromptingLevel")
    key.SetValue("MyComputer", "Enabled")
    key.SetValue("LocalIntranet", "Enabled")
    key.SetValue("Internet", "Enabled")
    key.SetValue("TrustedSites", "Enabled")
    key.SetValue("UntrustedSites", "Disabled")
    key.Close()
    ```

    ```csharp
    Microsoft.Win32.RegistryKey key;
    key = Microsoft.Win32.Registry.LocalMachine.CreateSubKey("SOFTWARE\\MICROSOFT\\.NETFramework\\Security\\TrustManager\\PromptingLevel");
    key.SetValue("MyComputer", "Enabled");
    key.SetValue("LocalIntranet", "Enabled");
    key.SetValue("Internet", "AuthenticodeRequired");
    key.SetValue("TrustedSites", "Enabled");
    key.SetValue("UntrustedSites", "Disabled");
    key.Close();
    ```

3. アプリケーションをビルドして実行します。

## <a name="restrict-the-clickonce-trust-prompt"></a>ClickOnce 信頼プロンプトを制限する
 ユーザーが信頼について決定を求められる前に、既知の ID を持つ Authenticode 証明書を使用してソリューションに署名する必要があるように、信頼のプロンプトを制限します。

#### <a name="to-restrict-the-clickonce-trust-prompt-by-using-the-registry-editor"></a>レジストリ エディターを使用して ClickOnce 信頼プロンプトを制限するには

1. レジストリ エディターを開きます。

    1. **[スタート]** ボタンをクリックし、 **[ファイル名を指定して実行]** をクリックします。

    2. **[名前]** ボックスに「`regedit`」と入力し、 **[OK]** をクリックします。

2. 次のレジストリ キーを見つけます。

     **\HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\\.NETFramework\Security\TrustManager\PromptingLevel**

     このキーが存在しない場合は作成します。

3. 以下のサブキーがまだ存在しない場合は、それらを **文字列値** として追加します。次の表に、関連付けられている値を示します。

    |文字列値のサブキー|値|
    |-------------------------|-----------|
    |`UntrustedSites`|`Disabled`|
    |`Internet`|`AuthenticodeRequired`|
    |`MyComputer`|`AuthenticodeRequired`|
    |`LocalIntranet`|`AuthenticodeRequired`|
    |`TrustedSites`|`AuthenticodeRequired`|

#### <a name="to-restrict-the-clickonce-trust-prompt-programmatically"></a>ClickOnce 信頼プロンプトをプログラムから制限にするには

1. Visual Studio で、Visual Basic または Visual C# コンソール アプリケーションを作成します。

2. 編集のために *Program.vb* または *Program.cs* ファイルを開き、次のコードを追加します。

    ```vb
    Dim key As Microsoft.Win32.RegistryKey
    key = Microsoft.Win32.Registry.LocalMachine.CreateSubKey("SOFTWARE\MICROSOFT\.NETFramework\Security\TrustManager\PromptingLevel")
    key.SetValue("MyComputer", "AuthenticodeRequired")
    key.SetValue("LocalIntranet", "AuthenticodeRequired")
    key.SetValue("Internet", "AuthenticodeRequired")
    key.SetValue("TrustedSites", "AuthenticodeRequired")
    key.SetValue("UntrustedSites", "Disabled")
    key.Close()
    ```

    ```csharp
    Microsoft.Win32.RegistryKey key;
    key = Microsoft.Win32.Registry.LocalMachine.CreateSubKey("SOFTWARE\\MICROSOFT\\.NETFramework\\Security\\TrustManager\\PromptingLevel");
    key.SetValue("MyComputer", "AuthenticodeRequired");
    key.SetValue("LocalIntranet", "AuthenticodeRequired");
    key.SetValue("Internet", "AuthenticodeRequired");
    key.SetValue("TrustedSites", "AuthenticodeRequired");
    key.SetValue("UntrustedSites", "Disabled");
    key.Close();
    ```

3. アプリケーションをビルドして実行します。

## <a name="disable-the-clickonce-trust-prompt"></a>ClickOnce 信頼プロンプトを無効にする
 セキュリティ ポリシーでまだ信頼されていないソリューションをインストールするオプションがエンド ユーザーに表示されないように、信頼プロンプトを無効にすることができます。

#### <a name="to-disable-the-clickonce-trust-prompt-by-using-the-registry-editor"></a>レジストリ エディターを使用して ClickOnce 信頼プロンプトを無効にするには

1. レジストリ エディターを開きます。

    1. **[スタート]** ボタンをクリックし、 **[ファイル名を指定して実行]** をクリックします。

    2. **[名前]** ボックスに「`regedit`」と入力し、 **[OK]** をクリックします。

2. 次のレジストリ キーを見つけます。

     **\HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\\.NETFramework\Security\TrustManager\PromptingLevel**

     このキーが存在しない場合は作成します。

3. 以下のサブキーがまだ存在しない場合は、それらを **文字列値** として追加します。次の表に、関連付けられている値を示します。

    |文字列値のサブキー|値|
    |-------------------------|-----------|
    |`UntrustedSites`|`Disabled`|
    |`Internet`|`Disabled`|
    |`MyComputer`|`Disabled`|
    |`LocalIntranet`|`Disabled`|
    |`TrustedSites`|`Disabled`|

#### <a name="to-disable-the-clickonce-trust-prompt-programmatically"></a>ClickOnce 信頼プロンプトをプログラムから無効にするには

1. Visual Studio で、Visual Basic または Visual C# コンソール アプリケーションを作成します。

2. 編集のために *Program.vb* または *Program.cs* ファイルを開き、次のコードを追加します。

    ```vb
    Dim key As Microsoft.Win32.RegistryKey
    key = Microsoft.Win32.Registry.LocalMachine.CreateSubKey("SOFTWARE\MICROSOFT\.NETFramework\Security\TrustManager\PromptingLevel")
    key.SetValue("MyComputer", "Disabled")
    key.SetValue("LocalIntranet", "Disabled")
    key.SetValue("Internet", "Disabled")
    key.SetValue("TrustedSites", "Disabled")
    key.SetValue("UntrustedSites", "Disabled")
    key.Close()
    ```

    ```csharp
    Microsoft.Win32.RegistryKey key;
    key = Microsoft.Win32.Registry.LocalMachine.CreateSubKey("SOFTWARE\\MICROSOFT\\.NETFramework\\Security\\TrustManager\\PromptingLevel");
    key.SetValue("MyComputer", "Disabled");
    key.SetValue("LocalIntranet", "Disabled");
    key.SetValue("Internet", "Disabled");
    key.SetValue("TrustedSites", "Disabled");
    key.SetValue("UntrustedSites", "Disabled");
    key.Close();

    ```

3. アプリケーションをビルドして実行します。

## <a name="see-also"></a>こちらもご覧ください
- [ClickOnce アプリケーションのセキュリティ保護](../deployment/securing-clickonce-applications.md)
- [ClickOnce アプリケーションのコード アクセス セキュリティ](../deployment/code-access-security-for-clickonce-applications.md)
- [ClickOnce と Authenticode](../deployment/clickonce-and-authenticode.md)
- [信頼されたアプリケーションの配置の概要](../deployment/trusted-application-deployment-overview.md)
- [方法: ClickOnce のセキュリティ設定を有効にする](../deployment/how-to-enable-clickonce-security-settings.md)
- [方法: ClickOnce アプリケーションのセキュリティ ゾーンを設定する](../deployment/how-to-set-a-security-zone-for-a-clickonce-application.md)
- [方法: ClickOnce アプリケーションのカスタム アクセス許可を設定する](../deployment/how-to-set-custom-permissions-for-a-clickonce-application.md)
- [方法: アクセス許可が制限された ClickOnce アプリケーションをデバッグする](securing-clickonce-applications.md)
- [方法: ClickOnce アプリケーション用の信頼された発行者をクライアント コンピューターに追加する](../deployment/how-to-add-a-trusted-publisher-to-a-client-computer-for-clickonce-applications.md)
- [方法: アプリケーション マニフェストおよび配置マニフェストに再署名する](../deployment/how-to-re-sign-application-and-deployment-manifests.md)
