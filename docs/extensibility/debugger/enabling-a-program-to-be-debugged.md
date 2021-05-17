---
title: プログラムのデバッグを有効にする | Microsoft Docs
description: デバッグ エンジンを起動したり、デバッグ エンジンを既存のプログラムにアタッチしてプログラムをデバッグしたりする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], enabling for programs
ms.assetid: 61d24820-0cd9-48b6-8674-6813f7493237
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 4ed7ce97e6ff7e8801953877ed80afa7ca262f20
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105097228"
---
# <a name="enable-a-program-to-be-debugged"></a>デバッグするプログラムを有効にする
デバッグ エンジン (DE) によってプログラムをデバッグできるようにするには、まず、DE を起動するか、それを既存のプログラムにアタッチする必要があります。

## <a name="in-this-section"></a>このセクションの内容
 [ポートを取得する](../../extensibility/debugger/getting-a-port.md) プログラムのデバッグを有効にするための最初の手順として、ポートを取得する方法について説明します。

 [プログラムを登録する](../../extensibility/debugger/registering-the-program.md) プログラムのデバッグを有効にする次の手順 (それをポートに登録する) について説明します。 プログラムは、登録すると、アタッチまたは Just-In-Time (JIT) デバッグのプロセスによってデバッグできます。

 [プログラムにアタッチする](../../extensibility/debugger/attaching-to-the-program.md) プログラムにデバッガーをアタッチする次の手順について説明します。

 [起動ベースのアタッチ](../../extensibility/debugger/launch-based-attachment.md) プログラムへの起動ベースのアタッチについて説明します。これは、SDM によって起動されたときに自動的に行われます。

 [必要なイベントを送信する](../../extensibility/debugger/sending-the-required-events.md) デバッグエンジン (DE) を作成し、それをプログラムにアタッチするときに必要なイベントの手順を説明します。

## <a name="related-sections"></a>関連項目
 [カスタム デバッグ エンジンの作成](../../extensibility/debugger/creating-a-custom-debug-engine.md) デバッグ エンジン (DE) を定義し、DE インターフェイスによって実装されるサービスと、それらによって、デバッガーにさまざまな動作モード間を切り替えさせる方法について説明します。
