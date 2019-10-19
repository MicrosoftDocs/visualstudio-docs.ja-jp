---
title: コードマップのエクスポートと保存
ms.date: 05/16/2018
ms.topic: conceptual
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 991773953338e38331bad45bfa1149aeb27c748b
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72670801"
---
# <a name="share-code-maps"></a>コード マップの共有

コードマップは、Visual Studio プロジェクトの一部として、イメージとして、または XPS ファイルとして保存できます。

## <a name="share-a-code-map-with-other-visual-studio-users"></a>コードマップを他の Visual Studio ユーザーと共有する

マップを保存するには、 **[ファイル]** メニューを使用します。

-または-

マップを特定のプロジェクトの一部として保存するには、マップのツールバーで **共有** >  移動 を選択し、> を **\<CodeMapName に移動**します。次に、マップを保存するプロジェクトを選択します。

![マップを別のプロジェクトに移動する](../modeling/media/codemapsmovemapmenu.png)

Visual Studio では、マップは .dgml ファイルとして保存され*ます。* これは、Visual Studio Enterprise および Visual Studio Professional の他のユーザーと共有できます。

> [!NOTE]
> Visual Studio Professional を使用するユーザーとマップを共有する前に、グループを展開しておくこと、非表示のノードとグループ間リンクを表示しておくこと、マップに表示する必要のある削除済みのノードを取得しておくことが必要です。 そうしない場合、他のユーザーはそれらの項目を表示できなくなります。
>
> モデリング プロジェクト内のマップまたはモデリング プロジェクトから別の場所にコピーされたマップを保存すると、次のエラーが発生する可能性があります。
>
> "プロジェクト ディレクトリの外部で *fileName* を保存できません。 リンクされた項目はサポートされていません。"
>
> Visual Studio にはエラーが表示されます。ただし、保存したバージョンは生成されます。 このエラーを回避するには、モデリング プロジェクトの外部でマップを生成します。 その後、目的の場所にグラフを保存できます。 単にソリューション内の別の場所にファイルをコピーし、その後で保存しようとすると失敗します。

## <a name="export-a-code-map-as-an-image"></a>コードマップをイメージとしてエクスポートする

コードマップをイメージとしてエクスポートする場合は、Microsoft Word や PowerPoint などの他のアプリケーションにコピーできます。

1. コードマップのツールバーで、[**イメージとして電子メール**を**共有** > ] または **[イメージのコピー]** を選択します。

2. そのイメージを他のアプリケーションに貼り付けます。

## <a name="export-the-map-as-an-xps-file"></a>マップを XPS ファイルとしてエクスポートする

コードマップを XPS ファイルとしてエクスポートすると、Internet Explorer のような XML または XAML ビューアーで表示できます。

1. コードマップのツールバーで、[ > **電子メールをポータブル Xps として** **共有**する] または **[ポータブル xps として保存]** を選択します。

2. ファイルを保存する場所を参照します。

3. コード マップの名前を付けます。 **[名前を付けて保存]** ボックスが**xps ファイル (\* .xps)** に設定されていることを確認します。 **[保存]** をクリックします。

## <a name="see-also"></a>関連項目

- [依存関係をコードマップとマップする](../modeling/map-dependencies-across-your-solutions.md)