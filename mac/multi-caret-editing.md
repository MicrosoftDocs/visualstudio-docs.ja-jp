---
title: マルチキャレットの編集
description: Visual Studio for Mac でコードを編集するときに、複数の場所にテキストを挿入します。
author: cobey
ms.author: cobey
ms.date: 08/19/2019
ms.openlocfilehash: a21bebda057a772017fa1481e18f9801d1fbcbdf
ms.sourcegitcommit: 8e123bcb21279f2770b28696995450270b4ec0e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/25/2019
ms.locfileid: "75439050"
---
# <a name="multi-caret-editing"></a>マルチキャレットの編集

マルチキャレット編集を使用すると、_n_ 個の挿入ポイントを一度に追加できます。 マルチキャレット モードでは、マウスのクリックまたはキーボード コマンドを使用して、ドキュメントに新しいキャレットを追加できます。 プライマリ キャレットは赤いカーソルで示され、セカンダリ キャレットは薄い青色で表示されます。 マルチキャレット編集モードは、`ESC` キーを使用して無効にすることができます。

## <a name="enabling-multi-caret-editing"></a>マルチキャレット編集の有効化

### <a name="keyboard"></a>キーボード

キーボードを使用してマルチキャレット モードを有効にするには、いくつかの方法があります。 次の表に示すキーボード ショートカットを使用して、マルチキャレット編集の特定のモードにすることができます。

| ホット キー  | アクション                        | 
|---------| ------------------------------|
|  ⌥⇧.   | 次の一致にキャレットを挿入    | 
|  ⌥⇧;   | 一致するすべての項目にキャレットを挿入 | 
|  ⌥⇧,   | 最後のキャレットの削除             | 
|  ⌥⇧/   | 最後のキャレットを下へ移動          | 

これらの各動作は、コマンドを呼び出すときのキャレットの現在位置にアンカーされます。 たとえば、キャレットが "name" という単語の先頭にあって、"一致するすべての項目にキャレットを挿入" (⌥⇧;) を呼び出した場合、現在のドキュメント内にある "name" という単語の各インスタンスについて、その単語の先頭にキャレットが挿入されます。 同様に、"次の一致にキャレットを挿入" (⌥⇧.) コマンドを呼び出すと、"name" という単語の次のインスタンスにキャレットが置かれます。 このコマンドは複数回呼び出すことができます。

![マルチキャレット (キーボード)](media/multi-caret-keyboard.gif)

## <a name="mousetouchpad"></a>マウス/タッチパッド

カーソルを使用すると、マルチキャレットの特定の挿入ポイントを自由に選択できます。 キーボード ショートカットは一致する文字列にバインドされていますが、カーソルを使用すると、ドキュメント内の任意の場所に手動でキャレットを挿入することができます。 キャレットが設定されると、キーボードで入力したキー エントリが各キャレットで繰り返されます。

マウスを使用して複数のキャレットを挿入するには、⌘⌥ を押したままキャレットを入力する場所をクリックする必要があります。 ⌘⌥ キーを押している限り、挿入モードになります。 間違った場所にキャレットを挿入した場合は、⌘⌥ を押したまま同じ領域をもう一度クリックすることで、そのキャレットを削除できます。 すべてのキャレットを目的の場所に配置したら、⌘⌥ キーを離して入力を開始します。 次の GIF は、一連の挿入ポイントの選択と、誤って設定されたポイントの削除を示しています。

![マルチキャレット (マウス)](media/multi-caret-mouse.gif)

## <a name="see-also"></a>関連項目

- [クイック アクション (Windows 上の Visual Studio)](/visualstudio/ide/quick-actions)
- [コードのリファクタリング (Windows 上の Visual Studio)](/visualstudio/ide/refactoring-in-visual-studio)