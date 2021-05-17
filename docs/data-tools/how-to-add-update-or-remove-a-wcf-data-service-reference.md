---
title: WCF データ サービス参照を追加、更新、または削除する
description: Windows Communication Foundation (WCF) データ サービス参照を追加、更新、または削除する方法を確認します。
ms.date: 11/04/2016
ms.custom: SEO-VS-2020
ms.topic: how-to
helpviewer_keywords:
- service references [Visual Studio]
- WCF Data Service reference
- WCF data service references
- ADO.NET service references
- ADO.NET Data Service reference
ms.assetid: 892ebf37-3af4-472e-8744-92837677d611
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: 8d728df5f8af5dff5a7ea2456e1d40d47ddc7f76
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99866893"
---
# <a name="how-to-add-update-or-remove-a-wcf-data-service-reference"></a>方法: WCF データ サービス参照を追加、更新、または削除する

::: moniker range="vs-2017"
*サービス参照* によって、プロジェクトで 1 つ以上の [!INCLUDE[ssAstoria](../data-tools/includes/ssastoria_md.md)] を使用できます。 **[サービス参照の追加]** ダイアログ ボックスを使用すると、現在のソリューション内、ローカル、ローカルエリアネットワーク上、またはインターネット上で [!INCLUDE[ssAstoria](../data-tools/includes/ssastoria_md.md)] を検索できます。
::: moniker-end
::: moniker range=">=vs-2019"
**ソリューション エクスプローラー** の **[接続済みサービス]** ノードを使用して **Microsoft WCF Web サービス リファレンス プロバイダー** にアクセスできます。これにより、Windows Communication Foundation (WCF) データ サービス参照を管理できます。
::: moniker-end

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

## <a name="add-a-wcf-service-reference"></a>WCF サービス参照を追加する

### <a name="to-add-a-reference-to-an-external-service"></a>外部サービスへの参照を追加するには

::: moniker range="vs-2017"

1. **ソリューション エクスプローラー** で、サービスを追加するプロジェクトの名前を右クリックし、 **[サービス参照の追加]** をクリックします。

   [**サービス参照の追加**] ダイアログ ボックスが表示されます。

1. **[アドレス]** ボックスにサービスの URL を入力し、 **[検索]** をクリックしてサービスを検索します。 サービスでユーザー名とパスワードのセキュリティを実装する場合は、ユーザー名とパスワードの入力を求められることがあります。

    > [!NOTE]
    > 信頼できるソースのサービスのみを参照してください。 信頼できないソースの参照を追加すると、セキュリティが損なわれる可能性があります。

     **アドレス** 一覧から URL を選択することもできます。ここには、有効なサービス メタデータが見つかった以前の 15 個の URL が格納されます。

     検索が実行されると、進行状況バーが表示されます。 **[停止]** をクリックすると、いつでも検索を停止できます。

1. **サービス** の一覧で、使用するサービスのノードを展開し、エンティティ セットを選択します。

1. [**名前空間**] ボックスに、参照で使用する名前空間を入力します。

1. [**OK**] をクリックして、プロジェクトに参照を追加します。

     サービス クライアント (プロキシ) が生成され、サービスについて説明するメタデータが *app.config* ファイルに追加されます。
::: moniker-end
::: moniker range=">=vs-2019"
1. **ソリューション エクスプローラー** で、 **[接続済みサービス]** ノードをダブルクリックまたはタップします。

   **[サービスの構成]** タブが開きます。

1. **[Microsoft WCF Web サービス リファレンス プロバイダー]** を選択します。

   **[WCF Web サービス参照の構成]** ダイアログ ボックスが表示されます。

   ![[WCF Web サービスプロバイダー] ダイアログ ボックスのスクリーンショット](media/vs-2019/configure-wcf-web-service-reference-dialog.png)


1. **[URI]** ボックスにサービスの URL を入力し、 **[検索]** をクリックしてサービスを検索します。 サービスでユーザー名とパスワードのセキュリティを実装する場合は、ユーザー名とパスワードの入力を求められることがあります。

    > [!NOTE]
    > 信頼できるソースのサービスのみを参照してください。 信頼できないソースの参照を追加すると、セキュリティが損なわれる可能性があります。

     **URI** 一覧から URL を選択することもできます。ここには、有効なサービス メタデータが見つかった以前の 15 個の URL が格納されます。

     検索が実行されると、進行状況バーが表示されます。 **[停止]** をクリックすると、いつでも検索を停止できます。

1. **サービス** の一覧で、使用するサービスのノードを展開し、エンティティ セットを選択します。

1. [**名前空間**] ボックスに、参照で使用する名前空間を入力します。

1. **[完了]** をクリックして、プロジェクトに参照を追加します。

     サービス クライアント (プロキシ) が生成され、サービスについて説明するメタデータが *app.config* ファイルに追加されます。

::: moniker-end

### <a name="to-add-a-reference-to-a-service-in-the-current-solution"></a>現在のソリューションのサービスへの参照を追加するには

::: moniker range="vs-2017"

1. **ソリューション エクスプローラー** で、サービスを追加するプロジェクトの名前を右クリックし、 **[サービス参照の追加]** をクリックします。

    [**サービス参照の追加**] ダイアログ ボックスが表示されます。

1. **[検出]** をクリックします。

    現在のソリューションのすべてのサービス ([!INCLUDE[ssAstoria](../data-tools/includes/ssastoria_md.md)] と WCF サービスの両方) が **[サービス]** 一覧に追加されます。

1. **サービス** の一覧で、使用するサービスのノードを展開し、エンティティ セットを選択します。

1. [**名前空間**] ボックスに、参照で使用する名前空間を入力します。

1. [**OK**] をクリックして、プロジェクトに参照を追加します。

    サービス クライアント (プロキシ) が生成され、サービスについて説明するメタデータが *app.config* ファイルに追加されます。
::: moniker-end
::: moniker range=">=vs-2019"
1. **ソリューション エクスプローラー** で、 **[接続済みサービス]** ノードをダブルクリックまたはタップします。 

   **[サービスの構成]** タブが開きます。

1. **[Microsoft WCF Web サービス リファレンス プロバイダー]** を選択します。

   **[WCF Web サービス参照の構成]** ダイアログ ボックスが表示されます。

1. **[検出]** をクリックします。

    現在のソリューションのすべてのサービス ([!INCLUDE[ssAstoria](../data-tools/includes/ssastoria_md.md)] と WCF サービスの両方) が **[サービス]** 一覧に追加されます。

1. **サービス** の一覧で、使用するサービスのノードを展開し、エンティティ セットを選択します。

1. [**名前空間**] ボックスに、参照で使用する名前空間を入力します。

1. **[完了]** をクリックして、プロジェクトに参照を追加します。

    サービス クライアント (プロキシ) が生成され、サービスについて説明するメタデータが *app.config* ファイルに追加されます。

::: moniker-end

## <a name="update-a-service-reference"></a>サービス参照の更新

[!INCLUDE[ssAstoria](../data-tools/includes/ssastoria_md.md)] の Entity Data Model が変更される場合があります。 この場合は、サービス参照を更新する必要があります。

### <a name="to-update-a-service-reference"></a>サービス参照を更新するには

- **ソリューション エクスプローラー** で、サービス参照を右クリックし、 **[サービス参照の更新]** をクリックします。

     参照が元の場所から更新されている間、進行状況を示すダイアログ ボックスが表示され、メタデータの変更を反映するためにサービス クライアントが再生成されます。

## <a name="remove-a-service-reference"></a>サービス参照の削除

サービス参照が使用されなくなった場合は、ソリューションから削除できます。

### <a name="to-remove-a-service-reference"></a>サービス参照を削除するには

- **ソリューション エクスプローラー** で、サービス参照を右クリックし、 **[削除]** をクリックします。

     サービス クライアントがソリューションから削除され、サービスを説明するメタデータが *app.config* ファイルから削除されます。

    > [!NOTE]
    > サービス参照を参照するコードは、手動で削除する必要があります。

## <a name="see-also"></a>関連項目

- [Visual Studio での Windows Communication Foundation サービスと WCF データ サービス](../data-tools/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio.md)
