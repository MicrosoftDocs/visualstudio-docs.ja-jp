---
description: この関数は、クライアント ディスク上の現在のローカル ディレクトリと、ソース管理下にある対応するプロジェクトの差異を表示します。
title: SccDirDiff 関数 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccDirDiff
helpviewer_keywords:
- SccDirDiff function
ms.assetid: 26c9ba92-e3b9-4dd2-bd5e-76b17745e308
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e938cdaedf8541d787673371cfce3d07e005711f
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112904644"
---
# <a name="sccdirdiff-function"></a>SccDirDiff 関数
この関数は、クライアント ディスク上の現在のローカル ディレクトリと、ソース管理下にある対応するプロジェクトの差異を表示します。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccDirDiff(
   LPVOID    pContext,
   HWND      hWnd,
   LPCSTR    lpDirName,
   LONG      dwFlags,
   LPCMDOPTS pvOptions
);
```

### <a name="parameters"></a>パラメーター
 pContext

[入力] ソース管理プラグインのコンテキスト構造体。

 hWnd

[入力] ソース管理プラグインが、提供するすべてのダイアログ ボックスの親として使用できる IDE ウィンドウへのハンドル。

 lpDirName

[入力] ビジュアルな差異を表示するローカル ディレクトリの完全修飾パス。

 dwFlags

[入力] コマンド フラグ (「解説」を参照してください)。

 pvOptions

[入力] ソース管理プラグイン固有のオプション。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装では、次のいずれかの値が返されることが予期されています。

|値|説明|
|-----------|-----------------|
|SCC_OK|ディスク上のディレクトリは、ソース コード管理下にあるプロジェクトと同じです。|
|SCC_I_FILESDIFFER|ディスク上のディレクトリは、ソース コード管理下にあるプロジェクトと異なります。|
|SCC_I_RELOADFILE|ファイルまたはプロジェクトを再度読み込む必要があります。|
|SCC_E_FILENOTCONTROLLED|ディレクトリはソース コード管理されていません。|
|SCC_E_NOTAUTHORIZED|ユーザーはこの操作の実行が許可されていません。|
|SCC_E_ACCESSFAILURE|ソース管理システムへのアクセス中に問題が発生しました。ネットワークまたは競合の問題が原因になっている可能性があります。 再試行することをお勧めします。|
|SCC_E_NONSPECIFICERROR<br /><br /> SCC_E_UNKNOWNERROR|不特定のエラーです。|
|SCC_E_FILENOTEXIST|ローカル ディレクトリが見つかりませんでした。|

## <a name="remarks"></a>解説
 この関数は、指定されたディレクトリに対する変更の一覧をユーザーに表示するようにソース管理プラグインに指示するために使用されます。 プラグインによって、選択された形式で独自のウィンドウが開き、ディスク上のユーザーのディレクトリとバージョン管理下にある対応するプロジェクトの差異が表示されます。

 プラグインでディレクトリの比較がサポートされている場合は、"クイック diff" オプションがサポートされていない場合でも、ファイル名に基づいたディレクトリの比較がサポートされる必要があります。

|`dwFlags`|解釈|
|---------------|--------------------|
|SCC_DIFF_IGNORECASE|大文字と小文字を区別しない比較 (クイック diff またはビジュアルに使用できます)。|
|SCC_DIFF_IGNORESPACE|空白を無視します (クイック diff またはビジュアルに使用できます)。|
|SCC_DIFF_QD_CONTENTS|ソース管理プラグインによってサポートされている場合、ディレクトリをバイト単位で自動的に比較します。|
|SCC_DIFF_QD_CHECKSUM|プラグインでサポートされている場合、チェックサムを使用してディレクトリを自動的に比較します。サポートされていない場合は、SCC_DIFF_QD_CONTENTS にフォールバックします。|
|SCC_DIFF_QD_TIME|プラグインでサポートされている場合、タイムスタンプを使用してディレクトリを自動的に比較します。サポートされていない場合は、SCC_DIFF_QD_CHECKSUM または SCC_DIFF_CONTENTS にフォールバックします。|

> [!NOTE]
> この関数では、[SccDiff](../extensibility/sccdiff-function.md) と同じコマンド フラグを使用します。 ただし、ソース管理プラグイン プロバイダーで、ディレクトリの "クイック diff" 操作をサポートしないことを選択できます。

## <a name="see-also"></a>関連項目
- [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)
