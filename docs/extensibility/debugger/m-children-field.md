---
description: このタスクに登録されている子タスクのリスト。
title: m_children フィールド | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- m_children field, ContingentProperties class [.NET Framework debug engines]
ms.assetid: 0a3b5653-7bc0-4a7a-8963-9020bc52b9cb
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 311ab164551e46fbe1c30b5a6045a7993a900a67
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112901371"
---
# <a name="m_children-field"></a>m_children フィールド
このタスクに登録されている子タスクのリスト。

 **名前空間:** <xref:System.Threading.Tasks?displayProperty=fullName>

 **アセンブリ:** mscorlib (*mscorlib.dll* 内)

 この内部メンバーには、.NET Framework からはアクセスできないため、次の構文では共通中間言語 (CIL) を使用しています。

## <a name="syntax"></a>構文

```csharp
.field public class System.Collections.Generic.List`1<class System.Threading.Tasks.Task> m_children
```

## <a name="remarks"></a>解説
 タスクの実行中は、タスクを実行するスレッドだけがこの配列にアクセスします。

 タスクが完了した場合、その他のスレッドは、このフィールドに対して何も追加または削除しない限り、このフィールドにアクセスできます。

## <a name="see-also"></a>関連項目
- [ContingentProperties クラス](../../extensibility/debugger/contingentproperties-class-internal-members.md)
