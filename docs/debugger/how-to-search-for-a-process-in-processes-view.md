---
title: '方法: プロセス ビューでプロセスを検索 |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Processes view
- processes, searching for
ms.assetid: 7cb97b37-4a95-4f1b-9eee-4910aa9c115b
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2a6b57226b14963759bb4d78afff3beb5559a63e
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/12/2019
ms.locfileid: "64798984"
---
# <a name="how-to-search-for-a-process-in-processes-view"></a>方法: プロセス ビューでプロセスを検索する
プロセス ビューで特定のプロセスを検索するには、検索条件として、プロセス ID またはモジュールの文字列を使用します。 検索の最初の方向を指定することもできます。 プロセス ツリー内の選択したプロセスの属性は、ダイアログ ボックスのフィールドが表示されます。

### <a name="to-search-for-a-process-in-processes-view"></a>プロセス ビューでプロセスを検索するには

1. そのため、ウィンドウを整列 Spy++ は、アクティブな[プロセス ビュー](../debugger/processes-view.md)ウィンドウが表示されます。

2. **検索**] メニューの [選択**プロセスの検索**

    [プロセス検索 ダイアログ ボックス](../debugger/process-search-dialog-box.md)が開きます。

3. 検索条件として、プロセス ID またはモジュールの文字列を入力します。

4. 値を指定しないすべてのフィールドをオフにします。

   > [!TIP]
   > モジュールによって所有されているすべてのプロセスを検索するには、オフ、**プロセス**ボックスに、モジュール名を入力し、**モジュール**ボックス。 使用して**次を検索**プロセスの検索を続行します。

5. 選択**を**または**ダウン**方向を検索します。

6. **[OK]** をクリックします。

   強調表示されて、一致するプロセスが見つかった場合、**プロセス ビュー**ウィンドウ。