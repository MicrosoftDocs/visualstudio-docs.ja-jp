---
title: SccPopulateDirList 関数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccPopulateDirList
helpviewer_keywords:
- SccPopulateDirList function
ms.assetid: dfff634b-b155-498b-a356-6eb252ac4fad
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9a6508b8cfde2f08eb40201973fec899ee11956b
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66353547"
---
# <a name="sccpopulatedirlist-function"></a>SccPopulateDirList 関数
この関数は、ディレクトリと (必要に応じて) ファイルがソース コントロールが確認するディレクトリの一覧に格納されているかを判断します。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccPopulateDirList(
   LPVOID        pContext,
   LONG          nDirs,
   LPCSTR*       lpDirPaths,
   POPDIRLISTFUNCpfnPopulate,
   LPVOID        pvCallerData,
   LONG          fOptions
);
```

#### <a name="parameters"></a>パラメーター
 pContext

[in]ソース管理プラグインのコンテキストのポインター。

 nDirs

[in]内のディレクトリ パスの数、`lpDirPaths`配列。

 lpDirPaths

[in]確認へのディレクトリ パスの配列。

 pfnPopulate

[in]各ディレクトリのパスと (必要に応じて) ファイル名にするために呼び出すコールバック関数`lpDirPaths`(を参照してください[POPDIRLISTFUNC](../extensibility/popdirlistfunc.md)詳細については)。

 pvCallerData

[in]コールバック関数に渡される値は変更されません。

 方法は限られて

[in]ディレクトリの処理方法を制御する値の組み合わせ (の「PopulateDirList フラグ」セクションを参照して[特定のコマンドで使用されるビットフラグ](../extensibility/bitflags-used-by-specific-commands.md)使用可能な値)。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグイン実装は、次の値のいずれかを返すが必要です。

|[値]|説明|
|-----------|-----------------|
|SCC_OK|操作が正常に完了しました。|
|SCC_E_UNKNOWNERROR|エラーが発生しました。|

## <a name="remarks"></a>Remarks
 これらのディレクトリとのみ (必要に応じて) 実際には、ソース管理リポジトリ内にあるファイル名は、コールバック関数に渡されます。

## <a name="see-also"></a>関連項目
- [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [特定のコマンドで使用されるビットフラグ](../extensibility/bitflags-used-by-specific-commands.md)
- [POPDIRLISTFUNC](../extensibility/popdirlistfunc.md)
- [エラー コード](../extensibility/error-codes.md)