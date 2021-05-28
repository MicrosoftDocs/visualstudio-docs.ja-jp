---
title: 'ワークフロー デザイナー - 方法: 引数デザイナーを使用する'
description: 引数デザイナーについて、および引数デザイナーを使用して、アクティビティとの間でデータをやり取りできるようにする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- System.Activities.Presentation.View.ArgumentDesigner.UI
- System.Activities.Presentation.View.DesignTimeArgument.UI
ms.assetid: 64813fd5-1ea1-499a-98b4-ab2a44b7ee5e
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 9b97368a942747046aa7641771f84a9f2ed41e11
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99894102"
---
# <a name="how-to-use-the-argument-designer"></a>引数デザイナーを使用する方法

引数デザイナーを使用すると、アクティビティとの間のデータの受け渡しを簡単に行うことができます。 デザイナーにアクセスするには、デザイン キャンバスの左下隅にある **[引数]** ボタンをクリックします。 デザイナーには、表形式で表示される引数のリストが含まれています。そのリストは、 **[既定値]** 列以外の各列見出しで並べ替えることができます。 各引数には、名前、方向 (入力、出力、入力/出力、またはプロパティ)、型、および既定の式の値 (存在する場合) が含まれます。 名前および既定の式の値は編集可能なテキスト フィールドで、型および方向はドロップダウンです。 詳細については、[変数と引数 (.NET)](/dotnet/framework/windows-workflow-foundation/variables-and-arguments) に関するページを参照してください。

## <a name="to-create-a-new-argument"></a>新しい引数を作成するには

1. Visual Studio でワークフロー ソリューションまたはアクティビティ ソリューションを開きます。

2. デザイン キャンバスの左下隅にある **[引数]** ボタンをクリックして、引数デザイナーを開きます。 引数デザイナーが表示されます。

3. **[引数の作成]** というラベルの付いた空の行をクリックします。 新しい引数を格納する行が新規に追加されます。引数に使用される既定値は、 **[名前]** が argumentx (x は、初期値の 1 から自動的にインクリメントされて一意の引数名となる整数)、 **[方向]** が **[入力]** 、 **[引数の型]** が **[文字列]** となります。 **[既定値]** には、値は追加されません。 これらの値は、ワークフローのデザイン プロセス中にいつでも変更できます。

    > [!NOTE]
    > 引数を削除するには、引数をクリックして選択し、**Del** キーを押します。

## <a name="see-also"></a>関連項目

- [ワークフロー デザイナーの使用](developing-applications-with-the-workflow-designer.md)
- [変数と引数](/dotnet/framework/windows-workflow-foundation/variables-and-arguments)
