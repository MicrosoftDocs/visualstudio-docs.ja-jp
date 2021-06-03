---
title: '方法: 信頼のリストのセキュリティを構成する'
description: 信頼の決定を信頼のリストに保存することによって、Office ソリューションのインストールのオプションをエンド ユーザーに提供するかどうかを制御するように、ClickOnce の信頼プロンプトを構成します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- permissions [Office development in Visual Studio
- inclusion lists [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: ddbc74c00c1e1f74ce078586d624e2da4dbd8163
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99954021"
---
# <a name="how-to-configure-inclusion-list-security"></a>方法: 信頼のリストのセキュリティを構成する
  管理者のアクセス許可がある場合は、信頼の決定を信頼のリストに保存することによって、Office ソリューションをインストールするオプションをエンド ユーザーに提供するかどうかを制御するように、[!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] 信頼プロンプトを構成します。 信頼のリストの詳細については、「[信頼のリストを使用して Office ソリューションを信頼する](../vsto/trusting-office-solutions-by-using-inclusion-lists.md)」を参照してください。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

 5 つのそれぞれのゾーンにあるソリューションでは、次のオプションを設定できます。

- [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] 信頼プロンプト キーと信頼のリストを有効にする。 エンド ユーザーが、任意の証明書で署名された Office ソリューションに信頼を付与できるようにすることができます。

- [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] 信頼プロンプト キーと信頼のリストを制限する。 発行者を識別する証明書で署名された Office ソリューションをエンド ユーザーがインストールできるようにすることができますが、それはまだ信頼されていません。

- [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] 信頼プロンプト キーと信頼のリストを無効にする。 明示的に信頼された証明書で署名されていない Office ソリューションをエンド ユーザーがインストールできないようにすることができます。

## <a name="enable-the-inclusion-list"></a>信頼のリストを有効にする
 ゾーンから取得する Office ソリューションのインストールと実行のオプションをエンド ユーザーに提示する場合は、そのゾーンの信頼のリストを有効にします。

### <a name="to-enable-the-inclusion-list-by-using-the-registry-editor"></a>レジストリ エディターを使用して、信頼のリストを有効にするには

1. レジストリ エディターを開きます。

    1. **[スタート]** ボタンをクリックし、 **[ファイル名を指定して実行]** をクリックします。

    2. **[名前]** ボックスに「**regedt32.exe**」と入力し、 **[OK]** をクリックします。

2. 次のレジストリ キーを見つけます。

     **\HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\\.NETFramework\Security\TrustManager\PromptingLevel**

     このキーが存在しない場合は作成します。

3. 以下のサブキーがまだ存在しない場合は、関連付けられている値と共に、それらを "**文字列値**" として追加します。

    |文字列値のサブキー|値|
    |-------------------------|-----------|
    |**Internet**|**AuthenticodeRequired**|
    |**UntrustedSites**|**Disabled**|
    |**MyComputer**|**Enabled**|
    |**LocalIntranet**|**Enabled**|
    |**TrustedSites**|**Enabled**|

     既定では、**Internet** には **AuthenticodeRequired** の値があり、**UntrustedSites** には **Disabled** の値があります。

### <a name="to-enable-the-inclusion-list-programmatically"></a>プログラムによって信頼のリストを有効にするには

1. Visual Basic または Visual C# コンソール アプリケーションを作成します。

2. 編集のために *Program.vb* または *Program.cs* ファイルを開き、次のコードを追加します。

    ```vb
    Dim key As Microsoft.Win32.RegistryKey
    key = Microsoft.Win32.Registry.LocalMachine.CreateSubKey("SOFTWARE\MICROSOFT\.NETFramework\Security\TrustManager\PromptingLevel")
    key.SetValue("MyComputer", "Enabled")
    key.SetValue("LocalIntranet", "Enabled")
    key.SetValue("Internet", "AuthenticodeRequired")
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

## <a name="restrict-the-inclusion-list"></a>信頼のリストを制限する
 ユーザーが信頼について決定を求められる前に、既知の ID を持つ Authenticode 証明書を使用してソリューションに署名する必要があるように、信頼のリストを制限します。

### <a name="to-restrict-the-inclusion-list"></a>信頼のリストを制限するには

1. レジストリ エディターを開きます。

    1. **[スタート]** ボタンをクリックし、 **[ファイル名を指定して実行]** をクリックします。

    2. **[名前]** ボックスに「**regedt32.exe**」と入力し、 **[OK]** をクリックします。

2. 次のレジストリ キーを見つけます。

     **\HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\\.NETFramework\Security\TrustManager\PromptingLevel**

     このキーが存在しない場合は作成します。

3. 以下のサブキーがまだ存在しない場合は、関連付けられている値と共に、それらを "**文字列値**" として追加します。

    |文字列値のサブキー|値|
    |-------------------------|-----------|
    |**UntrustedSites**|**Disabled**|
    |**Internet**|**AuthenticodeRequired**|
    |**MyComputer**|**AuthenticodeRequired**|
    |**LocalIntranet**|**AuthenticodeRequired**|
    |**TrustedSites**|**AuthenticodeRequired**|

     既定では、**Internet** には **AuthenticodeRequired** の値があり、**UntrustedSites** には **Disabled** の値があります。

### <a name="to-restrict-the-inclusion-list-programmatically"></a>プログラムによって信頼のリストを制限するには

1. Visual Basic または Visual C# コンソール アプリケーションを作成します。

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

## <a name="disable-the-inclusion-list"></a>信頼のリストを無効にする
 信頼できる既知の証明書で署名されているソリューションのみをエンド ユーザーがインストールできるように、信頼のリストを無効にすることができます。

### <a name="to-disable-the-inclusion-list"></a>信頼のリストを無効にするには

1. レジストリ エディターを開きます。

    1. **[スタート]** ボタンをクリックし、 **[ファイル名を指定して実行]** をクリックします。

    2. **[名前]** ボックスに「**regedt32.exe**」と入力し、 **[OK]** をクリックします。

2. まだ存在しない場合は、次のレジストリ キーを作成します。

     **\HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\\.NETFramework\Security\TrustManager\PromptingLevel**

3. 以下のサブキーがまだ存在しない場合は、関連付けられている値と共に、それらを "**文字列値**" として追加します。

    |文字列値のサブキー|値|
    |-------------------------|-----------|
    |**UntrustedSites**|**Disabled**|
    |**Internet**|**Disabled**|
    |**MyComputer**|**Disabled**|
    |**LocalIntranet**|**Disabled**|
    |**TrustedSites**|**Disabled**|

### <a name="to-disable-the-inclusion-list-programmatically"></a>プログラムによって信頼のリストを無効にするには

1. Visual Basic または Visual C# コンソール アプリケーションを作成します。

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
- [信頼のリストによる Office ソリューションへの信頼の付与](../vsto/trusting-office-solutions-by-using-inclusion-lists.md)
- [Office ソリューションをセキュリティで保護する](../vsto/securing-office-solutions.md)
