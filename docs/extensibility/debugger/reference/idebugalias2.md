---
description: 変数の数値の別名を表し、式エバリュエーター (EE) で別名のアプリケーション ドメインを取得できるようにします。
title: IDebugAlias2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugAlias2 interface
ms.assetid: 5252dcbb-8bfe-4d8a-a8e5-b022b194df19
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: f6ca97fbe23e9b0c84c39e591c0fd9cfb997fca5
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105059042"
---
# <a name="idebugalias2"></a>IDebugAlias2
> [!IMPORTANT]
> Visual Studio 2015 では、この方法による式エバリュエーターの実装は非推奨です。 CLR 式エバリュエーターの実装については、[CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)および[マネージド式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)に関する記事をご覧ください。

 変数の数値の別名を表し、式エバリュエーター (EE) で別名のアプリケーション ドメインを取得できるようにします。

## <a name="syntax"></a>構文

```
IDebugAlias2 : IDebugAlias
```

## <a name="notes-for-implementers"></a>実装側の注意
 このインターフェイスは、マネージド デバッグ エンジン (DE) によって実装されます。

## <a name="methods"></a>メソッド
 このインターフェイスには、[IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md) インターフェイスのメソッドに加えて、次のメソッドが実装されています。

|メソッド|説明|
|------------|-----------------|
|[GetAppDomainId](../../../extensibility/debugger/reference/idebugalias2-getappdomainid.md)|アプリケーション ドメインの識別子を取得します。|

## <a name="remarks"></a>解説
 別名は、文字列形式の 10 進数の後に # 文字が続いたものです (たとえば、1001#)。

## <a name="requirements"></a>必要条件
 ヘッダー: Ee.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
