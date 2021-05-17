---
description: 実行可能ファイルを起動します。
title: IDebugPortEx2::LaunchSuspended | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortEx2::LaunchSuspended
helpviewer_keywords:
- IDebugPortEx2::LaunchSuspended
ms.assetid: 34b2cf99-2e52-4757-8969-1d12ac517ec0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: fdffb6f87285e9f33d6abaf864b4d45345a304ca
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105072495"
---
# <a name="idebugportex2launchsuspended"></a>IDebugPortEx2::LaunchSuspended
実行可能ファイルを起動します。

## <a name="syntax"></a>構文

```cpp
HRESULT LaunchSuspended( 
   LPCOLESTR        pszExe,
   LPCOLESTR        pszArgs,
   LPCOLESTR        pszDir,
   BSTR             bstrEnv,
   DWORD            hStdInput,
   DWORD            hStdOutput,
   DWORD            hStdError,
   IDebugProcess2** ppPortProcess
);
```

```csharp
int LaunchSuspended( 
   string             pszExe,
   string             pszArgs,
   string             pszDir,
   string             bstrEnv,
   uint               hStdInput,
   uint               hStdOutput,
   uint               hStdError,
   out IDebugProcess2 ppPortProcess
);
```

## <a name="parameters"></a>パラメーター
`pszExe`\
[入力] 起動する実行可能ファイルの名前。 これは、`pszDir` パラメーターに指定されている作業ディレクトリに対する完全なパスまたは相対パスにすることができます。

`pszArgs`\
[入力] 実行可能ファイルに渡す引数。 引数がない場合は、null 値にすることができます。

`pszDir`\
[入力] 実行可能ファイルによって使用される作業ディレクトリの名前。 作業ディレクトリが不要な場合は、null 値にすることができます。

`bstrEnv`\
[入力] null で終わる文字列の環境ブロックと、それに続く追加の NULL ターミネータ。

`hStdInput`\
[入力] 代替入力ストリームへのハンドル。 リダイレクトが不要な場合は 0 にすることができます。

`hStdOutput`\
[入力] 代替出力ストリームへのハンドル。 リダイレクトが不要な場合は 0 にすることができます。

`hStdError`\
[入力] 代替エラー出力ストリームへのハンドル。 リダイレクトが不要な場合は 0 にすることができます。

`ppPortProcess`\
[出力] 起動されたプロセスを表す [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 このメソッドでは、プロセスを起動し、一時中止にしてコードが実行されないようにします。 [ResumeProcess](../../../extensibility/debugger/reference/idebugportex2-resumeprocess.md) メソッドが呼び出されて、プロセスが再開します。

 プログラムは、デバッグ エンジンから起動することもできます。 詳細については、「[プログラムの起動](../../../extensibility/debugger/launching-a-program.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [IDebugPortEx2](../../../extensibility/debugger/reference/idebugportex2.md)
- [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)
- [ResumeProcess](../../../extensibility/debugger/reference/idebugportex2-resumeprocess.md)
- [プログラムの起動](../../../extensibility/debugger/launching-a-program.md)
