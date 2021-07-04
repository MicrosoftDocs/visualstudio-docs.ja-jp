---
title: デバッグ パッケージ | Microsoft Docs
description: デバッグ インターフェイスを使用してセッション デバッグ マネージャーと通信することによって、デバッグ パッケージが Visual Studio シェルで動作して UI を処理するしくみについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- debugging [Debugging SDK], packages
ms.assetid: 99947fd4-fb87-4c69-b26c-65634e17d285
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8be920ae352067a6e77593ca0a922474d68851d9
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112905671"
---
# <a name="debug-package"></a>デバッグ パッケージ
デバッグ パッケージは Visual Studio シェルで動作し、すべての UI を処理します。 Visual Studio のデバッグ インターフェイスを使用し、セッション デバッグ マネージャー (SDM) と通信します。

 SDM を通じて送信された中断イベントによって、デバッガーが実行モードから中断モードに切り替わり、中断が発生したプログラムにフォーカスが変更されます。 デバッグ パッケージでは、イベントによって送信された情報からスタック フレームとスレッドを追跡します。

 デバッグ パッケージには、言語またはランタイム環境の依存関係はありません。 デバッグ パッケージを実装または変更する必要はありません。

 デバッグ パッケージは *vsdebug.dll* によって実装されます。

## <a name="see-also"></a>関連項目
- [セッション デバッグ マネージャー](../../extensibility/debugger/session-debug-manager.md)
- [スタック フレーム](../../extensibility/debugger/stack-frames.md)
- [スレッド](../../extensibility/debugger/threads.md)
- [デバッガー コンポーネント](../../extensibility/debugger/debugger-components.md)
