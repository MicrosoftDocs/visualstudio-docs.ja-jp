---
description: この関数は、キューに置かれた状態イベントを取得します。
title: SccGetEvents 関数 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccGetEvents
helpviewer_keywords:
- SccGetEvents function
ms.assetid: 32f8147d-6dcc-465e-b07b-42da5824f9b0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 9438ac10301e2da43b26a88575e44a8ad2c0bf82
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112901059"
---
# <a name="sccgetevents-function"></a>SccGetEvents 関数
この関数は、キューに置かれた状態イベントを取得します。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccGetEvents (
   LPVOID pvContext,
   LPSTR  lpFileName,
   LPLONG lpStatus,
   LPLONG pnEventsRemaining
);
```

### <a name="parameters"></a>パラメーター
 pvContext

[入力] ソース管理プラグインのコンテキスト構造体。

 lpFileName

[入力、出力] ソース管理プラグインによって、返されたファイル名 (最大 _MAX_PATH 文字) が配置されるバッファー。

 lpStatus

[入力、出力] 状態コードを返します (有効な値については、「[ファイルの状態コード](../extensibility/file-status-code-enumerator.md)」を参照してください)。

 pnEventsRemaining

[入力、出力] この呼び出しの後にキューに残されたエントリの数を返します。 この数値が大きい場合、呼び出し元では、[SccQueryInfo](../extensibility/sccqueryinfo-function.md) を呼び出して、すべての情報を一度に取得することを決定できます。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装では、次のいずれかの値が返されることが予期されています。

|値|説明|
|-----------|-----------------|
|SCC_OK|イベントの取得に成功しました。|
|SCC_E_OPNOTSUPPORTED|この関数はサポートされません。|
|SCC_E_NONSPECIFICERROR|不特定のエラーです。|

## <a name="remarks"></a>解説
 この関数は、アイドル処理中に呼び出され、ソース管理下にあるファイルの状態更新があるかどうかを確認します。 ソース管理プラグインでは、認識しているすべてのファイルの状態を保持し、プラグインによって状態の変更が通知されるたびに、状態および関連付けられたファイルがキューに格納されます。 `SccGetEvents` が呼び出されると、キューの最上位要素が取得され、返されます。 この関数は、以前にキャッシュされた情報のみを返すように制限されており、非常に迅速なターンアラウンドが必要です (つまり、ディスクの読み取りや、ソース管理システムの状態の確認はありません)。そうしないと、IDE のパフォーマンスが低下し始めることがあります。

 レポートする状態更新がない場合、ソース管理プラグインでは `lpFileName` で示されるバッファーに空の文字列を格納します。 それ以外の場合、プラグインでは、状態情報が変更されたファイルの完全なパス名を格納し、適切な状態コード (「[ファイルの状態コード](../extensibility/file-status-code-enumerator.md)」で詳細に説明されている値の 1 つ) を返します。

## <a name="see-also"></a>関連項目
- [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [ファイルの状態コード](../extensibility/file-status-code-enumerator.md)
