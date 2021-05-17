---
title: ポート サプライヤーの実装 | Microsoft Docs
description: ポート サプライヤーの実装について説明します。これは、DCOM 以外のマシンにデバッグする場合、または新しいデバイスでサポートが必要な場合に必要になります。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], implementing port suppliers
- port suppliers, implementing
ms.assetid: 6b8579df-58df-4c7f-8112-6015993e8765
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 98cc83ac9640241f0f97dc6e4adaacf8f90599b7
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105059913"
---
# <a name="implement-a-port-supplier"></a>ポート サプライヤーを実装する
ポート サプライヤーから、セッション デバッグ マネージャー (SDM) への要求時にポートが提供されます。 DCOM 以外のマシンにデバッグする場合、または新しいデバイスでサポートが必要な場合は、ポート サプライヤーを実装する必要があります。 たとえば、携帯電話にデバッグを提供するには、携帯電話に接続するポート (通常は IR またはセル接続) に接続し、電話で実行されているプロセスとプログラムを列挙するポート サプライヤーを設定する場合があります。

 Windows ベースのマシンでのデバッグ プログラム (リモート デバッグを含む) の場合、Visual Studio ではネイティブおよび共通言語ランタイム (CLR) のプロセス用にポート サプライヤーが提供されるため、独自のポート サプライヤーを設定する必要はありません。

## <a name="in-this-section"></a>このセクションの内容
 [ポート サプライヤーを実装して登録する](../../extensibility/debugger/implementing-and-registering-a-port-supplier.md)では、SDM とポート サプライヤーおよびそのポートとのやりとりについて説明します。

 [必要なポート サプライヤー インターフェイス](../../extensibility/debugger/required-port-supplier-interfaces.md)では、ポート サプライヤーを取得するために実装する必要があるインターフェイスについて説明します。

## <a name="related-sections"></a>関連項目
 [デバッガーの概念](../../extensibility/debugger/debugger-concepts.md) 主要なデバッグ アーキテクチャの概念について説明します。

## <a name="see-also"></a>関連項目
 [Visual Studio デバッガーの機能拡張](../../extensibility/debugger/visual-studio-debugger-extensibility.md)
