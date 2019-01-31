---
title: 起動時間の改善
ms.date: 11/15/2017
ms.topic: conceptual
helpviewer_keywords:
- startup time [Visual Studio]
- optimizing performance [Visual Studio]
- speed up start time [Visual Studio]
ms.assetid: d1508121-8499-4084-8eb5-fa89fa7b17d3
author: gewarren
ms.author: gewarren
manager: jillfra
f1_keywords:
- vs.performancecenter
ms.prod: visual-studio-dev15
ms.workload:
- multiple
ms.openlocfilehash: 873977e8ab1180eb6671a34304b033515b6fc36e
ms.sourcegitcommit: 2193323efc608118e0ce6f6b2ff532f158245d56
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/25/2019
ms.locfileid: "54949299"
---
# <a name="optimize-visual-studio-startup-time"></a>Visual Studio の起動時間の最適化

Visual Studio は、可能な限り迅速かつ効率的に起動するように設計されています。 ただし、特定の Visual Studio の拡張機能とツール ウィンドウは、その読み込み時に起動時間に悪影響を与える可能性があります。 **[Visual Studio のパフォーマンスの管理]** ダイアログ ボックスでは、起動に時間がかかる拡張機能とツール ウィンドウの動作を制御することができます。 パフォーマンスの向上に関するより一般的なヒントについては、「[Visual Studio のパフォーマンスのヒントとテクニック](../ide/visual-studio-performance-tips-and-tricks.md)」を参照してください。

## <a name="startup-behavior"></a>起動の動作

起動時間が長くならないように、Visual Studio 2017 では、_要求に応じて_読み込む方法を使用して拡張機能を読み込みます。 この動作は、Visual Studio の起動後すぐに拡張機能を開くのではなく、必要に応じて開くことを意味します。 また、前の Visual Studio セッションでツール ウィンドウが開いたままである場合、スタートアップ時間が長くなる可能性があるため、Visual Studio は起動時間に影響しないようにより合理的な方法でツール ウィンドウを開きます。

Visual Studio で起動の遅延が検出されると、ポップアップ メッセージが表示され、拡張機能またはツール ウィンドウが原因で遅延が発生していることを警告します。 メッセージには **[Visual Studio のパフォーマンスの管理]** ダイアログ ボックスへのリンクが表示されます。 このダイアログ ボックスには、メニュー バーで **[ヘルプ]** > **[Visual Studio のパフォーマンスの管理]** の順に選択することでアクセスすることもできます。

![Visual Studio のパフォーマンスの管理 - "拡張機能...によって Visual Studio の速度が遅くなっていることを検出しました。" という内容のポップアップ](../ide/media/vside_perfdialog_popup.png)

ダイアログ ボックスには、起動のパフォーマンスに影響している拡張機能とツール ウィンドウが一覧されます。 起動時のパフォーマンスを向上させるために、拡張機能とツール ウィンドウの設定を変更することができます。

## <a name="a-nameextensions-to-change-extension-settings-to-improve-startup-solution-load-and-typing-performance"></a><a name="extensions" />拡張機能の設定を変更して、起動時、ソリューションの読み込み時、および入力時のパフォーマンスを向上させるには

1. メニュー バーで **[ヘルプ]** > **[Visual Studio のパフォーマンスの管理]** の順に選択して、**[Visual Studio のパフォーマンスの管理]** ダイアログ ボックスを開きます。

    拡張機能が Visual Studio の起動、ソリューションの読み込み、または入力の遅延の原因となっている場合は、**[Visual Studio のパフォーマンスの管理]** ダイアログ ボックスの **[拡張機能]** > **[スタートアップ]** (あるいは **[ソリューションの読み込み]** または **[入力]**) に拡張機能が表示されます。

    ![Visual Studio のパフォーマンスの管理 - 拡張機能の表示](../ide/media/vside_perfdialog_extensions.png)

2. 無効にする拡張機能を選択してから、**[無効にする]** ボタンを選択します。

**拡張機能マネージャー**または **[Visual Studio のパフォーマンスの管理]** ダイアログ ボックスを使用すれば、今後のセッションでいつでも拡張機能を再度有効にすることができます。

## <a name="a-nametool-windows-to-change-tool-window-settings-to-improve-startup-time"></a><a name="tool-windows" />ツール ウィンドウの設定を変更して起動時間を向上させるには

1. メニュー バーで **[ヘルプ]** > **[Visual Studio のパフォーマンスの管理]** の順に選択して、**[Visual Studio のパフォーマンスの管理]** ダイアログ ボックスを開きます。

    ツール ウィンドウが Visual Studio の起動の遅延の原因となっている場合は、**[Visual Studio のパフォーマンスの管理]** ダイアログ ボックスの **[ツール ウィンドウ]** > **[スタートアップ]** にツール ウィンドウが表示されます。

2. 動作を変更するツール ウィンドウを選択します。

3. 次の 3 つのオプションのいずれかを選択します。

   - **既定動作を使用します:** ツール ウィンドウの既定の動作。 このオプションを選択したままにすると、起動時のパフォーマンスは向上しません。

   - **起動時にウィンドウを表示しない:** Visual Studio を開いたときに、指定したツール ウィンドウが常に閉じられます。前のセッションで開いたままの場合でも同じです。 ツール ウィンドウは、必要なときに対応するメニューから開くことができます。

   - **起動時にウィンドウを自動的に隠す:** ツール ウィンドウが前のセッションで開いたままの場合、このオプションを選択すると、起動時にツール ウィンドウのグループが折りたたまれ、ツール ウィンドウが初期化されないようになります。 このオプションは、ツール ウィンドウを頻繁に使用する場合に適しています。 ツール ウィンドウがまだ使用可能でも、Visual Studio の起動時間には悪影響しなくなります。

     ![Visual Studio のパフォーマンスの管理 - ツール ウィンドウの表示](../ide/media/vside_perfdialog_toolwindows.png)

> [!NOTE]
> Visual Studio 2017 より前のバージョンには、**ライトウェイト ソリューション ロード**という機能がありました。 Visual Studio 2017 バージョン 15.5 以降では、この機能を使用できなくなりました。 Visual Studio 2017 バージョン 15.5 以降の場合、マネージド コードを含む大規模なソリューションで、ライトウェイト ソリューション ロードなしでも以前よりはるかに速く読み込むことができます。

## <a name="see-also"></a>関連項目

- [Visual Studio のパフォーマンスの最適化](../ide/optimize-visual-studio-performance.md)
- [Visual Studio のパフォーマンスのヒントとテクニック](../ide/visual-studio-performance-tips-and-tricks.md)
- [Visual Studio ブログ - Visual Studio 2017 バージョン 15.6 でソリューションの読み込みを速くする](https://blogs.msdn.microsoft.com/visualstudio/2018/04/04/load-solutions-faster-with-visual-studio-2017-version-15-6/)