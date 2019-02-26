---
title: IDebugProviderProgramNode2::UnmarshalDebuggeeInterface |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProviderProgramNode2::UnmarshalDebuggeeInterface
helpviewer_keywords:
- IDebugProviderProgramNode2::UnmarshalDebuggeeInterface
ms.assetid: 2e4653c5-10f1-493c-9973-f31d266c5d48
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 86c20e7c6828cfbf3ec31ba5dcbec9c7ee8478df
ms.sourcegitcommit: b0d8e61745f67bd1f7ecf7fe080a0fe73ac6a181
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/22/2019
ms.locfileid: "56706224"
---
# <a name="idebugproviderprogramnode2unmarshaldebuggeeinterface"></a>IDebugProviderProgramNode2::UnmarshalDebuggeeInterface
プロセスの境界を越えて、指定したインターフェイスを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT UnmarshalDebuggeeInterface(
   REFIID riid,
   void** ppvObject
);
```

```csharp
int UnmarshalDebuggeeInterface(
   ref Guid   riid,
   out IntPtr ppvObject
);
```

#### <a name="parameters"></a>パラメーター
 `riid`

 [in]インターフェイスの GUID を取得します。

 `ppvObject`

 [out]必要なインターフェイスを実装するオブジェクトを返します。 [C++] これは、必要なインターフェイスの型に直接キャストできます。 [C#] を使用して、<xref:System.Runtime.InteropServices.Marshal.GetObjectForIUnknown%2A>必要なインターフェイスを取得します。

## <a name="return-value"></a>戻り値
 成功した場合、返します`S_OK`、それ以外のエラー コードを返します。

## <a name="remarks"></a>Remarks
 デバッグ エンジンがで実行されているときに、このメソッドを使用、[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]プロセス領域とデバッグ中のプログラムが、独自のプロセス空間内で実行されています。

## <a name="see-also"></a>関連項目
- [IDebugProviderProgramNode2](../../../extensibility/debugger/reference/idebugproviderprogramnode2.md)