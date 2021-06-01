---
title: 起動後のアタッチ | Microsoft Docs
description: プログラムが起動したとき、デバッグ セッションはデバッグ エンジンをプログラムにアタッチする準備ができています。 デバッグ エンジンとの通信のために設計方法を選択します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debug engines, attaching to programs
ms.assetid: 5a3600a1-dc20-4e55-b2a4-809736a6ae65
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 9010d2619b76c2932ca1a8a5aed8db6c6a5cf075
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105055324"
---
# <a name="attach-after-a-launch"></a>起動後にアタッチする
プログラムが起動すると、デバッグ セッションはデバッグ エンジン (DE) をそのプログラムにアタッチする準備ができています。

## <a name="design-decisions"></a>設計上の決定
 通信は共有アドレス空間の方が行いやすいため、2 つの設計方法から選択する必要があります。つまり、デバッグ セッションと DE の間の通信を設定します。 あるいは、DE とプログラムの間の通信を設定します。 以下のいずれかを選択します。

- デバッグ セッションと DE との間の通信を設定する方が合理的な場合は、デバッグ セッションによって DE が共同作成され、DE がプログラムにアタッチするように求められます。 この設計では、デバッグ セッションと DE が一緒に 1 つのアドレス空間を使用し、実行時環境とプログラムが一緒にもう 1 つを使用します。

- DE とプログラムの間の通信を設定する方が合理的な場合は、実行時環境によって DE が共同作成されます。 この設計では、SDM が 1 つのアドレス空間を使用し、DE、実行時環境およびプログラムが一緒にもう 1 つを使用します。 この設計は、インタープリターで実装される DE がスクリプト化された言語を実行する際に一般的です。

    > [!NOTE]
    > DE がプログラムにアタッチする方法は、実装によって異なります。 また、DE とプログラムの間の通信も実装によって異なります。

## <a name="implementation"></a>実装
 プログラムでは、セッション デバッグ マネージャー (SDM) が、起動するプログラムを表す [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md) オブジェクトを最初に受け取ると、[Attach](../../extensibility/debugger/reference/idebugprogram2-attach.md) メソッドを呼び出して、[IDebugEventCallback2](../../extensibility/debugger/reference/idebugeventcallback2.md) オブジェクトを渡します。これは後からデバッグ イベントを SDM に渡すために使用されます。 次に、`IDebugProgram2::Attach` メソッドが [OnAttach](../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md) メソッドを呼び出します。 SDM が `IDebugProgram2` インターフェイスを受け取る方法の詳細については、「[ポートへの通知](../../extensibility/debugger/notifying-the-port.md)」を参照してください。

 デバッグ中のプログラムと同じアドレス空間で DE を実行する必要がある場合: 通常 DE はスクリプトを実行しているインタープリターの一部であるため、`IDebugProgramNodeAttach2::OnAttach` メソッドによって `S_FALSE` が返されます。 `S_FALSE` 戻り値は、アタッチ プロセスが完了したことを示します。

 ただし、DE が SDM のアドレス空間で実行されている場合: `IDebugProgramNodeAttach2::OnAttach` メソッドによって `S_OK` が返されます。そうでない場合、[IDebugProgramNodeAttach2](../../extensibility/debugger/reference/idebugprogramnodeattach2.md) インターフェイスが、デバッグしているプログラムに関連付けられた [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md) オブジェクトにまったく実装されていません。 このケースでは、[Attach](../../extensibility/debugger/reference/idebugengine2-attach.md) メソッドがやがて呼び出されて、アタッチ操作が完了します。

 後のケースでは、[GetProgramId](../../extensibility/debugger/reference/idebugprogram2-getprogramid.md) メソッドを `IDebugEngine2::Attach` メソッドに渡された `IDebugProgram2` オブジェクトに対して呼び出し、`GUID` をローカル プログラム オブジェクトに格納し、`IDebugProgram2::GetProgramId` メソッドがこのオブジェクトに対して後から呼び出されたときに、この `GUID` を返す必要があります。 `GUID` は、さまざまなデバッグ コンポーネントに対してプログラムを一意に識別するために使用されます。

 `IDebugProgramNodeAttach2::OnAttach` メソッドによって `S_FALSE` が返されるケースでは、プログラムで使用される `GUID` がそのメソッドに渡されます。また、ローカル プログラム オブジェクトに `GUID` を設定するのは `IDebugProgramNodeAttach2::OnAttach` メソッドです。

 これで、DE がプログラムにアタッチされ、スタートアップ イベントを送信する準備が整いました。

## <a name="see-also"></a>こちらもご覧ください
- [プログラムへ直接アタッチする](../../extensibility/debugger/attaching-directly-to-a-program.md)
- [ポートへの通知](../../extensibility/debugger/notifying-the-port.md)
- [タスクのデバッグ](../../extensibility/debugger/debugging-tasks.md)
- [IDebugEventCallback2](../../extensibility/debugger/reference/idebugeventcallback2.md)
- [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md)
- [[アタッチ]](../../extensibility/debugger/reference/idebugprogram2-attach.md)
- [GetProgramId](../../extensibility/debugger/reference/idebugprogram2-getprogramid.md)
- [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)
- [IDebugProgramNodeAttach2](../../extensibility/debugger/reference/idebugprogramnodeattach2.md)
- [OnAttach](../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md)
- [[アタッチ]](../../extensibility/debugger/reference/idebugengine2-attach.md)
