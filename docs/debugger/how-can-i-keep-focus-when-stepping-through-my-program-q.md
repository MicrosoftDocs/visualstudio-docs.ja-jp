---
title: アプリのステップ実行時にフォーカスを保持する |Microsoft Docs
ms.custom: seodec18
ms.date: 11/04/2016
ms.topic: conceptual
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
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 48c4bd882dd1704099b24f07f744a1615cf7d412
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72734177"
---
# <a name="how-can-i-keep-focus-when-stepping-through-my-app"></a>アプリのステップ実行時にフォーカスを保持するにはどうすればよいですか。
## <a name="description"></a>説明
 プログラムで、ウィンドウのアクティブ化が正しく動作しません。 デバッガーでプログラムをステップ実行すると、プログラムがフォーカスを保持できないため、問題を再現できなくなります。 どのようにすればフォーカスを保持できますか。

## <a name="solution"></a>解決策:
 コンピューターがもう 1 台ある場合は、リモート デバッグを行います。 リモート コンピューター上でプログラムを操作し、ホスト上でデバッガーを実行します。 詳細については、「[方法: リモートコンピューターを選択](/previous-versions/visualstudio/visual-studio-2010/w8wtw2f3(v=vs.100))する」を参照してください。

## <a name="see-also"></a>関連項目
- [ネイティブ コードのデバッグに関する FAQ](../debugger/debugging-native-code-faqs.md)
- [実行中のプロセスへのアタッチ](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)
- [ネイティブ コードのデバッグ](../debugger/debugging-native-code.md)