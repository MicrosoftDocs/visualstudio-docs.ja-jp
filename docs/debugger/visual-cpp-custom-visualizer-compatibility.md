---
title: Visual C と C++ のカスタム ビジュアライザーの互換性
ms.date: 01/28/2019
ms.prod: visual-studio-dev16
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- debugging assertions
- assertions, debugging
- assertions, assertion failures
- Assertion Failed dialog box
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
monikerRange: '>= vs-2019'
ms.openlocfilehash: 32e38dd3bba8a1127d8756972b73e8b47a514f1b
ms.sourcegitcommit: a83c60bb00bf95e6bea037f0e1b9696c64deda3c
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 02/18/2019
ms.locfileid: "56335182"
---
# <a name="visual-cc-custom-visualizer-compatibility"></a>Visual C と C++ のカスタム ビジュアライザーの互換性

Visual Studio 2019 以降、Visual C には、そのメモリを消費するコンポーネントをホストするための外部の 64 ビット プロセスを使用する、強化されたデバッガーが含まれています。 この更新プログラムの一環として、新しいデバッガーに対応できるようにする Visual C と C++ の式エバリュエーターに特定の拡張機能を更新する必要があります。

移動してこの外部プロセスの使用量をオフにすることができる場合は、従来の C と C++ EE アドインまたは C と C++ のカスタム ビジュアライザーを使用している現在、**ツール** > **オプション** >  **デバッグ**にしてからオフ**ロード デバッグ記号は、外部プロセス (ネイティブのみ) で**します。 このオプションを選択解除した場合は、IDE (devenv.exe) プロセス内でのメモリ使用量が大幅に増加が発生します。 そのため、大規模なプロジェクトをデバッグする場合は、このデバッグ オプションの互換性を確保する、拡張機能の所有者を使用することをお勧めします。

従来の C と C++ EE アドインまたは C と C++ のカスタム ビジュアライザーの所有者の場合でワーカー プロセスの拡張機能の読み込みを選択の詳細についてを見つけることができます、 [Concord 機能拡張サンプル wiki](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Worker-Process-Remoting)します。 検索することも、 [C と C++ のカスタム ビジュアライザー サンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/tree/master/CppCustomVisualizer)します。