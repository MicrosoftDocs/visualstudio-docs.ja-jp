---
title: 終了とデタッチ | Microsoft Docs
description: 通常の終了とは、デバッグ対象のプログラムが、ブレークポイント、例外、ランタイム エラー、または無限ループが発生することなく、最後まで実行されることです。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- programs, termination events
- debug engines, detaching from programs
ms.assetid: 268c1e51-6363-45d1-964c-1ab99bdfa4f9
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8662809b50dbfec3046af1d0d6b6fa151c3a33e0
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105057833"
---
# <a name="termination-and-detaching"></a>終了とデタッチ
次のセクションでは、通常の終了について説明します。

## <a name="discussion"></a>ディスカッション
 [IDebugLoadCompleteEvent2](../../extensibility/debugger/reference/idebugloadcompleteevent2.md) または [IDebugEntryPointEvent2](../../extensibility/debugger/reference/idebugentrypointevent2.md) インターフェイスが続行された後、デバッグ対象のアプリケーションにブレークポイント、例外、ランタイム エラー、または無限ループが発生しない場合、デバッグ対象のプログラムは最後まで実行されます。 このプロセスが通常の終了です。

 通常の終了を実装するには、[IDebugProgramDestroyEvent2](../../extensibility/debugger/reference/idebugprogramdestroyevent2.md) を送信する必要があります。 通常の終了のためには、[IDebugProgramDestroyEvent2::GetExitCode](../../extensibility/debugger/reference/idebugprogramdestroyevent2-getexitcode.md) メソッドを実行する必要があります。

## <a name="see-also"></a>関連項目
- [カスタム デバッグ エンジンの作成](../../extensibility/debugger/creating-a-custom-debug-engine.md)
