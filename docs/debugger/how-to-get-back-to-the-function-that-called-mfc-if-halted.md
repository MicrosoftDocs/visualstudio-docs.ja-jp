---
title: 停止した場合に MFC を呼び出した関数に戻る | Microsoft Docs
description: Visual Studio デバッガーで実行が停止している場合に MFC を呼び出した関数に戻る方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.debug.mfc
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- functions [C++], debugging
- function calls, returning to calling function
- debugging [MFC], returning to calling function
- debugging [MFC], functions
- Break command
- programs, halting
- functions [debugger]
ms.assetid: d254a5a9-afbd-4923-9d7a-7422d824cabf
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 31bbb064aad5a43738b2f345cf31a20767c55e69
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112384682"
---
# <a name="how-to-get-back-to-the-function-that-called-mfc-if-halted"></a>方法: 停止した場合に MFC を呼び出した関数に戻る

> [!NOTE]
> 実際に画面に表示されるダイアログ ボックスとメニュー コマンドは、アクティブな設定またはエディションによっては、ヘルプの説明と異なる場合があります。 設定を変更するには、 **[ツール]** メニューの **[設定のインポートとエクスポート]** をクリックします。 詳細については、「[リセット設定](../ide/environment-settings.md#reset-settings)」を参照してください。

**[デバッグ]** メニューの **[中断]** コマンドでプログラムを中断した場合に MFC 内で実行が停止されたとします。そのとき、問題が自分自身で作成したコードにあることが明らかな場合は、[呼び出し履歴] ウィンドウを使用することにより、呼び出し元の関数に戻ることができます。 詳細については、[[呼び出し履歴] ウィンドウの使用](../debugger/how-to-use-the-call-stack-window.md)に関するページをご覧ください。

コードがメッセージ ポンプ内で中断する場合があります。 この場合、呼び出し履歴にユーザー コードは存在しません。 この問題を回避するには、 **[中断]** コマンドではなく、ブレークポイントを使用する必要があります。適宜、条件とヒット カウントを組み合わせて使用します。 詳細については、「 [Breakpoints and Tracepoints](/previous-versions/ktf38f66(v=vs.100))」を参照してください。

## <a name="navigate-to-the-function-from-which-mfc-was-called"></a>MFC の呼び出し元の関数を参照する

- **[呼び出し履歴]** ウィンドウを使用します。

## <a name="see-also"></a>関連項目

- [ネイティブ コードのデバッグに関する FAQ](../debugger/debugging-native-code-faqs.md)
- [ネイティブ コードのデバッグ](../debugger/debugging-native-code.md)