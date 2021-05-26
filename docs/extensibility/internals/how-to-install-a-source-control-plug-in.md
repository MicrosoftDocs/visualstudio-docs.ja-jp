---
title: '方法: ソース管理プラグインをインストールする |Microsoft Docs'
description: ソース管理プラグインを Visual Studio にインストールする方法について説明します。そのためには、これを Visual Studio ソース管理プラグイン API と統合し、その DLL を登録します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- installation [Visual Studio SDK], source control plug-ins
- source control plug-ins, installing
ms.assetid: 9e2e01d9-7beb-42b2-99b2-86995578afda
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 4a0798cb7763ff2766d2de2bb00a80759be8fd3e
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105078813"
---
# <a name="how-to-install-a-source-control-plug-in"></a>方法: ソース管理プラグインをインストールする
ソース管理プラグインを作成するには、次の 3 つの手順を実行します。

1. このドキュメントのソース管理プラグイン API リファレンスのセクションで定義されている関数を使用して、DLL を作成します。

2. ソース管理プラグイン API 定義の関数を実装します。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] でそれが呼び出されたときに、プラグインからインターフェイスとダイアログ ボックスを使用できるようにします。

3. 適切なレジストリ エントリを作成して、DLL を登録します。

## <a name="integration-with-visual-studio"></a>Visual Studio との統合
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] では、ソース管理プラグイン API に準拠するソース管理プラグインがサポートされています。

### <a name="register-the-source-control-plug-in"></a>ソース管理プラグインの登録
 実行中の統合開発環境 (IDE) でソース管理システムを呼び出すことができるようにするには、最初に、API をエクスポートするソース管理プラグイン DLL を見つける必要があります。

#### <a name="to-register-the-source-control-plug-in-dll"></a>ソース管理プラグイン DLL を登録するには

1. **HKEY_LOCAL_MACHINE** キーの、会社名のサブキーに続いて製品名のサブキーを指定する **SOFTWARE** サブキーに 2 つのエントリを追加します。 パターンは **HKEY_LOCAL_MACHINE\SOFTWARE\\\<company name>\\\<product name>\\\<entry>**  = *value* です。 2 つのエントリには、常に **SCCServerName** および **SCCServerPath** が呼び出されます。 それぞれが標準文字列です。

    たとえば、会社名が Microsoft で、ソース管理製品が SourceSafe という名前の場合、このレジストリ パスは **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SourceSafe** になります。 このサブキーの最初のエントリ **SCCServerName** は、ユーザーが判読できる、製品を指定する文字列です。 2 つ目のエントリである **SCCServerPath** は、IDE が接続するソース管理プラグイン DLL への完全なパスです。 次に、レジストリ エントリのサンプルを示します。

   |レジストリ エントリのサンプル|値の例|
   |---------------------------|------------------|
   |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SourceSafe\SCCServerName|Microsoft Visual SourceSafe|
   |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SourceSafe\SCCServerPath|*c:\vss\win32\ssscc.dll*|

   > [!NOTE]
   > SCCServerPath は、SourceSafe プラグインへの完全なパスです。 ソース管理プラグインでは、異なる会社名と製品名が使用されますが、レジストリ エントリのパスは同じです。

2. 次のオプションのレジストリ エントリを使用して、ソース管理プラグインの動作を変更できます。 これらのエントリは、**SccServerName** および **SccServerPath** と同じサブキーで使用します。

   - **HideInVisualStudioregistry** エントリは、ソース管理プラグインが [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] の **[プラグインの選択]** リストに表示されないようにする場合に使用できます。 このエントリは、ソース管理プラグインへの自動切り替えにも影響します。 このエントリは、ソース管理プラグインを置き換えるソース管理パッケージを提供する一方で、ソース管理プラグインを使用しているユーザーがソース管理パッケージに簡単に移行できるようにしたい場合に使用します。 ソース管理パッケージがインストールされると、このレジストリ エントリが設定され、プラグインが非表示になります。

      **HideInVisualStudio** は DWORD 値です。*1* に設定すると、プラグインが非表示になり、*0* に設定するとプラグインが表示されます。 レジストリ エントリが表示されない場合、既定の動作ではプラグインが表示されます。

   - **DisableSccManager** レジストリ エントリを使用して、通常は **[ファイル]**  >  **[ソース管理]** サブメニューに表示される **[\<Source Control Server> の起動]** メニュー オプションを無効または非表示にすることができます。 このメニュー オプションを選択すると、[SccRunScc](../../extensibility/sccrunscc-function.md) 関数が呼び出されます。 ソース管理プラグインでは外部プログラムがサポートされていない可能性があるため、 **[起動]** メニュー オプションを無効にしたり、非表示にしたりすることもできます。

      **DisableSccManager** は DWORD 値です。*0* に設定すると **[\<Source Control Server> の起動]** メニュー オプションが有効になります。また、*1* に設定するとメニュー オプションが無効になり、*2* に設定するとメニュー オプションが非表示になります。 このレジストリ エントリが表示されない場合、既定の動作ではメニュー オプションが表示されます。

   | レジストリ エントリのサンプル | 値の例 |
   | - |--------------|
   | HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SourceSafe\HideInVisualStudio | 1 |
   | HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SourceSafe\DisableSccManager | 1 |

3. **HKEY_LOCAL_MACHINE** キーの **SOFTWARE** サブキーに、サブキー **SourceCodeControlProvider** を追加します。

    このサブキーの下で、レジストリ エントリ **ProviderRegKey** が、手順 1 でレジストリに配置したサブキーを表す文字列に設定されます。 パターンは、**HKEY_LOCAL_MACHINE\SOFTWARE\SourceCodeControlProvider\ProviderRegKey** = *SOFTWARE\\<company name\>\\<product name\>* です。

    次に、このサブキーのサンプル コンテンツを示します。

   |レジストリ エントリ|値の例|
   |--------------------|------------------|
   |HKEY_LOCAL_MACHINE\SOFTWARE\SourceCodeControlProvider\ProviderRegKey|SOFTWARE\Microsoft\SourceSafe|

   > [!NOTE]
   > ソース管理プラグインでは、同じサブキーとエントリ名が使用されますが、値は異なります。

4. **SourceCodeControlProvider** サブキーの下に **InstalledSCCProviders** という名前のサブキーを作成し、そのサブキーの下に 1 つのエントリを配置します。

    このエントリの名前は、ユーザーが判読できるプロバイダーの名前 (SCCServerName エントリに指定された値と同じ) で、値はここでも手順 1 で作成したサブキーです。 パターンは、**HKEY_LOCAL_MACHINE\SOFTWARE\SourceCodeControlProvider\InstalledSCCProviders\\<display name\>**  = *SOFTWARE\\<company name\>\\<product name\>* です。

    次に例を示します。

   |レジストリ エントリのサンプル|値の例|
   |---------------------------|------------------|
   |HKEY_LOCAL_MACHINE\SOFTWARE\SourceCodeControlProvider\InstalledSCCProviders\Microsoft Visual SourceSafe|SOFTWARE\Microsoft\SourceSafe|

   > [!NOTE]
   > この方法で、複数のソース管理プラグインが登録されている可能性があります。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] では、インストールされている、ソース管理プラグイン API ベースのすべてのプラグインがこのようにして検索されます。

## <a name="how-an-ide-locates-the-dll"></a>IDE で DLL を検索する方法
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE では、2 つの方法で、ソース管理プラグイン DLL を検索できます。

- 既定のソース管理プラグインを検索し、ダイアログを表示せずに接続します。

- ユーザーが選択したものから、登録されているすべてのソース管理プラグインを検索します。

  最初の方法で DLL を検索するために、IDE では **HKEY_LOCAL_MACHINE\Software\SourceCodeControlProvider** サブキーでエントリ **ProviderRegKey** が検索されます。 このエントリの値は、別のサブキーを指しています。 次に、IDE では、**HKEY_LOCAL_MACHINE** の下の 2 番目のサブキーで **SccServerPath** という名前のエントリが検索されます。 このエントリの値により、IDE で DLL が参照されます。

> [!NOTE]
> IDE では、DLL は相対パス ( *.\NewProvider.DLL* など) から読み込まれません。 DLL への完全なパスを指定する必要があります (*c:\Providers\NewProvider.DLL* など)。 これで、未承認または偽装されたプラグイン DLL の読み込みを防ぐことができるので、IDE のセキュリティが強化されます。

 2 番目の方法で DLL を検索するために、IDE では **HKEY_LOCAL_MACHINE\Software\SourceCodeControlProvider\InstalledSCCProviders** サブキーですべてのエントリが検索されます。 各エントリには、名前と値があります。 IDE では、これらの名前の一覧がユーザーに表示されます。 ユーザーが名前を選択すると、選択した名前の、サブキーを指す値が IDE によって検索されます。 次に、IDE では、**HKEY_LOCAL_MACHINE** の下のそのサブキーで **SccServerPath** という名前のエントリが検索されます。 このエントリの値により、IDE で正しい DLL が参照されます。

 ソース管理プラグインでは、DLL を検索する両方の方法をサポートする必要があります。このため、**Providerregkey** を設定して、以前の設定を上書きします。 さらに重要なこととして、使用するソース管理プラグインをユーザーが選択できるように、**InstalledSccProviders** の一覧にそれ自体を追加する必要があります。

> [!NOTE]
> **HKEY_LOCAL_MACHINE** キーが使用されるため、特定のコンピューターに既定のソース管理プラグインとして登録できるソース管理プラグインは 1 つだけです (ただし、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] では、ユーザーは、特定のソリューションに対して実際に使用するソース管理プラグインを決定できます)。 インストール プロセス中に、ソース管理プラグインが既に設定されているかどうかを確認します。設定されている場合は、インストールする新しいソース管理プラグインを既定として設定するかどうかをユーザーに確認してください。 アンインストール中に、**HKEY_LOCAL_MACHINE\SOFTWARE\SourceCodeControlProvider** のすべてのソース管理プラグインに共通する他のレジストリ サブキーを削除しないでください。特定の SCC サブキーのみを削除します。

## <a name="how-the-ide-detects-version-1213-support"></a>IDE でのバージョン 1.2/1.3 のサポートの検出方法
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] では、プラグインでソース管理プラグイン API バージョン 1.2 と 1.3 の機能がサポートされているかどうかは、どのように検出されるのでしょうか? 高度な機能を宣言するには、ソース管理プラグインで対応する関数を実装する必要があります。

 最初に、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] では、[SccGetVersion](../../extensibility/sccgetversion-function.md) の呼び出しで返された値が確認されます。 これは、1.2 以上である必要があります。

 次に、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] では、[SccInitialize](../../extensibility/sccinitialize-function.md) の `lpSccCaps` 引数を調べて、特定の新機能がサポートされているかどうかが確認されます。

 これら両方の条件が満たされている場合は、バージョン 1.2 および 1.3 でサポートされている新しい関数を呼び出すことができます。

## <a name="see-also"></a>関連項目
- [ソース管理プラグインの使用を開始する](../../extensibility/internals/getting-started-with-source-control-plug-ins.md)
