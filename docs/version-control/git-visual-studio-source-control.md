---
title: Visual Studio でソース管理を簡単にする方法
titleSuffix: ''
description: Visual Studio で Git および GitHub を使用して、ご利用のコードに加えた変更を追跡し、必要に応じてそれらを元に戻す方法について説明します。
ms.date: 04/01/2021
ms.topic: conceptual
ms.author: tglee
author: TerryGLee
ms.manager: jmartens
ms.openlocfilehash: f6213174bbef5c4d5976e410f92b771b34ae6f23
ms.sourcegitcommit: 5fb684ff8729eb118aa91ce9f049c79eeb9747b1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2021
ms.locfileid: "108635389"
---
# <a name="how-visual-studio-makes-source-control-easy"></a>Visual Studio でソース管理を簡単にする方法

ご利用のコードの以前に動作していたバージョンに戻ることができたらと思ったことはありませんか。 コードのコピーをバックアップとして別の場所に手動で格納できることにお気づきですか。 ソース管理を使用すると、コードに加えた変更を時系列的に追跡できるため、進捗状況を追跡することも、特定のバージョンに戻すこともできます。 Visual Studio を使用すると、最も広く使用されている最新バージョンの管理システムである Git を容易に操作できるようになります。

## <a name="a-great-place-to-start-with-git--github"></a>Git および GitHub から開始するのに最適な場所

GitHub には、セキュリティで保護された無料のクラウド コード ストレージが用意されていて、ご利用のコードを格納し、任意のデバイスでどこからでもアクセスすることができます。 Visual Studio には、ファーストクラスの Git および GitHub 機能が付属しています。これにより、ソース管理を使用してコードの管理および他のユーザーとの共同作業を行うことが簡単になります。 まず、次の **[Git リポジトリの作成]** ダイアログ ボックスを使用して、Git および GitHub にコードを追加します。 これを行うには、メニュー バーから **[Git]**  >  **[Git リポジトリの作成]** の順に選択します。

:::image type="content" source="media/git-source-control-create-repository.png" alt-text="Visual Studio の [Git リポジトリの作成] ダイアログ ボックス。":::

また、GitHub を使用して、多数のオープンソース リポジトリから探索し、学習することもできます。 Visual Studio を使用すると、既存の GitHub リポジトリを簡単にクローンして参照できます。このため、学習環境として最適です。

## <a name="streamlined-and-intuitive-inner-loop-git-experience"></a>合理化されていて直感的な内部ループの Git エクスペリエンス

Visual Studio には、毎日のワークフロー (内部ループ) の生産性を最大限に高めることに重点を置いた、探索可能で直感的な Git 機能が用意されています。 加えた変更をコミットするためにコードから離れる必要はもうありません。 これらの機能には、最上位の Git メニュー、[Git 変更] ウィンドウ、Git にフォーカスしたステータス バーなどがあります。 Git は、総合的なエクスペリエンスとして Visual Studio と統合されています。たとえば、ソリューション エクスプローラーとコード エディターの両方に、ファースト クラスの Git 統合があります。

:::image type="content" source="media/git-source-control-inner-loop.png" alt-text="Git メニューと、ソリューション エクスプローラーの [Git 変更] タブが表示されている Visual Studio IDE。":::

## <a name="first-class-repository-management--collaboration"></a>ファーストクラスのリポジトリ管理とコラボレーション

Visual Studio には、強力なリポジトリ参照およびコラボレーションの機能が含まれていて、他のツールを使用する必要がありません。 受信/送信コミットを監視し、ブランチをプレビューし、コミットを比較することで、リポジトリを最新の状態に保ちます。 また、ブランチの管理と、コミットのスカッシュおよびチェリーピックを行うことで、リポジトリを管理します。

:::image type="content" source="media/git-source-control-repository-management.png" alt-text="Git メニューと、ソリューション エクスプローラーの [Git 変更] タブが強調表示されている Visual Studio IDE。":::

## <a name="interactive--smart-git-functionality"></a>インタラクティブでスマートな Git 機能

Visual Studio の Git 統合を使用すると、コンテキスト支援が提供され、適切な操作を求めるメッセージが表示されるため、信頼と信頼度が向上します。 また、単語の違いを表示/非表示にしたり、競合と相違点の間を移動したりできる競合解決エクスペリエンスも含まれています。

:::image type="content" source="media/git-source-control-interactive-functionality.png" alt-text="Git コンテキスト支援と競合解決が表示されている Visual Studio IDE。":::

## <a name="next-steps"></a>次のステップ

Visual Studio で Git と GitHub を使用する方法の詳細については、次の YouTube 動画をご覧ください: [Visual Studio で Git の使用を開始する](https://www.youtube.com/watch?v=GCZ9x3yqkyc&list=PLReL099Y5nRc-zbaFbf0aNcIamBQujOxP)

## <a name="see-also"></a>関連項目

- [Visual Studio で Git と GitHub の使用を開始する](/learn/modules/visual-studio-github-push/)
- [Visual Studio での新しい Git エクスペリエンス](git-with-visual-studio.md)
- [Git とチーム エクスプローラーを並べて比較する](git-team-explorer-feature-comparison.md)