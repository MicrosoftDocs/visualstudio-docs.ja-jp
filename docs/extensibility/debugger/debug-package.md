---
title: デバッグ パッケージ | Microsoft Docs
description: デバッグ インターフェイスを使用してセッション デバッグ マネージャーと通信することによって、デバッグ パッケージが Visual Studio シェルで動作して UI を処理するしくみについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], packages
ms.assetid: 99947fd4-fb87-4c69-b26c-65634e17d285
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 90c4c82895f7a30d4df9126a280c6c9ffa7ffa76
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105067908"
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
