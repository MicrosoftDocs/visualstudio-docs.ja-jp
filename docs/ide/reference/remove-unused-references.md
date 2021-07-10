---
title: 未使用の参照を削除する
description: '[Remove Unused References] (未使用の参照の削除) コマンドを使用し、使用していないプロジェクト参照と NuGet パッケージをクリーンアップする方法について説明します。'
ms.custom: SEO-VS-2021
ms.date: 06/01/2021
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jmartens
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
ms.openlocfilehash: 707769229ad7bc1864a135bade1df918d4b27847
ms.sourcegitcommit: f50bbdb15c4f9fca0fa245ca765183c378960cc5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/03/2021
ms.locfileid: "111352128"
---
# <a name="remove-unused-references"></a>Remove Unused References\(未使用の参照の削除\)

このリファクタリングは以下に適用されます。

- C#
- Visual Basic

**目的:** 使用されていない参照を削除する。

**使用するタイミング:** 使用していないプロジェクト参照と NuGet パッケージを消去したいとき。 

**使用する理由:** 使用されていないプロジェクト参照を削除すると、領域が節約され、アプリケーションの起動時間が短縮されます。各モジュールの読み込みには時間がかかります。また、使用されないメタデータをコンパイラに読み込ませないようにすることができます。

## <a name="how-to"></a>操作方法

1. ソリューション エクスプローラーでプロジェクト名または依存関係ノードを右クリックします。

2. **[Remove Unused References]\(未使用の参照の削除\)** を選択します。

    ![[Remove Unused References]\(未使用の参照の削除\) コマンド](media/remove-unused-references-command.png)

3. **[Remove Unused References]\(未使用の参照の削除\)** ダイアログが開き、ソース コードに含まれる、使われていない参照が表示されます。 未使用の参照は削除対象として事前選択されますが、[アクション] ドロップ ダウンから `Keep` を選択すると、参照を保持するオプションが表示されます。

    ![[Remove Unused References]\(未使用の参照の削除\) ダイアログ](media/remove-unused-references-dialog.png)

5. `Apply` をクリックすると、選択された参照が削除されます。 

## <a name="see-also"></a>関連項目

- [リファクタリング](../refactoring-in-visual-studio.md)