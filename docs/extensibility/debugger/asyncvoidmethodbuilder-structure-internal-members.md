---
description: このトピックでは、System.Runtime.CompilerServices.AsyncVoidMethodBuilder クラスの内部メンバーについて説明します。
title: AsyncVoidMethodBuilder 構造体 - 内部メンバー | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debug engines, AsyncVoidMethodBuilder structure [.NET Framework]
- AsyncVoidMethodBuilder structure [.NET Framework debug engines]
ms.assetid: fe2970ab-d4c5-4355-a8e4-772ee0a57178
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 4097bce1f7fd90c5b73a3bb450a873561d76d9c1
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105055337"
---
# <a name="asyncvoidmethodbuilder-structure---internal-members"></a>AsyncVoidMethodBuilder 構造体 - 内部メンバー
このトピックでは、<xref:System.Runtime.CompilerServices.AsyncVoidMethodBuilder> クラスの内部メンバーについて説明します。 このクラスに関する一般的な情報については、<xref:System.Runtime.CompilerServices.AsyncVoidMethodBuilder> のリファレンス トピックを参照してください。

 **名前空間:** <xref:System.Runtime.CompilerServices?displayProperty=fullName>

 **アセンブリ:** mscorlib (mscorlib.dll 内)

 これらの内部メンバーには、.NET Framework からはアクセスできないため、次の構文では共通中間言語 (CIL) を使用しています。

## <a name="syntax"></a>構文

```csharp
.class public sequential ansi sealed beforefieldinit System.Runtime.CompilerServices.AsyncVoidMethodBuilder
       extends System.ValueType
       implements System.Runtime.CompilerServices.IAsyncMethodBuilder
```

## <a name="internal-members"></a>内部メンバー

|名前|説明|
|----------|-----------------|
|[ObjectIdForDebugger プロパティ](../../extensibility/debugger/asyncvoidmethodbuilder-objectidfordebugger-property.md)|デバッガーに対してこのビルダーを一意に識別するために使用できるオブジェクトを取得します。|
|[m_objectIdForDebugger フィールド](../../extensibility/debugger/asyncvoidmethodbuilder-m-objectidfordebugger-field.md)|このビルダーを一意に識別するためにデバッガーで使用される遅延初期化オブジェクトを表します。|

## <a name="see-also"></a>関連項目
- <xref:System.Runtime.CompilerServices.AsyncVoidMethodBuilder>
- [.NET Framework の並列拡張機能の内部](../../extensibility/debugger/parallel-extension-internals-for-the-dotnet-framework.md)
