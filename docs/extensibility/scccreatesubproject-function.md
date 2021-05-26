---
description: この関数は、lpParentProjPath 引数で指定された既存の親プロジェクトの下に、指定された名前のサブプロジェクトを作成します。
title: SccCreateSubProject 関数 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccCreateSubProject
helpviewer_keywords:
- SccCreateSubProject function
ms.assetid: 08154aed-ae5c-463c-8694-745d0e332965
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 70568c27afb4bdb5794db64322113dffbd824452
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105074003"
---
# <a name="scccreatesubproject-function"></a>SccCreateSubProject 関数
この関数は、`lpParentProjPath` 引数で指定された既存の親プロジェクトの下に、指定された名前のサブプロジェクトを作成します。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccCreateSubProject(
   LPVOID pContext,
   HWND   hWnd,
   LPSTR  lpUser,
   LPCSTR lpParentProjPath,
   LPCSTR lpSubProjName,
   LPSTR  lpAuxProjPath,
   LPSTR  lpSubProjPath
);
```

### <a name="parameters"></a>パラメーター
 pContext

[入力] ソース管理プラグインのコンテキスト ポインター。

 hWnd

[入力] ソース管理プラグインが、提供するすべてのダイアログ ボックスの親として使用できる IDE ウィンドウへのハンドル。

 lpUser

[入力、出力] ユーザー名 (NULL 終端文字を含め、最大 SCC_USER_SIZE 文字)。

 lpParentProjPath

[入力] 親プロジェクトのパスを識別する出力文字列 (NULL 終端文字を含め、最大 SCC_PRJPATH_SIZE 文字)。

 lpSubProjName

[入力] 提案されるサブプロジェクト名 (NULL 終端文字を含め、最大 SCC_PRJPATH_SIZE 文字)。

 lpAuxProjPath

[入力、出力] プロジェクトを識別する補助文字列 (NULL 終端文字を含め、最大 SCC_PRJPATH_SIZE 文字)。

 lpSubProjPath

[入力、出力] サブプロジェクトのパスを識別する出力文字列 (NULL 終端文字を含め、最大 SCC_PRJPATH_SIZE 文字)。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装では、次のいずれかの値を返すことが想定されます。

|値|説明|
|-----------|-----------------|
|SCC_OK|サブオブジェクトは正常に作成されました。|
|SCC_E_INITIALIZEFAILED|親プロジェクトを初期化できませんでした。|
|SCC_E_INVALIDUSER|ユーザーがソース管理システムにログインできませんでした。|
|SCC_E_COULDNOTCREATEPROJECT|サブプロジェクトを作成できません。|
|SCC_E_PROJSYNTAXERR|プロジェクト構文が無効です。|
|SCC_E_UNKNOWNPROJECT|親プロジェクトがソース管理プラグインで認識されていません。|
|SCC_E_INVALIDFILEPATH|ファイル パスが無効であるか、または使用できません。|
|SCC_E_NOTAUTHORIZED|ユーザーはこの操作の実行が許可されていません。|
|SCC_E_ACCESSFAILURE|ソース管理システムへのアクセス中に問題が発生しました。ネットワークまたは競合の問題である可能性があります。 再試行することをお勧めします。|
|SCC_E_CONNECTIONFAILURE|ソース管理プラグイン接続の問題が発生しました。|
|SCC_E_NONSPECIFICERROR<br /><br /> SCC_E_UNKNOWNERROR|不特定のエラーです。|

## <a name="remarks"></a>解説
 名前を持つサブプロジェクトが既に存在する場合、関数は、既定の名前を変更して一意の名前を作成できます。たとえば、"_ \<number>" を追加します。 呼び出し元は、`lpUser`、`lpSubProjPath`、および `lpAuxProjPath` への変更を受け入れるように準備されている必要があります。 次に、`lpSubProjPath` 引数と `lpAuxProjPath` 引数が [Sccopenproject](../extensibility/sccopenproject-function.md)の呼び出しで使用されます。 返されるときに、これらが呼び出し元によって変更されないようにする必要があります。 これらの文字列を使用すると、ソース管理プラグインではプロジェクトに関連付ける必要がある情報を追跡することができます。 呼び出し元 IDE では、返されるときにこれらの 2 つのパラメーターは表示されません。表示に適していない可能性のある、書式設定された文字列をプラグインで使用できるためです。 関数は、成功またはエラー コードを返します。成功した場合は、変数 `lpSubProjPath` を新しいプロジェクトへの完全なプロジェクト パスで埋めます。

 この関数は [SccGetProjPath](../extensibility/sccgetprojpath-function.md)に似ていますが、ユーザーにプロジェクトの選択を求めるのではなく、プロジェクトは自動的に作成されます。 `SccCreateSubProject` 関数が呼び出された場合、`lpParentProjName` と `lpAuxProjPath` は空にはならず、有効なプロジェクトに対応します。 これらの文字列は通常、`SccGetProjPath` 関数または [SccGetParentProjectPath](../extensibility/sccgetparentprojectpath-function.md) の以前の呼び出しから IDE によって受信されます。

 `lpUser` 引数はユーザー名です。 IDE では、以前に `SccGetProjPath` から受信したものと同じユーザー名を渡すため、ソース管理プラグインでは、この名前を既定値として使用する必要があります。 ユーザーが既にプラグインとの開いている接続を使用している場合は、この関数が確認なしで動作できるように、プラグインはすべてのプロンプトを排除するよう試みる必要があります。 ただし、ログインが失敗した場合、プラグインはユーザーにログインを入力するよう求め、有効なログインを受信したら、その名前を `lpUser` に戻す必要があります。 この文字列はプラグインによって変更される可能性があるため、IDE では常にサイズのバッファーを割り当てます (null 終端文字用のスペースを含む、SCC_USER_LEN + 1 または SCC_USER_SIZE)。 この文字列が変更された場合、新しい文字列は有効な (少なくとも以前の文字列と同程度に有効な) ログイン名である必要があります。

## <a name="technical-notes-for-scccreatesubproject-and-sccgetparentprojectpath"></a>SccCreateSubProject と SccGetParentProjectPath に関するテクニカル ノート
 Visual Studio では、ソース管理へのソリューションやプロジェクトの追加が簡略化され、ユーザーがソース管理システム内の場所を選択するよう求められる回数は最小限に抑えられています。 ソース管理プラグインが新しい関数 `SccCreateSubProject` と `SccGetParentProjectPath` の両方をサポートしている場合、これらの変更は Visual Studio によってアクティブ化されます。 ただし、次のレジストリ エントリを使用すると、これらの変更を無効にして、以前の Visual Studio (ソース管理プラグイン API バージョン 1.1) の動作に戻すことができます。

 **[HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\8.0\SourceControl] "DoNotCreateSolutionRootFolderInSourceControl"=dword:00000001**

 このレジストリ エントリが存在しないか、または dword:00000000 に設定されている場合、Visual Studio では新しい関数 `SccCreateSubProject` と `SccGetParentProjectPath` を使用しようとします。

 このレジストリ エントリが dword:00000001 に設定されている場合は、Visual Studio がこれらの新しい関数を使用しようとしないため、ソース管理への追加の操作は以前のバージョンの Visual Studio の場合と同様に機能します。

## <a name="see-also"></a>関連項目
- [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [SccGetParentProjectPath](../extensibility/sccgetparentprojectpath-function.md)
- [SccGetProjPath](../extensibility/sccgetprojpath-function.md)
