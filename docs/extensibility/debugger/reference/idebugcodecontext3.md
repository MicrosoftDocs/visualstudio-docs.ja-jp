---
description: IDebugCodeContext2 インターフェイスを拡張し、モジュールおよびプロセス インターフェイスを取得できるようにします。
title: IDebugCodeContext3 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugCodeContext3 interface
ms.assetid: 524eb882-0ad5-4bfb-95eb-eb3abb3d0237
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 4dd0ffb94f25ae8ac9566571a645d706fa224cd8
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105088316"
---
# <a name="idebugcodecontext3"></a>IDebugCodeContext3
[IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md) インターフェイスを拡張し、モジュールおよびプロセス インターフェイスを取得できるようにします。

## <a name="syntax"></a>構文

```
IDebugCodeContext3 : IDebugCodeContext2
```

## <a name="notes-for-implementers"></a>実装側の注意
 デバッグ エンジンによって実装され、[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] デバッグ パッケージで使用されます。

## <a name="methods"></a>メソッド
 このインターフェイスでは、`IDebugCodeContext2` インターフェイスのメソッドに加えて、次のメソッドが実装されます。

|メソッド|説明|
|------------|-----------------|
|[GetModule](../../../extensibility/debugger/reference/idebugcodecontext3-getmodule.md)|デバッグ モジュールのインターフェイスへの参照を取得します。|
|[GetProcess](../../../extensibility/debugger/reference/idebugcodecontext3-getprocess.md)|デバッグ プロセスのインターフェイスへの参照を取得します。|

## <a name="remarks"></a>解説
 これは省略可能なインターフェイスであり、通常は実装する必要はありません。

## <a name="requirements"></a>必要条件
 ヘッダー: Msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
