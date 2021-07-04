---
description: この関数は、指定されたファイルのリストを列挙し、コールバック関数を介して各ファイルの名前変更に関する情報を提供します。
title: SccQueryChanges 関数 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccQueryChanges
helpviewer_keywords:
- SccQueryChanges function
ms.assetid: 4cd58eb3-6952-49b1-9620-8682e3eaa604
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: f93ed14671995502356ae4a19664b14bbd32ce7b
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112900474"
---
# <a name="sccquerychanges-function"></a>SccQueryChanges 関数
この関数は、指定されたファイルのリストを列挙し、コールバック関数を介して各ファイルの名前変更に関する情報を提供します。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccQueryChanges(
   LPVOID           pContext,
   LONG             nFiles,
   LPCSTR*          lpFileNames,
   QUERYCHANGESFUNC pfnCallback,
   LPVOID           pvCallerData
);
```

#### <a name="parameters"></a>パラメーター
 pContext

[入力] ソース管理プラグインのコンテキスト ポインター。

 nFiles

[入力] `lpFileNames` 配列内のファイルの数。

 lpFileNames

[入力] 情報を取得するファイル名の配列。

 pfnCallback

[入力] リスト内の各ファイル名に対して呼び出すコールバック関数 (詳細については、「[QUERYCHANGESFUNC](../extensibility/querychangesfunc.md)」を参照してください)。

 pvCallerData

[入力] 変更されずにコールバック関数に渡される値。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装では、次のいずれかの値が返されることが予期されています。

|値|説明|
|-----------|-----------------|
|SCC_OK|クエリ処理が正常に完了しました。|
|SCC_E_PROJNOTOPEN|プロジェクトがソース管理で開かれていません。|
|SCC_E_ACCESSFAILURE|ソース管理システムへのアクセス中に問題が発生しました。ネットワークまたは競合の問題である可能性があります。|
|SCC_E_NONSPECIFICERROR|指定されていないエラーまたは一般的なエラーが発生しました。|

## <a name="remarks"></a>解説
 クエリされる変更は名前空間に対するもので、具体的にはファイルの名前変更、追加、および削除です。

## <a name="see-also"></a>関連項目
- [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [QUERYCHANGESFUNC](../extensibility/querychangesfunc.md)
- [エラー コード](../extensibility/error-codes.md)
