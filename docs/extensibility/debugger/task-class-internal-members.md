---
title: Task クラス - 内部メンバー | Microsoft Docs
description: カスタム デバッガーの実装に役立つ System.Threading.Tasks.Task クラスの内部メンバーについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- debug engines, Task class [.NET Framework]
- Task class [.NET Framework debug engines]
ms.assetid: 28e47c3b-9323-424a-80ac-6cc3bf19e09b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 37691714d0168594b61a1a3849f7b65264e9999e
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112902892"
---
# <a name="task-class---internal-members"></a>Task クラス - 内部メンバー
この記事では、カスタム デバッガーの実装に役立つ <xref:System.Threading.Tasks.Task?displayProperty=fullName> クラスの内部メンバーについて説明します。 このクラスに関する一般的な情報については、<xref:System.Threading.Tasks.Task> のリファレンス記事を参照してください。

 **名前空間:** <xref:System.Threading.Tasks?displayProperty=fullName>

 **アセンブリ:** mscorlib (*mscorlib.dll* 内)

 これらの内部メンバーには、.NET Framework からはアクセスできないため、次の構文では共通中間言語 (CIL) を使用しています。

## <a name="syntax"></a>構文

```csharp
.class public auto ansi System.Threading.Tasks.Task
       extends System.Object
       implements System.Threading.IThreadPoolWorkItem,
                  System.IAsyncResult,
                  System.IDisposable,
                  System.Threading.ICancelableOperation
```

## <a name="members"></a>メンバー

### <a name="methods"></a>メソッド

|名前|説明|
|----------|-----------------|
|[SetNotificationForWaitCompletion メソッド](../../extensibility/debugger/setnotificationforwaitcompletion-method.md)|TASK_STATE_WAIT_COMPLETION_NOTIFICATION 状態ビットを設定またはクリアします。|
|[NotifyDebuggerOfWaitCompletion メソッド](../../extensibility/debugger/notifydebuggerofwaitcompletion-method.md)|デバッガーによってブレークポイント ターゲットとして使用されるプレースホルダー メソッド。|

### <a name="fields"></a>フィールド

|名前|説明|
|----------|-----------------|
|[m_action](../../extensibility/debugger/m-action-field.md)|<xref:System.Threading.Tasks.Task> オブジェクトで実行するコードを表すデリゲート。|
|[m_contingentProperties](../../extensibility/debugger/m-contingentproperties-field.md)|<xref:System.Threading.Tasks.Task> オブジェクトの追加のプロパティを格納します。|
|[m_parent](../../extensibility/debugger/m-parent-field.md)|<xref:System.Threading.Tasks.Task?displayProperty=fullName> 親プロパティのバッキング フィールド。|
|[m_stateFlags](../../extensibility/debugger/m-stateflags-field.md)|<xref:System.Threading.Tasks.Task> オブジェクトの現在の状態に関する情報を格納します。|
|[m_stateObject](../../extensibility/debugger/m-stateobject-field.md)|アクションで使用されるデータを表すオブジェクト。|
|[m_taskId](../../extensibility/debugger/m-taskid-field.md)|<xref:System.Threading.Tasks.Task.Id%2A?displayProperty=fullName> プロパティのバッキング フィールド。|
|[s_taskIdCounter](../../extensibility/debugger/s-taskidcounter-field.md)|<xref:System.Threading.Tasks.Task> オブジェクトの次に使用できる識別子。|
|[TASK_STATE_CANCELED](../../extensibility/debugger/task-state-canceled-field.md)|タスクが実行状態に達する前に取り消されたこと、またはタスクのキャンセルが確認され、例外なく完了したことを示します。|
|[TASK_STATE_EXECUTED](../../extensibility/debugger/task-state-executed-field.md)|タスクが実行中であることを示します。|
|[TASK_STATE_FAULTED](../../extensibility/debugger/task-state-faulted-field.md)|ハンドルされない例外が原因でタスクが完了したことを示します。|
|[TASK_STATE_RAN_TO_COMPLETION](../../extensibility/debugger/task-state-ran-to-completion-field.md)|タスクが正常に実行を完了したことを示します。|
|[TASK_STATE_WAITING_ON_CHILDREN](../../extensibility/debugger/task-state-waiting-on-children-field.md)|タスクのデリゲートの実行が完了し、アタッチされた子タスクが完了するまで暗黙的に待機していることを示します。|

## <a name="remarks"></a>解説
 次の内部メソッドにより、<xref:System.Threading.Tasks.Task> コード実行の開始がマークされるため、デバッガー エンジンの役に立ちます。

- `Execute`

- `ExecuteEntry`

- `ExecuteWithThreadLocal`

- `Finish`

- `InnerInvoke`

- `InternalWait`

## <a name="see-also"></a>こちらもご覧ください
- <xref:System.Threading.Tasks.Task?displayProperty=fullName>
- [.NET Framework の並列拡張機能の内部](../../extensibility/debugger/parallel-extension-internals-for-the-dotnet-framework.md)
