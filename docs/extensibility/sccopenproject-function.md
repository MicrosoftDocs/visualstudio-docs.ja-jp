---
description: この関数では、既存のソース管理プロジェクトを開くか、または新しいソース管理プロジェクトを作成します。
title: SccOpenProject 関数 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccOpenProject
helpviewer_keywords:
- SccOpenProject function
ms.assetid: d609510b-660a-46d7-b93d-2406df20434d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 1326319b483aa707b77e0d7142d816b01fc7d3b1
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112902398"
---
# <a name="sccopenproject-function"></a>SccOpenProject 関数
この関数では、既存のソース管理プロジェクトを開くか、または新しいソース管理プロジェクトを作成します。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccOpenProject (
   LPVOID        pvContext,
   HWND          hWnd,
   LPSTR         lpUser,
   LPCSTR        lpProjName,
   LPCSTR        lpLocalProjPath,
   LPSTR         lpAuxProjPath,
   LPCSTR        lpComment,
   LPTEXTOUTPROC lpTextOutProc,
   LONG          dwFlags
);
```

#### <a name="parameters"></a>パラメーター
 pvContext

[入力] ソース管理プラグインのコンテキスト構造体。

 hWnd

[入力] ソース管理プラグインが、提供するすべてのダイアログ ボックスの親として使用できる IDE ウィンドウへのハンドル。

 lpUser

[入力、出力] ユーザーの名前 (NULL 終端文字を含め、SCC_USER_SIZE 文字以下)。

 lpProjName

[入力] プロジェクトの名前を識別する文字列。

 lpLocalProjPath

[入力] プロジェクトの作業フォルダーのパス。

 lpAuxProjPath

[入力、出力] プロジェクトを識別する省略可能な補助文字列 (NULL 終端文字を含め、SCC_AUXPATH_SIZE 文字以下)。

 lpComment

[入力] 作成されている新しいプロジェクトへのコメント。

 lpTextOutProc

[入力] ソース管理プラグインからのテキスト出力を表示するための省略可能なコールバック関数。

 dwFlags

[入力] プロジェクトがソース管理プラグインで認識されていない場合、新しいプロジェクトを作成する必要があるかどうかを通知します。 値は `SCC_OP_CREATEIFNEW` と `SCC_OP_SILENTOPEN.` の組み合わせにすることができます。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装では、次のいずれかの値が返されることが予期されています。

|値|説明|
|-----------|-----------------|
|SCC_OK|プロジェクトを開くことに成功しました。|
|SCC_E_INITIALIZEFAILED|プロジェクトを初期化できませんでした。|
|SCC_E_INVALIDUSER|ユーザーがソース管理システムにログインできませんでした。|
|SCC_E_COULDNOTCREATEPROJECT|呼び出しの前にプロジェクトが存在しませんでした。`SCC_OPT_CREATEIFNEW` フラグは設定されましたが、プロジェクトを作成できませんでした。|
|SCC_E_PROJSYNTAXERR|プロジェクト構文が無効です。|
|SCC_E_UNKNOWNPROJECT|プロジェクトがソース管理プラグインで認識されておらず、`SCC_OPT_CREATEIFNEW` フラグは設定されませんでした。|
|SCC_E_INVALIDFILEPATH|ファイル パスが無効であるか、または使用できません。|
|SCC_E_NOTAUTHORIZED|ユーザーはこの操作の実行が許可されていません。|
|SCC_E_ACCESSFAILURE|ソース管理システムへのアクセス中に問題が発生しました。ネットワークまたは競合の問題が原因になっている可能性があります。 再試行することをお勧めします。|
|SCC_E_NONSPECFICERROR|不特定のエラー。ソース管理システムは初期化されませんでした。|

## <a name="remarks"></a>解説
 IDE ではユーザー名 (`lpUser`) を渡すか、または単純に空の文字列へのポインターを渡すことができます。 ユーザー名が存在する場合、ソース管理プラグインでは、それを既定値として使用する必要があります。 ただし、名前が渡されなかった場合、または指定された名前でログインに失敗した場合、プラグインではユーザーにログインを入力するよう求める必要があり、有効なログインを受け取ったら `lpUser` で有効な名前を返します。プラグインがユーザー名文字列を変更する可能性があるため、IDE では、常にサイズ (`SCC_USER_LEN`+1 または SCC_USER_SIZE、これには NULL 終端文字用の領域が含まれます) のバッファーを割り当てます。

> [!NOTE]
> IDE が実行する必要のある最初のアクションは、`SccOpenProject` 関数または [SccGetProjPath](../extensibility/sccgetprojpath-function.md) の呼び出しである可能性があります。 このため、その両方に同じ `lpUser` パラメーターがあります。

 `lpAuxProjPath` と `lpProjName` はソリューション ファイルから読み取られるか、または `SccGetProjPath` 関数の呼び出しから返されます。 これらのパラメーターには、ソース管理プラグインによってプロジェクトに関連付けられ、そのプラグインに対してのみ意味がある文字列が含まれています。 このような文字列がソリューション ファイル内に存在せず、ユーザーが参照する (これにより、`SccGetProjPath` 関数を通して文字列が返されます) よう求められていない場合、IDE では、`lpAuxProjPath` と `lpProjName` の両方に対して空の文字列を渡し、この関数から戻ったときにこれらの値がプラグインによって更新されることを期待します。

 `lpTextOutProc` は、コマンド結果の出力を表示する目的で IDE からソース管理プラグインに提供されるコールバック関数へのポインターです。 このコールバック関数は、「[LPTEXTOUTPROC](../extensibility/lptextoutproc.md)」で詳細に説明されています。

> [!NOTE]
> ソース管理プラグインでは、これを利用しようとする場合、[SccInitialize](../extensibility/sccinitialize-function.md) で `SCC_CAP_TEXTOUT` フラグを設定しておく必要があります。 そのフラグが設定されなかった場合、または IDE がこの機能をサポートしていない場合、`lpTextOutProc` は `NULL` になります。

 `dwFlags` パラメーターでは、開かれるプロジェクトが現在存在しない場合の結果を制御します。 これは、2 つのビットフラグ `SCC_OP_CREATEIFNEW` と `SCC_OP_SILENTOPEN` で構成されます。 開かれるプロジェクトが既に存在する場合、この関数は単純にプロジェクトを開き、`SCC_OK` を返します。 そのプロジェクトが存在せず、かつ `SCC_OP_CREATEIFNEW` フラグがオンである場合、ソース管理プラグインではソース管理システム内にプロジェクトを作成し、それを開いてから `SCC_OK` を返すことができます。 そのプロジェクトが存在せず、かつ `SCC_OP_CREATEIFNEW` フラグがオフである場合、プラグインでは次に `SCC_OP_SILENTOPEN` フラグを確認する必要があります。 そのフラグがオンでない場合、プラグインでは、ユーザーにプロジェクト名を入力するよう求めることができます。 そのフラグがオンである場合、プラグインでは単純に `SCC_E_UNKNOWNPROJECT` を返す必要があります。

## <a name="calling-order"></a>呼び出し順序
 イベントの通常の過程では、ソース管理セッションを開くために [SccInitialize](../extensibility/sccinitialize-function.md) が最初に呼び出されます。 セッションは、`SccOpenProject` の呼び出しと、それに続く他のソース管理プラグイン API 関数呼び出しで構成されている場合があり、[SccCloseProject](../extensibility/scccloseproject-function.md) の呼び出しで終了します。 このようなセッションは、[SccUninitialize](../extensibility/sccuninitialize-function.md) が呼び出される前に複数回繰り返される可能性があります。

 ソース管理プラグインが `SccInitialize` で `SCC_CAP_REENTRANT` ビットを設定した場合は、上記のセッション シーケンスが並列に何回も繰り返される可能性があります。 さまざまな `pvContext` 構造体によって、異なるセッションが追跡されます。ここで、各 `pvContext` は、一度には 1 つの開いているプロジェクトに関連付けられています。 `pvContext` パラメーターに基づいて、プラグインでは、いずれかの特定の呼び出しでどのプロジェクトが参照されるかを判定できます。 機能ビット `SCC_CAP_REENTRANT` が設定されていない場合、再入不可能なソース管理プラグインは、複数のプロジェクトを操作する機能が制限されます。

> [!NOTE]
> `SCC_CAP_REENTRANT` ビットは、ソース管理プラグイン API のバージョン 1.1 で導入されました。 これが設定されていないか、またはバージョン 1.0 で無視された場合は、バージョン 1.0 のすべてのソース管理プラグインが再入不可能であると見なされます。

## <a name="see-also"></a>関連項目
- [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [SccCloseProject](../extensibility/scccloseproject-function.md)
- [SccGetProjPath](../extensibility/sccgetprojpath-function.md)
- [SccInitialize](../extensibility/sccinitialize-function.md)
- [SccUninitialize](../extensibility/sccuninitialize-function.md)
- [文字列長の制限](../extensibility/restrictions-on-string-lengths.md)
- [LPTEXTOUTPROC](../extensibility/lptextoutproc.md)
