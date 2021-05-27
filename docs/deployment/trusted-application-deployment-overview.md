---
title: 信頼されたアプリケーションの配置の概要 | Microsoft Docs
description: 信頼されたアプリケーションの配置テクノロジを使用して、管理者特権のアクセス許可を持つ ClickOnce アプリケーションを配置する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, install without prompting
- ClickOnce deployment, security
- trusted application deployment
ms.assetid: b24a1702-8fbe-45b1-87a0-9618a0708f1d
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 76f8aec5cec1d06b3c6162524e02ae1bb2faefc0
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99927406"
---
# <a name="trusted-application-deployment-overview"></a>信頼されたアプリケーションの配置の概要
このトピックでは、信頼されたアプリケーションの配置テクノロジを使用して、昇格されたアクセス許可を持つ [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションを配置する方法の概要を示します。

 信頼されたアプリケーションの配置テクノロジは、 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 配置のテクノロジの一部です。このテクノロジを使用すると、どのような規模の組織でも、ユーザーに確認することなく、従来より安全な方法でマネージド アプリケーションにアクセス許可を付与できます。 信頼されたアプリケーションの配置の場合、組織に必要な処理は、信頼された発行元の一覧をクライアント コンピューターで構成することだけです。発行元は、Authenticode 証明書を使用して識別します。 その後は、信頼された発行元のいずれかによって署名されている [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションには、通常より高いレベルの信頼が与えられます。

> [!NOTE]
> 信頼されたアプリケーションの配置では、ユーザー コンピューターの構成を一度だけ実行する必要があります。 管理されたデスクトップ環境では、グローバル ポリシーを使用してこの構成を実行できます。 この方法がアプリケーションに適さない場合は、代わりに、アクセス許可を昇格する機能を使用します。 詳細については、「[ClickOnce アプリケーションの発行](../deployment/securing-clickonce-applications.md)」を参照してください。

## <a name="trusted-application-deployment-basics"></a>信頼されたアプリケーションの配置の基本
 次の表は、信頼されたアプリケーションの配置に関連するオブジェクトおよびロールを示しています。

|オブジェクトまたはロール|説明|
|--------------------|-----------------|
|administrator|クライアント コンピューターの更新と保守を担当する組織エンティティです。|
|信頼マネージャー|クライアント アプリケーションに対するセキュリティ処理を実施する、共通言語ランタイム (CLR) 内のサブシステムです。|
|publisher|アプリケーションに関する記述と保守を実行するエンティティです。|
|配置元|アプリケーションをパッケージ化し、ユーザーに配布するエンティティです。|
|証明書 (certificate)|公開キーと秘密キーで構成される暗号化署名です。一般には、その信頼性を保証できる証明機関 (CA: Certification Authority) から発行されます。|
|Authenticode 証明書|この証明書を使用できるユーザーの情報などを記述したメタデータを埋め込んだ証明書です。|
|証明機関|発行元の ID を検査し、それらの発行元に、発行元のメタデータを埋め込んだ証明書を発行する組織です。|
|root authority|他の証明機関が証明書を発行することを承認する証明機関です。|
|キー コンテナー|証明書を格納するための Microsoft Windows の論理ストレージ領域です。|
|信頼された発行元|クライアント コンピューターの証明書信頼リスト (CTL: Certificate Trust List) に Authenticode 証明書が追加された発行元です。|

 大規模な組織では、発行元と配置元のエンティティが異なる場合が少なくありません。

- 発行元は、 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションを作成するグループです。

- 配置元は、 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションを企業のデスクトップ コンピューターに配布するグループ (通常は、情報技術 (IT) 部門) です。

信頼されたアプリケーションの配置を活用するには、次の手順に従う必要があります。

1. 発行元の証明書を取得します。

2. 発行元をすべてのクライアント コンピューターの信頼された発行元ストアに追加します。

3. [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションを作成します。

4. 発行元の証明書で配置マニフェストに署名します。

5. アプリケーション配置をクライアント コンピューターに発行します。

### <a name="obtain-a-certificate-for-the-publisher"></a>発行元の証明書を取得する
 デジタル証明書は、Microsoft Authenticode 認証およびセキュリティ システムの主要なコンポーネントです。 Authenticode は、Windows オペレーティング システムの標準機能です。 すべての [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションには、信頼されたアプリケーションの配置の対象であるかどうかにかかわらず、デジタル証明書によって署名する必要があります。 Authenticode が [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] とどのように連携するかについては、「[ClickOnce と Authenticode](../deployment/clickonce-and-authenticode.md)」を参照してください。

### <a name="add-the-publisher-to-the-trusted-publishers-store"></a>発行元を信頼された発行元ストアに追加する
 開発した [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションに高いレベルの信頼を与えるには、そのアプリケーションを実行する各クライアント コンピューターに対して、発行元の証明書を信頼された発行元として追加する必要があります。 これは 1 回だけ実行する構成タスクです。 この構成が完了すると、同じ発行元の証明書で署名された [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションを必要なだけ配置し、そのすべてに高い信頼を与えて実行できます。

 Windows オペレーティング システムを実行する会社のイントラネットなど、管理されたデスクトップ環境にアプリケーションを配置する場合には、グループ ポリシーと一緒に新しい証明書信頼リスト (CTL) を作成することによって、信頼された発行者元クライアント コンピューターの発行元ストアに追加できます。 詳細については、「 [グループ ポリシー オブジェクト用の証明書信頼リストを作成する](/previous-versions/windows/it-pro/windows-server-2003/cc728449(v=ws.10))」を参照してください。

 管理されたデスクトップ環境にアプリケーションを配置しない場合には、次のような方法で信頼された発行元ストアに証明書を追加できます。

- <xref:System.Security.Cryptography?displayProperty=fullName> 名前空間。

- *CertMgr.exe*。これは、Internet Explorer のコンポーネントであるため、Windows 98 以降の全バージョンに含まれています。 詳細については、「[Certmgr.exe (証明書マネージャー ツール)](/dotnet/framework/tools/certmgr-exe-certificate-manager-tool)」を参照してください。

### <a name="create-a-clickonce-application"></a>ClickOnce アプリケーションを作成する
 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションは、マニフェスト ファイルと組み合わされた .NET Framework クライアント アプリケーションです。マニフェスト ファイルでは、アプリケーションについての説明を記述し、インストール パラメーターを指定します。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] の **[発行]** コマンドを使用すると、開発したプログラムを [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]アプリケーションに変換できます。 または、 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] に含まれているツールを使用して、 [!INCLUDE[winsdklong](../deployment/includes/winsdklong_md.md)]配置に必要なすべてのファイルを生成することもできます。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] を配置する手順の詳細については、「[チュートリアル: ClickOnce アプリケーションを手動で配置する](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)」を参照してください。

 信頼されたアプリケーションの配置は [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]に特有の機能であり、 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションに対してのみ使用できます。

### <a name="sign-the-deployment"></a>配置に署名する
 使用する証明書を取得したら、この証明書を使用して配置に署名する必要があります。 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] の発行ウィザードを使用してアプリケーションを配置する場合は、独自に証明書を指定しなければ、ウィザードが自動的にテスト証明書を生成します。 また、 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] の [プロジェクト デザイナー] ウィンドウを使用して、CA から取得した証明書を指定することもできます。  「[方法: 発行ウィザードを使用して ClickOnce アプリケーションを発行する](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)」も参照してください。

> [!CAUTION]
> テスト証明書を使用してアプリケーションを配置することはお勧めできません。

 また、SDK の *Mage.exe* ツールまたは *MageUI.exe* ツールを使用してアプリケーションに署名することもできます。 詳細については、「[チュートリアル: ClickOnce アプリケーションを手動で配置する](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)」を参照してください。 配置への署名に関連するコマンド ライン オプションの完全な一覧については、「[Mage.exe (マニフェストの生成および編集ツール)](/dotnet/framework/tools/mage-exe-manifest-generation-and-editing-tool)」を参照してください。

### <a name="publish-the-application"></a>アプリケーションを発行する
 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] マニフェストに署名した後は、すぐにアプリケーションをインストール場所に発行できます。 インストール場所には、Web サーバー、ファイル共有、またはローカル ディスクを使用できます。 信頼マネージャーは、クライアントが配置マニフェストに初めてアクセスした時点で、インストール済みの信頼された発行元を参照して、 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションの実行時に高いレベルの権限を与えるかどうかを判断する必要があります。 信頼マネージャーは、配置に署名する際に使用された証明書と、クライアントの信頼された発行元ストアに格納されている証明書とを比較することによって、この判断をします。 信頼マネージャーが一致する証明書を検出した場合は、アプリケーションの実行時に高い信頼が与えられます。

## <a name="trusted-application-deployment-and-permission-elevation"></a>信頼されたアプリケーションの配置とアクセス許可の昇格
 現在の発行元が信頼された発行元でない場合、信頼マネージャーは、アプリケーションのアクセス許可を昇格するためにアクセス許可の昇格機能を使用するかどうかをユーザーに確認します。 ただし、管理者がアクセス許可の昇格を無効にしている場合、アプリケーションは実行のためのアクセス許可を取得できません。 アプリケーションは実行されず、ユーザーに通知が表示されることもありません。 アクセス許可の昇格の詳細については、「[ClickOnce アプリケーションのセキュリティ](../deployment/securing-clickonce-applications.md)」を参照してください。

## <a name="limitations-of-trusted-application-deployment"></a>信頼されたアプリケーションの配置に関する制限事項
 信頼されたアプリケーションの配置は、Web 経由または会社のファイル共有から配置される [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションに昇格された信頼を与えるために使用できます。 CD で配布される [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションには既定で完全信頼が付与されるため、信頼されたアプリケーションの配置を使用する必要はありません。

## <a name="see-also"></a>関連項目
- [Mage.exe (マニフェストの生成および編集ツール)](/dotnet/framework/tools/mage-exe-manifest-generation-and-editing-tool)
- [チュートリアル: ClickOnce アプリケーションを手動で配置する](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)
