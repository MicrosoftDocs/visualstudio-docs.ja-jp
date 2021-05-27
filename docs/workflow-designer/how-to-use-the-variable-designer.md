---
title: 'ワークフロー デザイナー - 方法: 変数デザイナーを使用する'
description: 変数デザイナーを使用し、データ バインディング シナリオや条件ステートメントで使用する変数を作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- System.Activities.Presentation.View.DesignTimeVariable.UI
ms.assetid: 0318dfb0-bf8f-4f92-9b86-ae4c1b2161ad
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: a427b14db5be8081352ce54bf13900fa826202b9
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99894011"
---
# <a name="how-to-use-the-variable-designer"></a>変数デザイナーを使用する方法

変数デザイナーは、データ バインディングや条件ステートメントで使用する変数を作成するために使用します。 デザイナーにアクセスするには、デザイン キャンバスの左下隅にある **[変数]** ボタンをクリックします。 デザイナーには、表形式で表示される変数のリストが含まれています。そのリストは、 **[既定]** 列以外の各列見出しで並べ替えることができます。 それぞれの変数には、名前、変数の型、スコープ、および既定値 (存在する場合) があります。 名前および既定値は編集可能なテキスト フィールドで、型およびスコープはドロップダウン リストです。 スコープは、変数デザイナーの呼び出し時に選択されたアクティビティです。 選択したスコープ内に変数を作成できない場合は、対応するスコープに変数を作成できる直近の先祖アクティビティが既定のスコープとなります。 詳細については、[変数と引数 (.NET)](/dotnet/framework/windows-workflow-foundation/variables-and-arguments) に関するページを参照してください。

 いずれかの並べ替えコントロールをユーザーが明示的に使用するか、変数デザイナーを閉じてから開き直すか、または、別の変数を作成するまで、並べ替え順序は適用されません。

## <a name="to-create-a-new-variable"></a>新しい変数を作成するには

1. Visual Studio でワークフロー ソリューションまたはアクティビティ ソリューションを開きます。

2. デザイン キャンバスで、ワークフローのアクティビティを選択します。

3. 変数デザイナーを開くには、デザイン キャンバスの左下隅にある **[変数]** ボタンをクリックします。 変数デザイナーが表示されます。

4. **[変数の作成]** というラベルの付いた空の行をクリックします。 既定値を使用する新しい変数を含む行が新規に追加されます。既定値は、 **[名前]** では variablex (x は一意の変数名となるように初期値を 1 として自動的に増やされる整数)、 **[変数の型]** では **[文字列]** 、 **[スコープ]** では **[シーケンス]** となります。 **[既定値]** には、値は追加されません。 これらの値は、ワークフローのデザイン プロセス中にいつでも変更できます。

    > [!NOTE]
    > 変数を削除するには、変数をクリックして選択し、**Del** キーを押します。

## <a name="see-also"></a>関連項目

- [ワークフロー デザイナーの使用](developing-applications-with-the-workflow-designer.md)
- [変数と引数](/dotnet/framework/windows-workflow-foundation/variables-and-arguments)
- [方法: 引数デザイナーを使用する](../workflow-designer/how-to-use-the-argument-designer.md)
