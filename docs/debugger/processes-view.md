---
title: プロセス ビュー |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.externaltools.spyplus.processesview
helpviewer_keywords:
- Processes view
ms.assetid: e144e70e-eef2-45a7-a562-a177f177d9a1
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 99ba60021410f1965e05f7c5479231013d53cb71
ms.sourcegitcommit: b0d8e61745f67bd1f7ecf7fe080a0fe73ac6a181
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 02/22/2019
ms.locfileid: "56697625"
---
# <a name="processes-view"></a>プロセス ビュー
プロセス ビューには、システム上のすべてのアクティブなプロセスのツリーが表示されます。 プロセス ID とモジュール名が表示されます。 通常、実行中のプログラムに対応する特定のシステム プロセスを確認する場合は、プロセス ビューを使用します。 プロセスは、モジュール名で識別されますまたは「システム プロセスです」を指定します。

 Microsoft Windows では、複数のプロセスをサポートします。 各プロセスは、1 つまたは複数のスレッドを持つことができ、各スレッドは、いずれかを指定できます。 または関連付けられている複数の最上位レベルのウィンドウ。 各最上位ウィンドウには、一連のウィンドウを所有できます。 A + 記号は、レベルが折りたたまれていることを示します。 折りたたまれたビューは、プロセスごとに 1 行で構成されます。 をクリックして、+ 記号レベルを展開します。

 通常、実行中のプログラムに対応する特定のシステム プロセスを確認する場合は、プロセス ビューを使用します。 プロセスは、モジュール名で識別されますまたは「システム プロセスです」を指定します。 プロセスを検索するには、ツリーを折りたたむし、一覧を検索します。

## <a name="procedures"></a>手順

#### <a name="to-open-the-processes-view"></a>プロセス ビューを開く

1. **スパイ**] メニューの [選択**プロセス**します。

   ![Spy&#43; &#43;プロセス ビュー](../debugger/media/spy--_processes.png "スパイ + _Processes") spy++ プロセス ビュー

   上記の図は、展開プロセスとスレッドのノードを持つプロセス ビューを示しています。

### <a name="in-this-section"></a>このセクションの内容
 [プロセス ビューでプロセスを探して](../debugger/how-to-search-for-a-process-in-processes-view.md)プロセス ビューで、特定のプロセスを検索する方法について説明します。

 [プロセスのプロパティを表示する](../debugger/how-to-display-process-properties.md)メッセージに関する詳細情報を表示する方法について説明します。

### <a name="related-sections"></a>関連項目
 [Spy++ ビュー](../debugger/spy-increment-views.md) spy++ ツリー ビュー ウィンドウやメッセージ、プロセス、スレッドのについて説明します。

 [Spy++ の使用](../debugger/using-spy-increment.md)の spy++ ツールを紹介し、使用する方法について説明します。

 [プロセス検索 ダイアログ ボックス](../debugger/process-search-dialog-box.md)プロセス ビューで特定のプロセスのノードを検索するために使用します。

 [プロセス プロパティ ダイアログ ボックス](../debugger/process-properties-dialog-box.md)プロセス ビューで選択したプロセスのプロパティが表示されます。

 [Spy++ リファレンス](../debugger/spy-increment-reference.md)各 spy++ メニューおよびダイアログ ボックスについて説明するセクションが含まれています。