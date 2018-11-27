---
title: 新しいプロジェクトとソリューションを作成する
description: この記事では、Visual Studio for Mac でプロジェクトとソリューションを作成する方法について説明します。
author: conceptdev
ms.author: crdun
ms.date: 05/06/2018
ms.assetid: 5880BB10-0A12-47E2-8A82-7A2D59C4D579
ms.openlocfilehash: b6f355dbe10cf250ec397cb817643984b438a92e
ms.sourcegitcommit: 0a8ac5f2a685270d9ca79bb39d26fd90099bfa29
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/09/2018
ms.locfileid: "51294267"
---
# <a name="creating-new-projects-and-solutions"></a>新しいプロジェクトとソリューションを作成する

## <a name="creating-new-projects-and-solutions-from-a-template"></a>テンプレートから新しいプロジェクトとソリューションを作成する

ソリューションは、事前定義済みのテンプレートを利用していつでも作成できます。 ソリューションをこの方法で作成するには、 **[ファイル]、[新しいソリューション]** の順に移動し、必要なプラットフォームを選択し、必要なテンプレートを選択します。

![新しいソリューションを作成する](media/projects-and-solutions-image0.png)

これでソリューションが作成されます。ソリューションには、選択したテンプレートの種類によって、1 つまたは複数のプロジェクトを含めることができます。

コンテキスト アクションまたはメニュー バーを利用し、ソリューション エクスプローラーを操作できます。

新しいプロジェクトをソリューションに追加するには、ソリューション名を右クリックし、**[追加]、[新しいプロジェクトの追加]** の順に選択し、[新しいプロジェクト] ダイアログを表示します。

![新しいプロジェクトを追加する](media/projects-and-solutions-image4.png)

新しいプロジェクトを追加するこの方法を利用し、Xamarin のコード共有機能を最大限に活用できます。 共有プロジェクトまたはポータブル ライブラリ テンプレートを既存のソリューションに追加することで、あるソリューションのその他すべてのプロジェクト内で利用できる、プラットフォームに依存しないロジックを含めることができます。 プラットフォームに依存しないアプリケーションのビルド方法については、[関連ガイド](https://developer.xamarin.com/guides/cross-platform/application_fundamentals/code-sharing/)を参照してください。

## <a name="opening-recent-solutions"></a>最近使用したソリューションを開く

Visual Studio のランディング ページには、最近使用したプロジェクトの一覧が表示されます。

![ウェルカム ページの最近使用したソリューションのセクション](media/create-new-projects-recent.png)

フィルター ボックスを利用してこの一覧を絞り込んだり、一覧から個々の項目を削除したりできます。

## <a name="see-also"></a>関連項目

- [ソリューションとプロジェクトを作成する (Windows の Visual Studio)](/visualstudio/ide/creating-solutions-and-projects)