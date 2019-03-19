---
title: '方法: 信頼のリストのセキュリティを構成します。'
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- permissions [Office development in Visual Studio
- inclusion lists [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 1277499fd0af52a4e7138637ef8be332b56a4926
ms.sourcegitcommit: d0425b6b7d4b99e17ca6ac0671282bc718f80910
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/21/2019
ms.locfileid: "56596478"
---
# <a name="how-to-configure-inclusion-list-security"></a>方法: 信頼のリストのセキュリティを構成します。
  管理者のアクセス許可があればを構成できます、[!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)]信頼プロンプトのコントロールにエンドユーザーが信頼のリストに、信頼の決定を保存することによって、Office ソリューションをインストールするオプションを指定されたかどうか。 信頼のリストについては、次を参照してください。[リストによる Office のセキュリティ ソリューション](../vsto/trusting-office-solutions-by-using-inclusion-lists.md)します。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

 ソリューションの 5 つのゾーン内にある場合は、次のオプションを設定できます。

-   有効にする、[!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)]プロンプトのキーを信頼し、信頼のリスト。 任意の証明書で署名されている Office ソリューションに信頼を付与するエンドユーザーを許可することができます。

-   制限、[!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)]プロンプトのキーを信頼し、信頼のリスト。 エンドユーザー、パブリッシャーを識別するが既に信頼された証明書で署名されている Office ソリューションをインストールすることができます。

-   無効にする、[!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)]プロンプトのキーを信頼し、信頼のリスト。 エンドユーザーは、明示的に信頼された証明書で署名されていない Office ソリューションのインストールからできないようにすることができます。

## <a name="enable-the-inclusion-list"></a>信頼のリストを有効にします。
 エンドユーザーをインストールし、そのゾーンに由来する Office ソリューションの実行のオプションが表示する場合は、ゾーンの信頼のリストを有効にします。

### <a name="to-enable-the-inclusion-list-by-using-the-registry-editor"></a>レジストリ エディターを使用して、信頼のリストを有効にするには

1.  レジストリ エディターを開きます。

    1.  **[スタート]** ボタンをクリックし、**[ファイル名を指定して実行]** をクリックします。

    2.  **オープン**ボックスに「 **regedt32.exe**、順にクリックします**OK**します。

2.  次のレジストリ キーを探します。

     **\HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\\.NETFramework\Security\TrustManager\PromptingLevel**

     キーが存在しない場合は、それを作成します。

3.  次のサブキーとして追加**文字列値**がまだ存在しない、関連付けられている値を持つ場合は、します。

    |文字列値のサブキー|[値]|
    |-------------------------|-----------|
    |**インターネット**|**AuthenticodeRequired**|
    |**UntrustedSites**|**無効**|
    |**MyComputer**|**有効**|
    |**LocalIntranet**|**有効**|
    |**しません**|**有効**|

     既定では、**インターネット**、値を持つ**AuthenticodeRequired**と**UntrustedSites** 、値を持つ**無効**します。

### <a name="to-enable-the-inclusion-list-programmatically"></a>プログラムの信頼のリストを有効にするには

1.  Visual Basic または Visual C# コンソール アプリケーションを作成します。

2.  開く、 *Program.vb*または*Program.cs*を編集するためのファイルを開き、次のコードを追加します。

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

3.  アプリケーションをビルドして実行します。

## <a name="restrict-the-inclusion-list"></a>信頼のリストを制限します。
 信頼のリストを制限して、ソリューションは、ユーザーは、信頼の決定に求められる前に、既知の id が Authenticode 証明書で署名する必要があります。

### <a name="to-restrict-the-inclusion-list"></a>信頼のリストを制限するには

1.  レジストリ エディターを開きます。

    1.  **[スタート]** ボタンをクリックし、**[ファイル名を指定して実行]** をクリックします。

    2.  **オープン**ボックスに「 **regedt32.exe**、順にクリックします**OK**します。

2.  次のレジストリ キーを探します。

     **\HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\\します。NETFramework\Security\TrustManager\PromptingLevel**

     キーが存在しない場合は、それを作成します。

3.  次のサブキーとして追加**文字列値**がまだ存在しない、関連付けられている値を持つ場合は、します。

    |文字列値のサブキー|[値]|
    |-------------------------|-----------|
    |**UntrustedSites**|**無効**|
    |**インターネット**|**AuthenticodeRequired**|
    |**MyComputer**|**AuthenticodeRequired**|
    |**LocalIntranet**|**AuthenticodeRequired**|
    |**しません**|**AuthenticodeRequired**|

     既定では、**インターネット**、値を持つ**AuthenticodeRequired**と**UntrustedSites** 、値を持つ**無効**します。

### <a name="to-restrict-the-inclusion-list-programmatically"></a>プログラムで、信頼のリストを制限するには

1.  Visual Basic または Visual C# コンソール アプリケーションを作成します。

2.  開く、 *Program.vb*または*Program.cs*を編集するためのファイルを開き、次のコードを追加します。

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

3.  アプリケーションをビルドして実行します。

## <a name="disable-the-inclusion-list"></a>信頼のリストを無効にします。
 エンドユーザー: 信頼できると既知の証明書で署名されているソリューションのみをインストールできるように、信頼のリストを無効にすることができます。

### <a name="to-disable-the-inclusion-list"></a>信頼のリストを無効にするには

1.  レジストリ エディターを開きます。

    1.  **[スタート]** ボタンをクリックし、**[ファイル名を指定して実行]** をクリックします。

    2.  **オープン**ボックスに「 **regedt32.exe**、順にクリックします**OK**します。

2.  これがない場合は、次のレジストリ キーを作成します。

     **\HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\\します。NETFramework\Security\TrustManager\PromptingLevel**

3.  次のサブキーとして追加**文字列値**がまだ存在しない、関連付けられている値を持つ場合は、します。

    |文字列値のサブキー|[値]|
    |-------------------------|-----------|
    |**UntrustedSites**|**無効**|
    |**インターネット**|**無効**|
    |**MyComputer**|**無効**|
    |**LocalIntranet**|**無効**|
    |**しません**|**無効**|

### <a name="to-disable-the-inclusion-list-programmatically"></a>信頼のリストをプログラムで無効にするには

1.  Visual Basic または Visual C# コンソール アプリケーションを作成します。

2.  開く、 *Program.vb*または*Program.cs*を編集するためのファイルを開き、次のコードを追加します。

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

3.  アプリケーションをビルドして実行します。

## <a name="see-also"></a>関連項目
- [信頼のリストを使用して Office ソリューションを信頼](../vsto/trusting-office-solutions-by-using-inclusion-lists.md)
- [セキュリティで保護された Office ソリューション](../vsto/securing-office-solutions.md)
