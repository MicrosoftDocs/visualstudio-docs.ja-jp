---
description: 指定されたプロセスから、実行中のプログラムの一覧を取得します。
title: IDebugProgramProvider2::GetProviderProcessData | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramProvider2::GetProviderProcessData
helpviewer_keywords:
- IDebugProgramProvider2::GetProviderProcessData
ms.assetid: 90cf7b7f-53d2-487e-b793-94501a6e24dd
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ad388a552a34ebd49819987a20f4876193a96658
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105071481"
---
# <a name="idebugprogramprovider2getproviderprocessdata"></a>IDebugProgramProvider2::GetProviderProcessData
指定されたプロセスから、実行中のプログラムの一覧を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetProviderProcessData(
   PROVIDER_FLAGS         Flags,
   IDebugDefaultPort2*    pPort,
   AD_PROCESS_ID          processId,
   CONST_GUID_ARRAY       EngineFilter,
   PROVIDER_PROCESS_DATA* pProcess
);
```

```csharp
int GetProviderProcessData(
   enum_PROVIDER_FLAGS     Flags,
   IDebugDefaultPort2      pPort,
   AD_PROCESS_ID           ProcessId,
   CONST_GUID_ARRAY        EngineFilter,
   PROVIDER_PROCESS_DATA[] pProcess
);
```

## <a name="parameters"></a>パラメーター
`Flags`\
[入力] [PROVIDER_FLAGS](../../../extensibility/debugger/reference/provider-flags.md) 列挙型のフラグの組み合わせ。 この呼び出しで一般的なフラグは、次のとおりです。

|フラグ|説明|
|----------|-----------------|
|`PFLAG_REMOTE_PORT`|呼び出し元はリモート コンピューターで実行されています。|
|`PFLAG_DEBUGGEE`|呼び出し元は現在、デバッグ中です (マーシャリングに関する追加情報がノードごとに返されます)。|
|`PFLAG_ATTACHED_TO_DEBUGGEE`|呼び出し元はアタッチされましたが、デバッガーによって起動されませんでした。|
|`PFLAG_GET_PROGRAM_NODES`|呼び出し元が、返されるプログラム ノードの一覧を要求しています。|

`pPort`\
[入力] 呼び出しプロセスが実行されているポート。

`processId`\
[入力] 対象のプログラムを含むプロセスの ID を保持している [AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md) 構造体。

`EngineFilter`\
[入力] このプロセスのデバッグ割り当てられたデバッグ エンジンの GUID の配列 (これらは、指定されたエンジンがサポートしているものに基づいて実際に返されるプログラムをフィルター処理するために使用されます。エンジンが指定されていない場合は、すべてのプログラムが返されます)。

`pProcess`\
[出力] 要求された情報が格納される [PROVIDER_PROCESS_DATA](../../../extensibility/debugger/reference/provider-process-data.md) 構造体。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 通常、このメソッドはプロセスによって呼び出され、そのプロセスで実行されているプログラムの一覧を取得します。 返される情報は、[IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md) オブジェクトの一覧です。

## <a name="see-also"></a>関連項目
- [IDebugProgramProvider2](../../../extensibility/debugger/reference/idebugprogramprovider2.md)
- [IDebugDefaultPort2](../../../extensibility/debugger/reference/idebugdefaultport2.md)
- [AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md)
- [CONST_GUID_ARRAY](../../../extensibility/debugger/reference/const-guid-array.md)
- [PROVIDER_FLAGS](../../../extensibility/debugger/reference/provider-flags.md)
- [PROVIDER_PROCESS_DATA](../../../extensibility/debugger/reference/provider-process-data.md)
- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
