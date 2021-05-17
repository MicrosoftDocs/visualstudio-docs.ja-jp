---
title: アプリケーション配置の必要条件 | Microsoft Docs
description: '[必須コンポーネント] ダイアログ ボックスとブートストラップ パッケージの使用など、アプリケーションの配置の必須条件について説明します。'
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, platform detection
- ClickOnce deployment, prerequisites
- ClickOnce deployment, dependencies
- prerequisites, ClickOnce
- dependencies, ClickOnce
ms.assetid: fc6e047e-ad94-44e8-8ff5-b6d1f4ca7735
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: fe8312a4dcaa2efb0b783e89540e5ff9f71f15e6
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99837802"
---
# <a name="application-deployment-prerequisites"></a>アプリケーション配置の必要条件

アプリケーションを正常にインストールして実行するには、まず、アプリケーションが依存するすべてのコンポーネントを対象のコンピューターにインストールします。 たとえば、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] を使用して作成されたほとんどのアプリケーションは、.NET Framework に依存します。 その場合、アプリケーションをインストールする前に、共通言語ランタイムの適切なバージョンが、ターゲット コンピューター上に存在している必要があります。

 これらの必須コンポーネントは **[必須コンポーネント]** ダイアログ ボックスで選択でき、.NET Framework およびその他の再頒布可能コンポーネントはインストールの一部としてインストールできます。 この方法は *ブートストラップ* と呼ばれます。 *Setup.exe* (*ブートストラップ* とも呼ばれます) という Windows 実行可能プログラムが [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] によって生成されます。 ブートストラップは、アプリケーションが実行される前にこれらの必須コンポーネントをインストールします。 これらの必須条件の選択の詳細については、「[[必須コンポーネント] ダイアログ ボックス](../ide/reference/prerequisites-dialog-box.md)」を参照してください。

 各必須コンポーネントはブートストラップ パッケージです。 ブートストラップ パッケージは、必須コンポーネントのインストール方法を記述するマニフェスト ファイルを含むディレクトリおよびファイルのグループです。 アプリケーションの必須コンポーネントが **[必須コンポーネント]** ダイアログ ボックスに表示されない場合は、カスタム ブートストラップ パッケージを作成して Visual Studio に追加できます。 それにより、**[必須コンポーネント]** ダイアログ ボックスで必須コンポーネントを選択できるようになります。 詳細については、「[ブートストラップ パッケージの作成](../deployment/creating-bootstrapper-packages.md)」を参照してください。

 既定では、ブートストラップは ClickOnce の配置で有効です。 ClickOnce の配置に生成されるブートストラップは署名付きです。 ブートストラップは任意のコンポーネントに対して無効にできますが、これは、該当するコンポーネントの正しいバージョンが既にすべてのターゲット コンピューターにインストールされていることを確認した場合のみ行ってください。

## <a name="bootstrapping-and-clickonce-deployment"></a>ブートストラップと ClickOnce 配置
 アプリケーションをクライアント コンピューターにインストールする前に、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] はクライアントを検査して、アプリケーション マニフェストに一定の必要条件が指定されているかどうかを確認します。 次の要件があります。

- 最低限必要な共通言語ランタイムのバージョン。これはアプリケーション マニフェストにアセンブリ依存関係として指定されます。

- アプリケーションに最低限必要な Windows オペレーティング システムのバージョン。これは、アプリケーション マニフェストに `<osVersionInfo>` 要素を使用して指定されます。 (「[\<dependency> 要素](../deployment/dependency-element-clickonce-application.md)」を参照してください。)

- グローバル アセンブリ キャッシュ (GAC) にプレインストールされる必要があるすべてのアセンブリの最小バージョン。これは、アセンブリ マニフェストでアセンブリ依存関係の宣言によって指定されます。

  [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] で不足している必須コンポーネントを検出し、ブートストラップを使用して必須コンポーネントをインストールできます。 詳細については、「[方法: ClickOnce アプリケーションと共に必須コンポーネントをインストールする](../deployment/how-to-install-prerequisites-with-a-clickonce-application.md)」を参照してください。

> [!NOTE]
> [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] や *MageUI.exe* などのツールによって生成されたマニフェスト内の値を変更するには、アプリケーション マニフェストをテキスト エディターで編集した後に、アプリケーション マニフェストと配置マニフェストの両方に再署名する必要があります。 詳細については、「[方法: アプリケーション マニフェストおよび配置マニフェストに再署名](../deployment/how-to-re-sign-application-and-deployment-manifests.md)」を参照してください。

 Visual Studio と ClickOnce を使用してアプリケーションを配置する場合、既定で選択されるブートストラップ パッケージは、ソリューション内の .NET Framework のバージョンによって異なります。 ただし、対象の .NET Framework のバージョンを変更する場合は、**[必須コンポーネント]** ダイアログ ボックスのオプションを手動で更新する必要があります。

|対象の .NET Framework|選択されるブートストラップ パッケージ|
|---------------------------|------------------------------------|
|.NET Framework 4 Client Profile|.NET Framework 4 Client Profile<br /><br /> Windows インストーラー 3.1|
|.NET Framework 4|.NET Framework 4<br /><br /> Windows インストーラー 3.1|

 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 配置では、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 発行ウィザードで作成された *Publish.htm* ページが、アプリケーションのみをインストールするリンクまたはアプリケーションとブートストラップ コンポーネントの両方をインストールするリンクのいずれかを指します。

 ClickOnce 発行ウィザードまたは Visual Studio の [発行] ページを使用してブートストラップを生成する場合、*Setup.exe* は自動的に署名されます。 ただし、顧客の証明書を使用してブートストラップに署名する場合は、後でファイルに署名できます。

## <a name="bootstrapping-and-msbuild"></a>ブートストラップと MSBuild
 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] を使用せず、アプリケーションをコマンド ラインでコンパイルする場合は、Microsoft Build Engine (MSBuild) タスクを使用して [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ブートストラップ アプリケーションを作成できます。 詳細については、「[GenerateBootstrapper タスク](../msbuild/generatebootstrapper-task.md)」を参照してください。

 ブートストラップの代わりに、Microsoft SMS (Systems Management Server) などの電子ソフトウェア配布システムを使用して、コンポーネントを事前に配置することもできます。

## <a name="bootstrapper-setupexe-command-line-arguments"></a>ブートストラップ (Setup.exe) のコマンド ライン引数
 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] によって作成される *Setup.exe* と MSBuild タスクは、次のコマンド ライン引数セットをサポートします。 他の引数は、アプリケーション インストーラーに渡されます。

 ブートストラップ オプションを変更する場合は、未署名のブートストラップを変更し、後でブートストラップ ファイルに署名する必要があります。

| コマンドライン引数 | 説明 |
| - | - |
| **-?、-h、-help** | [ヘルプ] ダイアログ ボックスを表示します。 |
| **-url、-componentsurl** | このセットアップ用に保存されている URL とコンポーネントの URL を表示します。 |
| **-url=** `location` | *Setup.exe* が [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションを検索する URL を設定します。 |
| **-componentsurl=** `location` | *Setup.exe* が .NET Framework などの依存関係を検索する URL を設定します。 |
| **-homesite=** `true` **&#124;** `false` | `true` の場合、販売元のサイトの推奨場所から依存関係がダウンロードされます。 この設定は、 **-componentsurl** 設定よりも優先されます。 `false` の場合、 **-componentsurl** で指定された URL から依存関係がダウンロードされます。 |

## <a name="operating-system-support"></a>オペレーティング システムのサポート
 Visual Studio ブートストラップは、Windows Server 2008 Server Core ではサポートされていません。また、Windows Server 2008 R2 Server Core は機能が限定された、メンテナンスの容易なサーバー環境を提供するので、こちらでもサポートされていません。 たとえば、Server Core のインストール オプションでは、.NET Framework 3.5 Server Core プロファイルのみがサポートされています。そのため、完全な .NET Framework を必要とする Visual Studio の機能は実行できません。

## <a name="see-also"></a>関連項目
- [ClickOnce 配置ストラテジの選択](../deployment/choosing-a-clickonce-deployment-strategy.md)
- [ClickOnce のセキュリティと配置](../deployment/clickonce-security-and-deployment.md)