---
title: インターフェイスの抽出リファクタリング
ms.date: 01/26/2018
ms.topic: reference
author: gewarren
ms.author: gewarren
manager: jillfra
f1_keywords:
- vs.csharp.refactoring.extractinterface
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
ms.openlocfilehash: cdead60fbde711ac9b219a6bbcb635e329d51a0a
ms.sourcegitcommit: d3a485d47c6ba01b0fc9878cbbb7fe88755b29af
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2019
ms.locfileid: "57983201"
---
# <a name="extract-an-interface-refactoring"></a>インターフェイスの抽出リファクタリング

このリファクタリングは以下に適用されます。

- C#

- Visual Basic

**概要:** クラス、構造体、またはインターフェイスから既存のメンバーを使用するインターフェイスを作成できます。

**条件:** 他のクラス、構造体、またはインターフェイスによって継承可能なクラス、構造体、またはインターフェイスのメンバーがあること。

**理由:** インターフェイスは、オブジェクト指向設計の優れた構成要素であるため。 さまざまな動物のクラス (Dog、Cat、Bird) があり、これらすべてが Eat、Drink、Sleep などの共通メソッドを持つとします。 IAnimal のようなインターフェイスを使用すると、Dog、Cat、Bird に、これらのメソッド共通の "シグネチャ" を持たせることができます。

## <a name="extract-an-interface-refactoring"></a>インターフェイスの抽出リファクタリング

1. クラス名にカーソルを置きます。

   - C#: 

       ![強調表示されたコード - C#](media/extractinterface-highlight-cs.png)

   - Visual Basic: 

       ![強調表示されたコード - Visual Basic](media/extractinterface-highlight-vb.png)

2. 次のいずれかの操作を実行します。

   - **キーボード**
      - **Ctrl + R** キーを押し、次に **Ctrl + I** キーを押します。 (キーボード ショートカットは、選択したプロファイルによって異なる場合があります。)
      - 行の任意の場所で **Ctrl**+**.** キーを押すと、 **[クイック アクションとリファクタリング]** メニューをトリガーし、[プレビュー] ウィンドウ ポップアップから **[インターフェイスの抽出]** を選択します。
   - **マウス**
      - **[編集] > [リファクター] > [インターフェイスの抽出]** の順に選択します。
      - クラスの名前を右クリックして **[クイック アクションとリファクタリング]** メニューを選択し、[プレビュー] ウィンドウ ポップアップから **[インターフェイスの抽出]** を選択します。

3. 表示される **[インターフェイスの抽出]** ダイアログ ボックスで、必要な情報を入力します。

   ![インターフェイスの展開](media/extractinterface-dialog-same-file.png)


   | フィールド | 説明 |
   | - | - |
   | **新しいインターフェイス名** | 作成するインターフェイスの名前。 名前は既定値の I*ClassName* になります。ここで、*ClassName* は上で選択したクラスの名前になります。 |
   | **新しいファイル名** | インターフェイスを含む、生成されたファイルの名前。 インターフェイス名と同様に、この名前の既定値は I*ClassName* になります。ここで、*ClassName* は上で選択したクラスの名前です。 **現在のファイルに追加**するオプションを選択することもできます。 |
   | **インターフェイスを形成するパブリック メンバーを選択する** | インターフェイスに抽出する項目。 選択できる数に制限はありません。 |


4. **[OK]** をクリックします。

   指定した名前のファイルにインターフェイスが作成されます。 さらに、選択したクラスにそのインターフェイスが実装されます。

   - C#: 

      ![結果のクラス - C#](media/extractinterface-class-cs.png)
      
      
      ![結果のインターフェイス - C#](media/extractinterface-interface-cs.png)

   - Visual Basic: 

      ![結果のクラス - Visual Basic](media/extractinterface-class-vb.png)
      
      
      ![結果のインターフェイス - Visual Basic](media/extractinterface-interface-vb.png)

## <a name="see-also"></a>関連項目

- [リファクタリング](../refactoring-in-visual-studio.md)
- [.NET 開発者向けのヒント](../../ide/visual-studio-2017-for-dotnet-developers.md)
