---
title: ネイティブ コード内のスレッドをデバッグするためのヒント | Microsoft Docs
description: Visual Studio でマルチスレッド アプリをデバッグする場合は、ネイティブ コードでのスレッドのデバッグに関するヒントの一覧をご覧ください。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- threading [Visual Studio], debugging
- debugging [Visual Studio], threads
ms.assetid: 0374c8c6-57a3-4cfe-8047-2effef5ff5dc
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- cplusplus
ms.openlocfilehash: 85bdd804e25dfa91b649e95daacef4bfb322df64
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99940567"
---
# <a name="tips-for-debugging-threads-in-native-code"></a>ネイティブ コード内のスレッドのデバッグのヒント
ここでは、ネイティブ コード内のスレッドをデバッグするときに役立つヒントを紹介します。

- **[ウォッチ]** ウィンドウまたは **[クイック ウォッチ]** ダイアログ ボックスで「`@TIB`」と入力すると、[スレッド情報ブロック] の内容を表示できます。

- **[ウォッチ]** ウィンドウまたは **[クイック ウォッチ]** ダイアログ ボックスで「`@Err`」と入力すると、現在のスレッドの最終エラー コードを表示できます。

- マルチスレッド アプリケーションのデバッグには、C ランタイム ライブラリ (CRT) 関数を使用できます。 詳細については、「[_malloc_dbg](/cpp/c-runtime-library/reference/malloc-dbg)」をご覧ください。

## <a name="see-also"></a>関連項目
- [マルチスレッド アプリケーションのデバッグ](../debugger/debug-multithreaded-applications-in-visual-studio.md)
- [ネイティブ コードのデバッグ](../debugger/debugging-native-code.md)