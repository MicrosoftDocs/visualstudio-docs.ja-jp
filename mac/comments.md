---
title: コメント アウト コード
description: この記事では、Visual Studio for Mac のソース エディターでのコメントの使用について説明します
author: conceptdev
ms.author: crdun
ms.date: 05/06/2018
ms.assetid: 0FE5E929-1846-4F48-B5E3-70990FAF9504
ms.openlocfilehash: 1f792e5ba670854e4a3a9ce703212d18c16e5512
ms.sourcegitcommit: 0a8ac5f2a685270d9ca79bb39d26fd90099bfa29
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/09/2018
ms.locfileid: "51295658"
---
# <a name="comments"></a>コメント

コードをデバッグしたり、コードで実験したりするとき、一時的に、あるいは長期間、コードのブロックにコメントを付けると便利です。

コード ブロック全体にコメントを付けるには:

* コードを選択し、コンテキスト メニューから **[行コメントの切り替え]** を選択します。

OR

* 選択したコードで `cmd + /` キー バインドを使用します。

いずれの方法も、コード セクションにコメントを付けるか、コメントを解除するために利用できます。 C# ファイルの場合、行コメントのレベルを追加できます。レベルを追加すると、実際のコメントを維持しながら、コード領域にコメントを付けたり、コメントを解除したりできます。

![複数レベルのコメント](media/source-editor-image8.png)

コメントは、将来、コードを利用するかもしれない開発者のためにコードを記録しておく意味でも役立ちます。 以上の作業は通常、複数行コメントという形態で行われます。これは各言語で次のように追加されます。

**C#**

```csharp
/*
 This is a multi-line
 comment in C#
*/
```

**F#**

```fsharp
(*
 This is a multi-line
  comment in F#
*)
```

## <a name="see-also"></a>関連項目

- [コメント アウト コード (Windows の Visual Studio)](/visualstudio/ide/quickstart-editor#comment-out-code)