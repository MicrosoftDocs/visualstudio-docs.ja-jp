---
title: LPTEXTOUTPROC | Microsoft Docs
description: LPTEXTOUTPROC 関数ポインターについて説明します。 Visual Studio IDE には、エラーとステータスを表示する関数が実装されています。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- LPTEXTOUTPROC
helpviewer_keywords:
- SccMsgDataOnMessage structure
- SccMsgDataOnBeforeGetFile structure
- SccMsgDataIsCancelled structure
- LPTEXTOUTPROC callback function
- SccMsgDataOnAfterGetFile structure
ms.assetid: 2025c969-e3c7-4cf4-a5c5-099d342895ea
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: c313375efe8afd17dd5d76f55de4cdaf016bab40
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112903100"
---
# <a name="lptextoutproc"></a>LPTEXTOUTPROC

ユーザーが統合開発環境 (IDE) 内からソース管理操作を実行する場合、ソース管理プラグインでは、操作に関連するエラーまたはステータス メッセージの伝達が必要になることがあります。 このプラグインでは、この目的のために独自のメッセージ ボックスを表示できます。 ただし、よりシームレスな統合のためにプラグインから IDE に文字列を渡すことができ、IDE ではステータス情報を表示するためのネイティブな方法で文字列が表示されます。 このための機構が、`LPTEXTOUTPROC` 関数ポインターです。 IDE では、エラーとステータスを表示するために、この関数 (以下で詳しく説明します) が実装されています。

IDE は [SccOpenProject](../extensibility/sccopenproject-function.md) を呼び出すとき、この関数への関数ポインターを `lpTextOutProc` パラメーターとしてソース管理プラグインに渡します。 たとえば SCC 操作で、多数のファイルが含まれている [SccGet](../extensibility/sccget-function.md) の呼び出しの途中で、プラグインでは `LPTEXTOUTPROC` 関数を呼び出し、表示する文字列を定期的に渡すことができます。 IDE ではこれらの文字列が、必要に応じてステータス バー、出力ウィンドウ、または別のメッセージ ボックスに表示されることがあります。 IDE では特定のメッセージを **[キャンセル]** ボタンと一緒に表示することもできます。 これにより、ユーザーは操作を取り消すことができ、IDE ではこの情報をプラグインに返すことができます。

## <a name="signature"></a>署名
 IDE の出力関数のシグネチャは次のとおりです。

```cpp
typedef LONG (*LPTEXTOUTPROC) (
   LPSTR display_string,
   LONG mesg_type
);
```

## <a name="parameters"></a>パラメーター

display_string

表示するテキスト文字列。 この文字列は、キャリッジ リターンまたはライン フィードで終了することはできません。

mesg_type

メッセージの種類。 このパラメーターとしてサポートされる値の一覧を次の表に示します。

|値|説明|
|-----------|-----------------|
|`SCC_MSG_INFO, SCC_MSG_WARNING, SCC_MSG_ERROR`|メッセージは、情報、警告、またはエラーと見なされます。|
|`SCC_MSG_STATUS`|メッセージにステータスが表示され、ステータス バーに表示できます。|
|`SCC_MSG_DOCANCEL`|メッセージ文字列なしで送信されました。|
|`SCC_MSG_STARTCANCEL`|**[キャンセル]** ボタンの表示を開始します。|
|`SCC_MSG_STOPCANCEL`|**[キャンセル]** ボタンの表示を停止します。|
|`SCC_MSG_BACKGROUND_IS_CANCELLED`|バックグラウンド操作をキャンセルするかどうかを IDE に確認します。操作が取り消された場合、IDE は `SCC_MSG_RTN_CANCEL` を返し、それ以外の場合は `SCC_MSG_RTN_OK` を返します。 `display_string` パラメーターは、ソース管理プラグインによって提供される [SccMsgDataIsCancelled](#LinkSccMsgDataIsCancelled) 構造体としてキャストされます。|
|`SCC_MSG_BACKGROUND_ON_BEFORE_GET_FILE`|ファイルがバージョン コントロールから取得される前に、ファイルについて IDE に通知します。 `display_string` パラメーターは、ソース管理プラグインによって提供される [SccMsgDataOnBeforeGetFile](#LinkSccMsgDataOnBeforeGetFile) 構造体としてキャストされます。|
|`SCC_MSG_BACKGROUND_ON_AFTER_GET_FILE`|ファイルがバージョン コントロールから取得された後に、ファイルについて IDE に通知します。 `display_string` パラメーターは、ソース管理プラグインによって提供される [SccMsgDataOnAfterGetFile](#LinkSccMsgDataOnAfterGetFile) 構造体としてキャストされます。|
|`SCC_MSG_BACKGROUND_ON_MESSAGE`|バックグラウンド操作の現在のステータスを IDE に通知します。 `display_string` パラメーターは、ソース管理プラグインによって提供される [SccMsgDataOnMessage](#LinkSccMsgDataOnMessage) 構造体としてキャストされます。|

## <a name="return-value"></a>戻り値

|値|説明|
|-----------|-----------------|
|SCC_MSG_RTN_OK|文字列が表示されたか、操作が正常に完了しました。|
|SCC_MSG_RTN_CANCEL|ユーザーは操作を取り消す必要があります。|

## <a name="example"></a>例
 たとえば、IDE が 20 個のファイル名で [SccGet](../extensibility/sccget-function.md) を呼び出したとします。 ソース管理プラグインでは、ファイル取得の途中で操作がキャンセルされないようにする必要があります。 各ファイルを取得した後、`lpTextOutProc` を呼び出し、各ファイルのステータス情報をこれに渡して、報告するステータスがない場合は `SCC_MSG_DOCANCEL` メッセージを送信します。 プラグインで、IDE から戻り値 `SCC_MSG_RTN_CANCEL` を受け取った場合、プラグインでは取得操作がすぐに取り消されるため、ファイルはそれ以上取得されません。

## <a name="structures"></a>構造体

### <a name="sccmsgdataiscancelled"></a><a name="LinkSccMsgDataIsCancelled"></a> SccMsgDataIsCancelled

```cpp
typedef struct {
   DWORD dwBackgroundOperationID;
} SccMsgDataIsCancelled;
```

 この構造体は、`SCC_MSG_BACKGROUND_IS_CANCELLED` メッセージと共に送信されます。 これは、キャンセルされたバックグラウンド操作の ID を伝えるために使用されます。

### <a name="sccmsgdataonbeforegetfile"></a><a name="LinkSccMsgDataOnBeforeGetFile"></a> SccMsgDataOnBeforeGetFile

```cpp
typedef struct {
   DWORD dwBackgroundOperationID;
   PCSTR szFile;
} SccMsgDataOnBeforeGetFile;
```

 この構造体は、`SCC_MSG_BACKGROUND_ON_BEFORE_GET_FILE` メッセージと共に送信されます。 これは、取得しようとしているファイルの名前、および取得を実行中のバックグラウンド操作の ID を伝えるために使用されます。

### <a name="sccmsgdataonaftergetfile"></a><a name="LinkSccMsgDataOnAfterGetFile"></a> SccMsgDataOnAfterGetFile

```cpp
typedef struct {
   DWORD dwBackgroundOperationID;
   PCSTR szFile;
   SCCRTN sResult;
} SccMsgDataOnAfterGetFile;
```

 この構造体は、`SCC_MSG_BACKGROUND_ON_AFTER_GET_FILE` メッセージと共に送信されます。 これは、指定されたファイルを取得した結果と、取得を行ったバックグラウンド操作の ID を伝えるために使用されます。 結果として得られる内容については、[SccGet](../extensibility/sccget-function.md) の戻り値を参照してください。

### <a name="sccmsgdataonmessage"></a><a name="LinkSccMsgDataOnMessage"></a> SccMsgDataOnMessage

```cpp
typedef struct {
   DWORD dwBackgroundOperationID;
   PCSTR szMessage;
   BOOL bIsError;
} SccMsgDataOnMessage;
```

 この構造体は、`SCC_MSG_BACKGROUND_ON_MESSAGE` メッセージと共に送信されます。 これは、バックグラウンド操作の現在のステータスを伝えるために使用されます。 ステータスは IDE によって表示される文字列として表現され、`bIsError` はメッセージの重要度を示します (エラー メッセージの場合は `TRUE`、警告または情報メッセージの場合は `FALSE`)。 ステータスを送信するバックグラウンド操作の ID も付与されます。

## <a name="code-example"></a>コードの例
 以下に、`SCC_MSG_BACKGROUND_ON_MESSAGE` メッセージを送信する `LPTEXTOUTPROC` を呼び出す簡単な例を示し、呼び出しの構造体をキャストする方法を示します。

```cpp
LONG SendStatusMessage(
    LPTEXTOUTPROC pTextOutProc,
    DWORD         dwBackgroundID,
    LPCTSTR       pStatusMsg,
    BOOL          bIsError)
{
    SccMsgDataOnMessage msgData = { 0 };
    LONG                result  = 0;

    msgData.dwBackgroundOperationID = dwBackgroundID;
    msgData.szMessage               = pStatusMsg;
    msgData.bIsError                = bIsError;

    result = pTextOutProc(reinterpret_cast<LPCTSTR>(&msgData), SCC_MSG_BACKGROUND_ON_MESSAGE);
    return result;
}
```

## <a name="see-also"></a>関連項目
- [IDE で実装されるコールバック関数](../extensibility/callback-functions-implemented-by-the-ide.md)
- [ソース管理プラグイン](../extensibility/source-control-plug-ins.md)
