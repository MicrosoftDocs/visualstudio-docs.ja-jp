---
title: Visual Studio でロード テストで Web キャッシュ データを使用する仮想ユーザーの割合を指定する
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- load tests, virtual users
ms.assetid: f66d5d43-4121-4487-b27f-d0a0baaf7601
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.openlocfilehash: 1178cd08bf8d12b4fba61e858ca5631d103292c2
ms.sourcegitcommit: ae46be4a2b2b63da7e7049e9ed67cd80897c8102
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2018
ms.locfileid: "52895575"
---
# <a name="how-to-specify-the-percentage-of-virtual-users-that-use-web-cache-data"></a>方法: Web キャッシュ データを使用する仮想ユーザーの割合を指定する

**新しいロード テスト** ウィザードでロード テストを作成した後で、**ロード テスト エディター**を使用して、テストのニーズや目標に合わせてシナリオのプロパティを変更できます。 ロード テスト シナリオの各プロパティとその説明の一覧については、「[ロード テスト シナリオのプロパティ](../test/load-test-scenario-properties.md)」を参照してください。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

**新しいユーザーのパーセンテージ** プロパティは、**[プロパティ]** ウィンドウで設定します。 **ロード テスト エディター**でロード テスト シナリオのプロパティを編集します。

**[新しいユーザーのパーセンテージ]** プロパティは、Web ブラウザーによって実行されるキャッシュ処理をロード テストがシミュレートする方法に影響します。 既定では、**新しいユーザーのパーセンテージ** プロパティは 0% に設定されています。 **[新しいユーザーのパーセンテージ]** プロパティの値を 100% に設定した場合、ロード テストで Web パフォーマンス テストが実行されるたびに、Web サイトに初めてアクセスするかのように扱われます。つまり、ブラウザーのキャッシュに Web サイトへの以前のアクセスによるコンテンツがないユーザーとして扱われます。 したがって、Web テストのすべての要求が、イメージなどの依存要求もすべて含めて、ダウンロードされます。

> [!NOTE]
> キャッシュ可能な同一リソースが Web テスト内で複数回要求された場合は、要求はダウンロードされません。

イメージなどのキャッシュ可能なコンテンツをローカルにキャッシュしているリピーター ユーザーが非常に多い Web サイトのロード テストを実行する場合、**[新しいユーザーのパーセンテージ]** プロパティを 100% に設定すると、ダウンロード要求が実際の運用時より多く生成されます。 この場合は、初回アクセス ユーザーによる Web サイトへのアクセスが占める割合を推測し、それに基づいて **[新しいユーザーのパーセンテージ]** プロパティを設定する必要があります。

## <a name="to-specify-the-percentage-of-new-users-for-a-scenario"></a>シナリオの新しいユーザーのパーセンテージを指定するには

1. ロード テストを開きます。

     **ロード テスト エディター**が表示されます。 ロード テスト ツリーが表示されます。

2. ロード テスト ツリーの **[シナリオ]** フォルダーで、新しいユーザーのパーセンテージを変更するシナリオのノードを選びます。

3. **[表示]** メニューの **[プロパティ ウィンドウ]** をクリックします。

     **[プロパティ]** ウィンドウに、シナリオのカテゴリおよびプロパティが表示されます。

4. 新しいユーザーのパーセンテージの数値を入力して、**[新しいユーザーのパーセンテージ]** プロパティの値を設定します。

5. プロパティを変更したら、**[ファイル]** メニューの **[保存]** を選択します。 次に、**[新しいユーザーのパーセンテージ]** の新しい値を使って、ロード テストを実行します。

## <a name="see-also"></a>関連項目

- [ロード テスト シナリオの編集](../test/edit-load-test-scenarios.md)
- [チュートリアル: ロード テストの作成と実行](../test/walkthrough-create-and-run-a-load-test.md)
- [テスト コントローラーとテスト エージェント](configure-test-agents-and-controllers-for-load-tests.md)
- [ロード テスト シナリオのプロパティ](../test/load-test-scenario-properties.md)
- [ロード パターンを編集して、仮想ユーザー アクティビティをモデル化する](../test/edit-load-patterns-to-model-virtual-user-activities.md)