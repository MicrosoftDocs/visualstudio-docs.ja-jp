---
description: この関数では、指定されたファイルの履歴を表示します。
title: SccHistory 関数 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccHistory
helpviewer_keywords:
- SccHistory function
ms.assetid: a636d9d3-47c1-4b48-ac6b-bcfde19d6cf9
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 11a3056e34d15e2e04b687a518e86041dc270997
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105063852"
---
# <a name="scchistory-function"></a>SccHistory 関数
この関数では、指定されたファイルの履歴を表示します。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccHistory(
   LPVOID    pvContext,
   HWND      hWnd,
   LONG      nFiles,
   LPCSTR*   lpFileNames,
   LONG      fOptions,
   LPCMDOPTS pvOptions
);
```

#### <a name="parameters"></a>パラメーター
 `pvContext`

[入力] ソース管理プラグインのコンテキスト構造体。

 `hWnd`

[入力] ソース管理プラグインが、提供するすべてのダイアログ ボックスの親として使用できる IDE ウィンドウへのハンドル。

 `nFiles`

[入力] `lpFileName` 配列で指定されているファイルの数。

 `lpFileName`

[入力] ファイルの完全修飾名の配列。

 `fOptions`

[入力] コマンド フラグ (現在使用されていません)。

 `pvOptions`

[入力] ソース管理プラグイン固有のオプション。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装では、次のいずれかの値を返すことが想定されます。

|値|説明|
|-----------|-----------------|
|SCC_OK|バージョン履歴が正常に取得されました。|
|SCC_I_RELOADFILE|ソース管理システムでは、履歴のフェッチ中にディスク上のファイルを (たとえば、その古いバージョンを取得することによって) 実際に変更したため、IDE ではこのファイルを再度読み込む必要があります。|
|SCC_E_FILENOTCONTROLLED|ファイルはソース管理されていません。|
|SCC_E_OPNOTSUPPORTED|ソース管理システムでは、この操作はサポートされていません。|
|SCC_E_NOTAUTHORIZED|ユーザーはこの操作の実行が許可されていません。|
|SCC_E_ACCESSFAILURE|ソース管理システムへのアクセス中に問題が発生しました。ネットワークまたは競合の問題である可能性があります。 再試行することをお勧めします。|
|SCC_E_PROJNOTOPEN|プロジェクトが開かれていません。|
|SCC_E_NONSPECIFICERROR|不特定のエラーです。 ファイル履歴を取得できませんでした。|

## <a name="remarks"></a>解説
 ソース管理プラグインでは、`hWnd` を親ウィンドウとして使用して、各ファイルの履歴を表示する独自のダイアログ ボックスを表示できます。 あるいは、[SccOpenProject](../extensibility/sccopenproject-function.md) に提供される省略可能なテキスト出力コールバック関数を使用することもできます (これがサポートされている場合)。

 特定の状況では、確認されるファイルが、この呼び出しの実行中に変更される可能性があることに注意してください。 たとえば、[!INCLUDE[vsvss](../extensibility/includes/vsvss_md.md)] の履歴コマンドは、ユーザーに古いバージョンのファイルを取得する機会を提供します。 このような場合、ソース管理プラグインでは、IDE にそのファイルを再度読み込む必要があることを警告するために `SCC_I_RELOAD` を返します。

> [!NOTE]
> ソース管理プラグインがファイルの配列に対してこの関数をサポートしていない場合は、最初のファイルのファイル履歴しか表示できません。

## <a name="see-also"></a>関連項目
- [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [SccOpenProject](../extensibility/sccopenproject-function.md)
