---
title: チーム プロジェクト チェックイン ポリシーによるコード品質の向上 |Microsoft Docs
ms.custom: ''
ms.date: 2018-06-30
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- code quality, using check-in policies
- team-based development, enhancing code quality
ms.assetid: 0ab72c33-148a-4a8a-a7bf-046995514c84
caps.latest.revision: 27
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 6b76793a2be80e194f9056280614a9e9646c462d
ms.sourcegitcommit: 55f7ce2d5d2e458e35c45787f1935b237ee5c9f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2018
ms.locfileid: "47533978"
---
# <a name="enhancing-code-quality-with-team-project-check-in-policies"></a>チーム プロジェクト チェックイン ポリシーによるコード品質の向上
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このトピックの最新バージョンをご覧[チーム プロジェクト チェックイン ポリシーによるコード品質の向上](https://docs.microsoft.com/visualstudio/code-quality/enhancing-code-quality-with-team-project-check-in-policies)します。  
  
Team Foundation バージョン コントロール (TFVC) を使用する場合は、チーム プロジェクトのチェックイン ポリシーを作成して、 コードの品質向上とグループ開発の効率化を実現するための対策を適用できます。 チェックイン ポリシーとは、チーム プロジェクト レベルで設定され、コードをチェックインする前に開発者のコンピューターに適用される規則です。  
  
 これらのチーム プロジェクト チェックイン ポリシーを指定できます。  
  
-   **ビルド**： ビルド中に作成されたビルド ブレークが新しいチェックインの前に修正されていることを必須とします。  
  
-   **変更セットのコメント**: 変更をチェックインするときにユーザーがコメントを指定することを必須とします。  
  
-   **コード分析**: チェックインの前にコード分析を実行することを必須とします。  
  
-   **作業項目**: 1 つ以上の作業項目をチェックインに関連付けることを必須とします。  
  
> [!IMPORTANT]
>  チェックイン ポリシーを使用するには、[!INCLUDE[vststfsLong](../includes/vststfslong-md.md)] に接続する必要があります。  
  
## <a name="common-tasks"></a>一般的なタスク  
  
|タスク|関連する参照先|  
|----------|------------------------|  
|**作成し、チェックイン ポリシーを使用して:** のチーム プロジェクトの設定を使用してチェックイン ポリシーを作成する[!INCLUDE[esprscc](../includes/esprscc-md.md)]します。|[設定し、品質ゲートを適用](http://msdn.microsoft.com/library/bdc5666e-6cf0-45b2-a0a1-133c3f61e852)|  
|**コード分析チェックイン ポリシーの作成と使用:** コード分析規則の標準セットから選択することも、独自の規則セットを作成することもできます。|[コード分析を用いたチェックイン ポリシーの作成と使用](../code-quality/creating-and-using-code-analysis-check-in-policies.md)|  
  
## <a name="related-tasks"></a>関連タスク  
  
|タスク|関連する参照先|  
|----------|------------------------|  
|**開発環境の設定:** コードを作成または変更する前に、適切なソース コードを使用して開発環境およびテスト環境を設定する必要があります。 データベースを使用している場合は、そのデータベースのオフライン形式へのアクセス権も必要です。|[開発環境の設定](http://msdn.microsoft.com/en-us/7b686610-d379-4ca0-9608-73ef0e576e3a)|  
|**開発プロセスにおけるコード分析の使用:** チームのメンバーは、それぞれの開発コンピューターでコード分析を実行します。 Visual Studio では、開発者が個々のコード プロジェクトについてコード分析を構成および実行し、実行したコード分析で発見された問題を表示および分析して、警告用の作業項目を作成します。|[アプリケーション品質の分析](../code-quality/analyzing-application-quality-by-using-code-analysis-tools.md)|  
|**単体テストの作成および実行:** 単体テストを実行することにより、開発者およびテスト担当者は、C#、Visual Basic、.NET、および C++ のプロジェクトでクラスのメソッドに論理エラーがないかどうかをすばやく確認できます。 単体テストは、1 回作成するだけでよく、バグが追加されていないことを確認するために、ソース コードが変更されるたびに実行できます。|[コードの単体テスト](../test/unit-test-your-code.md)|  
|**作業項目と欠陥の追跡:** 作業項目を使用して、自分の作業とチーム プロジェクトに関する情報の両方を、追跡および管理できます。 作業項目は [!INCLUDE[esprfound](../includes/esprfound-md.md)] が作業の割り当てと進行状況を追跡するために使用するデータベース レコードです。 さまざまな種類の作業項目を使用して、顧客要件、製品バグ、開発タスクなどの作業を追跡できます。|[作業の追跡し、ワークフローの管理&#91;リダイレクト&#93;](http://msdn.microsoft.com/en-us/d2d8637d-0ef8-4ca3-874e-a04713344032)|  
  
## <a name="external-resources"></a>外部リソース  
  
### <a name="guidance"></a>ガイダンス  
 [Visual Studio 2012 を使用した継続的デリバリーのためのテスト – 第 2 章: 単体テスト: 内部のテスト](http://go.microsoft.com/fwlink/?LinkID=255188)



