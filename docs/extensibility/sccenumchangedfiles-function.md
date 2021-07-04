---
description: この関数では、ローカル ファイルのリストを指定すると、ソース コード管理データベースの対応するバージョンと異なるファイルが判別されます。
title: SccEnumChangedFiles 関数 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccEnumChangedFiles
helpviewer_keywords:
- SccEnumChangedFiles function
ms.assetid: 76cac510-107b-4c1a-ba60-9c39b6db2e71
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 2b0707c049013fd3a0272d1f024e4fdbc342bab1
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112904540"
---
# <a name="sccenumchangedfiles-function"></a>SccEnumChangedFiles 関数
この関数では、ローカル ファイルのリストを指定すると、ソース コード管理データベースの対応するバージョンと異なるファイルが判別されます。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccEnumChangedFiles(
   LPVOID  pContext,
   HWND    hWnd,
   LONG    cFiles,
   LPCSTR* lpFileNames,
   LONG*   plIsFileDifferent
);
```

### <a name="parameters"></a>パラメーター
 pContext

[in] ソース管理プラグインのコンテキスト ポインター。

 hWnd

[入力] 提供するすべてのダイアログ ボックスの親としてソース管理プラグインで使用できる IDE ウィンドウへのハンドル。

 cFiles

[入力] `lpFileNames` 配列で指定されているファイル名の数。 `plIsFileDifferent` 配列のサイズも指定します。

 lpFileNames

[入力] 確認するローカル ファイル名の配列。

 plIsFileDifferent

[入力、出力] 各ファイルの相違ステータスを示す値の配列 (配列には少なくとも `cFiles` 個のエントリがある必要があります)。 0 以外の場合は、ファイルが異なることを意味します。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装では、次のいずれかの値が返されることが予期されています。

|値|説明|
|-----------|-----------------|
|SCC_OK|操作は正常に完了しました。|
|SCC_UNSPECIFIEDERROR|一般的なエラー。|

## <a name="see-also"></a>関連項目
- [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)
