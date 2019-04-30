---
title: IDebugProgram2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2
helpviewer_keywords:
- IDebugProgram2 interface
ms.assetid: 8d73df73-cfff-4b8b-b426-d6051edb1939
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: daad54225170366d98a2df3465c7dba952098c4e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62870103"
---
# <a name="idebugprogram2"></a>IDebugProgram2
このインターフェイスは、プロセスで実行されているプログラムを表します。

## <a name="syntax"></a>構文

```
IDebugProgram2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装についてのメモ
 デバッグ エンジン (DE) とカスタム ポート サプライヤーは、プロセス内のプログラムを表すためには、このインターフェイスを実装します。 セッション デバッグ マネージャー (SDM) 情報を提供するには、このインターフェイスを実装も[アタッチ](../../../extensibility/debugger/reference/idebugprogram2-attach.md)します。

## <a name="notes-for-callers"></a>呼び出し元のノート
 [IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md)イベントが新しいプログラムのこのインターフェイスを返します。 このインターフェイスは、複数のインターフェイス上の多くのメソッドをパラメーターとしても使用されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表は、メソッドの`IDebugProgram2`します。

|メソッド|説明|
|------------|-----------------|
|[EnumThreads](../../../extensibility/debugger/reference/idebugprogram2-enumthreads.md)|このプログラムで実行されているスレッドを列挙します。|
|[GetName](../../../extensibility/debugger/reference/idebugprogram2-getname.md)|プログラムの名前を取得します。|
|[GetProcess](../../../extensibility/debugger/reference/idebugprogram2-getprocess.md)|このプログラムがで実行されているプロセスを取得します。|
|[Terminate](../../../extensibility/debugger/reference/idebugprogram2-terminate.md)|このプログラムを終了します。|
|[Attach](../../../extensibility/debugger/reference/idebugprogram2-attach.md)|このプログラムにアタッチします。|
|[CanDetach](../../../extensibility/debugger/reference/idebugprogram2-candetach.md)|デバッグ エンジン (DE) が、プログラムからデタッチできるかどうかを決定します。|
|[Detach](../../../extensibility/debugger/reference/idebugprogram2-detach.md)|このプログラムからデバッガーをデタッチします。|
|[GetProgramId](../../../extensibility/debugger/reference/idebugprogram2-getprogramid.md)|このプログラムには、グローバルに一意の識別子を取得します。|
|[GetDebugProperty](../../../extensibility/debugger/reference/idebugprogram2-getdebugproperty.md)|プログラムのプロパティを取得します。|
|[Execute](../../../extensibility/debugger/reference/idebugprogram2-execute.md)|停止状態からこのプログラムの実行が続行されます。 以前の実行状態がクリアされます。|
|[Continue](../../../extensibility/debugger/reference/idebugprogram2-continue.md)|停止状態からこのプログラムの実行が続行されます。 以前の実行状態が維持されます。|
|[Step](../../../extensibility/debugger/reference/idebugprogram2-step.md)|ステップを実行します。|
|[CauseBreak](../../../extensibility/debugger/reference/idebugprogram2-causebreak.md)|このプログラムが次の実行を停止する要求は、そのスレッドはコード実行のいずれかの時間です。|
|[GetEngineInfo](../../../extensibility/debugger/reference/idebugprogram2-getengineinfo.md)|このプログラムを実行するデバッグ エンジン (DE) の識別子と名前を取得します。|
|[EnumCodeContexts](../../../extensibility/debugger/reference/idebugprogram2-enumcodecontexts.md)|ソース ファイル内の指定位置のコード コンテキストを列挙します。|
|[GetMemoryBytes](../../../extensibility/debugger/reference/idebugprogram2-getmemorybytes.md)|このプログラムのメモリのバイト数を取得します。|
|[GetDisassemblyStream](../../../extensibility/debugger/reference/idebugprogram2-getdisassemblystream.md)|このプログラムまたはこのプログラムの一部の逆アセンブリのストリームを取得します。|
|[EnumModules](../../../extensibility/debugger/reference/idebugprogram2-enummodules.md)|このプログラムが読み込まれてが実行されているモジュールを列挙します。|
|[GetENCUpdate](../../../extensibility/debugger/reference/idebugprogram2-getencupdate.md)|このプログラムの編集と続行 (ENC) 更新プログラムを取得します。<br /><br /> カスタム デバッグ エンジンがこのメソッドを実装していません (常に返すことは`E_NOTIMPL`)。|
|[EnumCodePaths](../../../extensibility/debugger/reference/idebugprogram2-enumcodepaths.md)|このプログラムのコード パスを列挙します。|
|[WriteDump](../../../extensibility/debugger/reference/idebugprogram2-writedump.md)|ダンプ ファイルに書き込みます。|

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ:Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="remarks"></a>Remarks
 プログラムは、1 つまたは複数のプログラムのプロセスから成る中には、特定のランタイムのアーキテクチャで実行されているスレッド コンテナーです。

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [GetProgram](../../../extensibility/debugger/reference/idebugthread2-getprogram.md)
- [次へ](../../../extensibility/debugger/reference/ienumdebugprograms2-next.md)
- [Event](../../../extensibility/debugger/reference/idebugportevents2-event.md)
- [Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md)
- [DestroyProgram](../../../extensibility/debugger/reference/idebugengine2-destroyprogram.md)
- [Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
- [Attach_V7](../../../extensibility/debugger/reference/idebugprogramnode2-attach-v7.md)