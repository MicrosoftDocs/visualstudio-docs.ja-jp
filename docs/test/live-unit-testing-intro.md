---
title: Live Unit Testing の概要
description: Live Unit Testing の利点と、Live Unit Testing を使用してプロジェクトを単体テストする方法について説明します。
ms.date: 09/11/2017
ms.topic: conceptual
helpviewer_keywords:
- Live Unit Testing
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- dotnet
ms.openlocfilehash: 2c4da809455a859479d0421bffaa1b257a18c4b5
ms.sourcegitcommit: d4887ef2ca97c55e2dad9f179eec2c9631d91c95
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2021
ms.locfileid: "108798519"
---
# <a name="live-unit-testing-overview"></a>Live Unit Testing の概要

Live Unit Testing では、コードの変更に合わせて、自動的にリアルタイムで単体テストが実行されます。 これにより、安心してコードのリファクタリングと変更を行うことができます。 コードを編集すると、影響を受けたすべてのテストが Live Unit Testing によって自動的に実行され、変更によって回帰が発生していないことが確認されます。

Live Unit Testing では、単体テストによってコードが適切にカバーされているかどうかが示されます。 コード カバレッジがリアルタイムでグラフィカルに表示されます。 各コード行が含まれるテストの数と、単体テストによってカバーされていない行を、一目で確認できます。

1 つ以上の単体テスト プロジェクトが含まれるソリューションがある場合、Live Unit Testing を有効にするには、Visual Studio の最上位メニューから、 **[テスト]**  >  **[Live Unit Testing]**  >  **[開始]** の順に選択します。

> [!NOTE]
> Live Unit Testing は Visual Studio Enterprise エディションでのみ使用でき、.NET でのみサポートされています。

Live Unit Testing について詳細を学習するには:

- 入門用のチュートリアルを試してください: [Live Unit Testing の概要](live-unit-testing-start.md)。

- 詳細なドキュメントをお読みください: [Visual Studio Enterprise エディションで Live Unit Testing を使用する](live-unit-testing.md)。

- Live Unit Testing の新しい機能およびヒントとテクニックについては、「[Live Unit Testing についてよく寄せられる質問](live-unit-testing-faq.yml)」を参照してください。

- Live Unit Testing の概要とその機能については、Channel 9 のビデオをご覧ください。</p>

   > [!VIDEO https://channel9.msdn.com/Events/Visual-Studio/Visual-Studio-2017-Launch/T105/player]

## <a name="related-resources"></a>関連資料

- [コード テスト ツール](https://visualstudio.microsoft.com/vs/testing-tools/)
- [コードの単体テスト](unit-test-your-code.md)
