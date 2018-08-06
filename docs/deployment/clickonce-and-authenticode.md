---
title: ClickOnce と Authenticode |Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- .pfx files
- ClickOnce deployment, Authenticode
- Authenticode, ClickOnce
- ClickOnce deployment, certificates
- ClickOnce deployment, security
ms.assetid: ab5b6712-f32a-4e33-842f-e88ab4818ccf
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 2943766bb7b0df6d2e0974f8a8c1b52747f31526
ms.sourcegitcommit: 206e738fc45ff8ec4ddac2dd484e5be37192cfbd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2018
ms.locfileid: "39512211"
---
# <a name="clickonce-and-authenticode"></a>ClickOnce と Authenticode
*Authenticode* は、業界標準の暗号化を使用して、アプリケーションの発行元の信頼性を検証するデジタル証明書によってアプリケーション コードに署名する Microsoft テクノロジです。 アプリケーションの配置に Authenticode を使用し、 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] はトロイの木馬のリスクを軽減します。 トロイの木馬は、悪意のある第三者が、確立された信頼できるソースからの正規のプログラムと偽って示すウイルスやその他の有害なプログラムです。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 配置のデジタル証明書による署名は、アセンブリとファイルが改ざんされていないことを確認するためのオプションの手順です。  
  
 以下のセクションでは、Authenticode で使用するさまざまな種類のデジタル証明書、証明機関 (CA) を使用して証明書を検証するしくみ、証明書におけるタイムスタンプの役割、および証明書で使用できるストレージの方法について説明します。  
  
## <a name="authenticode-and-code-signing"></a>Authenticode とコード署名  
 *デジタル証明書* は、証明書の発行先であるアプリケーション発行者と証明書を発行した機関を示すメタデータと共に、暗号化公開キー/秘密キーのペアが格納されたファイルです。  
  
 Authenticode 証明書にはさまざまな種類があります。 それぞれの証明書は、異なる種類の署名用に構成されています。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションの場合、コード署名で有効な Authenticode 証明書が必要です。 電子メールのデジタル証明書など、別の種類の証明書によって [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションへの署名を試みた場合、アプリケーションは動作しません。 詳細については、次を参照してください。[コード署名の概要](http://go.microsoft.com/fwlink/?LinkId=179452)します。  
  
 コード署名の証明書は、次の 3 つの方法のいずれかで取得することができます。  
  
-   証明書の販売元から購入する。  
  
-   デジタル証明書の作成を担当する組織内のグループから受け取る。  
  
-   New-selfsignedcertificate PowerShell コマンドレットを使用するかを使用して、独自の証明書を生成*MakeCert.exe*に含まれている、[!INCLUDE[winsdklong](../deployment/includes/winsdklong_md.md)]します。  
  
### <a name="how-using-certificate-authorities-helps-users"></a>によりユーザー、証明機関を使用する方法  
 新規-自己署名証明書を使用して生成された証明書または*MakeCert.exe*ユーティリティが一般的と呼ばれる、*自己証明書*または*テスト証明書*。この種の証明書は、同じ動作はるか方法、 *.snk*ファイルで .NET Framework で動作します。 この証明書は、秘密/公開暗号化キーのペアのみで構成され、発行者に関する検証可能な情報を含んでいません。 自己証明書を使用すると、イントラネット上に信頼性の高い [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションを配置できます。 ただし、これらのアプリケーションをクライアント コンピューターで実行した場合は、 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] が、不明な発行元からのものとしてアプリケーションを識別します。 既定では、自己証明書によって署名され、インターネットを介して配置された [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションは、信頼されたアプリケーションの配置を利用できません。  
  
 これに対し、証明書販売元や企業内の部門などの CA から証明書を受け取る場合は、証明書によってユーザーのセキュリティが強化されます。 証明書によって、署名済みソフトウェアの発行者が識別されるだけでなく、署名を行った CA に問い合わせてその ID が検査されます。 CA がルート証明機関でない場合、Authenticode はルート証明機関まで "信頼チェーン" をたどって、その CA が証明書の発行を承認されているかどうかを検査します。 セキュリティを強化するために、可能であれば常に CA によって発行された証明書を使用することをお勧めします。  
  
 自己証明書を生成する詳細については、次を参照してください。 [New-selfsignedcertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate)または[MakeCert](/windows/desktop/SecCrypto/makecert)します。  
  
### <a name="timestamps"></a>タイムスタンプ  
 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションの署名に使用する証明書は、一定の期間 (通常は 12 か月) で期限切れになります。 新しい証明書を持つアプリケーションに再署名を繰り返さずに済むように、 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ではタイムスタンプがサポートされています。 アプリケーションがタイムスタンプ付きで署名されると、タイムスタンプが有効な場合は、有効期限が過ぎていても、その証明書が受け付けられます。 これにより、期限切れの証明書と有効なタイムスタンプを持つ [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションをダウンロードして実行できます。 また、期限切れの証明書を持つインストール済みのアプリケーションでは、引き続き、更新プログラムをダウンロードしてインストールできます。  
  
 アプリケーション サーバーにタイムスタンプを含めるには、タイムスタンプ サーバーが必要です。 タイムスタンプ サーバーを選択する方法については、「 [How to: Sign Application and Deployment Manifests](../ide/how-to-sign-application-and-deployment-manifests.md)」を参照してください。  
  
### <a name="update-expired-certificates"></a>有効期限が切れた証明書を更新します。  
 以前のバージョンの .NET Framework では、証明書の期限が切れているアプリケーションを更新すると、そのアプリケーションが機能しなくなる可能性がありました。 この問題を解決するには、次のいずれかの方法を使用します。  
  
-   .NET Framework のバージョンを 2.0 SP1 以降 (Windows XP の場合) または 3.5 以降 (Windows Vista の場合) に更新します。  
  
-   アプリケーションをアンインストールし、有効な証明書を含む新しいバージョンを再インストールします。  
  
-   証明書を更新するコマンド ライン アセンブリを作成します。 このプロセスの詳細な手順については、 [Microsoft サポートの記事 925521](http://go.microsoft.com/fwlink/?LinkId=179454)を参照してください。  
  
### <a name="store-certificates"></a>証明書を格納します。  
  
-   証明書を格納することができます、 *.pfx*キー コンテナーの内部にするか、ファイル システム上のファイルで格納できます。 Windows ドメインのユーザーは、多数のキー コンテナーを持つことができます。 既定では、 *MakeCert.exe*が保存することを指定しない限り、個人のキー コンテナーに証明書を保存、 *.pfx*代わりにします。 *Mage.exe*と*MageUI.exe*、[!INCLUDE[winsdkshort](../debugger/debug-interface-access/includes/winsdkshort_md.md)]を作成するためのツール[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]の展開では、どちらの方法で格納される証明書を使用することができます。  
  
## <a name="see-also"></a>関連項目  
 [ClickOnce のセキュリティと配置](../deployment/clickonce-security-and-deployment.md)   
 [セキュリティで保護された ClickOnce アプリケーション](../deployment/securing-clickonce-applications.md)   
 [信頼されたアプリケーション展開の概要](../deployment/trusted-application-deployment-overview.md)   
 [Mage.exe (マニフェストの生成および編集ツール)](/dotnet/framework/tools/mage-exe-manifest-generation-and-editing-tool)