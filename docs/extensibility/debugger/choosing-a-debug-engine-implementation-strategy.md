---
title: デバッグ エンジンの実装方法の選択 | Microsoft Docs
description: ランタイム アーキテクチャを使用して複数のデバッグ エンジンの実装方法から選択する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debug engines, implementation strategies
ms.assetid: 90458fdd-2d34-4f10-82dc-6d8f31b66d8b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 6126df3e4adb1e0d942669b561801be4449036df
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105055063"
---
# <a name="choose-a-debug-engine-implementation-strategy"></a>デバッグ エンジンの実装方法を選択する
ランタイム アーキテクチャを使用して、デバッグ エンジン (DE) の実装方法を決定します。 デバッグ中のプログラムに対してインプロセスでデバッグ エンジンを作成できます。 Visual Studio のセッション デバッグ マネージャー (SDM) に対してインプロセスでデバッグ エンジンを作成します。 または、その両方に対してアウトプロセスでデバッグ エンジンを作成します。 次のガイドラインは、これら 3 つの方法のいずれかを選択するのに役立ちます。

## <a name="guidelines"></a>ガイドライン
 DE を SDM とデバッグ中のプログラムの両方に対してアウトプロセスにすることはできますが、通常はそうする必要はありません。 プロセス境界を越えた呼び出しは比較的低速です。

 Win32 ネイティブ ランタイム環境用および共通言語ランタイム環境用のデバッグ エンジンは、既に用意されています。 どちらかの環境で DE を置き換える必要がある場合は、SDM でインプロセスで DE を作成する必要があります。

 それ以外の場合は、SDM に対してインプロセスで、またはデバッグ中のプログラムに対してインプロセスで DE を作成します。 DE の式エバリュエーターでプログラム シンボル ストアに頻繁にアクセスする必要があるかどうかを検討する必要があります。 または、高速アクセスのためにシンボル ストアをメモリに読み込むことができます。 次の方法も検討してください。

- 式エバリュエーターとシンボル ストアの間に多数の呼び出しがない場合、またはシンボル ストアを SDM のメモリ空間に読み取ることができる場合は、SDM に対してインプロセスで DE を作成します。 プログラムにアタッチするときは、デバッグ エンジンの CLSID を SDM に返す必要があります。 SDM では、この CLSID を使用して DE のインプロセス インスタンスを作成します。

- DE でシンボル ストアにアクセスするためにプログラムを呼び出す必要がある場合は、プログラムでインプロセスで DE を作成します。 この場合は、プログラムで DE のインスタンスを作成します。

## <a name="see-also"></a>関連項目
- [Visual Studio デバッガーの機能拡張](../../extensibility/debugger/visual-studio-debugger-extensibility.md)
