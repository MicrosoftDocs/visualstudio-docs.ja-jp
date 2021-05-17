---
title: プログラムの起動 |Microsoft Docs
description: IDE からデバッガーを実行するために、F5 キーを使用してプログラムをデバッグするときに実行される、一連のイベントについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debug engines, launching
- programs, launching
ms.assetid: 6857e9c6-e44a-468a-afa4-f7c4a0b77844
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: a21036d3a9661306d1efff5a66ae47f8f7404209
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105094719"
---
# <a name="launch-a-program"></a>プログラムを起動する
プログラムをデバッグするユーザーは、**F5** キーを押して、IDE からデバッガーを実行することができます。 これにより、最終的に IDE がデバッグ エンジン (DE) に接続され、その後で次のようにプログラムに接続 (アタッチ) されるという、一連のイベントが開始されます。

1. IDE は、最初にプロジェクト パッケージを呼び出して、ソリューションのアクティブなプロジェクトのデバッグ設定を取得します。 この設定には、開始ディレクトリ、環境変数、プログラムが実行されるポート、およびプログラムの作成に使用する DE (指定されている場合) が含まれます。 これらの設定は、デバッグ パッケージに渡されます。

2. DE が指定されている場合、DE はオペレーティング システムを呼び出してプログラムを起動します。 プログラムを起動した結果として、プログラムのランタイム環境が読み込まれます。 たとえば、プログラムが MSIL で記述されている場合、プログラムを実行するために共通言語ランタイムが呼び出されます。

    または

    DE が指定されていない場合は、ポートがオペレーティング システムを呼び出してプログラムを起動し、これによりプログラムのランタイム環境が読み込まれます。

   > [!NOTE]
   > DE を使用してプログラムを起動する場合は、同じ DE がプログラムにアタッチされる可能性があります。

3. DE またはポートのどちらがプログラムを起動したかに応じて、DE またはランタイム環境によってプログラムの説明 (ノード) が作成され、プログラムが実行されていることがポートに通知されます。

   > [!NOTE]
   > プログラム ノードはデバッグ可能なプログラムの簡易表現であるため、ランタイム環境でプログラム ノードを作成することをお勧めします。 プログラム ノードを作成および登録するためだけに、DE 全体を読み込む必要はありません。 DE が IDE のプロセスで実行されるように設計されていても、実際には IDE が実行されていない場合は、プログラム ノードをポートに追加できるコンポーネントが必要です。

   新しく作成されたプログラムは、同じ IDE から起動またはアタッチされた、関連する、または関連しない他のプログラムと共に、デバッグ セッションを作成します。

   プログラムによって、ユーザーが最初に **F5** キーを押したときに、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] のデバッグ パッケージが <xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg.DebugLaunch%2A> メソッドを介してプロジェクト パッケージ (起動中のプログラムの種類に関連付けられているもの) を呼び出します。その後、ソリューションのアクティブなプロジェクト デバッグ設定を含む <xref:Microsoft.VisualStudio.Shell.Interop.VsDebugTargetInfo2> 構造体を入力します。 この構造体は、<xref:Microsoft.VisualStudio.Shell.Interop.IVsDebugger2.LaunchDebugTargets2%2A> メソッドの呼び出しによってデバッグ パッケージに戻されます。 その後、デバッグ パッケージは、セッション デバッグ マネージャー (SDM) をインスタンス化します。これにより、デバッグ中のプログラムと、関連付けられているデバッグ エンジンが起動します。

   SDM に渡される引数の 1 つに、プログラムを起動するために使用される DE の GUID があります。

   DE の GUID が `GUID_NULL` でない場合、SDM は DE を共同作成してから、その [LaunchSuspended](../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md) メソッドを呼び出してプログラムを起動します。 たとえば、プログラムがネイティブ コードで記述されている場合、`IDebugEngineLaunch2::LaunchSuspended` はプログラムを実行するために `CreateProcess` と `ResumeThread` (Win32 関数) を呼び出す場合があります。

   プログラムを起動した結果として、プログラムのランタイム環境が読み込まれます。 その後、DE またはランタイム環境は、プログラムを記述するために [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md) インターフェイスを作成し、このインターフェイスを [AddProgramNode](../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md) に渡して、プログラムが実行されていることをポートに通知します。

   `GUID_NULL` が渡されると、ポートはプログラムを起動します。 プログラムが実行されると、ランタイム環境により、プログラムを記述して `IDebugPortNotify2::AddProgramNode` に渡す `IDebugProgramNode2` インターフェイスが作成されます。 これにより、プログラムが実行されていることがポートに通知されます。 その後、SDM は、実行中のプログラムにデバッグ エンジンをアタッチします。

## <a name="in-this-section"></a>このセクションの内容
 [ポートへの通知](../../extensibility/debugger/notifying-the-port.md) プログラムが起動し、ポートに通知された後の動作について説明します。

 [起動後のアタッチ](../../extensibility/debugger/attaching-after-a-launch.md) デバッグ セッションがいつプログラムに DE をアタッチする準備ができるかについて説明します。

## <a name="related-sections"></a>関連項目
 [デバッグ タスク](../../extensibility/debugger/debugging-tasks.md) プログラムの起動や式の評価などの、さまざまなデバッグ タスクへのリンクが含まれています。
