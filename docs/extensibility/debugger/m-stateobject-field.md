---
description: アクションによって使用されるデータを表すオブジェクト。
title: m_stateObject フィールド | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- m_stateObject field, Task class [.NET Framework debug engines]
ms.assetid: 68c54b22-3e1c-4031-b9c7-b972c519d8a0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: c2128073f47c76244a18e18005a431f9317686c3
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105054791"
---
# <a name="m_stateobject-field"></a>m_stateObject フィールド
アクションによって使用されるデータを表すオブジェクト。

 **名前空間:** <xref:System.Threading.Tasks?displayProperty=fullName>

 **アセンブリ:** mscorlib (*mscorlib.dll* 内)

 この内部メンバーには、.NET Framework からはアクセスできないため、次の構文では共通中間言語 (CIL) を使用しています。

## <a name="syntax"></a>構文

```
.field assembly object m_stateObject
```

## <a name="remarks"></a>解説
 これは <xref:System.Threading.Tasks.Task.%23ctor%2A> コンストラクターに含まれる `state` パラメーターです。 <xref:System.Threading.Tasks.Task.AsyncState%2A?displayProperty=fullName> プロパティのバッキング フィールドでもあります。

## <a name="see-also"></a>関連項目
- [Task クラス](../../extensibility/debugger/task-class-internal-members.md)
