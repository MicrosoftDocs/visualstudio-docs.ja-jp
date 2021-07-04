---
title: 自分のアプリをステップ実行しているときにフォーカスを保持する | Microsoft Docs
description: リモート デバッグを使用して、ウィンドウのアクティブ化に関する問題をデバッグするときに、プログラムがフォーカスを失わないようにします。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.debug.stepping
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging [C++], stepping
- focus, keeping
- stepping, focus
- windows, troubleshooting activation
ms.assetid: 11a30580-3a1a-4be8-a241-0abdc758302e
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 561e5d4dc009642ee7773cd60d004ef8a64261d6
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112386931"
---
# <a name="how-can-i-keep-focus-when-stepping-through-my-app"></a>自分のアプリをステップ実行しているときにフォーカスを保持するにはどうすればよいですか。
## <a name="description"></a>説明
 プログラムで、ウィンドウのアクティブ化が正しく動作しません。 デバッガーでプログラムをステップ実行すると、プログラムがフォーカスを保持できないため、問題を再現できなくなります。 どのようにすればフォーカスを保持できますか。

## <a name="solution"></a>ソリューション
 コンピューターがもう 1 台ある場合は、リモート デバッグを行います。 リモート コンピューター上でプログラムを操作し、ホスト上でデバッガーを実行します。 詳細については、[リモート コンピューターを選択する](/previous-versions/visualstudio/visual-studio-2010/w8wtw2f3(v=vs.100))」を参照してください。

## <a name="see-also"></a>関連項目
- [ネイティブ コードのデバッグに関する FAQ](../debugger/debugging-native-code-faqs.md)
- [実行中のプロセスへのアタッチ](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)
- [ネイティブ コードのデバッグ](../debugger/debugging-native-code.md)
