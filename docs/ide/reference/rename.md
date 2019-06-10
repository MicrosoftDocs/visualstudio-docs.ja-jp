---
title: 名前の変更のリファクタリング
ms.date: 01/26/2018
ms.topic: reference
author: gewarren
ms.author: gewarren
manager: jillfra
f1_keywords:
- vs.csharp.refactoring.rename
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
ms.openlocfilehash: 2b18f5763d68487e7642f5632c05516d2f1bd9e2
ms.sourcegitcommit: aeb1a1135dd789551e15aa5124099a5fe3f0f32b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2019
ms.locfileid: "66500936"
---
# <a name="rename-a-code-symbol-refactoring"></a>コード シンボルの名前の変更のリファクタリング

このリファクタリングは以下に適用されます。

- C#

- Visual Basic

**概要:** フィールド、ローカル変数、メソッド、名前空間、プロパティ、型などのコード シンボルの識別子の名前を変更します。

**条件:** すべてのインスタンスを検索して新しい名前をコピー/貼り付けすることなく、安全に名前を変更したいとき。

**理由:** プロジェクト全体で新しい名前をコピーおよび貼り付けることは、エラーにつながる可能性があるため。 このリファクタリング ツールでは、正確に名前変更操作が実行されます。

## <a name="how-to"></a>方法

1. 名前を変更する項目を強調表示するか、項目の内側にテキスト カーソルを置きます。

   - C#:

       ![強調表示されたコード - C#](media/rename-highlight-cs.png)

   - Visual Basic:

       ![強調表示されたコード - Visual Basic](media/rename-highlight-vb.png)

2. 次に、以下のいずれかを実行します。

   - **キーボード**
      - **Ctrl + R** キーを押し、次に **Ctrl + R** キーを押します。 選ばれているプロファイルによってキーボード ショートカットが異なる場合があることに注意してください。
   - **マウス**
      - **[編集] > [リファクター] > [名前の変更]** の順に選択します。
      - コードを右クリックし **[名前の変更]** を選択します。

3. 新しい名前を入力して、項目の名前を変更します。

   - C#:

      ![名前の変更のアニメーション - C#](media/rename-animated-cs.gif)

   - Visual Basic:

      ![名前の変更 - VB](media/rename-rename-vb.png)

   > [!TIP]
   > この新しい名前を使うように、コメントや他の文字列も更新できます。また、エディターの右上に表示される **[名前の変更]** ボックスのチェック ボックスを使って、保存前に[変更をプレビューする](../../ide/preview-changes.md)こともできます。

4. 変更を確認した後は、 **[適用]** ボタンを選ぶか、**Enter** キーを押すと、変更がコミットされます。

## <a name="remarks"></a>解説

- 競合が発生する可能性がある既存の名前を使うと、 **[名前の変更]** ボックスに警告が表示されます。

   ![名前変更の競合](media/rename-conflict-cs.png)

- シンボルの名前を変更する別の方法は、エディターでその名前を変更することです。 次に、シンボル名にカーソルを置き、**Ctrl**+ **を押します。** または、表示された電球アイコン メニューを展開して、 **[\<古い名前> を \<新しい名前> に変更]** を選択します。

## <a name="see-also"></a>関連項目

- [リファクタリング](../refactoring-in-visual-studio.md)
- [変更のプレビュー](../../ide/preview-changes.md)
