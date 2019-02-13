---
title: Visual Studio が遅いときにパフォーマンスを改善する
titleSuffix: ''
ms.date: 04/11/2018
ms.topic: conceptual
helpviewer_keywords:
- performance [Visual Studio]
author: gewarren
ms.author: gewarren
manager: jillfra
f1_keywords:
- vs.performancecenter
ms.workload:
- multiple
ms.openlocfilehash: df1d5b89115e6fa33be09bf41de3b51d4d584d57
ms.sourcegitcommit: 21d667104199c2493accec20c2388cf674b195c3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2019
ms.locfileid: "55913003"
---
# <a name="optimize-visual-studio-performance"></a>Visual Studio のパフォーマンスの最適化

この記事では、Visual Studio の動作が遅いときに試すべきことをいくつか紹介します。 パフォーマンス改善案は他にもあり、「[Visual Studio のパフォーマンスのヒントとテクニック](../ide/visual-studio-performance-tips-and-tricks.md)」でご確認いただけます。

## <a name="upgrade-to-visual-studio-2017-version-156-or-later"></a>Visual Studio 2017 バージョン 15.6 以降にアップグレードする

Visual Studio 2015 を現在使用している場合、[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2017) を無料でダウンロードし、パフォーマンスの改善をご確認ください。 Visual Studio 2017 では、ソリューションの読み込みが 2 ～ 3 倍速くなります。その他の面でもパフォーマンスが改善されます。 Visual Studio 2017 と Visual Studio 2015 の間には並行互換性があるので、試しても失うものはありません。

Visual Studio 2017 を現在使用している場合、15.6 以降のバージョンを実行していることを確認してください。 バージョン 15.6 ではソリューションの読み込みが最大 2 ～ 3 倍速くなることがデータによって示されています。 [ここから](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)ダウンロードしてください。

## <a name="extensions-and-tool-windows"></a>拡張機能とツール ウィンドウ

インストールした拡張機能が Visual Studio を遅くしていることがあります。 拡張機能を管理してパフォーマンスを改善する方法については、[拡張機能設定を変更してパフォーマンスを改善する](../ide/optimize-visual-studio-startup-time.md#extensions)方法に関するページを参照してください。

同様に、ツール ウィンドウが Visual Studio を遅くしていることがあります。 ツール ウィンドウを管理する方法については、[ツール ウィンドウ設定を変更してパフォーマンスを改善する](../ide/optimize-visual-studio-startup-time.md#tool-windows)方法に関するページを参照してください。

## <a name="hardware"></a>ハードウェア

ハードウェアのアップグレードを検討している場合、ソリッドステート ドライブ (SSD) がパフォーマンスの面で RAM を追加したり、より速い CPU に替えたりすることより効果があります。

SSD を追加する場合、最適なパフォーマンスを得るために、ハード ディスク ドライブ (HDD) ではなく、その SSD に Windows をインストールしてください。 お使いの Visual Studio ソリューションをどのドライブに置くかということはそれほど問題ではありません。

また、USB ドライブからはソリューションを実行しないでください。 ソリューションを HDD または SSD にコピーしてください。

## <a name="help-us-improve"></a>改善にご協力ください

お客様からのフィードバックは品質向上に役立ちます。 **問題の報告**機能を利用してトレースを “記録” し、Microsoft にご送信ください。 **[クイック起動]** の横にあるフィードバック アイコンを選択するか、メニュー バーで **[ヘルプ]**、**[フィードバックの送信]**、**[問題の報告]** の順に選択します。 詳細については、「[Visual Studio 2017 で問題を報告する方法](../ide/how-to-report-a-problem-with-visual-studio-2017.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [パフォーマンスのヒントとテクニック](../ide/visual-studio-performance-tips-and-tricks.md)
- [Visual Studio ブログ - Visual Studio 2017 バージョン 15.6 でソリューションの読み込みを速くする](https://blogs.msdn.microsoft.com/visualstudio/2018/04/04/load-solutions-faster-with-visual-studio-2017-version-15-6/)