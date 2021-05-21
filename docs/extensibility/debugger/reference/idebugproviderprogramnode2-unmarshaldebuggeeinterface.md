---
description: プロセス境界を越えて、指定されたインターフェイスを取得します。
title: IDebugProviderProgramNode2::UnmarshalDebuggeeInterface | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProviderProgramNode2::UnmarshalDebuggeeInterface
helpviewer_keywords:
- IDebugProviderProgramNode2::UnmarshalDebuggeeInterface
ms.assetid: 2e4653c5-10f1-493c-9973-f31d266c5d48
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 42b51d93f9c0cec3a2ee74b2dfc0f4621c608c07
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105083688"
---
# <a name="idebugproviderprogramnode2unmarshaldebuggeeinterface"></a>IDebugProviderProgramNode2::UnmarshalDebuggeeInterface
プロセス境界を越えて、指定されたインターフェイスを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT UnmarshalDebuggeeInterface(
   REFIID riid,
   void** ppvObject
);
```

```csharp
int UnmarshalDebuggeeInterface(
   ref Guid   riid,
   out IntPtr ppvObject
);
```

## <a name="parameters"></a>パラメーター
`riid`\
[in] 取得するインターフェイスの GUID。

`ppvObject`\
[out] 目的のインターフェイスを実装するオブジェクトを返します。 [C++] これは、目的のインターフェイス型に直接キャストできます。 [C#] <xref:System.Runtime.InteropServices.Marshal.GetObjectForIUnknown%2A> メソッドを使用して、目的のインターフェイスを取得します。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 このメソッドは、[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] プロセス空間でデバッグ エンジンが実行され、デバッグするプログラムが専用のプロセス空間で実行されている場合に使用されます。

## <a name="see-also"></a>関連項目
- [IDebugProviderProgramNode2](../../../extensibility/debugger/reference/idebugproviderprogramnode2.md)
