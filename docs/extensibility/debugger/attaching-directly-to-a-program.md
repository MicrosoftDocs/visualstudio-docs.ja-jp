---
title: プログラムに直接アタッチする | Microsoft Docs
description: Visual Studio IDE でこの手順を使用して、既に実行されているプロセスへのデバッグ エンジンのアタッチを実装する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- debug engines, attaching to programs
ms.assetid: ad2b7db8-821c-440c-ba07-c55c6a395e0f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 2f261d6492943ab0b0da878097685ae2773ddff4
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105055298"
---
# <a name="attach-directly-to-a-program"></a>プログラムに直接アタッチする
既に実行中のプロセスでプログラムをデバッグするユーザーは、通常、次のプロセスに従います。

1. IDE で、 **[ツール]** メニューの **[プロセスのデバッグ]** を選択します。

    **[プロセス]** ダイアログ ボックスが表示されます。

2. プロセスを選択し、 **[アタッチ]** ボタンをクリックします。

    **[プロセスにアタッチ]** ダイアログ ボックスが表示され、コンピューターにインストールされているすべてのデバッグ エンジン (DE) が一覧表示されます。

3. 選択したプロセスのデバッグに使用する DE を指定してから、 **[OK]** をクリックします。

   デバッグ パッケージによってデバッグ セッションが開始され、DE のリストが渡されます。 次に、デバッグ セッションによって、このリストがコールバック関数と共に選択されたプロセスに渡された後、実行中のプログラムを列挙するようにプロセスに指示されます。

   プログラムでは、ユーザーの要求に応答して、デバッグ パッケージでセッション デバッグ マネージャー (SDM) をインスタンス化し、選択した DE のリストを渡します。 リストと共に、デバッグ パッケージから SDM に [IDebugEventCallback2](../../extensibility/debugger/reference/idebugeventcallback2.md) インターフェイスを渡します。 デバッグ パッケージで [IDebugProcess2::Attach](../../extensibility/debugger/reference/idebugprocess2-attach.md) を呼び出し、選択されたプロセスに DE のリストを渡します。 その後、SDM でポートの [IDebugProcess2::EnumPrograms](../../extensibility/debugger/reference/idebugprocess2-enumprograms.md) を呼び出し、プロセスで実行されているプログラムを列挙します。

   この時点から、「[起動後にアタッチする](../../extensibility/debugger/attaching-after-a-launch.md)」で説明されているとおりに、各デバッグ エンジンがプログラムにアタッチされますが、2 つの例外があります。

   効率を高めるため、SDM とアドレス空間を共有するように実装された DE は、各 DE でアタッチ先の一連のプログラムを使用できるようにグループ化されます。 この場合は、[IDebugProcess2](../../extensibility/debugger/reference/idebugprocess2.md) で [IDebugEngine2::Attach](../../extensibility/debugger/reference/idebugengine2-attach.md) を呼び出し、アタッチ先のプログラムの配列を渡します。

   2 つ目の例外として、既に実行されているプログラムにアタッチしている DE によって送信されたスタートアップ イベントには、通常、エントリ ポイント イベントが含まれていません。

## <a name="see-also"></a>関連項目
- [起動後にスタートアップ イベントを送信する](../../extensibility/debugger/sending-startup-events-after-a-launch.md)
- [タスクのデバッグ](../../extensibility/debugger/debugging-tasks.md)
