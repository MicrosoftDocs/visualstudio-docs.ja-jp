---
description: この関数は、ソース管理の管理ツールを呼び出します。
title: SccRunScc 関数 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccRunScc
helpviewer_keywords:
- SccRunScc function
ms.assetid: bbe7c931-b17a-4779-9cf6-59e5f9f0c172
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: c865931ed52601761f0bd519bf360d584d49ec04
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112904114"
---
# <a name="sccrunscc-function"></a>SccRunScc 関数
この関数は、ソース管理の管理ツールを呼び出します。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccRunScc(
   LPVOID  pvContext,
   HWND    hWnd,
   LONG    nFiles,
   LPCSTR* lpFileNames
);
```

#### <a name="parameters"></a>パラメーター
 pvContext

[入力] ソース管理プラグインのコンテキスト構造体。

 hWnd

[入力] 提供するすべてのダイアログ ボックスの親としてソース管理プラグインで使用できる IDE ウィンドウへのハンドル。

 nFiles

[入力] `lpFileNames` 配列で指定されているファイルの数。

 lpFileNames

[入力] 選択されたファイル名の配列。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装では、次のいずれかの値が返されることが予期されています。

|値|説明|
|-----------|-----------------|
|SCC_OK|ソース管理の管理ツールが正常に呼び出されました。|
|SCC_I_OPERATIONCANCELED|操作は取り消されました。|
|SCC_E_INITIALIZEFAILED|ソース管理システムを初期化できませんでした。|
|SCC_E_ACCESSFAILURE|ソース管理システムへのアクセス中に問題が発生しました。ネットワークまたは競合の問題である可能性があります。|
|SCC_E_CONNECTIONFAILURE|ソース管理システムに接続できませんでした。|
|SCC_E_FILENOTCONTROLLED|選択したファイルはソース コード管理されていません。|
|SCC_E_NONSPECIFICERROR|不特定のエラーです。|

## <a name="remarks"></a>解説
 この関数を使用すると、呼び出し元は、外部管理ツールを通じてソース管理システムのすべての機能にアクセスできます。 ソース管理システムにユーザー インターフェイスがない場合、ソース管理プラグインでは、必要な管理機能を実行するためのインターフェイスを実装できます。

 この関数は、現在選択されているファイルの数およびファイル名の配列を使用して呼び出されます。 管理ツールでサポートされている場合は、ファイルの一覧を使用して、管理インターフェイスでファイルを事前に選択できます。それ以外の場合、リストは無視できます。

 通常、この関数は、ユーザーが **[\<Source Control Server> を起動]** を **[ファイル]**  ->  **[ソース管理]** メニューから選択したときに呼び出されます。 この **起動** メニュー オプションは、レジストリ エントリを設定することによって、常に無効にしたり非表示にしたりすることができます。 詳細については、「[方法: ソース管理プラグインをインストールする](../extensibility/internals/how-to-install-a-source-control-plug-in.md)」を参照してください。 この関数は、[SccInitialize](../extensibility/sccinitialize-function.md) が `SCC_CAP_RUNSCC` 機能ビットを返す場合にのみ呼び出されます (これらの機能ビットの詳細については、「[機能フラグ](../extensibility/capability-flags.md)」を参照してください)。

## <a name="see-also"></a>関連項目
- [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [方法: ソース管理プラグインのインストール](../extensibility/internals/how-to-install-a-source-control-plug-in.md)
- [機能フラグ](../extensibility/capability-flags.md)
- [SccInitialize](../extensibility/sccinitialize-function.md)
