---
title: "方法: インポートした名前空間を追加または削除する (Visual Basic) | Microsoft Docs"
ms.custom: 
ms.date: 06/21/2017
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-general
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- adding imported namespaces
- removing imported namespaces
- namespaces [Visual Studio], imported
- imported namespaces [Visual Studio]
- references [Visual Studio], imported namespaces
ms.assetid: 44cebec3-0ea0-47c2-8406-4edeab6a997e
caps.latest.revision: "11"
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 43947a2e239833459923f6991d4ee54d12876fe3
ms.sourcegitcommit: f40311056ea0b4677efcca74a285dbb0ce0e7974
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/31/2017
---
# <a name="how-to-add-or-remove-imported-namespaces-visual-basic"></a>方法 : インポートした名前空間を追加または削除する (Visual Basic)
名前空間をインポートすると、その名前空間の要素を、完全に修飾することなくコードで使うことができます。 たとえば、`System.Messaging.MessageQueue` クラスの `Create` メソッドにアクセスする場合、`System.Messaging` 名前空間をインポートすると、`MessageQueue.Create` とするだけで必要な要素をコードで参照できます。  

 インポートした名前空間は、**プロジェクト デザイナー**の **[参照]** ページで管理します。 このダイアログ ボックスで指定したインポートは、コンパイラに直接渡されて (`/imports`)、プロジェクト内のすべてのファイルに適用されます。 1 つのソース コード ファイルで名前空間を使うには、`Imports` ステートメントを使います。  

### <a name="to-add-an-imported-namespace"></a>インポートされた名前空間を追加するには  

1.  **ソリューション エクスプローラー**で、対象のプロジェクトの **[マイ プロジェクト]** ノードをダブルクリックします。  

2.  **プロジェクト デザイナー**で、**[参照設定]** タブをクリックします。  

3.  **[インポートされた名前空間]** ボックスの一覧で、追加する名前空間のチェック ボックスをオンにします。  

    > [!NOTE]
    >  名前空間をインポートするには、名前空間が参照されるコンポーネント内に存在する必要があります。 名前空間が一覧に表示されない場合は、名前空間を含むコンポーネントへの参照を追加する必要があります。 詳細については、「[プロジェクト内の参照の管理](managing-references-in-a-project.md)」を参照してください。  
  
### <a name="to-remove-an-imported-namespace"></a>インポートされた名前空間を削除するには  

1.  **ソリューション エクスプローラー**で、対象のプロジェクトの **[マイ プロジェクト]** ノードをダブルクリックします。  

2.  **プロジェクト デザイナー**で、**[参照設定]** タブをクリックします。  

3.  **[インポートされた名前空間]** ボックスの一覧で、削除する名前空間のチェック ボックスをオフにします。  

## <a name="user-imports"></a>ユーザー インポート  
 ユーザー インポートを使うと、名前空間全体ではなく、名前空間内の特定のクラスをインポートできます。 たとえば、アプリケーションで `Systems.Diagnostics` 名前空間をインポートしていても、必要なのはその中の `Debug` クラスだけであるものとします。 そのような場合は、`System.Diagnostics.Debug` をユーザー インポートとして定義し、`System.Diagnostics` のインポートを削除することができます。  

 後で本当に必要なのは `EventLog` クラスであることがわかった場合は、`System.Diagnostics.EventLog` をユーザー インポートとして入力し、更新機能を使って `System.Diagnostics.Debug` を上書きできます。  

#### <a name="to-add-a-user-import"></a>ユーザー インポートを追加するには  

1.  **ソリューション エクスプローラー**で、対象のプロジェクトの **[マイ プロジェクト]** ノードをダブルクリックします。  

2.  **プロジェクト デザイナー**で、**[参照設定]** タブをクリックします。  

3.  **[インポートされた名前空間]** の下のテキスト ボックスに、インポートする名前空間の、ルート名前空間を含む完全な名前を入力します。  

4.  **[ユーザー インポートの追加]** ボタンをクリックすると、名前空間が **[インポートされた名前空間]** の一覧に追加されます。  

    > [!NOTE]
    >  入力した名前空間が一覧に既にある名前空間のいずれかと一致する場合、**[ユーザー インポートの追加]** ボタンは使用できません。インポートを 2 回追加することはできません。  

#### <a name="to-update-a-user-import"></a>ユーザー インポートを更新するには  

1.  **ソリューション エクスプローラー**で、対象のプロジェクトの **[マイ プロジェクト]** ノードをダブルクリックします。  

2.  **プロジェクト デザイナー**で、**[参照設定]** タブをクリックします。  

3.  **[インポートされた名前空間]** の一覧で、変更する名前空間を選択します。  

4.  **[インポートされた名前空間]** の下のテキスト ボックスに、新しい名前空間の名前を入力します。  

5.  **[ユーザー インポートの更新]** ボタンをクリックすると、**[インポートされた名前空間]** の一覧の名前空間が更新されます。  

## <a name="see-also"></a>関連項目  
 [プロジェクト内の参照の管理](../ide/managing-references-in-a-project.md)
