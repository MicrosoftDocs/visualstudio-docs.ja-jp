---
title: プロセス | Microsoft Docs
description: この記事では、Visual Studio のデバッガー アーキテクチャにおけるプロセスの定義と役割について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], processes
ms.assetid: a6a1efdc-b243-40c8-a778-6f69f6b018be
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 46e25ddfbe60e1b9ee456e586c6f424fc489f626
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105067713"
---
# <a name="processes"></a>プロセス
デバッガー アーキテクチャでは、"*プロセス*" は次のようなものです。

- プログラム セットのコンテナーです。 スレッド セットのコンテナーである Windows プロセスによく似ています。

- 名前、識別子、または物理識別子を使用して識別できます。

- 実行中のすべてのプログラム (とそのスレッド) を列挙できます。

- それ自体、それが実行されているポート、それが搭載されているマシンを記述できます。

- 1 つ以上のプログラムの作成、作成したプログラムの終了、またはプログラムの停止を行うことができます。

- [IDebugProcess2](../../extensibility/debugger/reference/idebugprocess2.md) インターフェイスで表されます。これはプロセスの起動時に作成されます。 プロセスは、セッション デバッグ マネージャー (SDM) または [LaunchSuspended](../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md) のいずれかによって起動されます。

  デバッグ パッケージから[アタッチ](../../extensibility/debugger/reference/idebugprocess2-attach.md)を呼び出すことにより、デバッグ エンジン (DE) をプロセスにアタッチすることができます。これは、処理可能なプロセスで実行されているすべてのプログラムに DE をアタッチすることを意味します。 たとえば、共通言語ランタイム DE がプロセスにアタッチされる場合、マネージド コードを実行しているプログラムにのみアタッチされます。

## <a name="see-also"></a>こちらもご覧ください
- [Programs](../../extensibility/debugger/programs.md)
- [スレッド](../../extensibility/debugger/threads.md)
- [デバッガーの概念](../../extensibility/debugger/debugger-concepts.md)
- [デバッグ パッケージ](../../extensibility/debugger/debug-package.md)
- [デバッグ エンジン](../../extensibility/debugger/debug-engine.md)
- [IDebugProcess2](../../extensibility/debugger/reference/idebugprocess2.md)
- [LaunchSuspended](../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)
- [[アタッチ]](../../extensibility/debugger/reference/idebugprocess2-attach.md)
