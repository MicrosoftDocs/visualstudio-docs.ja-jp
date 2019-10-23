---
title: Visual C/C++カスタムビジュアライザーの互換性
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
ms.openlocfilehash: 9fdd44be89fde2fbc26038c8b88fff405876264f
ms.sourcegitcommit: 485ffaedb1ade71490f11cf05962add1718945cc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2019
ms.locfileid: "72430619"
---
# <a name="visual-cc-custom-visualizer-compatibility"></a>Visual C/C++カスタムビジュアライザーの互換性

Visual Studio 2019 以降、にC++は、メモリを集中的に使用するコンポーネントをホストするための外部64ビットプロセスを使用する、強化されたデバッガーが含まれています。 この更新プログラムの一部として、新しいデバッガーとC++互換性を持たせるために、C/式エバリュエーターの特定の拡張機能を更新する必要があります。

現在、従来のC++ c/EE アドインまたは c/C++カスタムビジュアライザーを使用している場合は、 **[ツール]**  >  [**オプション]**  >  **[デバッグ]** の順に移動し、[**読み込みデバッグ] の選択を解除して、この外部プロセスの使用をオフにすることができます。外部プロセスのシンボル (ネイティブのみ)** 。 このオプションの選択を解除すると、IDE (devenv.exe) プロセス内のメモリ使用量が大幅に増加します。 そのため、大規模なプロジェクトをデバッグする場合は、拡張機能の所有者と協力して、このデバッグオプションとの互換性を確保することをお勧めします。

レガシ C/C++ EE アドインまたは c/C++カスタムビジュアライザーの所有者は、concord 拡張機能の[サンプル wiki](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Worker-Process-Remoting)で、ワーカープロセスに拡張機能を読み込む方法についての詳細を参照できます。 [C/C++カスタムビジュアライザーのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/tree/master/CppCustomVisualizer)も参照できます。