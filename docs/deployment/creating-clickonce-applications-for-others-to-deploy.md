---
title: 開発者以外が配置する ClickOnce アプリケーションの作成 | Microsoft Docs
description: .NET Framework 3.5 や以前のバージョンの .NET Framework で開発され、顧客がホストする ClickOnce アプリケーションについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- preserved branding information
- useManifestForTrust element
- customer deployments [ClickOnce]
- multiple ClickOnce deployment and branding
- ClickOnce applications, previous .NET Framework versions
- application manifests [ClickOnce]
- <useManifestForTrust> element
- manifests [ClickOnce]
- trust applications, ClickOnce
- ClickOnce applications, deployed by others
- ClickOnce applications, previous .NET Framework
ms.assetid: d20766c7-4ef3-45ab-8aa0-3f15b61eccaa
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 9554cad786669ae4aa3b9aa84ecd6b996ee196f3
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99888473"
---
# <a name="create-clickonce-applications-for-others-to-deploy"></a>開発者以外が配置する ClickOnce アプリケーションを作成する
ClickOnce 配置を作成するすべての開発者が、アプリケーション自体の配置を計画しているわけではありません。 彼らの多くは、ClickOnce を使用してアプリケーションをパッケージ化した後に、大企業などの顧客にファイルを引き渡します。 この顧客が、ネットワーク上でアプリケーションをホストする責任者になります。 このトピックでは、バージョン 3.5 より前のバージョンの .NET Framework における、このような配置に固有のいくつかの問題について説明します。 次に、.NET Framework 3.5 の "信頼のためにマニフェストを使用する" 新機能を使用して提供される新しいソリューションについて説明します。 最後は、古いバージョンの .NET Framework をまだ使用している顧客のために ClickOnce 配置を作成する場合に推奨される方法を示して締めくくります。

## <a name="issues-involved-in-creating-deployments-for-customers"></a>顧客向けの配置の作成に伴う問題
 顧客に配置を提供する予定であるときには、いくつかの問題が発生します。 最初の問題は、コードの署名に関することです。 ネットワーク全体に配置するには、ClickOnce 配置の配置マニフェストとアプリケーション マニフェストの両方がデジタル証明書で署名されている必要があります。 これにより、マニフェストの署名時に、開発者の証明書を使用するか、顧客の証明書を使用するかという問いが生じます。

 どの証明書を使用するかという問いが重要なのは、ClickOnce アプリケーションの ID は、配置マニフェストのデジタル署名に基づくためです。 開発者が配置マニフェストに署名すると、顧客が大企業で、企業の複数の部門が、カスタマイズされたバージョンのアプリケーションを配置する場合に競合状態に至る可能性があります。

 たとえば、Adventure Works に財務部と人事部があるとします。 どちらの部門も、SQL データベースに格納されているデータからレポートを生成する ClickOnce アプリケーションを、Microsoft Corporation からライセンスします。 各部門には、Microsoft から、各部門のデータ向けにカスタマイズされたバージョンのアプリケーションが提供されます。 これらのアプリケーションが同じ Authenticode 証明書で署名されている場合、ユーザーが両方のアプリケーションを使用しようとすると、ClickOnce では 2 番目のアプリケーションは最初のものと同一だと見なされるため、エラーが発生することになります。 この場合、顧客は、アプリケーションによってローカルに格納されたすべてのデータの損失を含め、予測不能の望ましくない副作用を経験する可能性があります。

 コード署名に関連するその他の問題は、配置マニフェストの `deploymentProvider` 要素です。これは、アプリケーションの更新プログラムを探す場所を ClickOnce に指示する要素です。 この要素は、署名の前に配置マニフェストに追加する必要があります。 この要素が後で追加された場合は、配置マニフェストに再署名する必要があります。

### <a name="require-the-customer-to-sign-the-deployment-manifest"></a>顧客が配置マニフェストに署名するよう要求する
 配置が唯一ではないというこの問題の解決策の 1 つは、開発者がアプリケーション マニフェストに署名し、顧客が配置マニフェストに署名することです。 このアプローチは正しく機能しますが、他の問題が発生します。 Authenticode 証明書は保護された資産のままにしておく必要があるため、顧客は配置に署名するという目的で、開発者にただ証明書を提供することはできません。 .NET Framework SDK で無料で使用できるツールを使用して配置マニフェスト自体に署名することは可能ですが、このために必要な技術的知識は、顧客が喜んで提供する、または提供できる知識よりも多い可能性があります。 そのような場合、開発者は通常、アプリケーション、Web サイト、またはその他のメカニズムを作成し、顧客がそれを通して、顧客用バージョンのアプリケーションを署名のために送信できるようにします。

### <a name="the-impact-of-customer-signing-on-clickonce-application-security"></a>ClickOnce アプリケーション セキュリティに対する顧客の署名の影響
 顧客がアプリケーション マニフェストに署名する必要があることに、開発者と顧客が同意したとしても、信頼されたアプリケーションの配置に当てはまる場合は特に、アプリケーションの ID に関わるその他の問題が発生します。 (この機能の詳細については、「[信頼されたアプリケーションの配置の概要](../deployment/trusted-application-deployment-overview.md)」を参照してください。) 仮に Adventure Works が、Microsoft Corporation によって提供されるすべてのアプリケーションが完全な信頼で実行されるように、クライアント コンピューターを構成しようとしているとします。 Adventure Works が配置マニフェストに署名する場合、ClickOnce では Adventure Work のセキュリティ署名を使用して、アプリケーションの信頼レベルを決定します。

## <a name="create-customer-deployments-by-using-application-manifest-for-trust"></a>信頼のためのアプリケーション マニフェストを使用して顧客の配置を作成する
 .NET Framework 3.5 の ClickOnce には、開発者と顧客に、マニフェストにどのように署名する必要があるかのシナリオに対する新しいソリューションを提供する新しい機能が含まれています。 ClickOnce アプリケーション マニフェストでは、`<useManifestForTrust>` という名前の新しい要素をサポートしています。これを使用すると、開発者は、アプリケーション マニフェストのデジタル署名が、信頼の決定に使用する必要があるものだと示すことができます。 開発者は、*Mage.exe*、*MageUI.exe*、Visual Studio などの ClickOnce パッケージ化ツールを使用して、アプリケーション マニフェストにこの要素を追加するだけでなく、マニフェストに発行元の名前とアプリケーションの名前の両方を埋め込むことができます。

 `<useManifestForTrust>` を使用する場合は、証明機関によって発行された Authenticode 証明書を使用して配置マニフェストに署名する必要がありません。 代わりに、自己署名証明書として知られているもので署名することができます。 自己署名証明書は、標準的な .NET Framework SDK ツールを使用して顧客または開発者のいずれかによって生成され、その後、標準的な ClickOnce 配置ツールを使用して配置マニフェストに適用されます。 詳細については、「[MakeCert](/windows/desktop/SecCrypto/makecert)」を参照してください。

 自己署名証明書を配置マニフェストのために使用すると、いくつかの利点があります。 `<useManifestForTrust>` によって、顧客が独自の Authenticode 証明書を取得したり作成したりする必要がなくなり、顧客のための配置が簡素化され、同時に開発者は、アプリケーションに関する自社独自のブランド アイデンティティを維持することができます。 結果として、セキュリティが強化され、一意のアプリケーション ID を持つ、署名された配置のセットとなります。 これにより、同じアプリケーションを複数の顧客に配置することで発生する可能性のある競合が解消されます。

 `<useManifestForTrust>` を有効にして ClickOnce 配置を作成する手順を追った説明については、「[チュートリアル: 再署名が不要で商標を保持する ClickOnce アプリケーションを手動で配置する](../deployment/walkthrough-manually-deploying-a-clickonce-app-no-re-signing-required.md)」を参照してください。

### <a name="how-application-manifest-for-trust-works-at-run-time"></a>信頼のためのアプリケーション マニフェストは実行時にどのように機能するか
 信頼のためのアプリケーション マニフェストを使用すると、実行時にどのように機能するかをより深く理解するために、次の例について考えてみてください。 .NET Framework 3.5 をターゲットとする、ある ClickOnce アプリケーションが Microsoft によって作成されます。 アプリケーション マニフェストは、`<useManifestForTrust>` 要素を使用しており、Microsoft によって署名されています。 Adventure Works は、自己署名証明書を使用して配置マニフェストに署名します。 Adventure Works のクライアントは、Microsoft が署名したすべてのアプリケーションを信頼するように構成されています。

 ユーザーが配置マニフェストへのリンクをクリックすると、ClickOnce によって、アプリケーションがユーザーのコンピューターにインストールされます。 証明書と配置情報により、クライアント コンピューター上のそのアプリケーションは、ClickOnce に対して一意に識別されます。 ユーザーが同じアプリケーションを異なる場所から再度インストールしようとすると、ClickOnce はこの ID を使用して、アプリケーションがクライアントに既に存在することを確認できます。

 次に ClickOnce により、アプリケーション マニフェストに署名するために使用されている Authenticode 証明書が調べられます。これで、ClickOnce が付与する信頼のレベルが決まります。 Adventure Works は Microsoft が署名したすべてのアプリケーションを信頼するようにクライアントを構成したため、この ClickOnce アプリケーションには完全な信頼が付与されます。 詳細については、「[信頼されたアプリケーションの配置の概要](../deployment/trusted-application-deployment-overview.md)」を参照してください。

## <a name="create-customer-deployments-for-earlier-versions"></a>以前のバージョンのための顧客用デプロイを作成する
 古いバージョンの .NET Framework を使用している顧客に ClickOnce アプリケーションを配置しようとしている場合は、どうすればよいでしょうか。 以降のセクションでは、お勧めするいくつかのソリューションと一緒に、それぞれの長所と短所についてまとめています。

### <a name="sign-deployments-on-behalf-of-customer"></a>顧客に代わって配置に署名する
 考えられる配置方法の 1 つは、顧客独自の秘密キーを使用して顧客に代わって配置に署名するメカニズムを、開発者が作成することです。 これによって開発者は、秘密キーや複数の配置パッケージを管理する必要がなくなります。 開発者は、各顧客に同じ配置を提供するだけで済みます。 署名サービスを使用して、環境に合わせたカスタマイズを行うかどうかは顧客に委ねられます。

 この方法の短所の 1 つは、その実装に必要な時間と費用です。 そのようなサービスは .NET Framework SDK に用意されているツールを使用して構築できますが、製品のライフサイクルに、より多くの開発時間が追加されることになります。

 このトピックで前述したように、顧客ごとにアプリケーションのバージョンを用意するとアプリケーション ID が同じになるため、競合状態に至る可能性があります。 これが懸念される場合、開発者は、配置マニフェストを生成するときに使用する Name フィールドを変更して、各アプリケーションに一意の名前を付けることができます。 これにより、アプリケーションのバージョンごとに別個の ID が作成され、ID が競合するおそれがなくなります。 このフィールドは、Mage.exe の `-Name` 引数と、MageUI.exe の **[名前]** タブの **[名前]** フィールドに対応しています。

 たとえば、開発者が Application1 という名前のアプリケーションを作成したとします。 開発者は、Name フィールドを Application1 に設定して単一の配置を作成するのではなく、Application1-CustomerA や Application1-CustomerB のように、この名前に顧客固有のバリエーションを指定して複数の配置を作成することができます。

### <a name="deploy-using-a-setup-package"></a>セットアップ パッケージを使用して配置する
 2 つ目の考えられる配置方法は、Microsoft Setup プロジェクトを生成して、ClickOnce アプリケーションの初期配置を実行することです。 これは、いくつかの異なる形式のいずれかで提供できます。MSI の配置として、セットアップ実行可能ファイル (.EXE) として、またはバッチ スクリプトと共に使用するキャビネット (.cab) ファイルとして提供できます。

 開発者はこの手法を利用して、アプリケーション ファイル、アプリケーション マニフェスト、テンプレートとして機能する配置マニフェストが含まれる配置を顧客に提供します。 顧客はセットアップ プログラムを実行します。これにより、配置 URL (ユーザーによる ClickOnce アプリケーションのインストール元になるサーバーまたはファイル共有の場所) とデジタル証明書の入力を求めるダイアログが表示されます。 セットアップ アプリケーションでは、更新確認の間隔など、追加の ClickOnce 構成オプションのダイアログを表示することも選択できます。 この情報が収集されると、セットアップ プログラムによって、実際の配置マニフェストの生成と署名が行われ、指定されたサーバーの場所に ClickOnce アプリケーションが発行されます。

 この状況において、顧客が配置マニフェストに署名できる方法は 3 つあります。

1. 顧客は、証明機関 (CA) によって発行された有効な証明書を使用できます。

2. このアプローチのバリエーションとして、顧客は自己署名証明書を使用して配置マニフェストに署名することを選択できます。 これの短所は、インストールするかどうかの確認メッセージが表示されるときに、アプリケーションでは "不明な発行元" という表現が表示されることです。 ただし長所は、小規模な顧客が、証明機関によって発行される証明書の取得に必要な時間とコストを投じる必要がなくなるという点です。

3. 最後に、開発者が独自の自己署名証明書をセットアップ パッケージに含めることができます。 このようにすると、このトピックで前述したアプリケーション ID に関する潜在的問題が生じます。

   セットアップ配置プロジェクトによる方法の短所は、カスタムの配置アプリケーションを構築するために必要な時間とコストです。

### <a name="have-customer-generate-deployment-manifest"></a>顧客に配置マニフェストを生成してもらう
 考えられる 3 つ目の配置方法は、顧客にアプリケーション ファイルとアプリケーション マニフェストのみを渡すことです。 このシナリオでは、.NET Framework SDK を使用して配置マニフェストの生成と署名を行う役割を果たすのは顧客です。

 この方法の短所は、顧客側で、.NET Framework SDK ツールをインストールし、それらの使用に習熟している開発者またはシステム管理者を用意する必要がある点です。 一部の顧客では、自社での技術的労力がほとんど不要、またはまったく不要のソリューションが求められます。

## <a name="see-also"></a>関連項目
- [再署名を行わずテスト サーバーおよび運用サーバーのために ClickOnce アプリケーションを配置する](../deployment/deploying-clickonce-applications-for-testing-and-production-without-resigning.md)
- [チュートリアル: ClickOnce アプリケーションを手動で配置する](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)
- [チュートリアル: 再署名が不要で商標を保持する ClickOnce アプリケーションの手動配置](../deployment/walkthrough-manually-deploying-a-clickonce-app-no-re-signing-required.md)