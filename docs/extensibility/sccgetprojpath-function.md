---
description: この関数では、ユーザーに、ソース管理プラグインに対してのみ意味がある文字列であるプロジェクト パスを入力するよう求めます。
title: SccGetProjPath 関数 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccGetProjPath
helpviewer_keywords:
- SccGetProjPath function
ms.assetid: 1079847e-d45f-4cb8-9d92-1e01ce5d08f6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 93266464249b8de037a618bab55ede31988384cb
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112901072"
---
# <a name="sccgetprojpath-function"></a>SccGetProjPath 関数
この関数では、ユーザーに、ソース管理プラグインに対してのみ意味がある文字列であるプロジェクト パスを入力するよう求めます。 これは、ユーザーが次の操作を行っているときに呼び出されます。

- 新しいプロジェクトの作成

- 既存のプロジェクトのバージョン管理への追加

- 既存のバージョン管理プロジェクトを見つけようとする試み

## <a name="syntax"></a>構文

```cpp
SCCRTN SccGetProjPath (
   LPVOID pvContext,
   HWND   hWnd,
   LPSTR  lpUser,
   LPSTR  lpProjName,
   LPSTR  lpLocalPath,
   LPSTR  lpAuxProjPath,
   BOOL   bAllowChangePath,
   LPBOOL pbNew
);
```

### <a name="parameters"></a>パラメーター
 pvContext

[入力] ソース管理プラグインのコンテキスト構造体。

 hWnd

[入力] ソース管理プラグインが、提供するすべてのダイアログ ボックスの親として使用できる IDE ウィンドウへのハンドル。

 lpUser

[入力、出力] ユーザー名 (NULL 終端文字を含め、SCC_USER_SIZE 文字以下)。

 lpProjName

[入力、出力] IDE プロジェクト、プロジェクト ワークスペース、またはメイクファイルの名前 (NULL 終端文字を含め、SCC_PRJPATH_SIZE 文字以下)。

 lpLocalPath

[入力、出力] プロジェクトの作業パス。 `bAllowChangePath` が `TRUE` である場合、ソース管理プラグインではこの文字列を変更できます (NULL 終端文字を含め、_MAX_PATH 文字以下)。

 lpAuxProjPath

[入力、出力] 返されるプロジェクト パス用のバッファー (NULL 終端文字を含め、SCC_PRJPATH_SIZE 文字以下)。

 bAllowChangePath

[入力] これが `TRUE` である場合、ソース管理プラグインでは `lpLocalPath` 文字列を入力するよう求め、それを変更することができます。

 pbNew

[入力、出力] 受信される値は、新しいプロジェクトを作成するかどうかを示します。 返される値は、プロジェクトの作成に成功したことを示します。

|受信|解釈|
|--------------|--------------------|
|TRUE|ユーザーは新しいプロジェクトを作成できます。|
|FALSE|ユーザーは新しいプロジェクトを作成できません。|

|送信|解釈|
|--------------|--------------------|
|TRUE|新しいプロジェクトが作成されました。|
|FALSE|既存のプロジェクトが選択されました。|

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装では、次のいずれかの値が返されることが予期されています。

|値|説明|
|-----------|-----------------|
|SCC_OK|プロジェクトが正常に作成または取得されました。|
|SCC_I_OPERATIONCANCELED|操作は取り消されました。|
|SCC_E_ACCESSFAILURE|ソース管理システムへのアクセス中に問題が発生しました。ネットワークまたは競合の問題である可能性があります。|
|SCC_E_CONNECTIONFAILURE|ソース管理システムに接続しようとしているときに問題が発生しました。|
|SCC_E_NONSPECIFICERROR|未指定のエラーが発生しました。|

## <a name="remarks"></a>解説
 この関数の目的は、IDE でパラメーター `lpProjName` と `lpAuxProjPath` を取得できるようにすることです。 ソース管理プラグインでは、ユーザーにこれらの情報を入力するよう求めた後、これらの 2 つの文字列を IDE に戻します。 IDE では、これらの文字列をそのソリューション ファイル内に保持し、それをユーザーがこのプロジェクトを開くたびに [SccOpenProject](../extensibility/sccopenproject-function.md) に渡します。 これらの文字列を使用すると、プラグインでは、プロジェクトに関連付けられている情報を追跡できます。

 この関数が最初に呼び出されたとき、`lpAuxProjPath` は空の文字列に設定されます。 `lProjName` も空であるか、または IDE プロジェクトの名前を含んでいてもかまいません。ソース管理プラグインはこれを使用することも、無視することもできます。 この関数から正常に戻ると、プラグインは 2 つの対応する文字列を返します。 IDE では、これらの文字列について何も想定していません。それを使用することはなく、ユーザーによる変更も許可しません。 ユーザーがこれらの設定の変更を希望する場合、IDE では `SccGetProjPath` をもう一度呼び出し、前回受け取ったのと同じ値を渡します。 これにより、プラグインでは、これらの 2 つの文字列を完全に制御できるようになります。

 `lpUser` について、IDE ではユーザー名を渡すか、または単純に空の文字列へのポインターを渡すことができます。 ユーザー名が存在する場合、ソース管理プラグインでは、それを既定値として使用する必要があります。 ただし、名前が渡されなかった場合、または指定された名前でログインに失敗した場合、プラグインではユーザーにログインを入力するよう求める必要があり、有効なログインを受け取ったら `lpUser` でその名前を戻します。 プラグインがこの文字列を変更する可能性があるため、IDE では、常にサイズ (`SCC_USER_LEN`+1) のバッファーを割り当てます。

> [!NOTE]
> IDE が実行する最初のアクションは、`SccOpenProject` 関数または `SccGetProjPath` 関数のどちらかの呼び出しである可能性があります。 このため、その両方に同じ `lpUser` パラメーターがあります。これにより、ソース管理プラグインでは、どちらのときもユーザーをログインさせることができます。 この関数からの戻り値でエラーが示された場合でも、プラグインでは、この文字列に有効なログイン名を入力する必要があります。

 `lpLocalPath` は、ユーザーがプロジェクトを保持しているディレクトリです。 これは空の文字列であってもかまいません。 現在定義されているディレクトリが存在せず (ユーザーがソース管理システムからプロジェクトをダウンロードしようとしている場合など)、`bAllowChangePath` が `TRUE` である場合、ソース管理プラグインでは、ユーザーに入力を求めるか、または `lpLocalPath` に独自の文字列を格納するための他の何らかの方法を使用できます。 `bAllowChangePath` が `FALSE` である場合、ユーザーは既に指定されたディレクトリで作業しているため、プラグインでこの文字列を変更することはできません。

 ユーザーがソース管理下に置かれる新しいプロジェクトを作成する場合、`SccGetProjPath` が呼び出された時点では、ソース管理プラグインがこれを実際にソース管理システム内に作成しないことがあります。 代わりに、その文字列を `pbNew` の 0 以外の値と共に戻します。これは、そのプロジェクトがソース管理システム内に作成されることを示します。

 たとえば、Visual Studio の **[新しいプロジェクト]** ウィザードのユーザーが自分のプロジェクトをソース管理に追加した場合、Visual Studio がこの関数を呼び出すと、プラグインでは、その Visual Studio プロジェクトを格納するための新しいプロジェクトをソース管理システム内に作成しても問題がないかどうかを判定します。 そのウィザードが完了する前にユーザーが **[キャンセル]** をクリックした場合、プロジェクトは作成されません。 ユーザーが **[OK]** をクリックした場合、Visual Studio が `SccOpenProject` を呼び出して `SCC_OPT_CREATEIFNEW` を渡すと、ソース管理されたプロジェクトがその時点で作成されます。

## <a name="see-also"></a>関連項目
- [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [SccOpenProject](../extensibility/sccopenproject-function.md)
