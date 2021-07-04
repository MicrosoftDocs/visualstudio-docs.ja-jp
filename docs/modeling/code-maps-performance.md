---
title: コード マップが遅い
description: コード マップのパフォーマンスを向上させる方法と、表示の完了に必要な時間を最小限に抑える方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 05/16/2018
ms.topic: conceptual
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: d5a279a04b1bd76933df335bc0b2527ab4b2418f
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112389645"
---
# <a name="improve-performance-for-code-maps"></a>コード マップのパフォーマンスを向上させる

マップを初めて生成したときに、Visual Studio は、見つかったすべての依存関係のインデックスを作成します。 このプロセスには、特に大規模なソリューションの場合に時間がかかることがありますが、その後、パフォーマンスは向上します。 コードが変更された場合、Visual Studio では、更新されたコードだけにインデックスが付け直されます。 マップの表示にかかる時間を最小限に抑えたい場合は、次の提案を検討してください。

- 目的の依存関係のみをマップする。

- ソリューション全体のマップを生成する前に、ソリューションのスコープを縮小する。

- コード マップ ツールバーの **[ビルドのスキップ]** を選択し、ソリューションの自動ビルドをオフにする。

- コード マップ ツールバーの **[親を含める]** を選択し、親項目の自動追加をオフにする。

   ![[ビルドのスキップ] ボタンと [親を含める] ボタン](../modeling/media/codemapsfilterskipbuildicons.png)

- コード マップ ファイルを直接編集し、不要なノードとリンクを削除する。 マップを変更しても、基のコードには影響しません。 「 [Customize code maps by editing the DGML files](../modeling/customize-code-maps-by-editing-the-dgml-files.md)」を参照してください。

プロジェクト項目の **[出力ディレクトリにコピー]** プロパティが **[常にコピーする]** に設定されていると、マップの生成や、**ソリューション エクスプローラー** からマップへの項目の追加に時間がかかることがあります。 パフォーマンスを向上させるには、このプロパティを **[新しい場合はコピーする]** または `PreserveNewest`に変更します。 「[インクリメンタル ビルドs](../msbuild/incremental-builds.md)」を参照してください。

完成されたマップには、ビルドに成功したコードの依存関係のみが表示されます。 特定のコンポーネントにビルド エラーが発生すると、そのエラーがマップに表示されます。 マップに基づいてアーキテクチャを決定する前に、コンポーネントが実際にビルドされ、その依存関係がマップ上に表示されていることを確認してください。
