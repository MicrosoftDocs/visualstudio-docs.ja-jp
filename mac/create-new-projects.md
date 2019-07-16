---
title: 新しいプロジェクトとソリューションを作成する
description: この記事では、Visual Studio for Mac でプロジェクトとソリューションを作成する方法について説明します。
author: heiligerdankgesang
ms.author: dominicn
ms.date: 05/23/2019
ms.assetid: 5880BB10-0A12-47E2-8A82-7A2D59C4D579
ms.openlocfilehash: dbfc0d951524bb9ffbbd4a2366679cfc6ae41925
ms.sourcegitcommit: 7fbfb2a1d43ce72545096c635df2b04496b0be71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/09/2019
ms.locfileid: "67693066"
---
# <a name="creating-a-new-project"></a>新規プロジェクトの作成

## <a name="opening-the-project-creation-dialog"></a>[プロジェクト作成] ダイアログを開く

Visual Studio for Mac では、いくつかの方法で新しいプロジェクトを作成できます。 Visual Studio for Mac を初めて開くと、ようこそ画面が表示されます。 ここから、 **[新規]** を選択して、プロジェクト作成画面に移動することができます。

> [!TIP]
> さらに、ようこそ画面から、最近使ったプロジェクトおよびソリューションを開いて検索することができます。 メニュー バーに移動し、 **[ファイル]、[最近のソリューション]** の順に選択することで、最近使ったプロジェクトを開くこともできます。

![ようこそ画面と新しいプロジェクトの作成](media/first-run-project.png)

Visual Studio for Mac が既に開いていてソリューションが読み込まれている場合は、メニューバーに進み、 **[ファイル]、[新しいソリューション]** の順に選択して、新しいソリューションを作成することができます。 この方法で新しいソリューションを作成する場合、既に読み込まれているソリューションは閉じられます。

## <a name="creating-a-new-project-from-a-template"></a>テンプレートからの新規プロジェクトの作成

**[新しいプロジェクト]** ダイアログには、既定では、最近ご使用になったテンプレートが "*使用時刻の新しい*" 順に並べ替えられて表示されます。

最近使ったテンプレートを使用したくない場合は、ダイアログの左側にあるカテゴリから選択できます。 各カテゴリには、選択できるプロジェクト テンプレートがいくつか含まれています。 プロジェクトの種類をクリックすると、画面の右側に説明が表示されます。

![[新しいプロジェクト] 画面](media/project-creation-screen.png)

## <a name="configuring-your-new-project"></a>ご自分の新しいプロジェクトを構成する

プロジェクト テンプレートを選択したら、後続の画面に、プロジェクトを設定するのに必須の構成手順が順次表示されます。これはプロジェクトの種類によって変わる場合があります。

すべてのプロジェクトで、新しいプロジェクトとファイルを格納する場所が必要です。 既存のソリューションにプロジェクトが追加されるのでなく、プロジェクトが新しいソリューションの一部になっている場合、ソリューション名も必須になります。

必要に応じて、この段階で Git ソース制御オプションを構成することもできます。 次の図は、.NET Core プロジェクトでの最終構成手順の例です。

![新規プロジェクトを構成する](media/configure-new-project.png)

## <a name="adding-additional-projects-to-a-solution"></a>ソリューションにさらにプロジェクトを追加する

ソリューションにさらにプロジェクトを追加するには、Solution Pad 内でソリューションを右クリックし、 **[追加]、[新しいプロジェクトの追加]** の順に選択するか、または **[追加]、[既存のプロジェクトの追加]** の順に選択します。

新しいプロジェクトの追加を選択すると、「[ご自分の新しいプロジェクトを構成する](#configuring-your-new-project)」に示すように、プロジェクトの作成が開始されます。

既存のプロジェクトを追加することを選択した場合は、ご利用のコンピューター上にある既存のプロジェクトを参照してそれをソリューションに追加できます。

## <a name="see-also"></a>関連項目

- [ソリューションとプロジェクトを作成する (Windows の Visual Studio)](/visualstudio/ide/creating-solutions-and-projects)