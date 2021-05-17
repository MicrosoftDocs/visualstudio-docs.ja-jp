---
title: ポートへの通知 | Microsoft Docs
description: プログラムを起動した後でポートに通知する方法について説明します。 この記事には、詳しい説明が含まれています。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- ports, notification
ms.assetid: f9fce48e-7d4e-4627-a0fb-77b75428146a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 7793dddb1a6bdd448b2b5a912f59b625bdca733e
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105054752"
---
# <a name="notify-the-port"></a>ポートに通知する
プログラムを起動した後、次のようにポートに通知する必要があります。

1. ポートでは、新しいプログラム ノードを受け取ったときに、デバッグ セッションにプログラム作成イベントを送り返します。 このイベントには、プログラムを表すインターフェイスが含まれています。

2. デバッグ セッションでは、アタッチできるデバッグ エンジン (DE) の識別子をプログラムに対して照会します。

3. デバッグ セッションでは、そのプログラムで使用可能な DE のリストにその DE があるかどうかを確認します。 デバッグ セッションでは、最初にデバッグ パッケージによって渡されたソリューションのアクティブなプログラム設定から、このリストを取得します。

    この使用可能リストに DE が存在する必要があります。そうでない場合、DE はプログラムにアタッチされません。

   プログラムを使用して、ポートで最初に新しいプログラム ノードを受け取ると、そのプログラムを表す [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md) インターフェイスが作成されます。

> [!NOTE]
> これを、後でデバッグ エンジン (DE) によって作成される `IDebugProgram2` インターフェイスと混同しないようにしてください。

 ポートでは、COM の `IConnectionPoint` インターフェイスを介して [IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md) プログラム作成イベントをセッション デバッグ マネージャー (SDM) に送り返します。

> [!NOTE]
> これを、後で DE によって送信される `IDebugProgramCreateEvent2` インターフェイスと混同しないようにしてください。

 ポートでは、イベント インターフェイス自体と共に、[IDebugPort2](../../extensibility/debugger/reference/idebugport2.md)、[IDebugProcess2](../../extensibility/debugger/reference/idebugprocess2.md)、[IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md) インターフェイスを送信します。これらは、それぞれポート、プロセス、プログラムを表します。 SDM では、[IDebugProgram2:: GetEngineInfo](../../extensibility/debugger/reference/idebugprogram2-getengineinfo.md) を呼び出して、プログラムをデバッグできる DE の GUID を取得します。 この GUID は、最初に [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md) インターフェイスから取得されています。

 SDM では、DE が使用可能な DE のリストにあるかどうかを確認します。 SDM では、最初にデバッグ パッケージによって渡されたソリューションのアクティブなプログラム設定から、このリストを取得します。 この使用可能リストに DE が存在する必要があります。そうでない場合、それはプログラムにアタッチされません。

 DE の ID が判明すると、SDM でプログラムにアタッチする準備が完了します。

## <a name="see-also"></a>関連項目
- [プログラムの起動](../../extensibility/debugger/launching-a-program.md)
- [起動後にアタッチする](../../extensibility/debugger/attaching-after-a-launch.md)
- [タスクのデバッグ](../../extensibility/debugger/debugging-tasks.md)
