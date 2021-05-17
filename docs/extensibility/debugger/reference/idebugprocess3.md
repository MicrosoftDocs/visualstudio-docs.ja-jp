---
description: このインターフェイスは、実行中のプロセスとそのプログラムを表します。
title: IDebugProcess3 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess3
helpviewer_keywords:
- IDebugProcess3 interface
ms.assetid: 7bd6b952-cf34-4e66-b8f6-d472dac3748f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d08169b196e01b5e2a7effdfe54829d17a970ef3
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105076512"
---
# <a name="idebugprocess3"></a>IDebugProcess3
このインターフェイスは、実行中のプロセスとそのプログラムを表します。 このインターフェイスは、[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) インターフェイスのいくつかのメソッドの置き換えとして存在します。 プロセス内のすべてのプログラムを制御できます。

> [!NOTE]
> [Continue](../../../extensibility/debugger/reference/idebugprogram2-continue.md)、[Execute](../../../extensibility/debugger/reference/idebugprogram2-execute.md)、および [Step](../../../extensibility/debugger/reference/idebugprogram2-step.md) メソッドは非推奨となり、使用できなくなりました。 代わりに、`IDebugProcess3` インターフェイスの対応するメソッドを使用してください。

## <a name="syntax"></a>構文

```
IDebugProcess3 : IDebugProcess2
```

## <a name="notes-for-implementers"></a>実装側の注意
 このインターフェイスは、プログラムをグループとして管理するためにカスタム ポート サプライヤーによって実装されます。 プログラムがグループとして管理されている場合は、その実行を制御し、式エバリュエーターの言語を設定できます。 このインターフェイスは、ポート サプライヤーによって実装される必要があります。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 このインターフェイスは、このプロセスで識別されるプログラムのグループと対話するために、主にセッション デバッグ マネージャー (SDM) によって呼び出されます。

 このインターフェイスを取得するには、[IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md) インターフェイスの [QueryInterface](/cpp/atl/queryinterface) を呼び出します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 `IDebugProcess3` では、[IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md) から継承されたメソッドに加えて以下のメソッドが実装されます。

|メソッド|説明|
|------------|-----------------|
|[Continue](../../../extensibility/debugger/reference/idebugprocess3-continue.md)|プロセスの実行またはステップ実行を続行します。|
|[実行](../../../extensibility/debugger/reference/idebugprocess3-execute.md)|プロセスの実行を開始します。|
|[Step](../../../extensibility/debugger/reference/idebugprocess3-step.md)|プロセスの 1 つの命令またはステートメントをステップ前進します。|
|[GetDebugReason](../../../extensibility/debugger/reference/idebugprocess3-getdebugreason.md)|デバッグのためにプロセスが起動された理由を取得します。|
|[SetHostingProcessLanguage](../../../extensibility/debugger/reference/idebugprocess3-sethostingprocesslanguage.md)|デバッグ エンジンが適切な式エバリュエーターを読み込むことができるように、ホスティング言語を設定します。|
|[GetHostingProcessLanguage](../../../extensibility/debugger/reference/idebugprocess3-gethostingprocesslanguage.md)|このプロセスに対して現在設定されている言語を取得します。|
|[DisableENC](../../../extensibility/debugger/reference/idebugprocess3-disableenc.md)|このプロセスのエディット コンティニュ (ENC) を無効にします。<br /><br /> カスタム ポート サプライヤーでは、このメソッドは実装されません (常に `E_NOTIMPL` を返す必要があります)。|
|[GetENCAvailableState](../../../extensibility/debugger/reference/idebugprocess3-getencavailablestate.md)|このプロセスの ENC 状態を取得します。<br /><br /> カスタム ポート サプライヤーでは、このメソッドは実装されません (常に `E_NOTIMPL` を返す必要があります)。|
|[GetEngineFilter](../../../extensibility/debugger/reference/idebugprocess3-getenginefilter.md)|利用できるデバッグ エンジンの一意の識別子からなる配列を取得します。|

## <a name="requirements"></a>必要条件
 ヘッダー: Msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
