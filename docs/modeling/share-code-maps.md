---
title: コード マップのエクスポートと保存
description: コード マップを Visual Studio プロジェクトの一部として、イメージとして、または XPS ファイルとして保存する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 05/16/2018
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 324f8fe7ee34f469d31ad1ce6cf6bd25ab97f225
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99899824"
---
# <a name="share-code-maps"></a>コード マップの共有

コード マップを Visual Studio プロジェクトの一部として、イメージとして、または XPS ファイルとして保存することができます。

## <a name="share-a-code-map-with-other-visual-studio-users"></a>コード マップを他の Visual Studio ユーザーと共有する

マップを保存するには、 **[ファイル]** メニューを使用します。

または

特定のプロジェクトの一部としてマップを保存するには、マップのツールバーで、 **[共有]**  >  **[\<CodeMapName>.dgml の移動先]** の順にクリックし、マップの保存先のプロジェクトを選択します。

![マップを別のプロジェクトに移動する](../modeling/media/codemapsmovemapmenu.png)

Visual Studio では、マップは *.dgml* ファイル形式で保存され、他の Visual Studio Enterprise および Visual Studio Professional ユーザーと共有できます。

> [!NOTE]
> Visual Studio Professional を使用するユーザーとマップを共有する前に、グループを展開しておくこと、非表示のノードとグループ間リンクを表示しておくこと、マップに表示する必要のある削除済みのノードを取得しておくことが必要です。 そうしない場合、他のユーザーはそれらの項目を表示できなくなります。
>
> モデリング プロジェクト内のマップまたはモデリング プロジェクトから別の場所にコピーされたマップを保存すると、次のエラーが発生する可能性があります。
>
> "プロジェクト ディレクトリの外部で *fileName* を保存できません。 リンクされた項目はサポートされていません。"
>
> Visual Studio にはエラーが表示されます。ただし、保存したバージョンは生成されます。 このエラーを回避するには、モデリング プロジェクトの外部でマップを生成します。 その後、目的の場所にグラフを保存できます。 単にソリューション内の別の場所にファイルをコピーし、その後で保存しようとすると失敗します。

## <a name="export-a-code-map-as-an-image"></a>コード マップをイメージとしてエクスポートする

マップをイメージとしてエクスポートするとき、Microsoft Word や PowerPoint などの他のアプリケーションにコピーできます。

1. コード マップ ツールバーで、 **[共有]**  >  **[画像として電子メールで送信]** または **[イメージのコピー]** の順にクリックします。

2. そのイメージを他のアプリケーションに貼り付けます。

## <a name="export-the-map-as-an-xps-file"></a>マップを XPS ファイルとしてエクスポートする

コード マップを XPS ファイルとしてエクスポートすると、Internet Explorer のような XML または XAML ビューアーで表示できます。

1. コード マップ ツールバーで、 **[共有]**  >  **[ポータブル XPS として電子メールで送信]** または **[ポータブル XPS として保存]** の順にクリックします。

2. ファイルを保存する場所を参照します。

3. コード マップの名前を付けます。 **[保存の種類]** ボックスが [**XPS ファイル (\*.xps)** ] に設定されていることを確認します。 **[保存]** を選択します。

## <a name="see-also"></a>関連項目

- [コード マップを使用して依存関係をマップする](../modeling/map-dependencies-across-your-solutions.md)
