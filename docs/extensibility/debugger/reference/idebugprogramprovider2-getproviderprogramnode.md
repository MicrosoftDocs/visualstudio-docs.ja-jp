---
description: 特定のプログラムのプログラム ノードを取得します。
title: IDebugProgramProvider2::GetProviderProgramNode | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramProvider2::GetProviderProgramNode
helpviewer_keywords:
- IDebugProgramProvider2::GetProviderProgramNode
ms.assetid: e62e8e83-acbb-4c52-aedf-ffbd4670db29
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 07e7184c189d501b2fcb604590eeb121bae8ccdc
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105065282"
---
# <a name="idebugprogramprovider2getproviderprogramnode"></a>IDebugProgramProvider2::GetProviderProgramNode
特定のプログラムのプログラム ノードを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetProviderProgramNode(
   PROVIDER_FLAGS       Flags,
   IDebugDefaultPort2*  pPort,
   AD_PROCESS_ID        processId,
   REFGUID              guidEngine,
   UINT64               programId,
   IDebugProgramNode2** ppProgramNode
);
```

```csharp
int GetProviderProgramNode(
   enum_PROVIDER_FLAGS    Flags,
   IDebugDefaultPort2     pPort,
   AD_PROCESS_ID          ProcessId,
   ref Guid               guidEngine,
   ulong                  programId,
   out IDebugProgramNode2 ppProgramNode
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

`pPort`\
[入力] 呼び出しプロセスが実行されているポート。

`processId`\
[入力] 対象のプログラムを含むプロセスの ID を保持している [AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md) 構造体。

`guidEngine`\
[入力] プログラムがアタッチされているデバッグ エンジンがある場合、その GUID。

`programId`\
[入力] プログラム ノードを取得する対象のプログラムの ID。

`ppProgramNode`\
[出力] 要求されたプログラム ノードを表す [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md) オブジェクト。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDebugProgramProvider2](../../../extensibility/debugger/reference/idebugprogramprovider2.md)
- [PROVIDER_FLAGS](../../../extensibility/debugger/reference/provider-flags.md)
- [AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md)
- [IDebugDefaultPort2](../../../extensibility/debugger/reference/idebugdefaultport2.md)
- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
