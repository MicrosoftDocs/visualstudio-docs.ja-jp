---
title: フォアグラウンド アプリのデバッグ中にデバッガー ウィンドウを使用する | Microsoft Docs
Description: フォアグラウンドで実行しなければならないプログラムをデバッグする場合は、リモート デバッグを使用してそれをバックグラウンドで実行しないようにします。
ms.custom: SEO-VS-2020, seodec18
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.debug.background
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- foreground program debugging
- remote debugging, debugging foreground programs
- debugging [Visual Studio], while observing foreground programs
- focus, debugging while observing foreground programs
- debugging [Visual Studio], foreground programs
ms.assetid: 9e67a308-1c81-42ab-966b-7fc3c1d2bf7a
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 420a4073e4c00f66775bf55565c2ee8645d90f49
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99911377"
---
# <a name="how-can-i-use-debugger-windows-while-debugging-a-foreground-program"></a>フォアグラウンド プログラムのデバッグ中にデバッガー ウィンドウを使用するには
## <a name="problem-description"></a>問題の説明
 画面の描画時に発生する問題がデバッグの対象です。 この問題を観察するには、プログラムをフォアグラウンドで実行する必要がありますが、そうするとデバッガー ウィンドウにアクセスできなくなります。 どうしたらいいのでしょうか。

## <a name="solution"></a>ソリューション
 コンピューターがもう 1 台ある場合は、リモート デバッグを行います。 2 台のコンピューターをセットアップすると、リモート コンピューター上で画面の描画状態を観察しながら、ホスト上でデバッガーを実行できます。 リモート デバッグの詳細については、「[リモート デバッグ](../debugger/remote-debugging.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [ネイティブ コードのデバッグに関する FAQ](../debugger/debugging-native-code-faqs.md)
- [ネイティブ コードのデバッグ](../debugger/debugging-native-code.md)