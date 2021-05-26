---
description: この関数では、指定されたプロジェクトの親プロジェクト パスを特定します。
title: SccGetParentProjectPath 関数 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccGetParentProjectPath
helpviewer_keywords:
- SccGetParentProjectPath function
ms.assetid: 62a71579-36b3-48b9-a1c8-04ab100efa08
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 305f226117bbb9cf906231a0b9bbaa24c1d87a8e
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105063982"
---
# <a name="sccgetparentprojectpath-function"></a>SccGetParentProjectPath 関数
この関数では、指定されたプロジェクトの親プロジェクト パスを特定します。 この関数は、ユーザーが Visual Studio プロジェクトをソース管理に追加しているときに呼び出されます。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccGetParentProjectPath(
   LPVOID pContext,
   HWND   hWnd,
   LPSTR  lpUser,
   LPCSTR lpProjPath,
   LPSTR  lpAuxProjPath,
   LPSTR  lpParentProjPath
);
```

### <a name="parameters"></a>パラメーター
 pContext

[入力] ソース管理プラグインのコンテキスト ポインター。

 hWnd

[入力] ソース管理プラグインが、提供するすべてのダイアログ ボックスの親として使用できる IDE ウィンドウへのハンドル。

 lpUser

[入力、出力] ユーザー名 (NULL 終端文字を含め、最大 SCC_USER_SIZE 文字)。

 lpProjPath

[入力] プロジェクト パスを識別する文字列 (NULL 終端文字を含め、最大 SCC_PRJPATH_SIZE 文字)。

 lpAuxProjPath

[入力、出力] プロジェクトを識別する補助文字列 (NULL 終端文字を含め、最大 SCC_PRJPATH_SIZE 文字)。

 lpParentProjPath

[入力、出力] 親プロジェクト パスを識別する出力文字列 (NULL 終端文字を含め、最大 SCC_PRJPATH_SIZE 文字)。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装では、次のいずれかの値を返すことが想定されます。

|値|説明|
|-----------|-----------------|
|SCC_OK|親プロジェクト パスが正常に取得されました。|
|SCC_E_INITIALIZEFAILED|プロジェクトを初期化できませんでした。|
|SCC_E_INVALIDUSER|ユーザーがソース管理プラグインにログインできませんでした。|
|SCC_E_UNKNOWNPROJECT|プロジェクトがソース管理プラグインで認識されていません。|
|SCC_E_INVALIDFILEPATH|ファイル パスが無効であるか、または使用できません。|
|SCC_E_NOTAUTHORIZED|ユーザーはこの操作の実行が許可されていません。|
|SCC_E_ACCESSFAILURE|ソース管理システムへのアクセス中に問題が発生しました。ネットワークまたは競合の問題である可能性があります。 再試行することをお勧めします。|
|SCC_E_PROJSYNTAXERR|プロジェクト構文が無効です。|
|SCC_E_CONNECTIONFAILURE|ストアへの接続で問題が発生しました。|
|SCC_E_NONSPECIFICERROR<br /><br /> SCC_E_UNKNOWNERROR|不特定のエラーです。|

## <a name="remarks"></a>解説
 この関数は、成功またはエラー コードを返します。成功した場合は、変数 `lpParentProjPath` を指定されたプロジェクトへの完全なプロジェクト パスで埋めます。

 この関数は、既存のプロジェクトの親プロジェクト パスを返します。 ルート プロジェクトの場合、この関数は、渡されたプロジェクト パス (つまり、同じルート プロジェクト パス) を返します。 プロジェクト パスは、ソース管理プラグインに対してのみ意味がある文字列であることに注意してください。

 IDE は、`lpUser` および `lpAuxProjPath` パラメーターへの変更も受け付ける準備ができています。 IDE では、これらの文字列を保持し、それをユーザーが将来このプロジェクトを開いたときに [SccOpenProject](../extensibility/sccopenproject-function.md) に渡します。 そのため、これらの文字列を使用すると、ソース管理プラグインではプロジェクトに関連付ける必要がある情報を追跡することができます。

 この関数は、ユーザーにプロジェクトを選択するよう求めない点を除き、[SccGetProjPath](../extensibility/sccgetprojpath-function.md) と同じです。 また、新しいプロジェクトを作成することもなく、既存のプロジェクトを操作するだけです。

 `SccGetParentProjectPath` が呼び出された場合、`lpProjPath` と `lpAuxProjPath` は空にはならず、有効なプロジェクトに対応します。 これらの文字列は通常、`SccGetProjPath` 関数の以前の呼び出しから IDE によって受信されます。

 `lpUser` 引数はユーザー名です。 IDE では、以前に `SccGetProjPath` 関数から受信したものと同じユーザー名を渡すため、ソース管理プラグインでは、この名前を既定値として使用する必要があります。 ユーザーが既にプラグインとの開いている接続を使用している場合は、この関数が確認なしで動作できるように、プラグインはすべてのプロンプトを排除するよう試みる必要があります。 ただし、ログインが失敗した場合、プラグインはユーザーにログインを入力するよう求め、有効なログインを受信したら、その名前を `lpUser` に戻す必要があります。 プラグインがこの文字列を変更する可能性があるため、IDE では、常にサイズ (`SCC_USER_LEN`+1) のバッファーを割り当てます。 この文字列が変更された場合、新しい文字列は有効な (少なくとも以前の文字列と同程度に有効な) ログイン名である必要があります。

## <a name="technical-notes-for-scccreatesubproject-and-sccgetparentprojectpath"></a>SccCreateSubProject と SccGetParentProjectPath に関するテクニカル ノート
 Visual Studio では、ソース管理へのソリューションやプロジェクトの追加が簡略化され、ユーザーがソース管理システム内の場所を選択するよう求められる回数は最小限に抑えられています。 ソース管理プラグインが新しい関数 [SccCreateSubProject](../extensibility/scccreatesubproject-function.md) と `SccGetParentProjectPath` の両方をサポートしている場合、これらの変更は Visual Studio によってアクティブ化されます。 ただし、次のレジストリ エントリを使用すると、これらの変更を無効にして、以前の Visual Studio (ソース管理プラグイン API バージョン 1.1) の動作に戻すことができます。

 **[HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\8.0\SourceControl] "DoNotCreateSolutionRootFolderInSourceControl"=dword:00000001**

 このレジストリ エントリが存在しないか、または dword:00000000 に設定されている場合、Visual Studio では新しい関数 `SccCreateSubProject` と `SccGetParentProjectPath` を使用しようとします。

 このレジストリ エントリが dword:00000001 に設定されている場合は、Visual Studio がこれらの新しい関数を使用しようとしないため、ソース管理への追加の操作は以前のバージョンの Visual Studio の場合と同様に機能します。

## <a name="see-also"></a>関連項目
- [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [SccCreateSubProject](../extensibility/scccreatesubproject-function.md)
- [SccGetProjPath](../extensibility/sccgetprojpath-function.md)
