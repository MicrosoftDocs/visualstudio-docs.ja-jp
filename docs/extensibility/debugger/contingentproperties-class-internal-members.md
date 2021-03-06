---
description: System.Threading.Tasks.Task オブジェクトの追加のプロパティが含まれます。
title: ContingentProperties クラス - 内部メンバー | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- ContingentProperties class [.NET Framework debug engines]
- debug engines, ContingentProperties class [.NET Framework]
ms.assetid: c49d1362-ab1c-4b6d-9950-fcae40e0e66b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8fca0bf68de4493d0165f9e66e251945ba6168b2
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112905684"
---
# <a name="contingentproperties-class---internal-members"></a>ContingentProperties クラス - 内部メンバー
<xref:System.Threading.Tasks.Task> オブジェクトの追加プロパティが含まれています。

 **名前空間:** <xref:System.Threading.Tasks?displayProperty=fullName>

 **アセンブリ:** mscorlib (mscorlib.dll 内)

 これらの内部メンバーには、.NET Framework からはアクセスできないため、次の構文では共通中間言語 (CIL) を使用しています。

## <a name="syntax"></a>構文

```csharp
.class auto ansi nested assembly beforefieldinit ContingentProperties
       extends System.Object
```

## <a name="members"></a>メンバー

### <a name="fields"></a>フィールド

|名前|説明|
|----------|-----------------|
|[m_children](../../extensibility/debugger/m-children-field.md)|このタスクに登録されている子タスクの一覧。|

## <a name="remarks"></a>解説
 このクラスのフィールドは、必要なときにのみ、.NET Framework によって初期化されます。

## <a name="see-also"></a>関連項目
- [.NET Framework の並列拡張機能の内部](../../extensibility/debugger/parallel-extension-internals-for-the-dotnet-framework.md)
