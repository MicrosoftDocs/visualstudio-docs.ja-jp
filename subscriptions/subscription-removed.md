---
title: Visual Studio サブスクリプションが削除されたときに起こること | Microsoft Docs
author: evanwindom
ms.author: v-evwin
manager: cabuschl
ms.assetid: 34eaceda-f5db-41d6-bc23-ecf55fe1768e
ms.date: 04/22/2021
ms.topic: conceptual
description: 管理者が Visual Studio サブスクリプションを削除したときに起こることについて説明します。
ms.openlocfilehash: e0f33470092cacc096102cd7b671ddc89c9b0859
ms.sourcegitcommit: dd2fc6e03a789c044f8438096b8f112e4dba5557
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2021
ms.locfileid: "108641002"
---
# <a name="what-happens-when-an-admin-removes-my-subscription"></a>管理者がサブスクリプションを削除したときに起こること
Visual Studio サブスクリプションが、職場または学校の組織の管理者によって割り当てられた場合、ある時点で管理者によって削除される可能性があります。  理由としては、ジョブ ロールや組織の購入プランの変更などが考えられます。  この記事では、管理者がサブスクリプションを削除した場合に予期されることについて説明します。  

> [!TIP]
> 管理者がサブスクリプションを削除する場合は、別のサブスクリプションを発行することを計画している可能性があります。  サブスクリプションが削除されたという通知を受け取った場合は、管理者に連絡して、別のサブスクリプションが利用可能かどうかを確認することをお勧めします。  

## <a name="how-do-my-benefits-change"></a>特典についての変更
特定の特典について生じる変更は、特典自体によって異なります。  いくつかの例を紹介し、Azure 資産などにアクセスできるようにするために必要な手順について説明します。 

### <a name="visual-studio-ide"></a>Visual Studio IDE
Visual Studio IDE のライセンスは、割り当てられているサブスクリプションに依存しています。  サブスクリプションが削除されると、有料サブスクリプションで提供されているすべてのバージョンの IDE にアクセスできなくなります。  引き続き Visual Studio が必要な場合は、無料バージョンの [Visual Studio Code](https://code.visualstudio.com/) をインストールすることを検討してください。  

### <a name="individual-azure-credits"></a>個別の Azure クレジット
サブスクリプションが削除されると、個別の Azure クレジットの料金は発生しなくなります。  既に獲得しているクレジットは 30 日間利用できます。  その時点で、資産は使用できなくなります。 

サブスクリプションが削除された場合に、資産が失われないようにするには、次のいずれかの操作を行ってください。
- サブスクリプションを従量課金制に変換します。  詳細については、「[「Azure DevTest の従量課金制のサブスクリプション](vs-azure-payg.md)」の記事を参照してください。  クレジット カードなどの支払い方法をこのサブスクリプションに関連付ける必要があります。 
- 別の Azure サブスクリプションが使用可能な場合は、そちらにアセットを移動します。  たとえば、別の Visual Studio サブスクリプションの一部として Azure サブスクリプションを持っている場合です。  [新しいサブスクリプションにリソースを移動する](https://docs.microsoft.com/azure/azure-resource-manager/management/move-resource-group-and-subscription)手順については、Azure のドキュメントを参照してください。  

  > [!IMPORTANT]
  > 既存の Azure 資産が失われないように、Azure 資産を別の Azure サブスクリプションに移行するか、既存の Azure サブスクリプションを従量課金制に変更することが重要です。 
 
### <a name="software-downloads-and-product-keys"></a>ソフトウェアのダウンロードとプロダクト キー
サブスクリプション ポータル内からのソフトウェア ダウンロードとプロダクト キーへのアクセスは失われます。 

### <a name="azure-devops"></a>Azure DevOps
Azure DevOps へのアクセスに必要なライセンスは失われます。   

### <a name="other-benefits"></a>その他の利点 
サブスクリプションを削除した場合の影響は異なります。  
- 期間固定の特典: パートナーから提供される特典の多くは、期間が固定されているプランです。  サブスクリプションを削除する前にそれらをアクティブ化した場合、その多くは影響を受けず、通常の期間が終了するまでそのまま使用できます。  サブスクライバー ポータルからこれらの特典にアクセスしている場合は、パートナー サイトで直接アクセスする必要があります。  たとえば、Pluralsight サブスクリプション と Visual Studio サブスクリプションをアクティブ化していて、Visual Studio サブスクリプションが削除された場合、トレーニング サブスクリプションの残り時間はまだありますが、Pluralsight の Web サイトに直接サインインする必要があります。 
- 認証を必要とする特典: Visual Studio にサインインするたびに認証される特典を使用している場合、サブスクリプションが削除されると、それらの特典は利用できなくなります。  
- 以前にアクティブ化されていない特典: サブスクリプションが削除されると、追加の特典をアクティブ化できなくなります。  

## <a name="support-resources"></a>サポート リソース
- Visual Studio サブスクリプションの販売、サブスクリプション、アカウント、課金のサポートについては、[Visual Studio サブスクリプション サポート](https://my.visualstudio.com/gethelp)にお問い合わせください。
- Visual Studio IDE、Azure DevOps、またはその他の Visual Studio の製品やサービスに関する質問がありますか。  [Visual Studio のサポート](https://visualstudio.microsoft.com/support/)にアクセスしてください。

## <a name="see-also"></a>関連項目
- [Visual Studio ドキュメント](/visualstudio/)
- [Azure DevOps ドキュメント](/azure/devops/)
- [Azure ドキュメント](/azure/)
- [Microsoft 365 ドキュメント](/microsoft-365/)

## <a name="next-steps"></a>次のステップ
- [Azure DevOps](https://azure.microsoft.com/services/devops/) 機能に関する詳細情報
- [エディション別の Visual Studio IDE 機能](https://visualstudio.microsoft.com/vs/compare/)に関する詳細情報