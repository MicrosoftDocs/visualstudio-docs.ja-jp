---
title: '方法: 追加、更新、または WCF データ サービス参照の削除 |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
helpviewer_keywords:
- service references [Visual Studio]
- WCF Data Service reference
- WCF data service references
- ADO.NET service references
- ADO.NET Data Service reference
ms.assetid: 892ebf37-3af4-472e-8744-92837677d611
caps.latest.revision: 14
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 970f3828319e2e9c016baa66bb1e5fc2032b81ce
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387031"
---
# <a name="how-to-add-update-or-remove-a-wcf-data-service-reference"></a>方法: WCF データ サービス参照を追加、更新、または削除する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

A *service リファレンス*アクセスを 1 つまたは複数のプロジェクト[!INCLUDE[ssAstoria](../includes/ssastoria-md.md)]します。 使用して、**サービス参照の追加**を検索 ダイアログ ボックス[!INCLUDE[ssAstoria](../includes/ssastoria-md.md)]でローカルに、ローカル エリア ネットワーク、またはインターネット上の現在のソリューションです。  
  
 [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]  
  
## <a name="adding-a-service-reference"></a>サービス参照の追加  
  
#### <a name="to-add-a-reference-to-an-external-service"></a>外部サービスへの参照を追加するには  
  
1. **ソリューション エクスプ ローラー**をクリックして、サービスを追加するプロジェクトの名前を右クリックして**サービス参照の追加**します。  
  
     **サービス参照の追加** ダイアログ ボックスが表示されます。  
  
2. **アドレス**ボックス、サービスの URL を入力して、クリックして**移動**サービスを検索します。 サービスは、ユーザー名とパスワードのセキュリティを実装する場合は、ユーザー名とパスワードを求める場合があります。  
  
    > [!NOTE]
    > 信頼できるソースのサービスのみを参照してください。 信頼できないソースの参照を追加すると、セキュリティが損なわれる可能性があります。  
  
     URL を選択することも、**アドレス**一覧で、有効なサービスのメタデータが見つかりましたが、以前の 15 Url が格納されます。  
  
     検索が実行されているときに、進行状況バーが表示されます。 クリックして、いつでも検索を停止する**停止**します。  
  
3. **サービス**一覧で、ノードを使用して、エンティティ セットを選択するサービスを展開します。  
  
4. **Namespace**ボックスに、参照で使用する名前空間を入力します。  
  
5. クリックして**OK**プロジェクトへの参照を追加します。  
  
     サービス クライアント (プロキシ) が生成され、サービスを説明するメタデータが app.config ファイルに追加します。  
  
#### <a name="to-add-a-reference-to-a-service-in-the-current-solution"></a>現在のソリューションでサービスへの参照を追加するには  
  
1. **ソリューション エクスプ ローラー**をクリックして、サービスを追加するプロジェクトの名前を右クリックして**サービス参照の追加**します。  
  
     **サービス参照の追加** ダイアログ ボックスが表示されます。  
  
2. クリックして**検出**します。  
  
     すべてのサービス (両方[!INCLUDE[ssAstoria](../includes/ssastoria-md.md)]および WCF サービス) で、現在のソリューションに追加されます、**サービス**一覧。  
  
3. **サービス**一覧で、ノードを使用して、エンティティ セットを選択するサービスを展開します。  
  
4. **Namespace**ボックスに、参照で使用する名前空間を入力します。  
  
5. クリックして**OK**プロジェクトへの参照を追加します。  
  
     サービス クライアント (プロキシ) が生成され、サービスを説明するメタデータが app.config ファイルに追加します。  
  
## <a name="updating-a-service-reference"></a>サービス参照の更新  
 エンティティ データ モデル、[!INCLUDE[ssAstoria](../includes/ssastoria-md.md)]も変更されます。 この場合、サービス参照を更新する必要があります。  
  
#### <a name="to-update-a-service-reference"></a>サービス参照を更新するには  
  
- **ソリューション エクスプ ローラー**サービス参照を右クリックし、クリックして**サービス参照の更新**します。  
  
     元の場所から、参照を更新し、メタデータの変更を反映する、サービス クライアントを再生成中に、進行状況 ダイアログ ボックスが表示されます。  
  
## <a name="removing-a-service-reference"></a>サービス参照の削除  
 サービス参照が使用されていないが場合、は、ソリューションから削除できます。  
  
#### <a name="to-remove-a-service-reference"></a>サービス参照を削除するには  
  
- **ソリューション エクスプ ローラー**サービス参照を右クリックし、クリックして**削除**します。  
  
     サービス クライアントは、ソリューションから削除して、サービスを説明するメタデータが app.config ファイルから削除されます。  
  
    > [!NOTE]
    > サービス参照を参照するコードは、手動で削除する必要があります。  
  
## <a name="see-also"></a>関連項目  
 [Visual Studio での Windows Communication Foundation サービスと WCF データ サービス](../data-tools/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio.md)
