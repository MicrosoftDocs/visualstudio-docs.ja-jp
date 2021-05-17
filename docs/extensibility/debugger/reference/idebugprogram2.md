---
description: このインターフェイスは、プロセスで実行されているプログラムを表します。
title: IDebugProgram2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2
helpviewer_keywords:
- IDebugProgram2 interface
ms.assetid: 8d73df73-cfff-4b8b-b426-d6051edb1939
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 2f6effa250749f448ed1a02c4b7a699d50b7388e
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105084403"
---
# <a name="idebugprogram2"></a>IDebugProgram2
このインターフェイスは、プロセスで実行されているプログラムを表します。

## <a name="syntax"></a>構文

```
IDebugProgram2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 デバッグ エンジン (DE) とカスタム ポート サプライヤーでは、このインターフェイスを実装して、プロセス内のプログラムを表します。 また、セッション デバッグ マネージャー (SDM) では、このインターフェイスを実装して、[Attach](../../../extensibility/debugger/reference/idebugprogram2-attach.md) する情報を提供します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 [IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md) イベントでは、新しいプログラムについてこのインターフェイスが返されます。 このインターフェイスは、複数のインターフェイスの多くのメソッドのパラメーターとしても使用されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、`IDebugProgram2` のメソッドを示します。

|メソッド|説明|
|------------|-----------------|
|[EnumThreads](../../../extensibility/debugger/reference/idebugprogram2-enumthreads.md)|このプログラムで実行されているスレッドを列挙します。|
|[GetName](../../../extensibility/debugger/reference/idebugprogram2-getname.md)|プログラムの名前を取得します。|
|[GetProcess](../../../extensibility/debugger/reference/idebugprogram2-getprocess.md)|このプログラムが実行されているプロセスを取得します。|
|[Terminate](../../../extensibility/debugger/reference/idebugprogram2-terminate.md)|このプログラムを終了します。|
|[[アタッチ]](../../../extensibility/debugger/reference/idebugprogram2-attach.md)|このプログラムにアタッチします。|
|[CanDetach](../../../extensibility/debugger/reference/idebugprogram2-candetach.md)|デバッグ エンジン (DE) をプログラムからデタッチできるかどうかを判別します。|
|[[デタッチ]](../../../extensibility/debugger/reference/idebugprogram2-detach.md)|このプログラムからデバッガーをデタッチします。|
|[GetProgramId](../../../extensibility/debugger/reference/idebugprogram2-getprogramid.md)|このプログラムのグローバル一意識別子を取得します。|
|[GetDebugProperty](../../../extensibility/debugger/reference/idebugprogram2-getdebugproperty.md)|プログラムのプロパティを取得します。|
|[実行](../../../extensibility/debugger/reference/idebugprogram2-execute.md)|停止された状態からこのプログラムの実行を続行します。 以前の実行状態はすべてクリアされます。|
|[続行](../../../extensibility/debugger/reference/idebugprogram2-continue.md)|停止された状態からこのプログラムの実行を続行します。 以前の実行状態はすべて保持されます。|
|[Step](../../../extensibility/debugger/reference/idebugprogram2-step.md)|ステップを実行します。|
|[CauseBreak](../../../extensibility/debugger/reference/idebugprogram2-causebreak.md)|いずれかのスレッドで次にコードが実行されたときにこのプログラムの実行を停止するように要求します。|
|[GetEngineInfo](../../../extensibility/debugger/reference/idebugprogram2-getengineinfo.md)|このプログラムを実行しているデバッグ エンジン (DE) の名前と ID を取得します。|
|[EnumCodeContexts](../../../extensibility/debugger/reference/idebugprogram2-enumcodecontexts.md)|ソース ファイル内の指定された位置のコード コンテキストを列挙します。|
|[GetMemoryBytes](../../../extensibility/debugger/reference/idebugprogram2-getmemorybytes.md)|このプログラムのメモリのバイトを取得します。|
|[GetDisassemblyStream](../../../extensibility/debugger/reference/idebugprogram2-getdisassemblystream.md)|このプログラムまたはこのプログラムの一部の逆アセンブリ ストリームを取得します。|
|[EnumModules](../../../extensibility/debugger/reference/idebugprogram2-enummodules.md)|このプログラムによって読み込まれ、実行されているモジュールを列挙します。|
|[GetENCUpdate](../../../extensibility/debugger/reference/idebugprogram2-getencupdate.md)|このプログラムのエディット コンティニュ (ENC) の更新を取得します。<br /><br /> カスタム デバッグ エンジンでは、このメソッドは実装されません (常に `E_NOTIMPL` を返す必要があります)。|
|[EnumCodePaths](../../../extensibility/debugger/reference/idebugprogram2-enumcodepaths.md)|このプログラムのコード パスを列挙します。|
|[WriteDump](../../../extensibility/debugger/reference/idebugprogram2-writedump.md)|ダンプをファイルに書き込みます。|

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="remarks"></a>解説
 プログラムは特定の実行時アーキテクチャで実行されるスレッド コンテナーであり、プロセスは 1 つ以上のプログラムで構成されます。

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [GetProgram](../../../extensibility/debugger/reference/idebugthread2-getprogram.md)
- [次へ](../../../extensibility/debugger/reference/ienumdebugprograms2-next.md)
- [Event](../../../extensibility/debugger/reference/idebugportevents2-event.md)
- [[アタッチ]](../../../extensibility/debugger/reference/idebugengine2-attach.md)
- [DestroyProgram](../../../extensibility/debugger/reference/idebugengine2-destroyprogram.md)
- [Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
- [Attach_V7](../../../extensibility/debugger/reference/idebugprogramnode2-attach-v7.md)
