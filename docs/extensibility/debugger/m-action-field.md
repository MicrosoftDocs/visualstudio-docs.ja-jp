---
description: System.Threading.Tasks.Task オブジェクトで実行するコードを表すデリゲート。
title: m_action フィールド | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- m_action field, Task class [.NET Framework debug engines]
ms.assetid: 201838c2-260d-4071-b6c3-f526874e19c9
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 838494eb612ffaa18931e42227619b22bc297b4f
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112901475"
---
# <a name="m_action-field"></a>m_action フィールド
<xref:System.Threading.Tasks.Task> オブジェクトで実行するコードを表すデリゲート。

 **名前空間:** <xref:System.Threading.Tasks?displayProperty=fullName>

 **アセンブリ:** mscorlib (*mscorlib.dll* 内)

 この内部メンバーには、.NET Framework からはアクセスできないため、次の構文では共通中間言語 (CIL) を使用しています。

## <a name="syntax"></a>構文

```csharp
.field assembly object m_action
```

## <a name="remarks"></a>解説
 これは <xref:System.Threading.Tasks.Task.%23ctor%2A> コンストラクターに含まれる `action` パラメーターです。

## <a name="see-also"></a>関連項目
- [Task クラス](../../extensibility/debugger/task-class-internal-members.md)
