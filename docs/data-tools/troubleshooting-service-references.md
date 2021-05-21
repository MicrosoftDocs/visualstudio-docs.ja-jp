---
title: サービス参照のトラブルシューティング
description: Visual Studio で Windows Communication Foundation (WCF) または WCF Data Services の参照を使用しているときに発生する可能性のある一般的な問題を確認します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: troubleshooting
f1_keywords:
- msvse_wcf.Err.ReferenceGroup_NamespaceConflictsOther
- msvse_wcf.Err.AddSvcRefDlg_NothingSelectedOnGo
- msvse_wcf.Err.ErrorOnOK
- msvse_wcf.cfg.ConfigurationErrorsException
helpviewer_keywords:
- service references [Visual Studio], troubleshooting
- WCF services, troubleshooting
ms.assetid: 3b531120-1325-4734-90c6-6e6113bd12ac
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: 909291e3f9762593a58df93a9ccc7fe2e82b7952
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99866360"
---
# <a name="troubleshoot-service-references"></a>サービス参照をトラブルシューティングする

このトピックでは、Visual Studio で Windows Communication Foundation (WCF) または WCF Data Services の参照を使用しているときに発生する可能性のある一般的な問題の一覧を示します。

## <a name="error-returning-data-from-a-service"></a>サービスからデータを取得しているときのエラー

サービスから `DataSet` または `DataTable` を取得しているときに、"受信メッセージの最大サイズ クォータを超えました" という例外が発生することがあります。 サービス拒否攻撃を受ける可能性を制限するため、一部のバインドの `MaxReceivedMessageSize` プロパティは既定で比較的小さい値に設定されています。 この値を大きくして、例外を回避することができます。 詳細については、「<xref:System.ServiceModel.HttpBindingBase.MaxReceivedMessageSize%2A>」を参照してください。

このエラーを修復するには:

1. **ソリューション エクスプローラー** で、*app.config* ファイルをダブルクリックしてを開きます。

2. `MaxReceivedMessageSize` プロパティを見つけて、それをより大きい値に変更します。

## <a name="cannot-find-a-service-in-my-solution"></a>ソリューションでサービスが見つからない

**[サービス参照の追加]** ダイアログ ボックスの **[探索]** ボタンをクリックすると、ソリューション内の 1 つ以上の WCF サービス ライブラリ プロジェクトがサービスの一覧に表示されません。 これは、サービス ライブラリはソリューションに追加されていても、まだコンパイルされていない場合に、発生する可能性があります。

このエラーを修復するには:

- **ソリューション エクスプローラー** で、WCF サービス ライブラリ プロジェクトを右クリックして、 **[ビルド]** をクリックします。

## <a name="error-accessing-a-service-over-a-remote-desktop"></a>リモート デスクトップ経由でサービスにアクセスしているときのエラー

ユーザーがリモート デスクトップ接続経由で Web ホスト WCF サービスにアクセスし、ユーザーに管理者権限がない場合は、NTLM 認証が使用されます。 ユーザーが管理アクセス許可を持っていない場合、次のエラー メッセージが表示されることがあります: "この HTTP 要求は、クライアントの認証方式 '匿名' では承認されません。 サーバーから受信した認証ヘッダーは 'NTLM' でした。"

このエラーを修復するには:

1. Web サイト プロジェクトで、 **[プロパティ]** ページを開きます。

2. **[開始オプション]** タブで、 **[NTLM 認証]** チェック ボックスをオフにします。

    > [!NOTE]
    > WCF サービスだけが含まれる Web サイトについてのみ、NTLM 認証を無効にする必要があります。 WCF サービスのセキュリティは、*web.config* ファイルの構成によって管理されます。 これにより、NTLM 認証は不要になります。

## <a name="access-level-for-generated-classes-setting-has-no-effect"></a>[生成されたクラスのアクセス レベル] の設定が有効にならない

**[サービス参照の構成]** ダイアログ ボックスの **[生成されたクラスのアクセス レベル]** オプションを **[内部]** または **[フレンド]** に設定すると、機能しないことがあります。 ダイアログ ボックスではオプションが設定されているように見えますが、結果のサポート クラスは `Public` のアクセス レベルで生成されます。

これは、<xref:System.Xml.Serialization.XmlSerializer> を使用してシリアル化されものなど、特定の型での既知の制限です。

## <a name="error-debugging-service-code"></a>サービス コードをデバッグしているときのエラー

クライアント コードから WCF サービスのコードにステップインすると、シンボルがないというエラーが表示されることがあります。 これは、ソリューションの一部であったサービスが、ソリューションから移動または削除されたときに、発生する可能性があります。

現在のソリューションの一部である WCF サービスに参照を初めて追加すると、サービス プロジェクトとサービス クライアント プロジェクトの間に明示的なビルド依存関係が追加されます。 これにより、クライアントが常に最新のサービス バイナリにアクセスすることが保証されます。これは、クライアント コードからサービス コードへのステップインなどのデバッグ シナリオに特に重要です。

サービス プロジェクトがソリューションから削除された場合、この明示的なビルド依存関係が無効になります。 必要に応じてサービス プロジェクトがリビルドされることを、Visual Studio で保証できなくなります。

このエラーを修正するには、サービス プロジェクトを手動でリビルドする必要があります。

1. **[ツール]** メニューの **[オプション]** をクリックします。

2. **[オプション]** ダイアログ ボックスで、 **[プロジェクトとソリューション]** を展開し、 **[全般]** を選択します。

3. **[ビルド構成の詳細を表示]** チェック ボックスがオンになっていることを確認して、 **[OK]** をクリックします。

4. WCF サービス プロジェクトを読み込みます。

5. **[構成マネージャー]** ダイアログ ボックスで、 **[アクティブ ソリューション構成]** を **[デバッグ]** に設定します。 詳細については、[構成を作成および編集する](../ide/how-to-create-and-edit-configurations.md)」を参照してください。

6. **ソリューション エクスプローラー** で WCF サービス プロジェクトを選択します。

7. **[ビルド]** メニューの **[リビルド]** をクリックして、WCF サービス プロジェクトをリビルドします。

## <a name="wcf-data-services-do-not-display-in-the-browser"></a>ブラウザーに WCF Data Services が表示されない

[!INCLUDE[ss_data_service](../data-tools/includes/ss_data_service_md.md)] でデータの XML 表現を表示しようとすると、Internet Explorer でデータが RSS フィードとして誤って解釈されることがあります。 RSS フィードを表示するオプションが無効になっていることを確認してください。

このエラーを解決するには、RSS フィードを無効にします。

1. Internet Explorer で、**[ツール]** メニューの **[インターネット オプション]** をクリックします。

2. **[コンテンツ]** タブの **[フィード]** セクションで、 **[設定]** をクリックします。

3. **[フィードの設定]** ダイアログ ボックスで、 **[フィードの読み取りビューを有効にする]** チェック ボックスをオフにして、 **[OK]** をクリックします。

4. **[OK]** をクリックして **[インターネット オプション]** ダイアログ ボックスを閉じます。

## <a name="see-also"></a>こちらもご覧ください

- [Visual Studio での Windows Communication Foundation サービスと WCF データ サービス](../data-tools/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio.md)
