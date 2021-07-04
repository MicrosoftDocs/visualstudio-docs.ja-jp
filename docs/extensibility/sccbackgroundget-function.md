---
description: この関数では、指定された各ファイルを、ユーザー操作なしでソース管理から取得します。
title: SccBackgroundGet 関数 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccBackgroundGet
helpviewer_keywords:
- SccBackgroundGet function
ms.assetid: 69817e52-b9ac-4f4d-820b-2cc9c384f0dc
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 316a02e84b4d51f309aecdd98d0409c85ccbdbef
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112901241"
---
# <a name="sccbackgroundget-function"></a>SccBackgroundGet 関数
この関数では、指定された各ファイルを、ユーザー操作なしでソース管理から取得します。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccBackgroundGet(
   LPVOID  pContext,
   LONG    nFiles,
   LPCSTR* lpFileNames,
   LONG    dwFlags,
   LONG    dwBackgroundOperationID
);
```

### <a name="parameters"></a>パラメーター
 pContext

[入力] ソース管理プラグインのコンテキスト ポインター。

 nFiles

[入力] `lpFileNames` 配列で指定されているファイルの数。

 lpFileNames

[入力、出力] 取得するファイルの名前の配列。

> [!NOTE]
> 名前は、完全修飾されたローカル ファイル名である必要があります。

 dwFlags

[入力] コマンド フラグ (`SCC_GET_ALL`、`SCC_GET_RECURSIVE`)。

 dwBackgroundOperationID

[入力] この操作に関連付けられている一意の値。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装では、次のいずれかの値が返されることが予期されています。

|値|説明|
|-----------|-----------------|
|SCC_OK|操作は正常に完了しました。|
|SCC_E_BACKGROUNDGETINPROGRESS|バックグラウンドでの取得が既に進行中です (ソース管理プラグインでは、同時バッチ操作をサポートしていない場合にのみ、これを返す必要があります)。|
|SCC_I_OPERATIONCANCELED|操作が完了する前に取り消されました。|

## <a name="remarks"></a>解説
 この関数は、ソース管理プラグインが読み込まれたスレッドとは異なるスレッド上で常に呼び出されます。 この関数は、完了するまで返すことは想定されていません。ただし、同時にファイルの複数のリストを使用して複数回呼び出すことができます。

 `dwFlags` 引数の使用は [SccGet](../extensibility/sccget-function.md) と同じです。

## <a name="see-also"></a>関連項目
- [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [SccGet](../extensibility/sccget-function.md)
