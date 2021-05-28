---
description: このタスクに登録されている子タスクのリスト。
title: m_children フィールド | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- m_children field, ContingentProperties class [.NET Framework debug engines]
ms.assetid: 0a3b5653-7bc0-4a7a-8963-9020bc52b9cb
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 90394afd982f22977d3d3ed74850032bfb5634c8
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105094693"
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
