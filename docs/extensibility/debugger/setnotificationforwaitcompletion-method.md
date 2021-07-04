---
title: SetNotificationForWaitCompletion メソッド | Microsoft Docs
description: デバッガーが状態ビットを使用して、Promise スタイルのタスクの非同期メソッド本体からステップアウトする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- SetNotificationForWaitCompletion method, Task class [.NET Framework debug engines]
ms.assetid: da149c9a-20f4-4543-a29e-429c8c1d2e19
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 6ec469ed4f9c4fa2e503b2350235299a81a94bf9
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112902112"
---
# <a name="setnotificationforwaitcompletion-method"></a>SetNotificationForWaitCompletion メソッド
TASK_STATE_WAIT_COMPLETION_NOTIFICATION 状態ビットを設定またはクリアします。

 **名前空間:** <xref:System.Threading.Tasks?displayProperty=fullName>

 **アセンブリ:** mscorlib (*mscorlib.dll* 内)

## <a name="syntax"></a>構文

```vb
internal void SetNotificationForWaitCompletion(bool enabled)
```

### <a name="parameters"></a>パラメーター
 `enabled`

 ビットを設定するには `true`、ビットを設定解除するには `false`。

## <a name="exceptions"></a>例外

## <a name="remarks"></a>解説
 このビットは、非同期メソッドの本体からステップアウトするために、デバッガーによって設定されます。 `enabled` が `true` の場合、このメソッドは、まだ完了していないタスクに対してのみ呼び出す必要があります。 `enabled` が `false` の場合、このメソッドは、完了したタスクに対して呼び出すことができます。 どちらの場合も、Promise スタイルのタスクに対してのみ使用してください。

## <a name="requirements"></a>必要条件

## <a name="see-also"></a>関連項目
- [Task クラス](../../extensibility/debugger/task-class-internal-members.md)
