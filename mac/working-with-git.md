---
title: Git の使用
description: Visual Studio for Mac で Git を使用します。
author: jmatthiesen
ms.author: jomatthi
ms.date: 05/06/2018
ms.assetid: 852B6A9D-AEFA-4EF4-A5DD-94A506019D20
ms.custom: video
ms.openlocfilehash: 767c08505877391d71ca085097a0464d516f4f24
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/20/2020
ms.locfileid: "70108023"
---
# <a name="working-with-git"></a>Git の使用

Git は、チームが同じドキュメントで同時に作業できるようにする分散型バージョン管理システムです。 つまり、すべてのファイルを含む中央サーバーがありますが、中央のソースからリポジトリがチェックアウトされるときには、リポジトリ全体がローカル マシンにクローンされます。

以下のセクションでは、Visual Studio for Mac のバージョン コントロールに Git を使用する方法について説明します。

## <a name="git-version-control-menu"></a>Git バージョン管理メニュー

次の図は、Visual Studio for Mac の [バージョン コントロール] メニュー項目で提供されるオプションを示しています。

![[バージョン コントロール] メニュー項目](media/version-control-gitVersionControlMenu.png)

## <a name="push-and-pull"></a>プッシュおよびプル

プッシュとプルは、Git 内で最もよく使用される 2 つのアクションです。 リモート リポジトリに他のユーザーが行った変更を同期するためには、そこから**プル**する必要があります。 これを行うには、Visual Studio for Mac で **[バージョン コントロール] > [ソリューションの更新]** を選択します。

ファイルを更新して、レビューし、それらをコミットしたら、他のユーザーが変更にアクセスできるようにそれらをリモート リポジトリに**プッシュ**する必要があります。 これを行うには、Visual Studio for Mac で **[バージョン コントロール] > [変更をプッシュ]** を選択します。 これにより、[プッシュ] ダイアログが表示され、コミットされた変更表示して、プッシュするブランチを選択できます。

![コミットするブランチを表示するダイアログ](media/version-control-gitPush.png)

[コミット] ダイアログで変更のコミットとプッシュを同時に行うこともできます。

![コミットとプッシュを同時に行う方法を示すオプション](media/version-control-commitPush.png)

## <a name="blame-log-and-merge"></a>変更履歴、ログ、およびマージ

以下に示すようにウィンドウの下部に、5 つのタブが表示されます。

![[バージョン コントロール] タブ](media/version-control-gitTabs.png)

次の操作を実行できます。

* **ソース** - ソース コード ファイルが表示されます。
* **変更** - ローカル ファイルとベース ファイルの間のコードの変更を表示します。 異なるハッシュでファイルの異なるバージョンを比較することもできます。

    ![[変更] タブ](media/version-control-gitChange.png)

* **変更履歴** - コードの各セクションに関連付けられているユーザーのユーザー名が表示されます。
* **ログ** - すべてのコミット、時間、日付、メッセージ、およびファイルに対して責任を持っているユーザーが表示されます。

    ![[ログ] タブ](media/version-control-gitLog.png)

* **マージ** - 作業内容をコミットするときに競合のマージがある場合にこれを使用することができます。 自分や他の開発者が行った変更視覚的に表現し、コードの両方のセクションを正常に結合することができます。

## <a name="switching-branches"></a>ブランチの切り替え

既定では、リポジトリに作成された最初のブランチは、**マスター** ブランチと呼ばれます。 マスター ブランチと他のブランチの間に技術的な違いは何もありませんが、マスター ブランチは開発チームで最も頻繁に "ライブ" または "運用" ブランチと見なされるブランチです。

マスター (またはそのマスターの他のブランチ) からブランチすることで独立した開発ラインを作成することができます これにより、その時点の新しいバージョンのマスター ブランチが提供され、"ライブ" とは別に開発できるようになります。 ソフトウェア開発における機能では頻繁にこの方法でブランチを使用します。

ユーザーは、各リポジトリで必要な数のブランチを作成できますが、リポジトリの整理された状態を維持するために、ブランチの使用が終了したら削除することをお勧めします。

Visual Studio for Mac でブランチを表示するには、 **[バージョン コントロール] > [ブランチとリモートを管理する]** を参照します。

![[ブランチ] ビュー](media/version-control-gitBranch2.png)

一覧で別のブランチを選択してそのブランチに切り替え、 **[ブランチに切り替え]** ボタンをクリックします。

新しいブランチを作成するには、Git リポジトリ構成ダイアログの **[新規]** ボタンを選択します。 新しいブランチ名を入力します。

![新しいブランチの作成](media/version-control-gitBranch.png)

リモート ブランチを_追跡_ブランチに設定することもできます。 詳しくは、[Git ドキュメント](https://git-scm.com/book/en/v2/Git-Branching-Remote-Branches#Tracking-Branches)の追跡ブランチの説明を参照してください。

Solution Pad でプロジェクト名の横にある現在のブランチを参照します。

 ![ソリューション パッドに表示された現在のブランチ](media/version-control-gitBranchName.png)

## <a name="reviewing-and-committing"></a>確認とコミット

ファイルの変更を確認するには、このトピックで前に示した、各ドキュメントの [変更]、[変更履歴]、[ログ]、[マージ] タブを使用します。

**[バージョン コントロール] > [ソリューションの確認とコミット]** メニュー項目を参照して、プロジェクトのすべての変更を確認します。

![コードの確認の表示](media/version-control-gitReviewCommit.png)

これにより、プロジェクトの各ファイルのすべての変更を表示し、[元に戻す]、[修正プログラムの作成]、[コミット] のオプション選択できます。

リモート リポジトリに対してファイルをコミットするには、[コミット] を押し、コミット メッセージを入力して、 **[コミット]** ボタンで確認します。

![ファイルをコミットする](media/version-control-gitCommit.png)

変更をコミットした後、他のユーザーが表示できるようにそれらをリモート リポジトリにプッシュします。

## <a name="related-video"></a>関連ビデオ

> [!Video https://channel9.msdn.com/Shows/Visual-Studio-Toolbox/Visual-Studio-for-Mac-Manage-Projects-with-Git/player]

## <a name="see-also"></a>参照

* [Visual Studio 2017 と Azure Repos Git を使用してコードを共有する](/azure/devops/repos/git/share-your-code-in-git-vs-2017)
