---
title: ファイルの追跡 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- msbuild, file tracking
ms.assetid: e6c66ac0-3464-451f-9192-3b98dca21b4a
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 7770da734143b2b6185b266137eeb46ba25bd32a
ms.sourcegitcommit: d0425b6b7d4b99e17ca6ac0671282bc718f80910
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/21/2019
ms.locfileid: "56640611"
---
# <a name="file-tracking"></a>ファイルの追跡
ファイルの追跡では、特定のプロセスとその子プロセスについて、Windows ファイル システムの呼び出しをログに記録します。 下記の関数を呼び出すことで、このログ記録のオンとオフを切り替えるタイミングを制御したり、使用するログ ファイルを指定したりできます。

- [EndTrackingContext](../msbuild/endtrackingcontext.md) 現在のコンテキストの追跡を停止します。

- [ResumeTracking](../msbuild/resumetracking.md) [SuspendTracking](../msbuild/suspendtracking.md) の呼び出し後に追跡を再開します。

- [SetThreadCount](../msbuild/setthreadcount.md) 追跡に使用するスレッドの数を設定します。

- [StartTrackingContext](../msbuild/starttrackingcontext.md) 新しい追跡コンテキストを開始します。

- [StartTrackingContextWithRoot](../msbuild/starttrackingcontextwithroot.md) 指定されたルートで新しい追跡コンテキストを開始します。

- [StopTrackingAndCleanup](../msbuild/stoptrackingandcleanup.md) 追跡を終了し、使用されているリソースを解放します。

- [SuspendTracking](../msbuild/suspendtracking.md) 追跡を一時的に中断します。

- [WriteAllTLogs](../msbuild/writealltlogs.md) すべてのコンテキストに対する追跡ログを書き出します。

- [WriteContextTLogs](../msbuild/writecontexttlogs.md) 現在のコンテキストに対する追跡ログを書き出します。