---
title: '方法: マネージド コードの複数のスレッドの管理 | Microsoft Docs'
description: マネージド VSPackage 拡張機能で非同期メソッドを呼び出す場合、または Visual Studio UI スレッドから操作を実行する場合に、コードで複数のスレッドを管理する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 59730063-cc29-4dae-baff-2234ad8d0c8f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 7b301770a54baf0416aa9fcc838a9a6633252fbe
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105073132"
---
# <a name="how-to-manage-multiple-threads-in-managed-code"></a>方法: マネージド コードの複数のスレッドを管理する
非同期メソッドを呼び出すか、Visual Studio UI スレッド以外のスレッドで実行される操作を持つマネージド VSPackage 拡張機能がある場合、次のガイドラインに従う必要があります。 別のスレッドでの作業が完了するまで待機する必要がないため、UI スレッドの応答性を維持できます。 スタック領域を占有する余分なスレッドがないため、コードの効率を向上させることができます。また、デッドロックや応答のないコードを避けることができるため、より信頼性が高く、デバッグが容易になります。

 一般に、UI スレッドから別のスレッドに切り替えることも、その逆の切り替えを行うこともできます。 メソッドから制御が戻ると、現在のスレッドは、最初に呼び出されたスレッドになります。

> [!IMPORTANT]
> 次のガイドラインでは、<xref:Microsoft.VisualStudio.Threading> 名前空間の API (特に <xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory> クラス) を使用します。 この名前空間に含まれる API は、[!INCLUDE[vs_dev12](../extensibility/includes/vs_dev12_md.md)] の新機能です。 <xref:Microsoft.VisualStudio.Shell.ThreadHelper> プロパティ `ThreadHelper.JoinableTaskFactory` から <xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory> を取得できます。

## <a name="switch-from-the-ui-thread-to-a-background-thread"></a>UI スレッドからバックグラウンド スレッドに切り替える

1. UI スレッドを使用していて、バックグラウンド スレッドで非同期作業を行う場合は、`Task.Run()` を使用します。

    ```csharp
    await Task.Run(async delegate{
        // Now you're on a separate thread.
    });
    // Now you're back on the UI thread.

    ```

2. UI スレッドを使用していて、バックグラウンド スレッドで作業を実行している間に同期的にブロックする場合は、<xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory.Run%2A> 内の <xref:System.Threading.Tasks.TaskScheduler> プロパティ `TaskScheduler.Default` を使用します。

    ```csharp
    // using Microsoft.VisualStudio.Threading;
    ThreadHelper.JoinableTaskFactory.Run(async delegate {
        await TaskScheduler.Default;
        // You're now on a separate thread.
        DoSomethingSynchronous();
        await OrSomethingAsynchronous();
    });
    ```

## <a name="switch-from-a-background-thread-to-the-ui-thread"></a>バックグラウンド スレッドから UI スレッドに切り替える

1. バックグラウンドスレッドを使用していて、UI スレッドで何らかの処理を行う場合は、<xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory.SwitchToMainThreadAsync%2A> を使用します。

    ```csharp
    // Switch to main thread
    await ThreadHelper.JoinableTaskFactory.SwitchToMainThreadAsync();
    ```

     <xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory.SwitchToMainThreadAsync%2A> メソッドを使用して、UI スレッドに切り替えることができます。 このメソッドでは、現在の非同期メソッドの継続を使用して UI スレッドにメッセージをポストします。また、スレッド フレームワークの残りの部分と通信して、正しい優先順位を設定し、デッドロックを回避します。

     バックグラウンド スレッド メソッドが非同期ではなく、非同期にすることができない場合でも、次の例のように、<xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory.Run%2A> を使用して作業をラップすることで、`await` 構文を使用して UI スレッドに切り替えることができます。

    ```csharp
    ThreadHelper.JoinableTaskFactory.Run(async delegate {
        // Switch to main thread
        await ThreadHelper.JoinableTaskFactory.SwitchToMainThreadAsync();
        // Do your work on the main thread here.
    });
    ```
