---
title: Visual Studio での接続されたエクスペリエンス
description: 接続されたエクスペリエンスでは、クライアント コンピューターからインターネットに接続し、顧客にサービスが提供されます。
ms.date: 05/20/2021
ms.topic: conceptual
helpviewer_keywords: ''
author: SayyedaM
ms.author: sayyedamussa
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.openlocfilehash: 689fc40be8aee959023777a3fac6d9134ee979ea
ms.sourcegitcommit: 8b75524dc544e34d09ef428c3ebbc9b09f14982d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2021
ms.locfileid: "113222891"
---
# <a name="connected-experiences-in-visual-studio"></a>**Visual Studio での接続されたエクスペリエンス** #

Visual Studio は、効率的にコードを作成できるように設計されたクライアント ソフトウェア アプリケーションと接続されたエクスペリエンスで構成されています。 接続されたエクスペリエンスの例としては、[NuGet](/nuget/consume-packages/install-use-packages-visual-studio) パッケージの更新、[IntelliCode](/visualstudio/intellicode/overview) の提案の選択、[Live Share](/visualstudio/liveshare/quickstart/share) による別の開発者との共同作業が挙げられます。 

## <a name="choose-whether-these-connected-experiences-are-available-to-use"></a>このような接続されたエクスペリエンスを使用できるようにするかどうかを選択する ##

どの接続済みのエクスペリエンスを使用するかを選択することができます。 特定の接続されたエクスペリエンスを使用するには、Visual Studio の EULA のさまざまな追加条項に同意する必要があります。 これらのエクスペリエンスは、マイクロソフトが所有するオンライン サービスや、サードパーティーによって所有されているサービスである場合があります。 たとえば、GitHub の接続されたエクスペリエンスを使用する場合、[GitHub のプライバシーについての声明](https://docs.github.com/github/site-policy/github-privacy-statement)と [GitHub 利用規約](https://docs.github.com/github/site-policy/github-terms-of-service)、[GitHub 企業向け利用規約](https://docs.github.com/github/site-policy/github-corporate-terms-of-service)、および[その他の製品条項](https://docs.github.com/github/site-policy/github-additional-product-terms)が適用されます。 [問題を報告する](/visualstudio/ide/how-to-report-a-problem-with-visual-studio)場合は、[Microsoft の使用条件](https://www.microsoft.com/legal/terms-of-use)と [Microsoft プライバシー ステートメント](https://privacy.microsoft.com/en-us/privacystatement)に同意したことになります。 NuGet サービスを使用する場合は、[NuGet の使用条件](https://www.nuget.org/policies/Terms)と [Microsoft プライバシー ステートメント](https://privacy.microsoft.com/en-us/privacystatement)に同意したことになります。 

Visual Studio をインストールする場合は、[必要に応じて、インストールするワークロードとコンポーネントを選択できます](/visualstudio/install/install-visual-studio)。 ワークロードとコンポーネントはサードパーティーのソフトウェアを活用でき、機能によっては接続されたエクスペリエンスを有効にすることができます。 たとえば、[Azure 開発ワークロードをダウンロードすると、クラウド アプリを Azure に発行することができます](https://visualstudio.microsoft.com/vs/features/azure/)。 インストールの選択によっては、[ツールとオプション] メニューを使用して接続されたエクスペリエンスに接続し、構成し、使用することもできます。 たとえば、サーバーに接続したり、Azure サービス認証を追加したり、IntelliCode または LiveShare の設定を変更したりできます。  

また、組織の[ファイアウォール設定](/visualstudio/install/install-and-use-visual-studio-behind-a-firewall-or-proxy-server)を使用して、サービスへの接続を有効または無効にすることもできます。 エンドポイントへの接続を無効にすると、関連する Visual Studio 機能のパフォーマンスが低下したり、無効になったりする可能性があることに注意してください。 

最後に、Visual Studio Marketplace には、ファーストまたはサードパーティーの接続されたエクスペリエンスを可能にする拡張機能が用意されています。 Visual Studio Marketplace には、[Visual Studio Marketplace の使用条件](https://cdn.vsassets.io/v/M146_20190123.39/_content/Microsoft-Visual-Studio-Marketplace-Terms-of-Use.pdf)と [Microsoft プライバシー ステートメント](https://privacy.microsoft.com/en-us/privacystatement)が適用されます。 各拡張機能には、そのオファリングに関連する特定の使用条件およびプライバシー ステートメントに対する契約が必要です。  


## <a name="required-service-data"></a>必要なサービス データ ##

必要なサービス データには、基になるサービスをセキュリティで保護し、最新の状態に保ち、想定どおりに実行するために必要な、接続されたエクスペリエンスの操作に関連する情報を含めることができます。 IntelliCode など、コンテンツを分析する接続されたエクスペリエンスを使用することを選択した場合は、接続されたエクスペリエンスを提供するために、モデルに対して選択したコードも送信され、処理されます。 必要なサービス データには、接続されたエクスペリエンスでタスク (NuGet パッケージの更新など) を実行するために必要な情報を含めることもできます。 特定のサービスを使用するかどうかを選択することで、必要なサービス データを管理できます。 サービスを使用しない場合、必要なサービス データは収集されません。 

診断データはデバイスで実行されているソフトウェアに関連するため、必要なサービスデータは診断データとは異なります。 [Visual Studio カスタマー エクスペリエンス向上プログラム (VSCEIP) に参加するかどうかによって、診断データのプライバシー設定が制御されます](/visualstudio/ide/visual-studio-experience-improvement-program)が、この設定は必要なサービス データが送信されるかどうかには影響しません。 

## <a name="diagnostic-data-collection"></a>診断データ コレクション ##

診断データは Visual Studio をセキュリティで保護された最新の状態に保ち、問題を検出、診断、修正し、さらに製品の機能強化を行うためにも使用されます。 診断データは、ユーザーのデバイスで実行されている Visual Studio クライアント ソフトウェアについて収集され、マイクロソフトに送信されます。

オプトアウトすると、任意の診断データ収集を選択しないことになります。 Visual Studio をセキュリティで保護し、常に最新の状態にし、予想どおりに実行させるには、一部の診断データ収集が必須です。 必須の診断データ収集は、[VSCEIP](/visualstudio/ide/visual-studio-experience-improvement-program) のオプトアウトを選択しても影響を受けません。 
