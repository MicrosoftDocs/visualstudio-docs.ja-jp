---
description: このメソッドは、デバッグ エンジン (DE) によってプロセスを起動します。
title: IDebugEngineLaunch2::LaunchSuspended | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngineLaunch2::LaunchSuspended
helpviewer_keywords:
- IDebugEngineLaunch2::LaunchSuspended
ms.assetid: 5dd2643e-c20a-470e-9024-2a423eb39856
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 2db2ce2a35cd8be6599fca3e01bc69a6680012b2
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105066023"
---
# <a name="idebugenginelaunch2launchsuspended"></a>IDebugEngineLaunch2::LaunchSuspended
このメソッドは、デバッグ エンジン (DE) によってプロセスを起動します。

## <a name="syntax"></a>構文

```cpp
HRESULT LaunchSuspended ( 
   LPCOLESTR             pszMachine,
   IDebugPort2*          pPort,
   LPCOLESTR             pszExe,
   LPCOLESTR             pszArgs,
   LPCOLESTR             pszDir,
   BSTR                  bstrEnv,
   LPCOLESTR             pszOptions,
   LAUNCH_FLAGS          dwLaunchFlags,
   DWORD                 hStdInput,
   DWORD                 hStdOutput,
   DWORD                 hStdError,
   IDebugEventCallback2* pCallback,
   IDebugProcess2**      ppDebugProcess
);
```

```csharp
int LaunchSuspended(
   string               pszServer,
   IDebugPort2          pPort,
   string               pszExe,
   string               pszArgs,
   string               pszDir,
   string               bstrEnv,
   string               pszOptions,
   enum_LAUNCH_FLAGS    dwLaunchFlags,
   uint                 hStdInput,
   uint                 hStdOutput,
   uint                 hStdError,
   IDebugEventCallback2 pCallback,
   out IDebugProcess2   ppProcess
);
```

## <a name="parameters"></a>パラメーター
`pszMachine`\
[入力] プロセスを起動するコンピューターの名前。 ローカル コンピューターを指定するには、null 値を使用します。

`pPort`\
[入力] プログラムが実行されるポートを表す [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md) インターフェイス。

`pszExe`\
[入力] 起動する実行可能ファイルの名前。

`pszArgs`\
[入力] 実行可能ファイルに渡す引数。 引数がない場合は、null 値にすることができます。

`pszDir`\
[入力] 実行可能ファイルによって使用される作業ディレクトリの名前。 作業ディレクトリが不要な場合は、null 値にすることができます。

`bstrEnv`\
[入力] NULL で終わる文字列の環境ブロックと、それに続く追加の NULL ターミネータ。

`pszOptions`\
[入力] 実行可能ファイルのオプション。

`dwLaunchFlags`\
[入力] セッションの [LAUNCH_FLAGS](../../../extensibility/debugger/reference/launch-flags.md) を指定します。

`hStdInput`\
[入力] 代替入力ストリームへのハンドル。 リダイレクトが不要な場合は 0 にすることができます。

`hStdOutput`\
[入力] 代替出力ストリームへのハンドル。 リダイレクトが不要な場合は 0 にすることができます。

`hStdError`\
[入力] 代替エラー出力ストリームへのハンドル。 リダイレクトが不要な場合は 0 にすることができます。

`pCallback`\
[入力] デバッガー イベントを受け取る [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) オブジェクト。

`ppDebugProcess`\
[出力] 起動されたプロセスを表す、結果の [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 通常、[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] は [LaunchSuspended](../../../extensibility/debugger/reference/idebugportex2-launchsuspended.md) メソッドを使用してプログラムを起動してから、一時停止されたプログラムにデバッガーをアタッチします。 ただし、状況によっては、デバッグ エンジンがプログラムを起動することが必要な場合があります (たとえば、デバッグ エンジンがインタープリターの一部であり、デバッグ中のプログラムがインタープリター言語である場合)。そのような場合、[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] は `IDebugEngineLaunch2::LaunchSuspended` メソッドを使用します。

 [ResumeProcess](../../../extensibility/debugger/reference/idebugenginelaunch2-resumeprocess.md) メソッドは、プロセスが一時停止状態で正常に起動された後にプロセスを開始するために呼び出されます。

## <a name="see-also"></a>関連項目
- [IDebugEngineLaunch2](../../../extensibility/debugger/reference/idebugenginelaunch2.md)
- [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)
- [LAUNCH_FLAGS](../../../extensibility/debugger/reference/launch-flags.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
- [LaunchSuspended](../../../extensibility/debugger/reference/idebugportex2-launchsuspended.md)
- [ResumeProcess](../../../extensibility/debugger/reference/idebugenginelaunch2-resumeprocess.md)
