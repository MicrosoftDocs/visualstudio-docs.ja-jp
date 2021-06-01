---
title: プログラムへのアタッチ | Microsoft Docs
description: プログラムが適切なポートに登録された後に、プログラムにアタッチするデバッガーを Visual Studio によって実装する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- debug engines, attaching to programs
ms.assetid: 9a3f5b83-60b5-4ef0-91fe-a432105bd066
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d880edbea79f56cbd2c90905b0bc2f712dba59b1
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105055272"
---
# <a name="attach-to-the-program"></a>プログラムにアタッチする
プログラムを適切なポートに登録した後で、デバッグ対象のプログラムにデバッガーをアタッチする必要があります。

## <a name="choose-how-to-attach"></a>アタッチ方法を選択する
 セッション デバッグ マネージャー (SDM) がデバッグ対象のプログラムへのアタッチを試行する方法は 3 つあります。

1. [LaunchSuspended](../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md) メソッドを使用してデバッグ エンジンによって起動されるプログラムの場合 (典型的なインタープリター言語など)、SDM は、アタッチ対象のプログラムに関連付けられている [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md) オブジェクトから [IDebugProgramNodeAttach2](../../extensibility/debugger/reference/idebugprogramnodeattach2.md) インターフェイスを取得します。 SDM が `IDebugProgramNodeAttach2` インターフェイスを取得できる場合、SDM は次に [OnAttach](../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md) メソッドを呼び出します。 `IDebugProgramNodeAttach2::OnAttach` メソッドは `S_OK` を返して、プログラムにアタッチしなかったことと、プログラムにアタッチするために他の方法を試行できることを示します。

2. SDM がアタッチ対象のプログラムから [IDebugProgramEx2](../../extensibility/debugger/reference/idebugprogramex2.md) インターフェイスを取得できる場合、SDM は [Attach](../../extensibility/debugger/reference/idebugprogramex2-attach.md) メソッドを呼び出します。 この方法は、ポート サプライヤーによってリモートで起動されたプログラムの場合に一般的です。

3. `IDebugProgramNodeAttach2::OnAttach` または `IDebugProgramEx2::Attach` メソッドを使用してプログラムにアタッチできない場合、SDM は `CoCreateInstance` 関数を呼び出してデバッグ エンジンを読み込み (まだ読み込まれていない場合)、その後、[Attach](../../extensibility/debugger/reference/idebugengine2-attach.md) メソッドを呼び出します。 この方法は、ポート サプライヤーによってローカルに起動されたプログラムの場合に一般的です。

    また、カスタム ポート サプライヤーが、カスタム ポート サプライヤーの `IDebugProgramEx2::Attach` メソッドの実装において、`IDebugEngine2::Attach` メソッドを呼び出すこともできます。 このケースでは通常、カスタム ポート サプライヤーは、リモート マシン上でデバッグ エンジンを起動します。

   アタッチが実行されるのは、セッション デバッグ マネージャー (SDM) が [Attach](../../extensibility/debugger/reference/idebugengine2-attach.md) メソッドを呼び出すときです。

   デバッグ対象のアプリケーションと同じプロセスで DE を実行する場合は、[IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md) の次のメソッドを実装する必要があります。

- [GetHostName](../../extensibility/debugger/reference/idebugprogramnode2-gethostname.md)

- [GetHostPid](../../extensibility/debugger/reference/idebugprogramnode2-gethostpid.md)

- [GetProgramName](../../extensibility/debugger/reference/idebugprogramnode2-getprogramname.md)

  `IDebugEngine2::Attach` メソッドが呼び出されたら、`IDebugEngine2::Attach` メソッドの実装で次の手順を実行します。

1. [IDebugEngineCreateEvent2](../../extensibility/debugger/reference/idebugenginecreateevent2.md) イベント オブジェクトを SDM に送信します。 詳細については、「[イベントの送信](../../extensibility/debugger/sending-events.md)」を参照してください。

2. `IDebugEngine2::Attach` メソッドに渡された [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md) オブジェクトに対して、[GetProgramId](../../extensibility/debugger/reference/idebugprogram2-getprogramid.md) メソッドを呼び出します。

     これによって、プログラムの識別に使用される `GUID` が返されます。 `GUID` は、DE に対してローカル プログラムを表すオブジェクトに格納される必要があります。また、`IDebugProgram2::GetProgramId` メソッドが `IDebugProgram2` インターフェイスで呼び出されたときに返される必要があります。

    > [!NOTE]
    > `IDebugProgramNodeAttach2` インターフェイスを実装すると、プログラムの `GUID` が `IDebugProgramNodeAttach2::OnAttach` メソッドに渡されます。 この `GUID` は、`IDebugProgram2::GetProgramId` メソッドから返されるプログラムの `GUID` で使用されます。

3. [IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md) イベント オブジェクトを送信して、DE に対してプログラムを表すローカルの `IDebugProgram2`オブジェクトが作成されたことを SDM に通知します。 詳細については、「[イベントの送信](../../extensibility/debugger/sending-events.md)」を参照してください。

    > [!NOTE]
    > これは、`IDebugEngine2::Attach` メソッドに渡されたのと同じ `IDebugProgram2` オブジェクトではありません。 以前渡された `IDebugProgram2` オブジェクトはポートでのみ認識される別のオブジェクトです。

## <a name="see-also"></a>こちらもご覧ください
- [起動ベースのアタッチ](../../extensibility/debugger/launch-based-attachment.md)
- [イベントの送信](../../extensibility/debugger/sending-events.md)
- [LaunchSuspended](../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)
- [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md)
- [IDebugProgramNodeAttach2](../../extensibility/debugger/reference/idebugprogramnodeattach2.md)
- [OnAttach](../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md)
- [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)
- [GetProgramId](../../extensibility/debugger/reference/idebugprogram2-getprogramid.md)
- [IDebugProgramEx2](../../extensibility/debugger/reference/idebugprogramex2.md)
- [[アタッチ]](../../extensibility/debugger/reference/idebugprogramex2-attach.md)
- [[アタッチ]](../../extensibility/debugger/reference/idebugengine2-attach.md)
