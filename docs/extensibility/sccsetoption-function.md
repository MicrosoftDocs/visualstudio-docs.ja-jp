---
description: この関数では、ソース管理プラグインの動作を制御するオプションを設定します。
title: SccSetOption 関数 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccSetOption
helpviewer_keywords:
- SccSetOption function
ms.assetid: 4b5e6666-c24c-438a-a9df-9c52f58f8175
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 18e33cbb8dbee9b332456826ed33e46e4d2e76de
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112904101"
---
# <a name="sccsetoption-function"></a>SccSetOption 関数
この関数では、ソース管理プラグインの動作を制御するオプションを設定します。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccSetOption(
   LPVOID pvContext,
   LONG   nOption,
   LONG   dwVal
);
```

#### <a name="parameters"></a>パラメーター
 pvContext

[入力] ソース管理プラグインのコンテキスト構造体。

 nOption

[入力] 設定しているオプション。

 dwVal

[入力] オプションの設定。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装では、次のいずれかの値が返されることが予期されています。

|値|説明|
|-----------|-----------------|
|SCC_OK|オプションが正常に設定されました。|
|SCC_I_SHARESUBPROJOK|`nOption` が `SCC_OPT_SHARESUBPROJ` だった場合に返されます。ソース管理プラグインでは、IDE で送信先フォルダーを設定できます。|
|SCC_E_OPNOTSUPPORTED|オプションが設定されていません。依存しないようにする必要があります。|

## <a name="remarks"></a>解説
 IDE では、ソース管理プラグインの動作を制御するためにこの関数を呼び出します。 最初のパラメーター `nOption` は設定されている値を示し、2 番目の `dwVal` はその値の処理方法を示します。 プラグインには、`pvContext``,` に関連付けられたこの情報が格納されるので、IDE では [SccInitialize](../extensibility/sccinitialize-function.md) を呼び出した後にこの関数を呼び出す必要があります (ただし、[SccOpenProject](../extensibility/sccopenproject-function.md) を呼び出すたびに必ずしも必要になるとは限りません)。

 オプションとその値の概要:

|`nOption`|`dwValue`|説明|
|---------------|---------------|-----------------|
|`SCC_OPT_EVENTQUEUE`|`SCC_OPT_EQ_DISABLE`<br /><br /> `SCC_OPT_EQ_ENABLE`|バックグラウンド イベント キューを有効または無効にします。|
|`SCC_OPT_USERDATA`|任意の値|[OPTNAMECHANGEPFN](../extensibility/optnamechangepfn.md) コールバック関数に渡されるユーザー値を指定します。|
|`SCC_OPT_HASCANCELMODE`|`SCC_OPT_HCM_NO`<br /><br /> `SCC_OPT_HCM_YES`|IDE で現在操作のキャンセルがサポートされるかどうかを示します。|
|`SCC_OPT_NAMECHANGEPFN`|[OPTNAMECHANGEPFN](../extensibility/optnamechangepfn.md) コールバック関数へのポインター|名前変更コールバック関数へのポインターを設定します。|
|`SCC_OPT_SCCCHECKOUTONLY`|`SCC_OPT_SCO_NO`<br /><br /> `SCC_OPT_SCO_YES`|(ソース管理ユーザー インターフェイスを使用して) 手動によるファイルのチェックアウトを IDE で許可するか、またはソース管理プラグインを使用してのみチェックアウトする必要があるかを示します。|
|`SCC_OPT_SHARESUBPROJ`|なし|ソース管理プラグインで IDE によるローカル プロジェクト フォルダーの指定を許可する場合、プラグインでは `SCC_I_SHARESUBPROJOK` を返します。|

## <a name="scc_opt_eventqueue"></a>SCC_OPT_EVENTQUEUE
 `nOption` が `SCC_OPT_EVENTQUEUE` の場合、IDE ではバックグラウンド処理を無効 (または再有効化) しています。 たとえば、コンパイル中に IDE では、任意の種類のアイドル状態の処理を停止するようにソース管理プラグインに対して指示する場合があります。 コンパイル後、プラグインのイベント キューを最新の状態に保つために、バックグラウンド処理を再び有効にします。 `nOption` の `SCC_OPT_EVENTQUEUE` 値に対応する 2 つの値 (つまり、`SCC_OPT_EQ_ENABLE` と `SCC_OPT_EQ_DISABLE`) を `dwVal` に使用できます。

## <a name="scc_opt_hascancelmode"></a>SCC_OPT_HASCANCELMODE
 `nOption` の値が `SCC_OPT_HASCANCELMODE` の場合、IDE ではユーザーが長い操作をキャンセルすることができます。 `dwVal` を `SCC_OPT_HCM_NO` (既定値) に設定すると、IDE にキャンセル モードがないことを示します。 ユーザーがキャンセルできるようにする場合は、ソース管理プラグインに独自の [キャンセル] ボタンが用意されている必要があります。 `SCC_OPT_HCM_YES` は、IDE で操作をキャンセルする機能が用意されていることを示します。そのため、SCC プラグインでは、独自の [キャンセル] ボタンが表示されている必要はありません。 IDE で `dwVal` が `SCC_OPT_HCM_YES` に設定されている場合、`lpTextOutProc` コールバック関数に送信された `SCC_MSG_STATUS` および `DOCANCEL` メッセージに応答する準備ができています (「[LPTEXTOUTPROC](../extensibility/lptextoutproc.md)」を参照してください)。 IDE でこの変数が設定されていない場合、プラグインではこれら 2 つのメッセージを送信できません。

## <a name="scc_opt_namechangepfn"></a>SCC_OPT_NAMECHANGEPFN
 NOption が `SCC_OPT_NAMECHANGEPFN` に設定されていて、ソース管理プラグインと IDE の両方でこれを許可している場合、プラグインでは実際にソース管理操作中にファイルの名前変更や移動を行うことができます。 `dwVal` は、[OPTNAMECHANGEPFN](../extensibility/optnamechangepfn.md) 型の関数ポインターに設定されます。 ソース管理操作中に、プラグインではこの関数を呼び出して、3 つのパラメーターを渡すことができます。 これらは、ファイルの (完全修飾パスを持つ) 前の名前、そのファイルの (完全修飾パスを持つ) 新しい名前、IDE に関連する情報へのポインターです。 IDE では、`nOption` を `SCC_OPT_USERDATA` に設定して `dwVal` がデータを指すようにして `SccSetOption` を呼び出すことで、この最後のポインターを送信します。 この関数のサポートは省略可能です。 この機能を使用する VSSCI プラグでは、関数ポインターとユーザー データ変数を `NULL` に初期化する必要があります。また指定されていない場合は、rename 関数を呼び出すことはできません。 また、指定された値を保持するか、`SccSetOption` への新しい呼び出しに応じてこれを変更する準備ができている必要があります。 これは、ソース管理コマンド操作の途中では発生しませんが、コマンド間で発生する可能性があります。

## <a name="scc_opt_scccheckoutonly"></a>SCC_OPT_SCCCHECKOUTONLY
 nOption が `SCC_OPT_SCCCHECKOUTONLY` に設定されている場合、IDE では、ソース管理システムのユーザー インターフェイスを介して、現在開いているプロジェクト内のファイルを手動でチェックアウトしてはならないことを示しています。 代わりに、ファイルをチェックアウトする場合は、IDE コントロールのソース管理プラグインのみを使用する必要があります。 `dwValue` が `SCC_OPT_SCO_NO` に設定されている場合は、ファイルがプラグインによって正常に処理され、ソース管理 UI でチェックアウトできることを意味します。 `dwValue` が `SCC_OPT_SCO_YES` に設定されている場合は、プラグインのみがファイルのチェックアウトを許可され、ソース管理システムの UI を呼び出すことはできません。 これは、IDE に "擬似ファイル" が含まれている可能性がある状況のためです。この場合、IDE でのみチェックアウトするのが理にかなっています。

## <a name="scc_opt_sharesubproj"></a>SCC_OPT_SHARESUBPROJ
 `nOption` が `SCC_OPT_SHARESUBPROJ` に設定されている場合、IDE では、ソース管理からファイルを追加するときに指定されたローカル フォルダーをソース管理プラグインで使用できるかどうかをテストします。 この場合、`dwVal` パラメーターの値は問題になりません。 [SccAddFromScc](../extensibility/sccaddfromscc-function.md) が呼び出されたときにソース管理からファイルが追加されるローカルの送信先フォルダーを IDE で指定することがプラグインによって許可されている場合、プラグインでは `SccSetOption` 関数が呼び出されたときに `SCC_I_SHARESUBPROJOK` を返す必要があります。 次に、IDE では `SccAddFromScc` 関数の `lplpFileNames` パラメーターを使用して、送信先フォルダーを渡します。 プラグインでは、この送信先フォルダーを使用して、ソース管理から追加されたファイルを配置します。 `SCC_OPT_SHARESUBPROJ` オプションを設定したときにプラグインで `SCC_I_SHARESUBPROJOK` が返されない場合、プラグインでは現在のローカル フォルダーにのみファイルを追加できることが、IDE で前提とされています。

## <a name="see-also"></a>関連項目
- [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [SccInitialize](../extensibility/sccinitialize-function.md)
- [SccOpenProject](../extensibility/sccopenproject-function.md)
- [SccAddFromScc](../extensibility/sccaddfromscc-function.md)
- [LPTEXTOUTPROC](../extensibility/lptextoutproc.md)
- [OPTNAMECHANGEPFN](../extensibility/optnamechangepfn.md)
