---
title: 複数の構成でクラウド サービスを構成する
description: ServiceDefinition.csdef、ServiceConfiguration.Local.cscfg および ServiceConfiguration.Cloud.cscfg ファイルを変更して、Azure クラウド サービス プロジェクトを構成する方法について説明します。
ms.custom: SEO-VS-2020
author: ghogen
manager: jmartens
ms.workload: azure-vs
ms.topic: how-to
ms.date: 11/11/2017
ms.author: ghogen
ms.openlocfilehash: b5b4a5bedd77855aa41c4bf5e565738fc8fb4f0e
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99844100"
---
# <a name="configuring-your-azure-project-in-visual-studio-to-use-multiple-service-configurations"></a>Visual Studio での複数のサービス構成を使用した Azure プロジェクトの構成

Visual Studio の Azure クラウド サービス プロジェクトには、`ServiceDefinition.csdef`、`ServiceConfiguration.Local.cscfg` および `ServiceConfiguration.Cloud.cscfg` の 3 つの構成ファイルが含まれています。

- `ServiceDefinition.csdef` はクラウド サービスとそのロールの要件を説明し、すべてのインスタンスに適用される設定を提供するために Azure にデプロイされます。 設定は Azure サービス ホスト ランタイム API を使用して実行時に読み込むことができます。 クラウド サービスが停止しているときにのみ、このファイルを Azure 上で更新できます。
- `ServiceConfiguration.Local.cscfg` および `ServiceConfiguration.Cloud.cscfg` は、定義ファイル内の設定の値を指定し、各ロールが実行するインスタンスの数を指定します。 "ローカル" ファイルにはローカルでのデバッグで使用される値が含まれています。"クラウド" ファイルは Azure に `ServiceConfiguration.cscfg` としてデプロイされ、サーバー環境の設定を指定します。 このファイルは、Azure でクラウド サービスを実行しているときに更新できます。

構成設定の管理と変更は、Visual Studio の適用可能なロールのプロパティ ページを使用して行われます (ロールを右クリックして **[プロパティ]** を選択するか、ロールをダブルクリックします)。 **[サービス構成]** ボックスでどの構成が選択されても、変更は適用できます。 次のセクションで説明する点を除けば、Web ロールと worker ロールのプロパティはほぼ同じです。

![VS_Solution_Explorer_Roles_Properties](./media/vs-azure-tools-multiple-services-project-configurations/IC784076.png)

サービス定義ファイルとサービス構成ファイルの基になるスキーマの詳細については、[.csdef XML スキーマ](/azure/cloud-services/schema-csdef-file)と [.cscfg XML スキーマ](/azure/cloud-services/schema-cscfg-file)に関する記事を参照してください。 サービス構成の詳細については、「[クラウド サービスの構成方法](/azure/cloud-services/cloud-services-how-to-configure-portal)」を参照してください。

## <a name="configuration-page"></a>[構成] ページ

### <a name="service-configuration"></a>サービス構成

変更の影響を受ける `ServiceConfiguration.*.cscfg` ファイルを選択します。 既定では、ローカルとクラウドという種類があり、**[管理...]** コマンドを使用して構成ファイルのコピー、名前の変更、および削除ができます。 これらのファイルがクラウド サービス プロジェクトに追加され、**[ソリューション エクスプローラー]** に表示されます。 ただし、構成の名前変更や削除は、このコントロールからのみ実行できます。

### <a name="instances"></a>インスタンス

**[インスタンス数]** プロパティに、このロールに対してサービスが実行するインスタンスの数を設定します。

**[VM サイズ]** プロパティには、**[極小]**、**[小]**、**[中]**、**[大]**、**[特大]** のいずれかを設定します。  詳細については、「[クラウド サービスのサイズを構成する](/azure/cloud-services/cloud-services-sizes-specs)」を参照してください。

### <a name="startup-action-web-role-only"></a>スタートアップ アクション (Web ロールのみ)

このプロパティを設定して、デバッグの開始時に Visual Studio が HTTP エンドポイントと HTTPS エンドポイントのいずれか、または両方のエンドポイント用に Web ブラウザーを起動するように指定します。

**[HTTPS エンドポイント]** オプションは、ロールの HTTPS エンドポイントを既に定義している場合にのみ使用できます。 HTTPS エンドポイントは、 **[エンドポイント]** プロパティ ページで定義できます。

HTTPS エンドポイントを既に追加している場合は、既定で [HTTPS エンドポイント] オプションが有効になり、Visual Studio はデバッグ開始時にこのエンドポイント用のブラウザーと HTTP エンドポイント用のブラウザーを起動します (どちらのスタート アップ オプションも有効であることが前提です)。

### <a name="diagnostics"></a>診断

既定では、Web ロールに対して診断が有効になっています。 Azure クラウド サービス プロジェクトとストレージ アカウントは、ローカル ストレージ エミュレーターを使用するように設定されています。 Azure にデプロイする準備ができたら、ビルダーのボタン (**[…]**) を選択すると、Azure Storage を代わりに使用できます。 要求時に、または自動的にスケジュールされた間隔で、ストレージ アカウントに診断データを転送できます。 Azure Diagnostics の詳細については、[Azure Cloud Services および Virtual Machines での診断の有効化](/azure/cloud-services/cloud-services-dotnet-diagnostics)に関するページを参照してください。

## <a name="settings-page"></a>[設定] ページ

**[設定]** ページで、名前と値のペアからなる設定を構成に追加できます。 ロール内でコードを実行すると、[Azure マネージド ライブラリ](/previous-versions/azure/dn602775(v=azure.11))で提供されるクラス (具体的には [GetConfigurationSettingValue](/previous-versions/azure/reference/ee772857(v=azure.100)) メソッド) を使用して、実行時に構成設定の値を読み取ることができます。

### <a name="configuring-a-connection-string-for-a-storage-account"></a>ストレージ アカウントの接続文字列の構成

接続文字列とは、ストレージ エミュレーターまたは Azure Storage アカウントの接続情報と認証情報を提供する設定です。 ロール内のコードが Azure Storage (BLOB、キュー、またはテーブル) にアクセスするたびに、接続文字列が必要になります。

> [!Note]
> Azure ストレージ アカウントの接続文字列には、定義された形式を使用する必要があります (「[Azure Storage の接続文字列を構成する](/azure/storage/common/storage-configure-connection-string)」をご覧ください)。

必要に応じてローカル ストレージを使用するように接続文字列を設定しておき、クラウド サービスのアプリケーションをデプロイするときに Azure Storage アカウントに設定することができます。 接続文字列を適切に設定していないと、ロールの起動に失敗したり、初期化状態、ビジー状態、停止状態を順に繰り返したりする可能性があります。

接続文字列を作成するには、**[設定の追加]** を選択し、**[型]** を "接続文字列" に設定します。

新規または既存の接続文字列については、"*値*" フィールドの右側にある **[...]** を選択して **[ストレージ接続文字列の作成]** ダイアログを開きます。

1. **[接続方法]** で **[サブスクリプション]** オプションを選択して、サブスクリプションからストレージ アカウントを選択します。 そうすると Visual Studio が、`.publishsettings` ファイルからストレージ アカウントの資格情報を自動的に取得します。
1. **[手動で入力された資格情報]** を選択すると、Azure Portal の情報を使用してアカウント名とキーを直接指定できます。 アカウント キーをコピーするには:
    1. Azure Portal でストレージ アカウントに移動し、**[キーの管理]** を選択します。
    1. アカウント キーをコピーするには、Azure Portal でストレージ アカウントに移動し、**[設定] > [アクセス キー]** を選択してから、コピー ボタンを使用してプライマリ アクセス キーをクリップボードにコピーします。
1. 接続オプションのいずれかを選択します。 **[カスタム エンドポイントの指定]** では、特定の BLOB の URL、テーブル、キューを指定するように求められます。 カスタム エンドポイントを使用すると、[カスタム ドメイン](/azure/storage/blobs/storage-custom-domain-name)を使用してアクセスをより正確に制御できます。 「[Azure Storage の接続文字列を構成する](/azure/storage/common/storage-configure-connection-string)」を参照してください。
1. **[OK]** を選択してから **[ファイル] > [保存]** を実行して、構成を新しい接続文字列に更新します。

Azure にアプリケーションを発行するときに、接続文字列用の Azure Storage アカウントを含むサービス構成をもう一度選択します。 アプリケーションを発行した後、アプリケーションが Azure Storage サービスに対して期待どおりに動作することを確認します。

サービス構成を更新する方法の詳細については、「[ストレージ アカウント用の接続文字列の管理](vs-azure-tools-configure-roles-for-cloud-service.md#manage-connection-strings-for-storage-accounts)」のセクションをご覧ください。

## <a name="endpoints-page"></a>[エンドポイント] ページ

Web ロールには、通常ポート 80 の HTTP エンドポイントが 1 つあります。 対して worker ロールには、任意の数の HTTP、HTTPS、TCP エンドポイントを含めることができます。 エンドポイントには、外部のクライアントが利用できる入力エンドポイント、またはサービスで実行されている他のロールが利用できる内部エンドポイントを指定できます。

- HTTP エンドポイントを外部クライアントおよび Web ブラウザーから利用できるようにするには、エンドポイントの種類を [入力] に変更し、名前とパブリック ポート番号を指定します。
- HTTPS エンドポイントを外部クライアントおよび Web ブラウザーから利用できるようにするには、エンドポイントの種類を **[入力]** に変更し、名前、パブリック ポート番号、管理証明書名を指定します。 管理証明書を指定する前に、**[証明書]** プロパティ ページで証明書も定義する必要があります。
- クラウド サービス内の他のロールからエンドポイントを内部利用できるようにするには、エンドポイントの種類を [内部] に変更し、名前とこのエンドポイントに使用可能なプライベート ポートを指定します。

## <a name="local-storage-page"></a>[ローカル ストレージ] ページ

**[ローカル ストレージ]** プロパティ ページを使用して、ロール用に 1 つ以上のローカル ストレージ リソースを予約できます。 ローカル ストレージ リソースは、ロールのインスタンスが実行されている Azure 仮想マシンのファイル システム内の予約されたディレクトリです。

## <a name="certificates-page"></a>[証明書] ページ

**[証明書]** プロパティ ページでは、証明書についての情報をサービス構成に追加します。 証明書はサービスと共にパッケージ化されないことに注意してください。[Azure Portal](https://portal.azure.com) を使用して、Azure に証明書を個別にアップロードする必要があります。

ここで証明書を追加すると、証明書に関する情報がサービス構成に追加されます。 証明書はサービスにパッケージ化されないため、Azure Portal を介して証明書を個別にアップロードする必要があります。

証明書をロールに関連付けるには、証明書の名前を指定します。 **[エンドポイント]** ページで HTTPS エンドポイントを構成するときに、この名前を使用して証明書を参照します。 次に、証明書ストアが **[ローカル コンピューター]** と **[現在のユーザー]** のどちらであるかと、ストアの名前を指定します。 最後に、証明書のサムプリントを入力します。 証明書が Current User\Personal (My) ストアに存在する場合、表示されたリストから証明書を選択することで、証明書のサムプリントを入力できます。 他の場所に存在する場合は、サムプリントの値を手動で入力します。

証明書ストアから証明書を追加すると、すべての中間証明書は自動的に構成設定に追加されます。 また、SSL に対してサービスを適切に構成するために、これらの中間証明書を Azure にアップロードする必要があります。

サービスに関連付けられた管理証明書がサービスに適用されるのは、サービスがクラウドで実行されている場合のみです。 サービスがローカル開発環境で実行されている場合には、コンピューティング エミュレーターが管理する標準の証明書が使用されます。
