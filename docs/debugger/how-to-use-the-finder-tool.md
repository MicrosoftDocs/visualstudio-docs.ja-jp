---
title: ファインダー ツールを使用する |　Microsoft Docs
description: Spy++ ツールの [ウィンドウ検索] ダイアログ ボックスでファインダー ツールを使用して、デバッグ セッション中にウィンドウのプロパティまたはメッセージを表示します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- Window Finder Tool
ms.assetid: 5841926b-08c3-4e43-88bd-4223d04f9aef
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: d48e9b580d25b521721fafa7dc475bdbe3532656
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99912228"
---
# <a name="how-to-use-the-finder-tool"></a>方法: ファインダー ツールを使用する
**[ウィンドウ検索]** ダイアログ ボックスで [ファインダー] ツールを使用して、ウィンドウのプロパティまたはメッセージを表示できます。 ファインダー ツールでは、無効になっている子ウィンドウを検索し、無効になっている子ウィンドウが重なっている場合にどのウィンドウを強調表示するかを識別することもできます。

 ![Spy&#43;&#43; の [ウィンドウ検索] ダイアログ ボックス](../debugger/media/icon_spy--_find.png "Icon_Spy++_Find") [ウィンドウ検索] ダイアログ ボックスのファインダー ツール

 上の図は、次の手順 3 の後の [ウィンドウ検索] ダイアログ ボックスを示しています。

### <a name="to-display-window-properties-or-messages"></a>ウィンドウのプロパティまたはメッセージを表示するには

1. Spy++ とターゲット ウィンドウが表示されるように、ご利用のウィンドウを配置します。

2. **[Spy]** メニューから **[ウィンドウ検索]** を選択します。

    [[ウィンドウ検索] ダイアログ ボックス](../debugger/find-window-dialog-box.md)が開きます。

3. **[ファインダー ツール]** をターゲット ウィンドウにドラッグします。

    そのツールをドラッグすると、 **[ウィンドウ検索]** ダイアログ ボックスに選択したウィンドウの詳細が表示されます。

   - または

     確認するウィンドウのハンドル (たとえば、デバッガーからコピーしたもの) がある場合は、それを **[ハンドル]** テキスト ボックスに入力します。

   > [!TIP]
   > 画面が乱雑にならないようにするには、 **[Spy を非表示]** オプションを選択します。 このオプションを選択すると、Spy++ のメイン ウィンドウが非表示になり、 **[ウィンドウ検索]** ダイアログ ボックスだけが他のアプリケーションの上に表示されます。 **[OK]** または **[キャンセル]** をクリックした場合、または **[Spy++ を非表示]** オプションをオフにした場合は、Spy++ のメイン ウィンドウが復元されます。

4. **[表示]** で、 **[プロパティ]** または **[メッセージ]** を選択します。

5. **[OK]** を押します。

    **[プロパティ]** を選択した場合は、[[ウィンドウのプロパティ] ダイアログ ボックス](../debugger/window-properties-dialog-box.md)が開きます。 **[メッセージ]** を選択した場合は、[[メッセージ ビュー]](../debugger/messages-view.md) ウィンドウが開きます。

## <a name="see-also"></a>関連項目
- [Spy++ ビュー](../debugger/spy-increment-views.md)
- [Spy++ の使用](../debugger/using-spy-increment.md)
- [Spy++ リファレンス](../debugger/spy-increment-reference.md)