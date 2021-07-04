---
title: デバッグ中に別のスレッドに切り替える
description: Visual Studio でマルチスレッド アプリケーションのデバッグ中に別のスレッドに切り替えるさまざまな方法を確認します。
ms.custom: SEO-VS-2020
ms.date: 04/27/2017
ms.topic: how-to
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- threads, switching [debugging]
ms.assetid: 5cd76c52-76fa-4fcc-b37e-e9f0ecac0e9e
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: a0a68047c5c9e772fc978c56f2cd70dc9454ca57
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112384695"
---
# <a name="how-to-switch-to-another-thread-while-debugging-in-visual-studio-c-visual-basic-c"></a>方法: Visual Studio でのデバッグ中に別のスレッドに切り替える (C#、Visual Basic、C++)
マルチスレッド アプリケーションをデバッグするとき、いくつかある方法のうちいずれかを使用して、現在作業中のスレッドから別のスレッドに切り替えることができます。

> [!NOTE]
> スレッドの実行順序を制御する場合は、[スレッドの凍結と凍結解除](../debugger/get-started-debugging-multithreaded-apps.md)を行う必要があります。

コード エディターと複数のマルチスレッド デバッグ ウィンドウでスレッドを調べる場合、黄色の矢印で現在のスレッドが示されます。 巻いた尾の付いた緑色の矢印は、現在のスレッド以外のスレッドに現在のデバッガー コンテキストがあることを示しています。

### <a name="to-switch-to-any-thread-that-appears"></a>表示されている任意のスレッドに切り替えるには

- **[スレッド]** または **[並列ウォッチ]** ウィンドウで、スレッドをダブルクリックします。

### <a name="to-switch-to-a-thread-in-a-source-window"></a>ソース ウィンドウでスレッドを切り替えるには

- 左端の余白で、スレッド マーカー アイコン ![スレッド マーカー](../debugger/media/dbg-thread-marker.png "ThreadMarker") を右クリックし、 **[切り替え先]** をポイントし、切り替え先のスレッドの名前をクリックします。 ショートカット メニューには、その場所にあるスレッドのみが表示されます。

     スレッド マーカーが表示されない場合は、 **[スレッド]** ウィンドウを右クリックし、 **[ソースのスレッドを表示する]** が選択されていることを確認します。

### <a name="to-switch-to-a-thread-in-the-debug-location-toolbar"></a>[デバッグの場所] ツール バーでスレッドを切り替えるには

1. **[デバッグの場所]** ツール バーで、**スレッド** の一覧をクリックします。

2. 一覧で、切り替え先のスレッドをクリックします。

## <a name="see-also"></a>関連項目
- [マルチスレッド アプリケーションのデバッグ](../debugger/debug-multithreaded-applications-in-visual-studio.md)
